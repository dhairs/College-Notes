## Minimizing Maximum Lateness Problem

Lets say we are given $n$ tasks indexed from $1$ to $n$. Task $i$ has a positive integer deadline $d$ and positive integer execution requirement $e$. We want to ([[Process Abstraction#^7479de|non-preemptively]]) schedule all $n$ tasks on a single resource beginning at time 0 such that the maximum 'lateness' of a task is minimized. A task with deadline $d$ and termination time $t$ is defined to have lateness $\text{max}(0,t-d)$.

We can restrict our attention to gap-free schedules so we are optimizing over $n!$ schedules.
