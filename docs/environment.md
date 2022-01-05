# Environment

Often you'll need to access environment variables of the running program. To do so, use the `Env` type.

```swift
// The type is inferred
let envBool: Bool? = Env.current.get("SOME_BOOL")
let envInt: Int? = Env.current.get("SOME_INT")
let envString: String? = Env.current.get("SOME_STRING")
```

## Dynamic member lookup

If you're feeling fancy, `Env` supports dynamic member lookup.

```swift
let db: String? = Env.DB_DATABASE
let dbUsername: String? = Env.DB_USER
let dbPass: String? = Env.DB_PASS
```

## .env file

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

## Custom Environments

You can load your environment from another location by passing your app the `--env` option.

If you have separate environment variables for different server configurations (i.e. local dev, staging, production), you can pass your program a separate `--env` for each configuration so the right environment is loaded.