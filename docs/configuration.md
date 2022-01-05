# Configuration

* [Run Commands](1\_configuration.md#run-commands)
  * [`serve`](1\_configuration.md#serve)
  * [`migrate`](1\_configuration.md#migrate)
  * [`queue`](1\_configuration.md#queue)

## Run Commands

When Alchemy is run, it takes an argument that determines how it behaves on launch. When no argument is passed, the default command is `serve` which boots the app and serves it on the machine.

There are also `migrate` and `queue` commands which help run migrations and queue workers/schedulers respectively.

You can run these like so.

```shell
swift run Server migrate
```

Each command has options for customizing how it runs. If you're running your app from Xcode, you can configure launch arguments by editing the current scheme and navigating to `Run` -> `Arguments`.

If you're looking to extend your Alchemy app with your own custom commands, check out [Commands](../digging-deeper/13\_commands.md).

### Serve

> `swift run` or `swift run Server serve`

| Option       | Default   | Description                                                           |
| ------------ | --------- | --------------------------------------------------------------------- |
| --host       | 127.0.0.1 | The host to listen on                                                 |
| --port       | 3000      | The port to listen on                                                 |
| --unixSocket | nil       | The unix socket to listen on. Mutually exclusive with `host` & `port` |
| --workers    | 0         | The number of workers to run                                          |
| --schedule   | false     | Whether scheduled tasks should be scheduled                           |
| --migrate    | false     | Whether any outstanding migrations should be run before serving       |
| --env        | env       | The environment to load                                               |

### Migrate

> `swift run Server migrate`

| Option     | Default | Description                                         |
| ---------- | ------- | --------------------------------------------------- |
| --rollback | false   | Should migrations be rolled back instead of applied |
| --env      | env     | The environment to load                             |

### Queue

> `swift run Server queue`

| Option     | Default   | Description                                                  |
| ---------- | --------- | ------------------------------------------------------------ |
| --name     | `nil`     | The queue to monitor. Leave empty to monitor `Queue.default` |
| --channels | `default` | The channels to monitor, separated by comma                  |
| --workers  | 1         | The number of workers to run                                 |
| --schedule | false     | Whether scheduled tasks should be scheduled                  |
| --env      | env       | The environment to load                                      |

_Up next:_ [_Services & Dependency Injection_](2\_fusion.md)

[_Table of Contents_](../Docs/#docs)
