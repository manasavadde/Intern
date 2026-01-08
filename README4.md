# Problem 4: Thread-Safe LRU Cache with TTL

## Approach
* I use a LinkedHashMap with access-order to track least recently used entries and evict them when the cache exceeds capacity.
* I ensure thread safety by synchronizing operations and optionally run a background thread to remove expired entries.

## Design Choices
* I chose LinkedHashMap with access-order to efficiently maintain LRU order without extra data structures.
* Each cache entry stores an absolute expiration timestamp to handle TTL expiration accurately
* synchronized all operations using a single lock to ensure thread safety across put, get, and cleanup.

# Assumptions
* Each key in the cache is unique, and storing a key again overwrites the previous value and TTL.
* TTL values are positive, and system clock is monotonic and consistent.
* The cache capacity is sufficient to hold the expected working set; evictions occur only when capacity is exceeded.

# Limitations
* All operations are synchronized on a single lock, which may become a bottleneck under high concurrency.
* The cache relies on system time, so clock changes may affect TTL accuracy.
* Background cleanup is periodic, so expired entries may remain in memory briefly until the next cleanup or access.
