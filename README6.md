# Problem 6: Partial Order Scheduling with Conflict Detection

## Approach
* I First, detect cycle in the task dependencies to ensure no circular constraints.
*  Then, perform a topological sort to determine a valid execution order. Finally, compute start times for each task while respecting mutual exclusion and durations to find the minimum total execution time.

## Design Choices
* Graph-based dependency modeling: Tasks and their dependencies are represented as a directed graph, enabling cycle detection.
* Topological sorting: Kahn’s algorithm is used to determine a valid execution order of tasks respecting dependencies.
* Mutual exclusion handling: Task start times are adjusted to ensure conflicting tasks do not run concurrently.
* Result encapsulation: A dedicated ScheduleResult object stores validity, execution order, start times, and total execution time.

## Assumptions
* All tasks, dependencies, and mutual exclusion constraints are known before scheduling.
* Task durations are fixed and positive, and absolute start times are measured in discrete units.
* Absolute execution order follows dependencies, and mutual exclusion applies only to tasks in the input constraints.

## Limitations
* The scheduler may become inefficient for extremely large task sets due to topological sorting and mutual exclusion checks.
* Mutual exclusion is handled conservatively, which can increase total execution time if many conflicts exist.
