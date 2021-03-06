# Working with Data

 Set of guidelines and best practices to make working with data easy for everyone.

## Best Practices

- Data is only useful as long as it’s being used.
- Think of the data state as a sieries of inmutable events. that means trating all the data as an event log. Consumers can subscribe to the relevant event log. Having a central place (the log) for continuous events make easy to create a stream of data to process and sets a source of truth.
- Use UTF-8 encoding in all the strings.
- `None` should represent missing or empty values. For example, for a `likes` field the default value should be `0`, `None` should be used in case this information is not available.
- Avoid empty strings except if they're required in a particular field. Use `null`/`None` instead.
- Use [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) date (`YYYY-MM-DD`) and time (`hh:mm:ss`) formats when possible (even when writing documents).
- Deprecate or remove old resources (database tables, code, streams). To deprecate, rename the old resource and not the new one. For example, if a new updates table is added, call it `updates` and rename the old one to something like `updates_old_[date]` if it can't be deleted.

## Naming Conventions

- Follow [Looker Naming Convention](https://looker.buffer.com/stories/liger/naming_conventions.md) for SQL.


## Batch Data Processing

Batch data processing, also known as ETL, is usually done by running jobs in a schedule.
Aim to keep these key properties when creating new jobs:

- **Reproducibility**. This can be archieved via immutable data along with versioned logic.
- **Determinism and idempotency**. They will produce the same result every time they are executed.
- **No side effects**. This allow jobs to be written, tested, reasoned-about and debugged in isolation, without the need to understand external context or history of events surrounding its execution.

These properties along with an inmutable staging area in the database gives the ability to recompute the state of the entire warehouse from scratch if needed.
