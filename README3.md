# Problem 3: Sliding Window with Dynamic Threshold

## Approach
* I maintain a sliding window average using a running sum to ensure O(1) updates per time unit.
* When a spike is detected, I enter strict mode for a fixed duration, after which the system automatically resets.

## Design Choices
* Used a running sum–based sliding window instead of recomputing averages to guarantee O(1) updates.
* Applied different multipliers for normal and strict modes to dynamically adjust sensitivity after spikes.
* I handle window boundary conditions explicitly to ensure correctness at the start of the stream.

## Assumptions
* The input array represents continuous time units with integer request counts.
* Window size, multipliers, and strict duration are valid positive values.
* Spikes are detected strictly based on exceeding the dynamic threshold, without external corrections.

## Limitations
* The solution assumes the entire input can fit in memory; extremely long streams may require batching or streaming modifications.
* It only tracks strict mode based on a fixed duration and does not adapt dynamically to multiple consecutive spikes beyond the configured strict period.
* The sliding window uses a fixed-size count-based approach, so it cannot directly handle variable-length or time-based windows without modification.
