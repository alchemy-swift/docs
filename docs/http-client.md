# HTTP Client

## Introduction

Alchemy provides a lightweight, `async` enabled, wrapper around the official Swift on the Server `async-http-client`. You get a high performance, easy to use interface that makes it easy for your app to communicate with other web applications.

## Making Requests

Out of the box, a default client is registered to your application's service container and comes with a request builder, conveniently accessible through the `Http` alias. You may use the `get`, `post`, `put`, `patch`, `delete`, etc functions to make requests.

```swift
let response = try await Http.get("https://swift.org")
```

Each request returns a `Client.Response` object that contains a variety of methods to help handle the response.

```swift
// Status
response.isOk // Bool
response.isSuccessful // Bool
response.isFailed // Bool
response.isClientError // Bool
response.isServerError // Bool
response.validateSuccessful() // throws -> Bool

// Headers
response.header("Header-Name") // String?

// Content
response.body // ByteContent?
response.data // Data?
response.string // String?
response.decode<D: Decodable>(type: D, using: ContentDecoder) // throws -> D
```

Like `Request`, `Client.Response` also conforms to `ContentInspector` so you can use subscripts and dynamic typing to access various fields the response.

```swift
let response = try await Http.get("https://example.com/users/1")
let userName = try response["name"].string
let userAge = try response.age.int
```

### Request Content

The reqest builder conforms to `RequestBuilder` and contains many methods for constructing requests. If you want to include some JSON content on your requests, you should use the `.withJSON()` function which takes a dictionary.

```swift
let response = try await Http.withJSON([
    "name": "Josh", 
    "age": 28
]).post("https://example.com/users")
```

You may also pass an `Encodable` type, optionally speciying the `JSONEncoder` with which to encode.

```swift
struct User: Codable {
    let name: String
    let age: Int
}

let user = User(name: "Louis", age: 34)
let response = try await Http
    .withJSON(user)
    .post("https://example.com/users")
```

#### Queries

If you'd like to specify a url query on the request, you may specify it directly in the url or use either `withQuery()` (for a single key / value pair) or `withQueries()` (for multiple query items).

```swift
let response = try await Http
    .withQuery("name", value: "Rachel")
    .get("https://example.com/users")

let response = try await Http
    .withQueries([
        "job": "Software Engineer",
        "page": 1,
    ])
    .get("https://example.com/users")
```

#### Making Form URL Encoded Requests

The `.withForm()` method lets you send data using the `application/x-www-form-urlencoded` content type. Like `withJSON()`, it takes either a dictionary or an `Encodable` type and an optional `URLEncodedFormEncoder`.

```swift
let response = try await Http.withForm([
    "name": "Josh", 
    "age": 28
]).post("https://example.com/users")

let user = User(name: "Cassidy", age: 26)
let response = try await Http.withForm(user).post("https://example.com/users")
```

#### Sending a Raw Request Body

Of course, you have full customization over the content of your request. If you'd prefer to send a raw request body, you can use the `.withBody()` to send either `Foundation.Data` or a swift-nio `ByteBuffer`.

```swift
// Foundation.Data
let data: Data = requestString.data(using: .utf8)!
let response = try await Http.withBody(data).post("https://example.com/photo")

// swift-nio ByteBuffer
let buffer = ByteBuffer(string: requestString)
let response = try await Http.withBody(buffer).post("https://example.com/photo")
```

#### Multipart Requests

If you need to make a `multipart/form-data` request, you'll use the `attach()` method. This takes a name, an attachment contents, and an optional filename.

```swift
let imageData: ByteBuffer = ...
let response = try await Http
    .attach("image", contents: imageData, filename: "photo.jpg")
    .post("https://example.com/photo")
```

You can also attach a streamed `File` or multiple `File` resources directly.

```swift
let image: File = Storage.get("images/kitten.jpg")
let upload: File = request.file("profile")!
let response = try await Http.attach([
    "kitten": image, 
    "profile": upload
]).post("https://example.com/photos")
```

### Headers

A header may be added to a request using the `withHeader()` method. Multiple headers may be added using `withHeaders()`.

```swift
let response = try await Http.withHeaders([
    "X-One": "foo",
    "X-Two": "bar"
]).get("https://example.com/users")
```

### Authentication

You may specify basic authentication credentials using `withBasicAuth()`.

```swift
let response = try await Http.withBasicAuth(username: "josh@withapollo.com", password: "secret").get(...)
```

#### Bearer Token

If you'd like to quickly add a bearer token to the request, you may use the `withToken()` method.

```swift
let response = Http.withToken("token").get(...)
```

### Timeout

You may specify a timeout for your request using `withTimeout()`, after which your request will be terminated and an error will be thrown.

```swift
let response = try await Http.withTimeout(.seconds(5)).get(...)
```

### Response Streaming

By default, any `Client.Response` will have it's body accumulated into a single `ByteBuffer` before returning, so that you don't need to worry about streamed responses. If you would like to explicitly allow a streamed response, you may do so with the `withStream()` function.

```swift
let response = try await Http.withStream().get("https://example.com/large_download")
let stream: ByteStream = response.body!.stream
```

### Custom Configurations

Under the hood, all you requests are made by the official Swift Server `async-http-client` library. If you'd like finer grain customization over the internal client configuration, you may specify one using `withClientConfig()`.

```swift
import AsyncHTTPClient

let config = HTTPClient.Configuration(...)
let response = try await Http.withClientConfig(config).get(...)
```

## Validating Responses

## Testing

### Asserts

### Stubbing

```swift
Http
    .get(url: "https://swift.org")
    .whenComplete { result in
        switch result {
        case .failure(let error):
            ...
        case .success(let response):
            ...
        }
    }
```