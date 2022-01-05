# Task Scheduling

You'll likely want to run various recurring tasks associated with your server. In the past, this may have been done utilizing `cron`, but it can be frustrating to have your scheduling logic disconnected from your code. To make this easy, Alchemy provides a clean API for scheduling repeated tasks & jobs.

## Scheduling

You can schedule recurring work for your application using the `schedule()` function. You'll probably want to do this in your `boot()` function. This returns a builder with which you can customize the frequency of the task.

```swift
struct ExampleApp: Application {
    func boot() {
        schedule { print("Good morning!") }
            .daily()
    }
}
```

### Scheduling Jobs

You can also schedule jobs to be dispatched. Don't forget to run a worker to run the dispatched jobs.

```swift
app.schedule(job: BackupDatabase())
    .daily(hr: 23)
```

## Schedule frequencies

A variety of builder functions are offered to customize your schedule frequency. If your desired frequency is complex, you can even schedule a task using a cron expression.

```swift
// Every week on tuesday at 8:00 pm
app.schedule { ... }
    .weekly(day: .tue, hr: 20)

// Every second
app.schedule { ... }
    .secondly()

// Every minute at 30 seconds
app.schedule { ... }
    .minutely(sec: 30)

// At 22:00 on every day-of-week from Monday through Friday.”
app.schedule { ... }
    .cron("0 22 * * 1-5")
```

## Running the Scheduler

Note that by default, your app won't actually schedule tasks. You'll need to pass the `--schedule` flag to either the `serve` (default) or `queue` command.

```bash
# Serves and schedules
swift run MyServer --schedule

# Runs a queue worker and schedules
swift run MyServer queue --schedule
```