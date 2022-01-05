# Server Configuration

## Environment

Often you'll need to access environment variables of the running program. To do so, use the `Env` type.

```swift
// The type is inferred
let envBool: Bool? = Env.current.get("SOME_BOOL")
let envInt: Int? = Env.current.get("SOME_INT")
let envString: String? = Env.current.get("SOME_STRING")
```

### Dynamic member lookup

If you're feeling fancy, `Env` supports dynamic member lookup.

```swift
let db: String? = Env.DB_DATABASE
let dbUsername: String? = Env.DB_USER
let dbPass: String? = Env.DB_PASS
```

### .env file

By default, environment variables are loaded from the process as well as the file `.env` if it exists in the working directory of your project.

Inside your `.env` file, keys & values are separated with an `=`.

```bash
# A sample .env file (a file literally titled ".env" in the working directory)

APP_NAME=Alchemy
APP_ENV=local
APP_KEY=
APP_DEBUG=true
APP_URL=http://localhost

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=5432
DB_DATABASE=alchemy
DB_USER=josh
DB_PASS=password

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=
```

### Custom Environments

You can load your environment from another location by passing your app the `--env` option.

If you have separate environment variables for different server configurations (i.e. local dev, staging, production), you can pass your program a separate `--env` for each configuration so the right environment is loaded.

There are a couple of options available for configuring how your server is running. By default, the server runs over `HTTP/1.1`.

## Enable TLS

You can enable running over TLS with `useHTTPS`.

```swift
func boot() throws {
    try useHTTPS(key: "/path/to/private-key.pem", cert: "/path/to/cert.pem")
}
```

## Enable HTTP/2

You may also configure your server with `HTTP/2` upgrades (will prefer `HTTP/2` but still accept `HTTP/1.1` over TLS). To do this use `useHTTP2`.

```swift
func boot() throws {
    try useHTTP2(key: "/path/to/private-key.pem", cert: "/path/to/cert.pem")
}
```

Note that the `HTTP/2` protocol is only supported over TLS, and so implies using it. Thus, there's no need to call both `useHTTPS` and `useHTTP2`; `useHTTP2` sets up both TLS and `HTTP/2` support.