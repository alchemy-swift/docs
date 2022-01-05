# Logging

To aid with logging, Alchemy provides a lightweight wrapper on top of [SwiftLog](https://github.com/apple/swift-log).

You can conveniently log to the various levels via static functions on the `Log` struct.

```swift
Log.trace("Here")
Log.debug("Testing")
Log.info("Hello")
Log.notice("FYI")
Log.warning("Hmmm")
Log.error("Uh oh")
Log.critical("Houston, we have a problem")
```

These log to `Log.logger`, an instance of `SwiftLog.Logger`, which defaults to a basic stdout logger. 

## Configuring Custom Loggers

`Log.logger` is a settable variable so you may set it to be a more complex `Logger` that outputs to wherever you need it to go. See [SwiftLog](https://github.com/apple/swift-log) for advanced usage and available log drivers.