
Of course! Here is a detailed, easy-to-understand explanation of the slides on Splay Trees, with a special focus on breaking down the mathematical analysis.

---

## Introduction: What Are Splay Trees?

Balanced Binary Search Trees (BSTs), like Red-Black Trees, guarantee that fundamental operations like `insert`, `delete`, and `find` will take ![](data:,) time in the worst case1. This is generally very good.

However, in many real-world scenarios, access patterns aren't random. You might access a few specific items far more often than others. A standard balanced BST doesn't take advantage of this. A frequently accessed item could still be far from the root.

Splay Trees are a type of self-adjusting BST that optimize for this. The core idea is simple: **whenever you access a node, you move it to the root of the tree**2. The hope is that frequently accessed items will stay near the top, making subsequent lookups for them extremely fast. The specific method used to move the node to the root is called **splaying**.

---

## The Splay Operation

A simple "rotate-to-root" heuristic (repeatedly rotating an accessed node `x` with its parent until it becomes the root) can lead to poor performance on certain access sequences3. Splay trees use a more sophisticated set of rotations to avoid these bad cases. The splay operation consists of repeating one of three special double-rotation steps until the accessed node `x` is at or near the root.

### 1. Zig Step

This is the final step when the node to be splayed, `x`, is a direct child of the root.

- **Condition:** `x`'s parent is the root4.
    
- **Action:** Perform a single rotation at `x` to make it the new root.
    

### 2. Zig-Zag Step

This occurs when `x` and its parent `p` are "opposite" children (one is a right child, the other is a left child).

- **Condition:** `x` is a right child and its parent `p` is a left child (or vice-versa)5.
    
- **Action:** Perform two successive rotations at `x`. This is equivalent to the standard double rotation in an AVL tree6.
    

### 3. Zig-Zig Step

This occurs when `x` and its parent `p` are "aligned" children (both are left children or both are right children). **This is the crucial operation that distinguishes splay trees from the naive rotate-to-root heuristic**7.

- **Condition:** `x` and `p` are both left children (or both right children)8.
    
- **Action:** First, rotate the **parent `p`** with the grandparent `g`. Then, rotate **`x`** with its new parent `p`9. This has a different, more "balancing" effect than rotating `x` twice.
    

To perform a full **splay**, you just repeat these steps on the accessed node `x` until it becomes the root of the tree10.

---

## Dictionary Operations in a Splay Tree

All standard dictionary operations in a splay tree are built upon a normal BST operation followed by a splay.

- **Find:** Perform a regular BST search for a key. If the key is found at node `x`, splay `x` to the root. If the key is not found, the search ends at some node `y`; in this case, splay `y` to the root11.
    
- **Insert:** Perform a regular BST insert. The new node `x` is added as a leaf. Then, splay `x` to the root12121212.
    
- **Delete:**
    
    1. First, `find` the key to be deleted. This automatically splays its node, `x`, to the root13.
        
    2. Remove `x`. This splits the tree into two disconnected subtrees: a left subtree ![](data:,) (with all keys smaller than `x`) and a right subtree ![](data:,) (with all keys larger than `x`)14.
        
    3. Merge these two subtrees using a `join` operation15.
        
- **Join(![](data:,), ![](data:,)):** This helper operation merges two trees where all keys in ![](data:,) are less than all keys in ![](data:,)16. To do this, find the largest key in ![](data:,) (node `x`) and splay it to the root of ![](data:,)17. Since `x` is the maximum element, its new root node in ![](data:,) will have no right child. You can then simply make the root of ![](data:,) the right child of `x`18.
    

---

## Amortized Analysis: The Math Explained

A single splay tree operation can be expensive, potentially taking ![](data:,) time. However, an expensive operation also significantly restructures the tree, making subsequent operations cheaper. **Amortized analysis** is a technique to find the average cost per operation over a long sequence.

The analysis uses the **potential method**. Think of the tree as having a "potential energy" value, ![](data:,).

- If an operation is cheap and improves the tree structure, its potential increases (we "save up" credit).
    
