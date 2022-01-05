<p align="center"><img src="https://user-images.githubusercontent.com/6025554/132588005-5f8a6a94-ec15-4cab-9be9-1e90e86d374f.png" width="400"></a></p>

> __Now fully `async/await`!__

Welcome to Alchemy, an elegant, batteries included backend framework for Swift. You can use it to build a production ready backend for your next mobile app, cloud project or website.

```swift
@main
struct App: Application {
    func boot() {
        get("/") { req in
            "Hello World!"
        }
    }
}
```

# About

Alchemy provides you with Swifty APIs for everything you need to build production-ready backends. It makes writing your backend in Swift a breeze by easing typical tasks, such as:

- [Simple, fast routing engine](docs/routing.md).
- [Powerful dependency injection container](docs/fusion.md).
- Expressive, Swifty [database ORM](docs/rune.md).
- Database agnostic [query builder](docs/query-builder.md) and [schema migrations](docs/migrations.md).
- [Robust job queues backed by Redis or SQL](docs/queues.md).
- First class support for [Plot](https://github.com/JohnSundell/Plot), a typesafe HTML DSL.
- [Supporting libraries to share typesafe backend APIs with Swift frontends](docs/papyrus.md).

## Why Alchemy?

Swift on the server is exciting but also relatively nascant ecosystem. Building a backend with it can be daunting and the pains of building in a new ecosystem can get in the way.

The goal of Alchemy is to provide a robust, batteries included framework with everything you need to build production ready backends. Stay focused on building your next amazing project in modern, Swifty style without sweating the details.

## Guiding principles

**1. Batteries Included**

With Routing, an ORM, advanced Redis & SQL support, Authentication, Queues, Cron, Caching and much more, `import Alchemy` gives you all the pieces you need to start building a production grade server app.

**2. Convention over Configuration**

APIs focus on simple syntax with lots of baked in convention so you can build much more with less code. This doesn't mean you can't customize; there's always an escape hatch to configure things your own way.

**3. Rapid Development**

Alchemy is designed to help you take apps from idea to implementation as swiftly as possible.

**4. Interoperability**

Alchemy is built on top of the lightweight, [blazingly](https://web-frameworks-benchmark.netlify.app/result?l=swift) fast [Hummingbird](https://github.com/hummingbird-project/hummingbird) framework. It is fully compatible with existing `swift-nio` and `vapor` components like [stripe-kit](https://github.com/vapor-community/stripe-kit), [soto](https://github.com/soto-project/soto) and even [fluent-kit](https://github.com/vapor/fluent-kit) so that you can easily integrate with all existing Swift on the Server work.

**5. Keep it Swifty** 

Swift is built to write concice, safe and elegant code. Alchemy leverages it's best parts to help you write great code faster and obviate entire classes of backend bugs. With v0.4.0 and above, it's API is completely `async/await` meaning you have access to all Swift's cutting edge concurrency features.

# Get Started

To get started check out the extensive docs starting with [Getting Started](docs/getting-started.md).
