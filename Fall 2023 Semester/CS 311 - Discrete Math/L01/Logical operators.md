### Negation (not) \[$\neg p$\]:

let $p$ be a proposition. Then, the negation of $p$ is $\neg p$ and means the statement "It is not the case $p$." This means that the statement $\neg p$ means "not p."

Therefore, the truth value of $\neg p$ is the opposite of the truth value for $p$

**Example:**
$p$: "Austin is in Central Texas"
$\neg p$: "It is not the case that Austin is in Central Texas"

**Example 2**:
$p$: $8-5=2$
$\neg p$: $8-5\neq2$

### Conjunction (and) \[$p\wedge q$\]

If we let $p$ and $q$ be propositions, then the _conjunction_ of $p$ **and** $q$ is denoted by $p\wedge q$.

**Read as "$p$ and $q$"**

The truth value of $p\wedge q$ is **true only when both** $p$ and $q$ are true, and false otherwise.

**Example:**
$p$: The sun is shining
$q$: It is raining

$p\wedge q$: The sun is shining and it is raining.

"The sun is shining, but it is raining."

### Disjunction (or) \[$p\vee q$\]

Let $p$ and $q$ be propositions. The disjunction of $p$ and $q$ is denoted by $p\vee q$.

**Read as $p$ or $q$**

Evaluates as false when both are false, otherwise is true.

**Example**:
$p$: "I will eat a hamburger"
$q$: "I will eat a slice of pizza"

$p\vee q$: "I will eat a hamburger _or_ I will eat a slice of pizza"

"I will eat either a hamburger or a slice of pizza"

### Implication (implies) \[$p \implies q$\]

_Note:_ does **not** mean "suggests."
_Note:_ does **not** mean "causes."

Let $p$ and $q$ be propositions. The implication of $p$ and $q$ is denoted by $p\implies q$.

**Read as $p$ implies $q$**

Think of it as "if I know this one thing, $p$ does it mean I know this other thing, $q$"

**Better put as "if $p$ _then_ $q$"**

Statements with it **must always** have a truth value.

**Only false when antecedent is true yet consequent is false, otherwise true.**

#### [[Truth Tables.md|Truth Table]]:

| p   | q   | $p\implies q$ |
| --- | --- | ------------- |
| T   | T   | T             |
| T   | F   | F             |
| F   | T   | T             |
| F   | F   | T             |

$p$ is the **antecedent**, and $q$ is the **consequent**.

**Example:**
If it's summer in Austin, it will be hot.

**Example 2:**
True or False:
$(\sqrt{4} =2 \wedge  \sqrt{9} = 4) \implies \sqrt{30} =5$

Antecedent must be true _and_ consequent must be false.

Antecedent is $\sqrt{4} =2 \wedge  \sqrt{9} = 4$, or "the square root of 4 is 2 **and** the square root of 9 is 4." This expression is false, thus the antecedent is false.

Consequently, the consequent (lol) does not matter, and the statement **is true**.

### Biconditional (if and only if) \[$p \leftrightarrow q$\]

Let $p$ and $q$ be propositions. The biconditional statement of $p$ and $q$ is denoted by $p \leftrightarrow q$.

**Read as $p$ if and only if $q$**

_Shorthand:_ $p\; \mathrm{iff}\; q$

The truth value of $p \leftrightarrow q$ is true only when $p$ and $q$ have the same truth values, false otherwise.

| p   | q   | $p\leftrightarrow q$ |
| --- | --- | -------------------- |
| T   | T   | T                    |
| T   | F   | F                    |
| F   | T   | F                    |
| F   | F   | T                    |

**Example:**
"You can take the flight if and only if you have a ticket"
