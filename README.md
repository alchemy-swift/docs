<p align="center"><img src="https://user-images.githubusercontent.com/6025554/132588005-5f8a6a94-ec15-4cab-9be9-1e90e86d374f.png" width="400"></a></p>

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

- [Simple, fast routing engine](Docs/3a_RoutingBasics.md).
- [Powerful dependency injection container](Docs/2_Fusion.md).
- Expressive, Swifty [database ORM](Docs/6a_RuneBasics.md).
- Database agnostic [query builder](Docs/5b_DatabaseQueryBuilder.md) and [schema migrations](Docs/5c_DatabaseMigrations.md).
- [Robust job queues backed by Redis or SQL](Docs/8_Queues.md).
- First class support for [Plot](https://github.com/JohnSundell/Plot), a typesafe HTML DSL.
- [Supporting libraries to share typesafe backend APIs with Swift frontends](Docs/4_Papyrus.md).

## Why Alchemy?

Swift on the server is exciting but also relatively nascant ecosystem. Building a backend with it can be daunting and the pains of building in a new ecosystem can get in the way.

The goal of Alchemy is to provide a robust, batteries included framework with everything you need to build production ready backends. Stay focused on building your next amazing project in modern, Swifty style without sweating the details.

## Guiding principles

**1. Batteries Included**

With Routing, an ORM, advanced Redis & SQL support, Authentication, Queues, Cron, Caching and much more, `import Alchemy` gives you all the pieces you need to start building a production grade server app.

**2. Convention over Configuration**

APIs focus on simple syntax with lots of baked in convention so you can build much more with less code. This doesn't mean you can't customize; there's always an escape hatch to configure things your own way.

**3. Ease of Use** 

A fully documented codebase organized in a single repo make it easy to get building, extending and contributing.

**4. Keep it Swifty** 

Swift is built to write concice, safe and elegant code. Alchemy leverages it's best parts to help you write great code faster and obviate entire classes of backend bugs.

# Get Started

To get started, check out [Getting Started](docs/getting-started.md) or the [Tutorial](other/tutorial.md)
