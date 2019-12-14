# LEC 1 - NOT ADDED TO ANKI

**Optimization Problems**

Given an input, find an ouput that satisfies certain constraints and optimizes a desired criterion

**Greedy Algorithm**

Builds a solution incrementally and at each stage, constructs an optimal partial solution according to some criteria

**Interval Scheduling Problem**

Include the greatest number of intervals that do not overlap in the return set given a set of intervals

**Interval Scheduling Optimal Sort**

Sort intervals by finish time

**Intuition of Interval Scheduling Sort by Finish Time**

Chosen intervals gives the most amount of time to fit other intervals

**What are the methods to prove greedy solutions?**

- Greedy "stays ahead"
- Promising Set

# LEC 2 - NOT ADDED TO ANKI

**Minimum-Maximum Lateness Scheduling Problem**

- Given jobs, a duraction and deadline for each job, and a release time. - 

- Return a schedule that maps jobs to start times for that job, and where jobs do not overlap. 

- The schedule must also minimize the amount of time we have missed the deadline.

**Schedule**

$s : i \mapsto s(i)$ where $s(i) \geq r$

**Min-Max Lateness Scheduling Solution**

Sort and schedule jobs by increasing deadline first

**Inversion in the schedule**

a pair of jobs $i, j$ such that $s(i) < s(j)$ but $d(i) > d(j)$

**Is every schedule with no gaps and no inversions optimal?**

Yes













