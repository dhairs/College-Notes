|      | [Logical operators](Logical%20operators.md) | Precedence |
| ---- | --------------------- | ---------- |
| high | $\neg$                | 1          |
| -    | $\wedge$              | 2          |
| -    | $\vee$                | 3          |
| -    | $\implies$            | 4          |
| low  | $\leftrightarrow$     | 5          |

**Example:**
$p\implies q\vee r$
actually means $p\implies (q\vee r)$

**Example 2:**
$p\implies q \implies r$
can be interpreted.
For this reason, **always use parentheses in this class.** They will also **always be provided for clarity.**
