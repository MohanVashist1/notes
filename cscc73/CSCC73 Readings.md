# CSCC73

## Legend

KT = Kleinberg and Tardos. *Algorithm Design.* Addison Wesley 2006.

DPV = Dasgupta, Papadimitriou, and Vazirani. *Algorithms.* McGraw-Hill 2006.

## Reading Notes

### LEC 1: Interval Scheduling (KT 4.1)

Greedy Algorithms are basically greedy. Greedy in the sense that they are built of a collection of smaller steps, where in each of theses smaller steps, the solution is optimized. The definition of "optimized" is actually pretty vague, and it depends on the problem we're solving.

There are also two basic methods for proving that a greedy approach results into an optimal solution

1. The Greedy Algorithm "**stays ahead**". This means that the greedy solution is better than all other solutions if not the same (in case there are multiple optimal solutions).
2. The **Exchange Argument**. This is were we consider any of the optimal solutions and then gradually transform it into a solution that the greedy algorithm can find without hurting the quality of the solution

It's usually better with an example, which is the following.

#### Interval Scheduling: The Greedy Algorithm Stays Ahead

Consider the Interval Scheduling Problem. We have a set of requests $R = \{ 1,2, ..., n \}$ where the $i$th request has an interval start time of $s(i)$ and a finish time of $f(i)$.

We consider a set of intervals **"Compatible"** if no two intervals overlap in terms of time.

We also consider the *largest Compatible set*, **optimal**, so that's what we're looking for. The largest Compatible set.

#### The Solution

The solution is to select the 