# Problem 5: Session Expiration with Idle and Absolute Timeout

## Approach
* I use a HashMap to track all sessions for fast lookup and store their creation and last access times.
* I check each session against idle timeout and absolute timeout whenever an event occurs to decide if it has expired.
* Events like ACCESS or LOGOUT are applied only to active sessions, ensuring expired sessions are ignored.

## Design Choices
* I chose a HashMap to store sessions for O(1) lookup by session ID, which scales well for large numbers of sessions.
* Each session stores creation time, last access time, expiration time, and status to clearly model its lifecycle.
* Timeouts are checked on every event to enforce idle and absolute expiration accurately.
* Processing events in timestamp order simplifies logic and avoids scanning all sessions unnecessarily.

## Assumptions
* All session events are processed in increasing timestamp order, so no future events arrive before past events.
* Absolute timeout is always greater than or equal to idle timeout, as specified.
* Session IDs are unique, and events for non-existent or expired sessions are ignored.

## Limitations
* Expiration is only checked when events occur or when getSessions() is called, so sessions may temporarily appear active between events.
* The current implementation uses a HashMap, so it does not automatically remove expired sessions in real-time.
* High-frequency events on a very large number of sessions may require more efficient data structures for automatic expiration.
