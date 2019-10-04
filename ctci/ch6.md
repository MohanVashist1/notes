# Chapter 6 - Big O

## Definition

- Big $O$ is the upper bound, but for interviewing, sometimes Big $O$ really means Big $\Theta$.
- Big $\Omega$ is the lower bound
- Big $\Theta$ refers to both

Cases:

- **Best Case**, we usually don't consider this, as we usually want the maximum amount of time something may take.
- **Worst Case**, usually the case we're looking for, but if the Worst Case is not very likely to happen, then we consider the...
- **Expected Case**, what case will usually happen

Big $O$, usually refers to time, but we also measure Space complexity.

When analyzing the Time Complexity of an Algorithm, we usually Drop the Constants (and Non-Dominant Terms with the same variable in general).

### Amortized Time

Consider the case when an Algorithm usually takes $O(1)$ time, but every $n$th run takes $O(n)$ for some reason. What is the Time Complexity? It should be the worst case, $O(n)$, but this definition is naive. We can take the $O(n)$ and distribute it amongst the $O(1)$s before it, resulting into $O(1)$ Amortized Time.