- If an operation is expensive, it must cause a large drop in potential (we "spend" our saved credit).
    

The Amortized Cost is defined as:

![](data:,)

where ΔΦ is the change in potential (Φafter​−Φbefore​).

### Key Definitions

1. **Weight ![](data:,):** We assign an arbitrary positive weight to each node `x` in the tree19. This is a powerful tool for the proof; by choosing different weighting schemes, we can prove different properties of the tree.
    
2. **Size ![](data:,):** The size of a node is the sum of the weights of all nodes in the subtree rooted at `x` (including `x` itself)20.
    
3. **Rank ![](data:,):** The rank of a node is defined as ![](data:,)21.
    
4. **Potential ![](data:,):** The potential of the entire tree is the sum of the ranks of all its nodes: ![](data:,)22.
    

### Amortized Cost of Splay Steps

The goal is to show that the amortized cost of each splay step is small. The actual cost is the number of rotations (1 for zig, 2 for zig-zag and zig-zig). Let's use ![](data:,) and ![](data:,) for the rank and size _before_ a step, and ![](data:,) and ![](data:,) for the values _after_23232323.

#### A Crucial Mathematical Fact (Fact 1)

The proofs for the zig-zag and zig-zig steps rely on this inequality:

If x and y are positive numbers such that x+y≤1, then log2​(x)+log2​(y)≤−224.

- **Explanation:** The function ![](data:,) increases as ![](data:,) increases. The sum ![](data:,) is maximized when ![](data:,) is as large as possible, so we can assume ![](data:,)25. The expression becomes ![](data:,). The quadratic ![](data:,) has its maximum value of ![](data:,) when ![](data:,)26. Therefore, the maximum value of the sum is ![](data:,).
    

#### Cost of a Zig Step

- **Actual Cost:** 1 rotation.
    
- **Amortized Cost Goal:** Show it's at most ![](data:,)27.
    
- Analysis: The only nodes whose sizes change are x and its parent p. The change in potential is ΔΦ=(r′(x)+r′(p))−(r(x)+r(p)). After the rotation, x takes p's old position, so its new size is p's old size. Thus, s′(x)=s(p), which means r′(x)=r(p)28. The change in potential simplifies to ΔΦ=r′(p)−r(x). Since the new parent p is now a child of x, its new size must be smaller, so r′(p)≤r′(x)29. This gives us ΔΦ≤r′(x)−r(x).
    
    The amortized cost is 1+ΔΦ≤1+r′(x)−r(x). This is bounded by the goal expression 3(r′(x)−r(x))+1 since r′(x)≥r(x)30.
    

#### Cost of a Zig-Zag Step

- **Actual Cost:** 2 rotations.
    
- **Amortized Cost Goal:** Show it's at most ![](data:,)31.
    
- Analysis: We need to prove 2+ΔΦ≤3(r′(x)−r(x))32. After a zig-zag, the new x occupies the spot of its old grandparent g, so s′(x)=s(g), which means r′(x)=r(g)33. The nodes whose sizes change are x, p, and g.
    
    The inequality becomes 2+(r′(x)+r′(p)+r′(g))−(r(x)+r(p)+r(g))≤3(r′(x)−r(x)).
    
    After substituting r′(x)=r(g) and rearranging, the slide shows this is equivalent to proving:
    
    ![](data:,)
    
    34
    
    - **Analyzing Part A:** Let's look at the sizes. The subtrees rooted at the new `p` and new `g` are contained within the new subtree of `x`, so ![](data:,)35. Dividing by ![](data:,) gives ![](data:,). Part A is ![](data:,). By **Fact 1**, this sum is ![](data:,)36.
        
    - Analyzing Part B: We need to show that −r(p)−r′(x)+2r(x)≤0. This is true because x was in p's subtree, so s(x)≤s(p), which means r(x)≤r(p)37. Also, after the splay step, x moves up the tree, so its size increases: s(x)≤s′(x), meaning r(x)≤r′(x)38. So we are subtracting two larger numbers from two smaller numbers, which is ≤0.
        
        Since Part A is ≤−2 and Part B is ≤0, their sum is ≤−2, and the inequality holds.
        

