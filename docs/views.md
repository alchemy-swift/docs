# Views

Out of the box, Alchemy supports [Plot](https://github.com/JohnSundell/Plot), a Swift DSL for writing type safe HTML. With Plot, returning HTML is simple and elegant. You can do so straight from a `Router` handler.

```swift
app.get("/website") { _ in
    return HTML {
        .head(
            .title("My website"),
            .stylesheet("styles.css")
        ),
        .body(
            .div(
                .h1(.class("title"), "My website"),
                .p("Writing HTML in Swift is pretty great!")
            )
        )
    }
}
```

## Control Flow

Plot also supports inline control flow with conditionals, loops, and even unwrapping. It's the perfect, type safe substitute for a templating language.

```swift
let animals: [String] = ...
let showSubtitle: Bool = ...
let username: String? = ...
HTML {
    .head(
        .title("My website"),
        .stylesheet("styles.css")
    ),
    .body(
        .div(
            .h1("My favorite animals are..."),
            .if(showSubtitle, 
                .h2("You found the subtitle")
            ),
            .ul(.forEach(animals) {
                .li(.class("name"), .text($0))
            }),
            .unwrap(username) {
                .p("Hello, \(username)")
            }
        )
    )
}
```

## HTMLView

You can use the `HTMLView` type to help organize your projects view and pages. It is a simple protocol with a single requirement, `var content: HTML`. Like `HTML`, `HTMLView`s can be returned directly from a `Router` handler.

```swift
struct HomeView: HTMLView {
    let showSubtitle: Bool
    let animals: [String]
    let username: String?

    var content: HTML {
        HTML {
            .head(
                .title("My website"),
                .stylesheet("styles.css")
            ),
            .body(
                .div(
                    .h1("My favorite animals are..."),
                    .if(self.showSubtitle, 
                        .h2("You found the subtitle")
                    ),
                    .ul(.forEach(self.animals) {
                        .li(.class("name"), .text($0))
                    }),
                    .unwrap(self.username) {
                        .p("Hello, \(username)")
                    }
                )
            )
        }
    }
}

app.get("/home") { _ in
    HomeView(showSubtitle: true, animals: ["Orangutan", "Axolotl", "Echidna"], username: "Kendra")
}
```

## Docs

Check out the [Plot docs](https://github.com/JohnSundell/Plot) for everything you can do with it.