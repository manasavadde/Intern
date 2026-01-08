## Problem 2: Deduplicating Event Stream with Partial Ordering

## Approach
* I first deduplicate events using a hash map keyed by eventId, keeping the event with the earliest timestamp.
* Then I group the deduplicated events by userId and sort each group by timestamp, since ordering between different users does not matter.

## Design Choices
* I use a HashMap for deduplication to achieve O(1) lookups and efficiently handle large, out-of-order event streams.
* Separated deduplication from ordering to keep the logic simple and maintainable.
* Events are grouped by userId so that ordering constraints are applied only where required.
* Per-user timestamp-based sorting avoids unnecessary global ordering and improves scalability.

## Assumption
* Each eventId uniquely identifies a logical event, and duplicates differ only in metadata like timestamp.
* The earliest timestamp among duplicates is always considered the correct one.
* Events can be processed in memory, or sufficient batching is available for large inputs.

## Limitations
* The solution assumes enough memory to store all events (or a batch) for deduplication and grouping.
* It does not handle late-arriving corrections after processing is complete (no reprocessing).
* Very large per-user event lists may still incur sorting overhead.