#### Cost of a Zig-Zig Step

- **Actual Cost:** 2 rotations.
    
- **Amortized Cost Goal:** Show it's at most ![](data:,)39.
    
- Analysis: The proof structure is very similar to the zig-zag step. We need to prove 2+ΔΦ≤3(r′(x)−r(x))40. The slide rearranges this into a different form:
    
    ![](data:,)
    
    41
    
    - **Analyzing Part C:** Let's look at the sizes. The old subtree of `x` and the new subtree of `g` are disjoint and contained within the new subtree of `x`. So ![](data:,)42. Dividing by ![](data:,) gives ![](data:,). Part C is ![](data:,). By **Fact 1**, this sum is ![](data:,)43.
        
    - Analyzing Part D: We need to show r′(p)−r(p)−r′(x)+r(x)≤0. This holds because r(p)≥r(x) (parent is larger than child) and r′(x)≥r′(p) (new parent is smaller than new root)44. Again, the term is ≤0.
        
        Since Part C is ≤−2 and Part D is ≤0, the inequality holds.
        

### Main Technical Lemma

Summing up the amortized costs of all the steps in a splay operation results in a telescoping sum (intermediate terms cancel out). This leads to the main result:

**Lemma 1:** The amortized cost of a splay operation at node `x` is at most ![](data:,), where `t` is the root of the tree _before_ the splay45.

---

## Performance Results (The Payoff)

This lemma allows us to prove several powerful theorems about splay tree performance simply by choosing clever node weights.

### Worst-Case Amortized Performance

Let's set the weight of every node to 146.

- The size ![](data:,) is just the number of nodes in `x`'s subtree.
    
- The size of the root `t` is `n`, so its rank is ![](data:,)47.
    
- The rank of any node `x`, ![](data:,), is non-negative.
    
- Plugging this into Lemma 1, the amortized cost of any splay operation is ![](data:,), which is ![](data:,).
    
- **Conclusion:** Over a sequence of operations, splay trees perform on par with other balanced BSTs like red-black trees48.
    

### Static Optimality Theorem

This is one of the most remarkable results. It states that if you have a sequence of `m` `find` operations where key ![](data:,) is accessed ![](data:,) times, the total cost for the splay tree is ![](data:,)49. This is asymptotically the same as the cost of the _best possible static BST_ you could have built if you knew the access frequencies in advance50.

- **Proof Sketch:** Set the weight of each node ![](data:,) to its access frequency, ![](data:,)51.
    
- The total weight of all nodes in the tree is ![](data:,). So the size of the root is ![](data:,), and its rank is ![](data:,)52.
    
- The size of any node ![](data:,) is at least its own weight, so ![](data:,). This means its rank ![](data:,)53.
    
- Plugging into Lemma 1, the amortized cost of accessing ![](data:,) is ![](data:,)54.
    
- The total cost is the sum of these amortized costs over all `m` accesses, which gives the desired bound.
    

### Working-Set and Sequential Access Theorems

- **Working-Set Theorem:** This theorem shows that splay trees have good **locality of reference**. If you access an item that you have accessed recently, the operation will be cheap. The cost depends on ![](data:,), the number of _distinct_ items accessed since the last access to the current item55. The total cost is bounded by a term involving ![](data:,)56. If ![](data:,) is small, the cost is low.
    
- **Sequential Access Theorem:** A direct consequence of the working-set property. If you access all `n` items in sorted order (![](data:,)), the total cost is only ![](data:,)57. This means each access takes, on average, constant time!
    

### Dynamic Optimality Conjecture

This is a famous open problem in computer science. It conjectures that splay trees are, to within a constant factor, as good as _any possible_ BST-based algorithm for any sequence of accesses58. If true, it would mean that in a very fundamental sense, splay trees are the "best possible" self-adjusting binary search tree.