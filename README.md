# Poja scheduled mailing template

This repository demonstrates how to add scheduled mailing to an application and serves as a template for the Poja platform.

It is based on the official guide: [Hello world with scheduled mailing](https://docs.poja.io/docs/hello-world-but-with-scheduled-tasks)
# poja-scheduled-mailing-template — cron-triggered tasks for Spring Boot

A [Poja](https://poja.io) starter template with **AWS EventBridge scheduled tasks** pre-configured. Define a cron expression in the dashboard — Poja fires your async worker automatically, no cron daemon or scheduler to run.

→ **[Full guide on docs.poja.io](https://docs.poja.io/docs/hello-world-but-with-scheduled-tasks)**

---

### What you get

Write one event class. Configure the schedule in the Poja console — no code change needed to update timing.

```java
// The event — in endpoint.event.model
public class DailyReportTriggered extends PojaEvent {
  @Override public Duration maxConsumerDuration() { return Duration.ofSeconds(20); }
  @Override public Duration maxConsumerBackoffBetweenRetries() { return Duration.ofMinutes(1); }
}

// The consumer — in service.event
@Service @AllArgsConstructor
public class DailyReportTriggeredService implements Consumer<DailyReportTriggered> {
  private final Mailer mailer;

  @Override
  public void accept(DailyReportTriggered event) {
    // your logic here — runs automatically on schedule
  }
}
```

Then in the Poja console → Scheduled Tasks → set **class name** + **cron expression**:

```
cron(0 6 * * ? *)   →  every day at 6:00 AM UTC
```

> Part of the [Poja platform](https://poja.io) — deploy Spring Boot without DevOps.
