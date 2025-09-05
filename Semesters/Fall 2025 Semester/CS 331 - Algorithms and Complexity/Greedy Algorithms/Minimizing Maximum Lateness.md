## Minimizing Maximum Lateness Problem

Lets say we are given $n$ tasks indexed from $1$ to $n$. Task $i$ has a positive integer deadline $d$ and positive integer execution requirement $e$. We want to ([[Process Abstraction#^7479de|non-preemptively]]) schedule all $n$ tasks on a single resource beginning at time 0 such that the maximum 'lateness' of a task is minimized. A task with deadline $d$ and termination time $t$ is defined to have lateness $\text{max}(0,t-d)$.

We can restrict our attention to gap-free schedules so we are optimizing over $n!$ schedules.

## Important Observation/Lemma

Suppose $S$ is a schedule in which task $j$ is executed immediately after task $i$ and $d_{j}\leq d_{i}$. Let $l_{1}$ denote the lateness of task $i$ in $S$.

Let $S'$ be the schedule that is the same as $S$ except that the order of execution of tasks $i$ and $j$ is interchanged. Let $l_{1}'$ denote the lateness of task $i$ in $S'$.

The lemma is that $l_{j}\geq \text{max}(l_{i}',l_{j}')$

This lemma implies that the earliest deadline rule yields an optimal schedule. Ties can be broken arbitrarily.