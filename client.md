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

## Building Requests

### Headers

### Content

### Attachments

## Validating Responses

## Testing

### Asserts

### Stubbing

```swift
HTTPClient.default
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