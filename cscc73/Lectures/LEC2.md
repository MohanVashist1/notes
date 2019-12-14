### LEC 2: Monday, September 9, 2019

- A1 Posted

#### Minimum-Maximum Lateness Scheduling (KT 4.2)

<u>Input:</u>

- $n$ jobs $1,2,..., n$
- a release time $r$
- for each job $i$
  - $t(i)$ = duration of $i$
  - $d(i)$ = deadline of $i$

We want to minimize the amount of time we have missed the deadline.

A <u>Schedule:</u> $s: i \mapsto s(i)$, where $s(i) \geq r$ (is a mapping from jobs to start time), specifies time when job $i$ is to start such that $\forall i, j$ where $i \neq j$ we have $[s(i), s(i)+d(i)]$ and  $[s(j), s(j)+d(j)]$ do not overlap.

The Lateness of job $i$ in schedule $s$ is defined as $l(s,i) = max(0, s(i)+t(i)-d(i))$

The maximum lateness of $s$ is $$max_{1 \leq i \leq n} l(s,i)$$

$r$ is essentially when the schedule starts

<u>Output:</u>

The output is the schedule of minimum lateness as we have defined it.

Example:

$r = 0, n = 4$

$t(a) = 4, d(a) = 5$

$t(b) = 3, d(b) = 3$

$t(c) = 2, d(c) = 8$

$t(d) = 1, d(d) = 2$

A possible schedule $s$ can be $s(d) = 1, s(a) = 3, s(b) = 7, s(c) = 11$

The lateness of this schedule is 7

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 2        | a    |
| 7        | b    |
| 5        | c    |
| 0        | d    |

Another possible schedule $s$ can be $s(d) = 0, s(a) = 1, s(b) = 5, s(c) = 8$

The lateness of this schedule is 5

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 0        | a    |
| 5        | b    |
| 2        | c    |
| 0        | d    |

<u>Fact 1:</u> There is an optimal schedule with no gaps in it

Another possible schedule $s$ can be $s(d) = 0, s(a) = 4, s(b) = 1, s(c) = 8$

The lateness of this schedule is 3

| $l(s,i)$ | $i$  |
| -------- | ---- |
| 3        | a    |
| 1        | b    |
| 2        | c    |
| 0        | d    |

This schedule is actually optimal for this set of jobs.

How should we sort these jobs? Brute force is $O(n!)$, so let's find a greedy way.

We'll first try to sort the jobs by **increasing deadline first**

Our algorithm outline will look like this

- Sort jobs in increasing deadline
- let $d[1...n]$ be deadlines of the sorted jobs
- let $t[1...n]$ be durations of the sorted jobs
- $F := r$ # finish of last job scheduled
- for $i := 1$ to $n$ do
  - $gs(i) :=F$
  - $F := F + t(i)$
- return $gs$

The running time of this algorithm is $\theta (n\log n)$

<u>Invariant:</u> $gs$ is a schedule with no gaps of the first $i$ jobs **(in increasing deadline)**

<u>Definition:</u> An **Inversion** in the schedule $s$ is a pair of jobs $i, j$ such that $s(i) < s(j)$ but $d(i) > d(j)$

<u>Fact 2:</u> All Schedules with no gaps and no inversions have the same lateness

<u>Theorem:</u> Every schedule with no gaps and no inversions is optimal.

The maximum number of inversions any schedule can have is $n^2$, just a fun fact

<u>Proof for Theorem:</u> We'll do this by contradiction.

Let $s$ be an optimal schedule with no gaps and at least one inversion

$\longrightarrow$ We're assume that $s$ has an inversion involving two successive jobs $i, j : s(j) = s(i) + t(i)$

or the inversion can be between non-successive jobs, like such:

$i'\rightarrow\rightarrow\rightarrow i\rightarrow j\rightarrow\rightarrow j'$ where $d(i') > d(j')$ and $d(i) < d(j)$

So we'll find a pair $i,j$ either way

consider the case where we swap $i,j$, we'll call this new schedule $s'$

Observations:

- $s'$ has fewer inversions than $s$.
- All jobs that are not $i,j$ have the same lateness in $s'$ and $s$
- $l(j, s') \leq l(j, s)$, this is good
- $l(i, s') \geq l(i, s)$, this is bad
- However, $l(i, s') \leq l(j, s)$, so the maximum lateness of any job in $s' \leq$ the maximum lateness of any job in $s$

