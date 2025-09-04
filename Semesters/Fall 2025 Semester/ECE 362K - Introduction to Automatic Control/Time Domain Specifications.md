
In some of the time domain specifications development, the author uses $\zeta=0.5$ to represent the average of the cases. It is **not** a good representation, but gives a starting point.

As the system becomes more complex (beyond 2nd order w/o zeros, we need to consider the entire response due to **all** poles/zeros.

You can use `stepinfo()` or `Lsiminfo()` in MATLAB to check the time domain specifications.