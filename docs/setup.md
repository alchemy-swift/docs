# Setup

## Installation

### CLI

The Alchemy CLI is installable with [Mint](https://github.com/yonaskolb/Mint).

```shell
mint install alchemy-swift/alchemy-cli
```

Creating an app with the CLI will let you pick between a backend or fullstack (`iOS` frontend, `Alchemy` backend, `Shared` library) project.

1. `alchemy new MyNewProject`
2. `cd MyNewProject` (if you selected fullstack, `MyNewProject/Backend`)
3. `swift run`
4. view your brand new app at http://localhost:3000

### Swift Package Manager

Alchemy is also installable through the [Swift Package Manager](https://github.com/apple/swift-package-manager).

```swift
dependencies: [
    .package(url: "https://github.com/alchemy-swift/alchemy", .upToNextMinor(from: "0.2.0"))
    ...
],
targets: [
    .target(name: "MyServer", dependencies: [
        .product(name: "Alchemy", package: "alchemy"),
    ]),
]
```

From here, conform to `Application` somewhere in your target and add the `@main` attribute.

```swift
@main
struct App: Application {
    func boot() {
        get("/") { _ in
            return "Hello from alchemy!"
        }
    }
}
```

Run your app with `swift run` and visit `localhost:3000` in the browser to see your new server in action.

## Editors

### Working with Xcode

You may also use Xcode to run your project to take advantage of all the great tools built into it; debugging, breakpoints, memory graphs, testing, etc.

When working with Xcode be sure to set a custom working directory.

#### Setting a Custom Working Directory

By default, Xcode builds and runs your project in a **DerivedData** folder, separate from the root directory of your project. Unfortunately this means that files your running server may need to access, such as a `.env` file or a `Public` directory, will not be available.

To solve this, edit your server target's scheme & change the working directory to your package's root folder. `Edit Scheme` -> `Run` -> `Options` -> `WorkingDirectory`.

### Working With VSCode

If you'd prefer to develop with VSCode, you should use the official Swift Server [VSCode extension](https://github.com/swift-server/vscode-swift) available on the [VSCode marketplace](https://marketplace.visualstudio.com/items?itemName=sswg.swift-lang).

## Start Coding!

Congrats, you're off to the races! Check out the rest of the guides for what you can do with Alchemy.
