## Idea

Intuitively, node $w$ is control-dependent on a node $u$ if $u$ determines whether $w$ is executed.

### Example of Basic Control Dependence


| ![[Control Dependence Example Basic.png]]                                      |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say that S1 and S2 are control-dependent on e.

### Example of Self Control Dependence



| ![[Control Dependence Example Self.png]]                                   |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say:
- S1 is control-dependent on e.
- e is control dependent on `START` and itself

### Example with Transitive Control Dependence


| ![[Control Dependence Example Transitive.png\|400]]                        |
| -------------------------------------------------------------------------- |
| https://www.cs.utexas.edu/~pingali/CS380C/2025/lectures/ssa/Dominators.pdf |

In this case, we would say:
- S1 and S3 are control-dependent on f
- They are transitively dependent on e, but e does not fully determine if S1 or S3 are executed, so S1 and S3 are **not** control-dependent on e
- However, we can say that f is control-dependent on e and S1 and S3 are transitively control-dependent on e

## Definition

For $w$ to be control-dependent on edge $u\to v$, $w$ must [[Dominators#Postdominators|postdominate]] $v$ for some CFG successor $v$ of $u$. $w$ can not $\text{pdom } u$.

Intuitively, if control flows from $u$ to $v$, it is guaranteed that $w$ will be executed. But from $u$