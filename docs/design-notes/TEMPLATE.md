# Mx: <name>

<!-- Keep it to 1–3 pages. Longer usually means the milestone is too big. -->

## 1. Goal

One paragraph: what this milestone adds, and what it deliberately doesn't.

## 2. Model

The state each node keeps (durable vs. volatile), the messages it sends and receives, and the tables or schema.

## 3. Protocol

Step by step, the happy path. Write it like pseudocode from a paper:
"on Prewrite(key, start_ts): if lock exists → LockConflict ..."

## 4. Invariants

Numbered statements that must ALWAYS be true. Each one must be testable. These become your property tests and checker assertions.

Example (M1): "For any key, a read at `ts` returns the value of the newest `write` record with `commit_ts ≤ ts`, or `SnapshotTooOld` if `ts < gc_safe_point`."

## 5. Failure cases

| What fails | At which step | What the system does | Why that's safe |
|------------|---------------|----------------------|-----------------|
|            |               |                      |                 |

Walk through the fault model: crash, lost request, lost response, duplicate, delay. A row that says "and then it works out somehow" is a bug you haven't found yet.

## 6. Tests

How each invariant gets checked (property test, simulator scenario, checker workload), plus which bugs you'll inject to prove the tests can fail.

## 7. Open questions

What you're unsure about.

## 8. References

The paper sections you relied on.
