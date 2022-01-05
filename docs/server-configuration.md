# Server Configuration

There are a couple of options available for configuring how your server is running. By default, the server runs over `HTTP/1.1`.

### Enable TLS

You can enable running over TLS with `useHTTPS`.

```swift
func boot() throws {
    try useHTTPS(key: "/path/to/private-key.pem", cert: "/path/to/cert.pem")
}
```

### Enable HTTP/2

You may also configure your server with `HTTP/2` upgrades (will prefer `HTTP/2` but still accept `HTTP/1.1` over TLS). To do this use `useHTTP2`.

```swift
func boot() throws {
    try useHTTP2(key: "/path/to/private-key.pem", cert: "/path/to/cert.pem")
}
```

Note that the `HTTP/2` protocol is only supported over TLS, and so implies using it. Thus, there's no need to call both `useHTTPS` and `useHTTP2`; `useHTTP2` sets up both TLS and `HTTP/2` support.