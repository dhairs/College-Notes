**1. Consider the design of a system that supports virtualization. The system uses the Intel**

**Extended Page Table (EPT) to support virtualization. However, while the per process**

**page will use a variety of page sizes, the hypervisor allocates memory to the guest**

**operating systems in units of 2MB pages. Compute the possible number of memory**

**accesses upon a TLB miss (there are several possibilities)**

Key Components of Intel EPT :

- TLB (Translation Lookaside Buffer): Caches virtual-to-physical address mappings. A

miss means the system must walk through the page tables to determine the mapping.

- Paging Hierarchy: The EPT uses a 4-level hierarchical structure similar to the x86-64 paging hierarchy: PML4 (Page-Map Level 4) & PDPT (Page Directory Pointer T able) Page Directory (PD) Page Table (PT) 2MB Pages for Guest OS Memory Allocation: Indicates that the hypervisor uses 2MB pages for the guest OS’s physical memory. A 2MB page eliminates the need for the Page T able level, as the page directory entry directly maps to the 2MB page.

Address Translation Steps:

Guest Virtual Address → Guest Physical Address (via guest page tables)

Guest Physical Address → Host Physical Address (via EPT)

Access Calculation

On a TLB miss, the system must walk through the page table hierarchy. The number of memory

accesses depends on several factors:

4-Level Page T able Walk (EPT hierarchy):

1 access to the PML4 entry

1 access to the PDPT entry

1 access to the PD entry

1 access to the 2MB page or its associated data

T otal: 4 memory accesses.

Guest OS Page T able Walk: If the guest OS uses 4KB pages, the guest virtual address

translation involves a 4-level page walk within the guest's page tables. This requires:

1 access to the guest PML4 entry1 access to the guest PDPT entry

1 access to the guest PD entry

1 access to the guest page table entry

T otal: 4 memory accesses.

Combined Memory Accesses: Both the guest page table walk and the EPT walk must occur to

resolve the full translation:

Guest Virtual → Guest Physical (4 accesses)

Guest Physical → Host Physical (4 accesses)

T otal: 8 memory accesses in the worst-case scenario.

Possible Variations

TLB Caching: If intermediate levels (e.g., PML4 or PDPT entries) are cached, fewer memory accesses are needed.

Large Pages (1GB Pages): If large pages are used at any level, fewer levels are walked,

reducing memory accesses.

Summary of Possible Access Counts

Best Case: Only 4 accesses (if large pages are used in both guest and EPT).

**2. Under which failure type we can categorize a software bug?**

A software bug can be categorized under intermittent or repeatable failures because it typically arises from flaws or errors in the design, implementation, or configuration of the software.

**3. Consider the following code:**

**Suppose a temporary failure occurs at the iteration marked by i = 5, j = 6, such that the**

**multiplier produced a wrong result. What will be the impact of this error? What can be**

**done at the software level to detect and/or correct this error? Show your modification to**

**the code.**

**Impact of the Error**

1. **Immediate Impact**:

○ The computation for B[5][6] will be incorrect because one of the operands in the

equation was faulty.

○ The incorrect value of B[5][6] will propagate if B is used as input in subsequent

iterations or steps.

2. **Propagated Impact**:○ If B[i][j] is reused in later iterations (e.g., in iterative solvers or feedback loops),

the error can spread and amplify over time, leading to incorrect results across the

dataset.

**Software-Level Detection and Correction**

T o detect or correct the error at the software level, you can implement techniques like

**redundant computation**, **error checking**, or **self-correction**. Here are some strategies:

**1. Redundant Computation (Recompute and Compare)**

● Recompute the value of B[i][j] independently and compare it with the original result.

● If the values differ, an error is detected, and the recomputation can correct it.

**2. Error Bounds Check**

● If the values of B[i][j] are expected to lie within a certain range, any deviation beyond

this range could be flagged as an error.

**3. Majority Voting**

● Compute the value of B[i][j] multiple times (e.g., three times) and use the majority

result to ensure correctness.

**4. Modification**

for (i = 1; i < N; i++) {

for (j = 1; j < N; j++) {

// Compute B[i][j] normally

float original = A[i][j] + Delta * (A[i+1][j+1] + A[i+1][j-1] + A[i-1][j+1] + A[i-1][j-1]) / 4;

// Redundant computation

float redundant = A[i][j] + Delta * (A[i+1][j+1] + A[i+1][j-1] + A[i-1][j+1] + A[i-1][j-1]) / 4;

// Compare results and correct if necessary

if (fabs(original - redundant) > ERROR

_

B[i][j] = redundant; // Correct the error

THRESHOLD) {} else {

B[i][j] = original; // Use the original result

}

}

}

**Explanation of the Modifications**

1. **Error Detection**:

○ A redundant computation ensures that any temporary failure during the first

computation is identified by comparing the two results.

○ An acceptable threshold (ERROR_THRESHOLD) can account for floating-point

rounding errors.

2. **Error Correction**:

○ If a mismatch is detected, the redundant computation replaces the faulty result.

3. **Performance Impact**:

○ This approach doubles the computation time for B[i][j] but ensures

robustness against temporary errors.

**4. You are running a distributed two-phase commit protocol. A network partition occurs.**

**What should the software do?**

In a distributed system running a **Two-Phase Commit (2PC)** protocol, a **network partition**

presents a critical challenge because some participants (nodes) may lose connectivity to others,

potentially jeopardizing the agreement on whether to commit or abort a transaction.

When a network partition occurs during a 2PC protocol:

1. 2. In the **Prepare Phase**, abort the transaction if the coordinator cannot reach all

participants.

In the **Commit Phase**, participants in the prepared state should block until the partition

resolves and retry communication with the coordinator.3. Use persistent logs, timeouts, and potentially consensus protocols to handle recovery

and ensure consistency.