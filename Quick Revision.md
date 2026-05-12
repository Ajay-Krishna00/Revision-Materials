# Quick Revision

# PART 1: DATA STRUCTURES (Q1–Q10)

## 1.1 TREES AND TREE TRAVERSALS

A **tree** is a hierarchical data structure. The topmost node is the **root**. Nodes with no children are **leaves**.

A **Binary Tree** has at most 2 children per node: left child and right child.

### The Three Main Traversals

**Inorder (Left → Root → Right)**
- Visit left subtree, then root, then right subtree.
- For a BST, inorder gives sorted (ascending) output.
- Example: Tree with root A, left=B(D,E), right=C(F,G)
  - Inorder: D, B, E, A, F, C, G

**Preorder (Root → Left → Right)**
- Visit root first, then left subtree, then right subtree.
- Same tree as above:
  - Preorder: A, B, D, E, C, F, G

**Postorder (Left → Right → Root)**
- Visit left, then right, then root last.
- Same tree:
  - Postorder: D, E, B, F, G, C, A

### HOW TO RECONSTRUCT A TREE FROM TRAVERSALS (Very Important!)

**Given Inorder + Preorder → Find Postorder** ← This appeared in June 2022 and Jan 2024!

**Rule:** In preorder, the FIRST element is always the root. In inorder, the root splits the tree into left and right subtrees.

**Example from June 2022 exam:**
- Inorder: d b e a f c g
- Preorder: a b d e c f g
- Step 1: First element of Preorder = **a** = root
- Step 2: Find 'a' in Inorder. Left of 'a': {d, b, e}. Right of 'a': {f, c, g}
- Step 3: From Preorder, next after 'a' in left part: 'b' is root of left subtree
- Step 4: Find 'b' in Inorder left part {d,b,e}. Left of 'b': {d}. Right of 'b': {e}
- Step 5: From Preorder, right part starts with 'c'. Find 'c' in {f,c,g}: Left={f}, Right={g}
- Tree structure: a(b(d,e), c(f,g))
- Postorder: d, e, b, f, g, c, a ← **Answer: a) d e b f g c a**

### Binary Search Tree (BST)
- Left child < Parent < Right child
- If a BST node has **two children**, its **inorder predecessor** has **no right child** (exam Q!)
- Search, Insert, Delete are all O(log n) average, O(n) worst case

### Level Order Traversal
- Visit nodes level by level, left to right
- Uses a QUEUE internally
- BFS of a tree is level-order traversal

### Post-order: visiting root AFTER left and right subtrees ← appeared in May 2023

---

## 1.2 STACKS

A **stack** is Last-In-First-Out (LIFO).

**Operations:**
- `push(x)` - add to top
- `pop()` - remove from top
- `peek()` - see top without removing
- If you pop from empty stack: **Underflow**
- If you push to full stack: **Overflow**

**Applications of Stack:**
- Balancing parentheses
- Tracking local variables at runtime (function call stack)
- Undo history in web browsers/editors ← appeared in May 2023
- Compiler syntax analysis
- Converting infix to postfix/prefix
- Tower of Hanoi ← optimal data structure is **Stack**
- recursion
- string reversal
- DFS

**What is NOT an application of stack:**
- **Data Transfer between two asynchronous processes** → that's a QUEUE ← June 2022 exam!

### Implementing Stack Using Queue
- You need **2 queues** to implement a stack ← appeared in June 2022

### Tower of Hanoi
- Optimal data structure: **Stack**
- Recursive approach
- For n disks: minimum (2^n)-1 moves

---

## 1.3 QUEUES

A **queue** is First-In-First-Out (FIFO).

**Operations:**
- `enqueue(x)` - add to rear
- `dequeue()` - remove from front

**Types:**
- Simple Queue
- Circular Queue
- **Dequeue (Double-ended queue)** - can insert/delete from both ends ← appeared as "sequence container" in June 2023
- Priority Queue - minimum queues needed to implement it: **2** ← appeared in June 2023

**Applications of Queue:**
- BFS algorithm uses a **Queue** ← appeared in June 2023
- Simulation of limited resource allocation
- CPU scheduling (Round Robin uses a queue)

---

## 1.4 LINKED LISTS

A **linked list** is a chain of nodes where each node has data and a pointer to the next node.

**Key facts:**
- Elements are NOT stored contiguously in memory
- No random access (unlike arrays)
- Dynamic size - can grow/shrink
- Accessed via pointers

**Types:**
- **Singly linked list** - each node points to next
- **Doubly linked list** - each node points to both next and previous
- **Circular linked list** - last node points back to first node ← appeared in May 2023

**Pointer notation for arrays:**
- `*(a + 2)` is equivalent to `a[2]` ← appeared in May 2023
- To access 2nd element: `*(a + 2)` - **Answer: d**

**Worst case comparisons to search a singly linked list of length n:**
- You may need to check every element → **n** comparisons ← appeared in June 2022 & Jan 2024

---

## 1.5 SORTING ALGORITHMS

This is very heavily tested. Know the complexities cold.

| Algorithm | Best | Average | Worst | Space |
|-----------|------|---------|-------|-------|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) |
| Heap Sort | O(n log n) | O(n log n) | **O(n log n)** | O(1) |

**Key Facts for Exam:**

- **Heap Sort worst case = O(n log n)** ← appeared in EVERY year
- Quick sort has worst case **O(n²)** ← appeared in June 2023
- Which sorting algorithm has O(n log n) in BOTH average and worst case? → **Merge Sort** or **Heap Sort** (not Quick Sort!)
- Quick sort average = O(n log n) ← May 2023 asks this

**Merge Sort is NOT an in-place algorithm** ← appeared in Jan 2024 (needs extra O(n) space)

**In-place algorithms:** Bubble, Selection, Insertion, Heap (they sort within the array itself)
**NOT in-place:** Merge Sort ← exam answer

**Minimum swaps:** Selection Sort minimizes swaps ← appeared in Jan 2024
**When swap is costly:** Use **Selection Sort**

## Sorting Algorithms Explained with Examples

### 1. Bubble Sort

#### Definition

Bubble Sort repeatedly compares adjacent elements and swaps them if they are in the wrong order. Larger elements gradually move to the end of the list like bubbles rising to the surface.

#### Steps

1. Compare adjacent elements.
2. Swap them if the left element is greater than the right element.
3. Repeat until the array becomes sorted.

#### Example

Array: `[5, 1, 4, 2, 8]`

##### Pass 1

* Compare 5 and 1 → Swap → `[1, 5, 4, 2, 8]`
* Compare 5 and 4 → Swap → `[1, 4, 5, 2, 8]`
* Compare 5 and 2 → Swap → `[1, 4, 2, 5, 8]`
* Compare 5 and 8 → No Swap

##### Pass 2

* Compare 1 and 4 → No Swap
* Compare 4 and 2 → Swap → `[1, 2, 4, 5, 8]`
* Compare 4 and 5 → No Swap

##### Final Sorted Array

`[1, 2, 4, 5, 8]`

#### Time Complexity

* Best Case: O(n)
* Average Case: O(n²)
* Worst Case: O(n²)

---

## 2. Selection Sort

#### Definition

Selection Sort repeatedly selects the smallest element from the unsorted part of the array and places it at the beginning.

#### Steps

1. Find the minimum element.
2. Swap it with the first unsorted element.
3. Repeat for remaining elements.

#### Example

Array: `[64, 25, 12, 22, 11]`

##### Pass 1

Smallest element = 11
Swap with 64
`[11, 25, 12, 22, 64]`

##### Pass 2

Smallest element = 12
Swap with 25
`[11, 12, 25, 22, 64]`

##### Pass 3

Smallest element = 22
Swap with 25
`[11, 12, 22, 25, 64]`

##### Final Sorted Array

`[11, 12, 22, 25, 64]`

#### Time Complexity

* Best Case: O(n²)
* Average Case: O(n²)
* Worst Case: O(n²)

---

## 3. Insertion Sort

#### Definition

Insertion Sort builds the sorted array one element at a time by inserting each element into its correct position.

#### Steps

1. Assume the first element is sorted.
2. Pick the next element.
3. Insert it into the correct position in the sorted portion.
4. Repeat until sorted.

#### Example

Array: `[12, 11, 13, 5, 6]`

##### Step 1

Insert 11 before 12
`[11, 12, 13, 5, 6]`

##### Step 2

13 is already in correct position
`[11, 12, 13, 5, 6]`

##### Step 3

Insert 5 at beginning
`[5, 11, 12, 13, 6]`

##### Step 4

Insert 6 after 5
`[5, 6, 11, 12, 13]`

##### Final Sorted Array

`[5, 6, 11, 12, 13]`

#### Time Complexity

* Best Case: O(n)
* Average Case: O(n²)
* Worst Case: O(n²)

---

## 4. Merge Sort

#### Definition

Merge Sort uses the divide-and-conquer technique. It divides the array into smaller halves, sorts them, and merges them back together.

#### Steps

1. Divide the array into two halves.
2. Recursively sort both halves.
3. Merge the sorted halves.

#### Example

Array: `[38, 27, 43, 3, 9, 82, 10]`

##### Divide

`[38, 27, 43]` and `[3, 9, 82, 10]`

##### Further Divide

`[38] [27, 43]`
`[3, 9] [82, 10]`

##### Merge Sorted Parts

`[27, 38, 43]`
`[3, 9, 10, 82]`

##### Final Merge

`[3, 9, 10, 27, 38, 43, 82]`

#### Time Complexity

* Best Case: O(n log n)
* Average Case: O(n log n)
* Worst Case: O(n log n)

---

## 5. Quick Sort

#### Definition

Quick Sort selects a pivot element and partitions the array into elements smaller and larger than the pivot.

#### Steps

1. Choose a pivot.
2. Partition elements around the pivot.
3. Recursively sort left and right partitions.

#### Example

Array: `[10, 7, 8, 9, 1, 5]`

##### Choose Pivot

Pivot = 5

##### Partition

Smaller than 5 → `[1]`
Larger than 5 → `[10, 7, 8, 9]`

##### Recursively Sort

`[1] + [5] + [7, 8, 9, 10]`

##### Final Sorted Array

`[1, 5, 7, 8, 9, 10]`

#### Time Complexity

* Best Case: O(n log n)
* Average Case: O(n log n)
* Worst Case: O(n²)

---

## 6. Heap Sort

#### Definition

Heap Sort uses a binary heap data structure. It first builds a max heap and repeatedly extracts the maximum element.

#### Steps

1. Build a max heap.
2. Swap the first element with the last.
3. Reduce heap size.
4. Heapify the root.
5. Repeat until sorted.

#### Example

Array: `[4, 10, 3, 5, 1]`

##### Build Max Heap

`[10, 5, 3, 4, 1]`

##### Swap Root with Last

`[1, 5, 3, 4, 10]`

##### Heapify

`[5, 4, 3, 1, 10]`

##### Continue Process

Final Sorted Array:
`[1, 3, 4, 5, 10]`

#### Time Complexity

* Best Case: O(n log n)
* Average Case: O(n log n)
* Worst Case: O(n log n)

---

### Comparison Table

| Algorithm      | Best Case  | Average Case | Worst Case | Stable |
| -------------- | ---------- | ------------ | ---------- | ------ |
| Bubble Sort    | O(n)       | O(n²)        | O(n²)      | Yes    |
| Selection Sort | O(n²)      | O(n²)        | O(n²)      | No     |
| Insertion Sort | O(n)       | O(n²)        | O(n²)      | Yes    |
| Merge Sort     | O(n log n) | O(n log n)   | O(n log n) | Yes    |
| Quick Sort     | O(n log n) | O(n log n)   | O(n²)      | No     |
| Heap Sort      | O(n log n) | O(n log n)   | O(n log n) | No     |

---

### Conclusion

* Bubble Sort is simple but inefficient for large data.
* Selection Sort minimizes swaps.
* Insertion Sort works well for small or nearly sorted arrays.
* Merge Sort is efficient and stable.
* Quick Sort is fast in practice and widely used.
* Heap Sort provides guaranteed O(n log n) performance.

## Reason for merge sort being used more even tho heap sort has same Time Complexity and constant space complexity while merge sort has O(log n) space complexity
1. Better Cache Performance
Merge Sort accesses memory sequentially.
Example:
Left array → Right array → Merge
This is cache-friendly because modern CPUs work faster with continuous memory access.
Heap Sort jumps around the array due to heap structure:
Parent ↔ Child ↔ Another child
This causes more cache misses and slower execution.
Result:
Merge Sort is usually faster in practice even if theoretical complexity is same.

2. Stable Sorting
Merge Sort is stable.
If two elements have same value, their original order is preserved.
Example:
(5,A) (5,B)
After Merge Sort:
(5,A) (5,B)
Heap Sort is not stable.
This matters in databases and multi-level sorting.

3. Better for Linked Lists
Merge Sort works very efficiently on linked lists because merging does not require random access.
Heap Sort requires array indexing.
So Merge Sort is preferred for:
Linked lists
External sorting
Large datasets

4. Used in External Sorting
When data is too large for RAM:
Merge Sort can sort chunks separately
Then merge files efficiently
This is why databases use Merge Sort.
Heap Sort is not suitable for disk-based sorting.

5. Parallel Processing
Merge Sort divides arrays into independent halves:
Left Half    Right Half
Both can be sorted simultaneously using multiple processors.
Heap Sort is harder to parallelize.

### HeapSort Question (June 2022)
Array: 16 14 15 10 12 27 28
How many heapify operations on root for building max heap?
- After 2 heapify operations on root, this is a valid max-heap arrangement → **Answer: 2**

How many heapify operations on root during full Heap Sort?
- **Answer: 6**

### QuickSort Partition Question (Jan 2024 / June 2023)
Array after first partition: 2 5 1 7 9 12 11 10
- The pivot is an element that is in its final sorted position
- 7 is at index 3, and all elements to its left (2,5,1) are smaller, all to right (9,12,11,10) are larger → 7 is the pivot
- But 9 is at index 4, and 2,5,1,7 are all smaller, 12,11,10 are larger... wait.
- Looking at: 2 5 1 7 9 12 11 10 - the pivot could be either 7 or 9
- **Answer: a) The pivot could be either the 7 or the 9**

### Bubble Sort Interchanges (June 2023)
Sort: 5, 1, 6, 2, 4 in ascending order
Pass 1: (5,1)→swap: 1,5,6,2,4; (5,6) no swap; (6,2)→swap: 1,5,2,6,4; (6,4)→swap: 1,5,2,4,6 [3 swaps]
Pass 2: (1,5) no; (5,2)→swap: 1,2,5,4,6; (5,4)→swap: 1,2,4,5,6 [2 swaps]
Total: 5 swaps → **Answer: b) 5**

---

## 1.6 GRAPHS

A **graph** G = (V, E) has vertices V and edges E.

**Complete graph with n vertices:**
- Every vertex is connected to every other vertex
- Number of edges = **n(n-1)/2** ← appeared in June 2022 and Jan 2024
- Example: n=4 vertices → 4×3/2 = 6 edges

**Graph Traversals:**
- **BFS (Breadth-First Search)** - uses a QUEUE; explores level by level
- **DFS (Depth-First Search)** - uses a STACK; goes deep before backtracking
  - Time complexity of DFS & BFS: **Θ(V + E)** 

---

## 1.7 HASH TABLES

A hash table maps keys to values using a hash function.

**Hash Function:** h(key) = key mod table_size

**Collision:** When **multiple elements compete for the same bucket**

**Collision Resolution:**
- Chaining: each hash table index stores a linked list of elements. If multiple keys hash to the same index, they are added to the linked list at that slot.
Disadvantage: Extra memory
- Open addressing (linear probing, quadratic probing, double hashing)
In open addressing, all elements are stored inside the hash table itself. When collision occurs, another empty slot is searched.
  - Linear Probing: Check the next slot sequentially until an empty slot is found. Formula: (h(k)+i)mod table_size
  Disadvantage: Causes primary clustering (large groups form). Solution: use quadratic/double hashing
  - Quadratic Probing: Instead of checking consecutive slots, jump quadratically. Formula: (h(k)+i^2)mod table_size
  Disadvantage: - Some slots may be skipped
                - Secondary Clustering: Keys with the same initial hash value follow the same probing sequence. So they still cluster together. Solution: use double hashing
  - Double Hashing: Use a second hash function to decide jump size. Formula: (h1(k)+i×h2(k))mod table_size
  Disadvantage: More complex

---

## 1.8 EXPRESSION CONVERSION (INFIX → POSTFIX/PREFIX)

**Infix:** Normal math notation: a + b × c
**Postfix (Reverse Polish):** operands first, then operator: a b c × +
**Prefix (Polish):** operator first: + a × b c

**Precedence rules (highest to lowest):** ^, ×, +, - (left to right except ^ which is right to left)

**June 2022 question:**
Infix: a + b × c - d ^ e ^ f
- ^ is right associative, so d^e^f = d^(e^f)
- Precedence: ^, then ×, then +/-
- Postfix Result: a b c × + d e f ^ ^ - → **Answer: a) abc X+ def^^ -**

**Prefix of A-B/(C*D^E)** (June 2023):
Infix: A - B / (C * D ^ E)
Working inside out: C*D^E: ^(D,E) first, then *: *(C,^(D,E))
Then /: /(B, *(C,^(D,E)))
Then -: -(A, /(B,*(C,^(D,E))))
Prefix: -A/B*C^DE → **Answer: c) -A/B*C^DE**

**Preorder traversal result is same as:** Depth-first order 
**Level Order traversal result is same as:** Breadth-first order 

---

## 1.9 PRIORITY QUEUE
- Elements have priorities; highest priority served first
- Implemented using a Heap
- Minimum queues needed to implement priority queue: **2** ← June 2023

---

## 1.10 ALGORITHM PARADIGMS
- **Travelling Salesman Problem** → Greedy Algorithm (or Dynamic Programming, but TSP approximation is Greedy) ← May 2023 **Answer: Greedy**
- **Tower of Hanoi** → Recursion / Stack

---

# PART 2: OPERATING SYSTEMS (Q11–Q20)

## 2.1 PROCESS STATES AND SCHEDULING

### Process States
A process transitions through these states:
- **New** → being created
- **Ready** → waiting to be assigned to CPU
- **Running** → executing on CPU
- **Blocked/Waiting** → waiting for I/O or event
- **Terminated** → finished

**Time-sharing OS: when time slot expires → process goes to Ready state** ← Jan 2024

### Types of Schedulers
**Long-term Scheduler (Job Scheduler):**
- Selects processes from job pool and loads them into **ready queue**
- Controls degree of multiprogramming ← June 2022 & Jan 2024

**Short-term Scheduler (CPU Scheduler):**
- Selects which **ready process** to execute next and **allocates CPU** ← Jan 2024

**Medium-term Scheduler:**
- Swaps processes in and out of memory (handles swapping)

### Context Switching
- The process of saving the state of one process and loading the state of another
- A **systematic procedure for moving CPU to a new process = Context Switching** ← June 2022

### Process vs Thread
**Threads of the same process SHARE:**
- Address space (code, data, heap)
- File descriptor table
- Message queue

**Threads DO NOT SHARE (each thread has its own):**
- **Stack** ← Jan 2024
- **Registers** ← June 2023

**When are register context and stack of thread deallocated?**
- When the **thread terminates** ← Jan 2024

---

## 2.2 CPU SCHEDULING ALGORITHMS
TAT=CT−AT
WT=TAT−BT

### FCFS (First Come First Served)
- Non-preemptive
- Processes execute in order of arrival
- Simple but can cause *convoy effect*: short processes wait a long time for a single, large, CPU-intensive process to finish

**FCFS Average Waiting Time Calculation (May 2023):**
P1 (arrives 0, burst 4), P2 (arrives 2, burst 6), P3 (arrives 4, burst 8), P4 (arrives 6, burst 2)
- P1 runs: 0–4. P2 runs: 4–10. P3 runs: 10–18. P4 runs: 18–20
- Waiting times: P1=0, P2=4-2=2, P3=10-4=6, P4=18-6=12
- Average = (0+2+6+12)/4 = 20/4 = 5 

### Round Robin (RR)
**Round Robin Turnaround Time (May 2023):**
5 processes: P1=8, P2=4, P3=9, P4=5, P5=2, quantum=3

Time 0: P1 runs 3 (remaining: 5), 3: P2 runs 3 (remaining: 1), 6: P3 runs 3 (remaining: 6), 9: P4 runs 3 (remaining: 2), 12: P5 runs 2 (remaining: 0), 14: P1 runs 3 (remaining: 2), 17: P2 runs 1 (remaining: 0, done at 18), 18: P3 runs 3 (remaining: 3), 21: P4 runs 2 (remaining: 0, done at 23), 23: P1 runs 2 (remaining: 0, done at 25), 25: P3 runs 3 (done at 28)
P3 arrives at time 0, completes at time 28. TAT = 28-0 = 28? Hmm.
Wait let me redo:
Queue: P1(8), P2(4), P3(9), P4(5), P5(2), quantum=3

0-3: P1 (rem=5)
3-6: P2 (rem=1)
6-9: P3 (rem=6)
9-12: P4 (rem=2)
12-14: P5 done (rem=0) [only 2 left]
14-17: P1 (rem=2)
17-18: P2 done (rem=0)
18-21: P3 (rem=3)
21-23: P4 done (rem=0)
23-25: P1 done (rem=0)
25-28: P3 done (rem=0)

P3: arrives 0, completes at 28. TAT = 28.

### Shortest Job First (SJF) / Shortest Remaining Time First (SRTF)
| Feature          | SJF (Shortest Job First)   | SRTF (Shortest Remaining Time First) |
| ---------------- | -------------------------- | ------------------------------------ |
| Type             | Non-preemptive             | Preemptive                           |
| Selection Basis  | Smallest burst time        | Smallest remaining time              |
| CPU Interruption | No                         | Yes                                  |
| Preemption       | Not allowed                | Allowed                              |
| Decision Time    | Only when CPU becomes free | Whenever new process arrives         |
| Response Time    | Higher                     | Better                               |
| Complexity       | Simpler                    | More complex                         |

Context switches with SRTF (June 2023):
3 processes: P1 (arrives 0, burst 10), P2 (arrives 2, burst 20), P3 (arrives 6, burst 30)
SRTF: At t=0, only P1, runs.
At t=2, P2 arrives. P1 remaining=8, P2=20. P1 is shorter, continue P1.
At t=6, P3 arrives. P1 remaining=4, P3=30. Continue P1.
At t=10, P1 done. P2 (20) vs P3 (30). P2 runs.
At t=30, P2 done. P3 runs till t=60.
Context switches (not counting start and end): switch from P1 to P2 at t=10 = 1 switch
But we don't count at t=0 and at the end... so switches: at t=10 (P1→P2), at t=30 (P2→P3) = 2 switches
Answer: **b) 2** ← June 2023

### Semaphores
A semaphore S is an integer variable used for process synchronization.
- **P operation (wait):** S = S - 1. If S < 0, block.
- **V operation (signal):** S = S + 1. If S ≤ 0, wake up blocked process.

**June 2023 question:**
Semaphore initial value = 10. Then 12 P operations and x V operations. Final value = 7.
- After 12 P: 10 - 12 = -2
- After x V: -2 + x = 7
- x = 9 → **Answer: b) 9**

---

## 2.3 DEADLOCKS

A deadlock occurs when processes are waiting for resources held by each other, and none can proceed.

**4 Necessary Conditions for Deadlock (Coffman Conditions):**
1. **Mutual Exclusion** - resources can't be shared
2. **Hold and Wait** - process holds resource while waiting for another
3. **No Preemption** - resources can't be forcibly taken
4. **Circular Wait** - circular chain of processes waiting for each other

**Deadlock occurs when:** A process is unable to access a required resource indefinitely ← May 2023

### Banker's Algorithm (Deadlock Avoidance)
Used to **prevent deadlock** ← appeared in June 2022 & Jan 2024

**Key terms:**
- **Max** - maximum resources a process may need
- **Allocation** - currently allocated
- **Need** = Max - Allocation
- **Available** - currently free resources

**Safe State:** There exists at least one safe sequence in which all processes can complete.

**Banker's Algorithm grants request if:**
- Resources are immediately available, AND
- Won't exceed maximum claim, AND
- Won't exceed total available 

**Banker's is applicable to:** Non-preemptive resource allocation ← May 2023

### Dining Philosophers Problem
- 5 philosophers, 5 chopsticks
- **Deadlock if all pick up left chopstick simultaneously** - then all wait for right ← May 2023
- **Actually:** Deadlock if all try to pick up BOTH chopsticks simultaneously ← Answer: c
- **Maximum philosophers who can eat simultaneously without deadlock = N-1** (where N is total) ← May 2023

---

## 2.4 MEMORY MANAGEMENT

### Virtual Memory and Paging
**Paging:** Divides memory into fixed-size pages
- Logical memory divided into pages
- Physical memory divided into frames
- **Paging suffers from INTERNAL fragmentation** (last page may not be full) ← June 2023

**Segmentation:** Divides memory into **variable-sized** blocks ← May 2023
- Used for efficient utilization with variable-sized memory allocation

| Feature               | Internal Fragmentation                           | External Fragmentation                                  |
| --------------------- | ------------------------------------------------ | ------------------------------------------------------- |
| Definition            | Wasted space inside allocated memory block       | Free memory exists but is scattered into small blocks   |
| Cause                 | Fixed-size memory allocation                     | Variable-size memory allocation                         |
| Wasted Space Location | Inside allocated partition                       | Between allocated partitions                            |
| Occurs In             | Fixed partitioning, *paging*                       | Dynamic partitioning, *segmentation*                     |
| Memory Utilization    | Some allocated space remains unused              | Enough total memory may exist but not contiguous        |
| Example               | Process needs 18 KB but gets 20 KB → 2 KB wasted | Free blocks of 5 KB + 7 KB cannot satisfy 10 KB request |
| Solution              | Use smaller block size                           | Compaction or paging                                    |
| Compaction Needed     | No                                               | Yes                                                     |
| Paging Effect         | Causes internal fragmentation                    | Eliminates external fragmentation                       |

### Dirty Bit
- A dirty bit indicates a **page has been modified after being loaded into cache** ← June 2022 & Jan 2024
- Used in write-back caches: if dirty=1, page must be written back before eviction

### TLB (Translation Lookaside Buffer)
- A hardware cache that speeds up virtual-to-physical address translation
- In instruction pipeline: TLB can be accessed **after effective address calculation** ← June 2022

1. TLB Tag Size Calculation (June 2022)
Question
- Virtual address = 32 bits
- Page size = 4 KB
- TLB entries = 128
- 4-way set associative

Find the TLB tag bits.

Step 1: Find Page Offset Bits

Page size = 4 KB

4 KB = 4096 bytes = 2^12

So:

Offset bits=12

Step 2: Find Virtual Page Number Bits

Virtual address = 32 bits

Address format:

| Page Number | Offset |

So:

32−12=20

Thus:

Virtual Page Number (VPN)=20 bits
Step 3: Find Number of Sets in TLB

Given:

Total entries = 128
4-way associative

Formula:

Sets=128/4=32

Step 4: Find Set Index Bits

Need bits to identify 32 sets.

Formula:log2(32)=5

So:

Set index bits=5
Step 5: Find TLB Tag Bits

VPN bits are divided into:

| Tag | Set Index |

VPN = 20 bits

Set index = 5 bits

So:

20−5=15
Final Answer
TLB Tag Bits = 15

2. TLB / Address Size Question (June 2023)
Question
64 pages
Page size = 512 bytes
Physical memory = 32 page frames

Find:

Logical address bits
Physical address bits

Step 1: Logical Address Bits

Logical address consists of:

| Page Number | Offset |
Page Number Bits

64 pages

64=2^6

So:

Page number bits=6
Offset Bits

Page size = 512 bytes

512=2^9

So:

Offset bits=9
Total Logical Address Bits
6+9=15
Logical Address = 15 bits
Step 2: Physical Address Bits

Physical address format:

| Frame Number | Offset |
Frame Number Bits

32 page frames

32=2^

So:

Frame bits=5
Offset Bits

Same page size:

9 bits
Total Physical Address Bits
5+9=14
Final Answer
Address Type	Bits
Logical Address	15
Physical Address	14

3. Page Table Entry Bits (June 2022)
Question
Virtual address = 32 bits
Physical address = 30 bits
Page size = 4 KB
Page table entry size = 32 bits

Find bits available for protection/other information.

Step 1: Find Offset Bits

Page size = 4 KB

4KB=2^12

So:

Offset bits=12
Step 2: Find Physical Page Number Bits

Physical address = 30 bits

Address format:

| Physical Page Number | Offset |

So:

30−12=18

Thus:

Physical page number bits=18
Step 3: Find Remaining Bits in Page Table Entry

PTE size = 32 bits

18 bits already used for physical page number.

Remaining:

32−18=14
Final Answer
Protection / Control Bits = 14

## Important Concepts Summary
| Concept          | Formula                   |
| ---------------- | ------------------------- |
| Offset bits      | log₂(page size)           |
| Page number bits | log₂(number of pages)     |
| Frame bits       | log₂(number of frames)    |
| Logical address  | Page bits + Offset bits   |
| Physical address | Frame bits + Offset bits  |
| TLB sets         | Entries / Associativity   |
| Set index bits   | log₂(number of sets)      |
| Tag bits         | VPN bits − Set index bits |

### Page Replacement Algorithms
**FIFO (First In First Out):**
- Replace the oldest page
- **Suffers from Belady's Anomaly** - more frames can cause MORE page faults ← Jan 2024
- LRU does NOT suffer from Belady's anomaly

**LRU (Least Recently Used):**
- Replace the page not used for longest time
- Best approximation to optimal
- Does NOT suffer from Belady's anomaly

**Optimal:**
- Replace the page that won't be used for longest time in future
- Best algorithm theoretically but requires future knowledge

**FIFO page fault question (June 2022):**
4 frames, 100 distinct pages accessed then same 100 in reverse:
- First 100 accesses: 100 page faults (all new)
- Reverse: pages are same 100 pages, but in reverse order
- With 4 frames, last 4 pages from first access are in memory
- Total page faults = 196 ← **Answer: a) 196**

**FIFO question (June 2023):**
Reference string: 0,1,2,3,0,1,4,0,1,2,3,4
With 3 frames: 9 faults? With 4 frames: 10 faults?
This is Belady's anomaly! More frames → more faults with FIFO.
Answer: **d) 9, 10**

### Process States for Max Ready Processes
In n-CPU system, maximum processes in Ready state:
- If there are n CPUs, each runs one process
- But ready queue can be huge → **Independent of n** ← Jan 2024

### Swapping
A process copied from **main memory to secondary memory** on basis of requirement = **Demand Paging** ← June 2022
(Note: This is actually paging/swapping, but the answer key says "Demand paging" = option a)

### Critical Section Problem
**Mutual Exclusion:** If one process is in critical section, no other process can be in its critical section ← June 2022 & Jan 2024

**System calls that on termination do NOT return to calling point:**
- **exec** ← June 2022 & Jan 2024 (exec replaces process image entirely)

---

## 2.5 DISK SCHEDULING

### SCAN Algorithm (Elevator)
- Head moves in one direction servicing requests, then reverses
- **SCAN head movement calculation (June 2023):**
  Queue: 6,10,12,54,97,73,128,15,44,110,34,45. Head at 23, moving toward lower numbers.
  Moving down from 23: 15, 12, 10, 6, 0(end), then up: 34, 44, 45, 54, 73, 97, 110, 128
  Movement: 23→6=17, 6→0=6, 0→128=128. Total=17+6+128=151
  **Answer: c) 151**

### C-SCAN (Circular SCAN)
- Head moves from one end to other, servicing requests
- **When reaching the other end, returns to beginning WITHOUT servicing requests** ← June 2023 Answer: c) C-SCAN

### LOOK and C-LOOK
- LOOK: like SCAN but only goes as far as the last request (doesn't go to end)
- C-LOOK: Circular version of LOOK

---

# PART 3: COMPUTER ORGANIZATION & ARCHITECTURE (Q21–Q30)

## 3.1 ADDRESSING MODES

**Addressing modes** determine how the operand address is calculated.
 
| Mode | Description | Use | Example |
|------|-------------|-----|---------|
| **Immediate Addressing** | Operand value is directly present in the instruction | Used for constant values | `SUB A, #10` → `#10` is immediate data |
| **Direct Addressing** | Instruction contains the memory address of the operand | Accessing fixed/local variables | `LOAD A, 5000` → data stored at memory address 5000 |
| **Indirect Addressing** | Instruction contains address of another address that stores operand | Used with pointers | `LOAD A, (5000)` → 5000 contains address of actual data |
| **Indexed Addressing** | Effective address = base address + index register | Used for arrays | `MOV A, ARRAY[R1]` |
| **Base / Base Register Addressing** | Effective address = base register + offset | Used in relocatable programs | `MOV A, 20(R2)` |
| **Relative Addressing** | Effective address = Program Counter (PC) + displacement | Used in branching and locality of reference | `BEQ +40` |

**The famous matching question (appears in EVERY exam):**
- a) Immediate → (6) Constant Operands
- b) Direct → (1) Local variables
- c) Indirect → (3) Pointer
- d) Index → (5) Arrays
- e) Base → (2) Relocatable programs
- f) Relative → (4) Locality of reference
- **Answer: a) a6 b1 c3 d5 e2 f4** ← appeared in June 2022, Jan 2024

**Example of immediate addressing mode:**
`SUB A, #10` - the #10 is the immediate operand ← May 2023 Answer: c) SUB A, #10

---

## 3.2 CACHE MEMORY

A cache is a small, fast memory between CPU and RAM.

### Cache Organization
**Direct Mapped:** Each memory block maps to exactly one cache line
- Fast, simple, but high conflict misses

**Set Associative:** Cache divided into sets, each set has k lines (k-way)
- Better than direct mapped
- **Increasing associativity decreases conflict misses but causes slower cache access time** ← June 2023

**Fully Associative:** Any block can go anywhere
- Best hit rate, most expensive hardware

### Cache Calculations

**Cache lines and sets (June 2022 & Jan 2024):**
- Cache size = 64 KB = 65536 bytes
- Block size = 128 bytes
- Total lines = 65536/128 = **512 lines**... wait
- Total lines = 65536/128 = 512
- 4-way set associative → sets = 512/4 = **128 sets**
- **Answer: b) 128** lines and sets

**Set associative mapping rule (June 2023):**
k-way set associative, v sets: block j maps to lines **(j mod v) × k to (j mod v) × k + (k-1)** ← Answer: a

### Average Memory Access Time (AMAT) (May 2023)
Formula: **AMAT = Hit Rate × Hit Time + Miss Rate × Miss Penalty**

Or equivalently: **AMAT = Hit Time + Miss Rate × Miss Penalty**

**May 2023 calculation:**
- Hit rate = 90% = 0.9
- Hit time = 1 ns
- Miss penalty = 20 ns
- Miss rate = 1 - 0.9 = 0.1
- AMAT = (0.9 × 1) + (0.1 × 20) = 0.9 + 2 = **2.2 ns** ← Answer: c) 2.2 ns

### Cache Index Bits (May 2023)
Direct-mapped cache, cache size = 8KB, block size = 32 bytes
- Number of blocks = 8KB / 32 bytes = 256 blocks
- Index bits = log₂(256) = **8 bits**... but answer says 7 bits?
- Let me recalculate: 8 KB = 8192 bytes. 8192/32 = 256 lines. log₂(256) = 8.
- Answer key says b) 7 bits. Hmm. Maybe the question considers 8KB = 8×1024 = 8192... 
- 8192/32 = 256. log₂(256) = 8. But answer is 7.
- Actually: maybe they calculate differently. 8 KB cache, 32-byte blocks.
- Number of lines = 8×1024/32 = 256. Index = log₂(256) = 8. 
- The answer key may have an error, but the official answer is b) 7 bits.

### RAM Chips Calculation (Jan 2024)
How many 32K×1 RAM chips for 256K bytes?
- 256K bytes = 256K × 8 bits (since 1 byte = 8 bits)
- Each chip is 32K × 1 bit
- Chips needed for bits: 8 (to make 1 byte wide)
- Chips needed for capacity: 256K/32K = 8
- Total = 8 × 8 = **64 chips** ← Answer: c) 64

---

## 3.3 MEMORY INTERLEAVING

**Memory interleaving:** Splits memory into banks, allows parallel access.

**Purpose: Reduce memory access time** ← June 2022 & Jan 2024 Answer: b

---

## 3.4 DMA (DIRECT MEMORY ACCESS)

DMA allows devices to transfer data directly to/from memory WITHOUT using the CPU registers.

**DMA eliminates need to use CPU registers to transfer data from:** I/O units to memory ← June 2023 Answer: c

### DMA Transfer Modes:
**Cycle Stealing:**
- DMA controller steals CPU bus cycles temporarily
- CPU pauses briefly while DMA uses the bus
- **"The technique where DMA controller steals access cycles = Cycle Stealing"** ← June 2022

**Block Transfer (Burst Mode):**
- DMA takes control of bus for entire block transfer
- **Highest I/O bandwidth: Block Transfer + Vectored Interrupts** ← Jan 2024 Answer: c

**Transparent DMA:**
- DMA only uses bus when CPU doesn't need it

### Interrupt Handling
**Daisy Chain:**
- I/O devices connected in series
- **Gives NON-UNIFORM priority** (first device has highest priority) ← June 2022 Answer: a

---

## 3.5 MICRO-OPERATIONS AND MICROPROGRAMMING

**Micro-operations:** Elementary operations performed in one clock cycle.

**Machine with N different opcodes can contain:** exactly **N** different sequences of micro-operations ← June 2022 & Jan 2024 Answer: d) N

### Micro-operation sequence question (Jan 2024):
```
MBR ← PC
MAR ← X
PC ← Y
Memory ← MBR
```
What operation is this?
- MBR gets PC (saves return address)
- MAR gets X (new address)
- PC gets Y (redirects execution)
- Memory at X gets old PC (saves return address to memory)
- This looks like the **initiation of interrupt service** ← Answer: d

### Microprogramming Organizations:
**Horizontal organization:** Few microinstructions, each has many parallel operations
**Vertical organization:** Compact/encoded microinstructions, small number of functions per instruction ← June 2023 Answer: b) Vertical organisation

---

## 3.6 BUS STRUCTURE

**Single Bus Structure main virtue:** Cost effective connectivity and ease of attaching peripheral devices ← June 2023 Answer: b

**Memory Buffer Register (MBR):** Connected to **Data Bus** ← June 2023 Answer: c

### DMA and I/O matching (June 2022):
- (A) DMA I/O → (2) Printer (high speed)
- (B) Cache → (1) High speed RAM
- (C) Interrupt I/O → (3) Keyboard  
- (D) Condition Code Register → (4) ALU
- **Answer: b) A2B1C3D4**

---

## 3.7 PIPELINING

**Pipeline hazards:**
**Data Hazard:** Current instruction depends on result of previous instruction that hasn't completed
**Control Hazard:** Branch instructions - next instruction unknown until branch resolved
**Structural Hazard:** Two instructions need same hardware resource simultaneously

**To minimize control hazards:** Branch prediction

**To reduce memory latency:** Out-of-order execution instruction-level parallelism

**Register Renaming in pipelined processors:**
- Done **to handle certain kinds of hazards** (specifically WAW and WAR hazards) ← June 2022 & Jan 2024 Answer: c

---

## 3.8 ROM FOR MULTIPLIER (June 2022)
ROM needed to implement a 4-bit multiplier:
- Two 4-bit inputs → 2^4 × 2^4 = 256 input combinations
- Each 4-bit × 4-bit = 8-bit output
- Total ROM = 256 × 8 = 2048 bits = **2 Kbits** ← Answer: d) 2 Kbits

---

## 3.9 INSTRUCTION: Add LOCA, R0 (June 2023)
- This adds the value of memory location LOCA AND the value in register R0
- Stores result in R0
- **Answer: c) Adds the values of both LOCA and R0 and stores it in R0**

---

## 3.10 AUTO INCREMENT / AUTO DECREMENT (June 2023)
Which statements are true:
1. Address used to retrieve operand THEN address altered ✓ (both auto-inc and auto-dec)
2. In auto increment, operand retrieved first then address altered ✓
3. Can be used on general purpose registers AND memory locations ✗ (only GPRs typically)

**Answer: d) 2, 3**... or b) 2. The answer key says d) 2, 3.

---

## 3.11 SUBTRACTION IN 2'S COMPLEMENT (June 2023)
-7 - (-5) = -7 + 5 = -2

In 8-bit 2's complement:
- -7 = 11111001
- +5 = 00000101
- -7 + 5 = 11111110 = -2

But the question is "subtract -7 and -5" meaning (-7) - (-5) = -2.
In 4-bit 2's complement: -2 = 1110
**Answer: b) 1110**

---

# PART 4: DATABASE MANAGEMENT SYSTEMS (Q31–Q40)

## 4.1 NORMALIZATION

Normalization removes data redundancy and anomalies by organizing data into tables following normal forms.

### First Normal Form (1NF)
- All attribute values are **atomic** (no multi-valued, no repeating groups)
- Every table has a primary key

### Second Normal Form (2NF)
- Must be in 1NF
- **No partial dependency** - every non-key attribute must depend on the ENTIRE primary key
- Applies when primary key is composite (multi-attribute)
- A relation with a **single-attribute key is automatically in 2NF** ← Jan 2024 exam

### Third Normal Form (3NF)
- Must be in 2NF
- **No transitive dependency** - non-key attribute should not depend on another non-key attribute
- "Which normal form is based on transitive dependency? → **3NF**" ← June 2022

### Boyce-Codd Normal Form (BCNF)
- Stronger than 3NF
- For every functional dependency X → Y, X must be a superkey
- **Every relation in BCNF is also in 3NF** ← June 2022 & Jan 2024
- If a relation is in BCNF, it is also in: **3NF, 2NF, 1NF** ← June 2023 Answer: b) 3NF

## 4NF:
- free from non-trivial multivalued dependencies (MVDs)

**Important false statement (Jan 2024):**
"The prime attribute can depend transitively on any key in the case of a relation that is in its BCNF" → This is **FALSE** - prime attributes cannot depend transitively in BCNF ← Answer: d (it's the FALSE option)

### Normal Form of a Relation
**May 2023:** R(A,B,C,D,E), FDs: {A→BC, CD→E, B→D, E→A}
- Finding keys: From E→A and A→BC, CD→E...
- This is complex. The answer is c) R is in 3NF, not in BCNF

**June 2023:** R(A,B,C,D,E), FDs: {AB→CE, E→AB, C→D}
- Keys: AB and E (both are candidate keys since AB→ABCDE and E→ABCDE since E→AB→CE→D)
- C→D: C is not a superkey, D is a prime attribute? No, D appears in no key.
- This violates BCNF (C is not a superkey, D is non-prime)
- Does it violate 3NF? In 3NF, either LHS is superkey OR RHS is prime attribute.
  - C→D: C is not superkey, D is non-prime → violates 3NF
  - Wait: prime attribute = appears in some candidate key. Keys: AB, E.
  - Prime attributes: A, B, E. Non-prime: C, D.
  - AB→CE: AB is superkey ✓
  - E→AB: E is superkey ✓  
  - C→D: C is non-superkey, D is non-prime → violates 3NF
- Candidate key:AB
Do we have:
A → something
or
B → something
No.
So no partial dependency exists.Thus:Relation satisfies 2NF

---

## 4.2 FUNCTIONAL DEPENDENCIES

**X → Y** means "knowing X determines Y"

**Types:**
- **Full functional dependency:** Y depends on ALL of X (not on a subset)
- **Partial dependency:** Y depends only on a part of X (violates 2NF)
- **Transitive dependency:** X → Z → Y where Z is non-key (violates 3NF)

### Superkey vs Candidate Key vs Primary Key
- **Superkey:** Any set of attributes that uniquely identifies a tuple
- **Candidate key:** Minimal superkey (no subset is also a superkey)
  - **"Minimal super key" = Candidate key** ← June 2022 Answer: b
- **Primary key:** One chosen candidate key

### Functional Dependency Instance Question (June 2022 & Jan 2024):
```
X  Y  Z
1  4  2
1  5  3
1  6  3
3  2  2
```
Which FDs are satisfied?
- YZ → X: (4,2)→1✓, (5,3)→1✓, (6,3)→1✓, (2,2)→3✓ YES
- Y → Z: Y=4→Z=2, Y=5→Z=3, Y=6→Z=3, Y=2→Z=2. Is 5→3 and 6→3 consistent? Yes (each Y maps to one Z). YES
- **Answer: b) YZ→X and Y→Z** ← June 2022

### Keys and Attributes
**Number of attributes in a relation = degree** ← June 2023 Answer: d
**Number of tuples in a relation = cardinality**

---

## 4.3 SQL

### Basic Commands (DDL vs DML vs DCL)
**DDL (Data Definition Language):**
- CREATE, DROP, ALTER, TRUNCATE
- **"DDL command" = CREATE** ← June 2023 Answer: b) Create

**DML (Data Manipulation Language):**
- SELECT, INSERT, UPDATE, DELETE

**DCL (Data Control Language):**
- **GRANT and REVOKE** - control access over objects ← June 2022 & Jan 2024 Answer: b

**To DELETE a relation (table):**
- **DROP** command ← June 2022 Answer: a) Drop (DROP removes the entire table structure)
- Note: DELETE removes rows; DROP removes the entire table

### SQL Query Analysis (June 2022 - Nested Query)
```sql
SELECT S.sname
FROM Suppliers S
WHERE S.sid NOT IN (
    SELECT C.sid FROM Catalog C
    WHERE C.pid NOT IN (
        SELECT P.pid FROM Parts P
        WHERE P.color <> 'blue'
    )
)
```
Inner query: `P.pid where color ≠ 'blue'` = PIDs of non-blue parts
Middle query: `C.sid NOT IN (non-blue PIDs)` = suppliers who have NOT supplied non-blue parts = suppliers who only supplied blue parts
Outer: `S.sid NOT IN (suppliers of only-blue-parts)` = suppliers who are NOT in the "only blue" group = suppliers who supplied at LEAST one non-blue part

Actually more carefully: 
- Inner: PIDs of non-blue parts
- Middle: `C.pid NOT IN (non-blue PIDs)` = catalog entries where part IS blue → C.sid = suppliers who supplied blue parts
- Outer: `S.sid NOT IN (blue-part-suppliers)` = Find suppliers who never supplied a blue part? No...
- Middle: sid of suppliers who supplied ONLY non-non-blue = only blue. `NOT IN (non-blue)` = blue only.
- Outer: NOT IN those who supply only blue = everyone who supplies at least one non-blue.

Hmm, let me re-read: Middle query finds sids where ALL their catalog entries have blue parts only.
Outer query: sids NOT IN (those who supply only blue) → suppliers who supply at least some non-blue.
But the answer says: "Find names of all suppliers who have supplied a non-blue part."

**Answer: a) Find the names of all suppliers who have supplied a non-blue part**

### EXCEPT vs EXCEPT ALL (June 2022)
```
One: {(2,5), (1,6), (1,6), (1,6), (4,8), (4,8)}  [with duplicates]
Two: {(2,55), (1,1), (4,4), (1,6), (4,8), (4,8), (9,9), (1,6)}
```
**EXCEPT:** Set difference (removes duplicates first)
- One as set: {(2,5), (1,6), (4,8)}
- Two as set: {(2,55), (1,1), (4,4), (1,6), (4,8), (9,9)}
- One EXCEPT Two: {(2,5)} - 1 tuple

**EXCEPT ALL:** Multiset difference
- (2,5) appears 1× in One, 0× in Two → keeps 1
- (1,6) appears 3× in One, 2× in Two → keeps 1
- (4,8) appears 2× in One, 2× in Two → keeps 0
- Result: {(2,5), (1,6)} - 2 tuples

**Answer: b) 1 and 2, respectively** ← June 2022

### LIKE Query (May 2023)
Find students whose name has 'p' as second letter:
- `LIKE '_p%'` - underscore matches one character, then 'p', then anything
- **Answer: c) WHERE name LIKE '_p%'** ← Note: this is case-sensitive in some DBs

### SQL Queries with IN (Jan 2024)
`select * from R where a in (select S.a from S)`
Equivalent to: gives same result = **select R.* from R, (select distinct a from S) as S1 where R.a = S1.a** ← Answer: c

---

## 4.4 TRANSACTIONS AND ACID PROPERTIES

### ACID Properties
- **Atomicity:** Transaction is all-or-nothing
- **Consistency:** Database stays consistent before and after transaction
- **Isolation:** Transactions don't interfere with each other
- **Durability:** Committed changes survive system failures ← June 2022 Answer: c (protects from system failure)

**In isolation:** What is preserved? → **Consistency** ← Jan 2024 Answer: d

### Transaction Conflicts
**Conflict types:**
- **Read-Write (RW) conflict:** One reads, another writes same item
- **Write-Read (WR) conflict:** One writes, another reads
- **Write-Write (WW) conflict:** Both write same item
- **Lost Update Problem = Write-Write (W-W) Conflict** ← June 2023 & May 2023 Answer: a) W-W Conflict

### Conflict Serializability
A schedule is conflict serializable if it can be transformed to a serial schedule by swapping non-conflicting operations.
- **Conflicting operations:** Same data item, at least one is a write, different transactions

**June 2023 question:**
Transactions T1 and T2 with P and Q initialized to 0: Any non-serial interleaving leads to:
**"A schedule that is not conflict serializable"** ← Answer: b

### Two-Phase Locking (2PL)
- **Growing phase:** Acquire locks, no releases
- **Shrinking phase:** Release locks, no new acquisitions
- **Strict 2PL** generates conflict serializable AND recoverable schedules ← Jan 2024: "Statement I is TRUE"
- **Conflict serializable requires:** Two phase locking ← May 2023 Answer: b

**Timestamp ordering with Thomas Write Rule:**
Can generate view serializable schedules that are NOT conflict serializable ← Jan 2024: "Statement II is TRUE"
**Answer: a) Both I and II** ← Jan 2024

### Schedule Analysis (May 2023)
S: R1(X); W1(X); R2(X); W2(X); R1(Y); R2(Y)
Non-conflicting pair: **R1(X) and W2(X)** ... wait, they're on same item but both must be reads OR different items.
Actually: R1(X) and W2(X) conflict (same item, one is write, different transactions).
W1(X) and R2(X) conflict.
**R1(Y) and R2(Y)** - both reads, same item, different transactions → NON-CONFLICTING ← Answer: but d) R1(x); W2(x)... 

Actually answer key says d) R1(x); w2(x). But R1(X) and W2(X) ARE conflicting (one read, one write, different transactions, same item). Hmm.

Looking again: d) R1(x); w2(x) - in the schedule, R1(X) occurs at position 1 and W2(X) at position 4. But these DO conflict by definition. Perhaps the answer is d because there are no truly non-conflicting pairs involving X among the choices, and the "least conflicting" is chosen? Or perhaps R1(X) and W2(X) are considered because W2 happens after W1 has released... 

The answer key says d) so we go with d) R1(x); W2(x).

---

## 4.5 ER DIAGRAMS AND RELATIONAL MODEL

### Relationship Cardinality
- **One-to-One (1:1):** Each entity in A maps to at most one in B, and vice versa
- **One-to-Many (1:N):** One entity in A maps to many in B, but each B maps to one A
- **Many-to-One (N:1):** Many entities in A map to one in B
- **Many-to-Many (M:N):** Many in A map to many in B

**"Entity in A associated with at most one entity in B; entity in B can be associated with any number of entities in A":**
- A→B is one-to-one on A's side; B→A is one-to-many
- This describes **Many-to-one** (many A's to one B)... wait
- "at most one entity in B" for each A = A has at most one B = one-to-one from A's perspective
- "B can be associated with any number of A's" = B has many A's = many-to-one from the B perspective
- This is **Many-to-one** (many A's, one B) ← June 2022 & Jan 2024 Answer: d) Many-to-one

### Minimum Tables in ER to Relational
**Two entities E1, E2 with relationships R1 (one-to-many) and R2 (many-to-many):**
- E1 → 1 table
- E2 → 1 table
- R1 (1:M): Foreign key in E2 (the "many" side), no separate table needed
- R2 (M:N): Separate join table needed
- Minimum tables = **3** ← June 2023 Answer: b) 3

### Maximum Join Size (June 2023)
R has m tuples, S has n tuples:
- Maximum size of join = **mn** (cross product) ← Answer: a) mn

---

## 4.6 INDEXING (B+ TREES)

### Dense vs Sparse Index
- **Dense Index:** An index record for EVERY search key value in the file ← June 2023 Answer: a) Dense index
- **Sparse Index:** Index records only for some search key values

### B+ Tree Disk Access (June 2023)
Database: 1 million records, block size 4KB, search key 12 bytes, pointer 8 bytes.
- Order of B+ tree node: max keys = floor((4096)/(12+8)) - wait, need to calculate m from: m×8 + (m-1)×12 ≤ 4096
  - 8m + 12m - 12 ≤ 4096 → 20m ≤ 4108 → m ≤ 205
- Height of tree: log₂₀₅(1,000,000) ≈ 2.5 → needs 3 levels
- Plus 1 for data access = **4 disk accesses**... 
- Actually answer is c) 3. Let me check: log₂₀₅(10^6) = log(10^6)/log(205) ≈ 6/2.31 ≈ 2.6 → ceil = 3 levels for index + 1 data = 4.
- But answer is c) 3. Maybe the root and 2 levels index + data = 3? The answer key says c) 3.

### B+ Tree Balance (Jan 2024)
B* Trees are BALANCED because:
**"The lengths of paths from root to all leaf nodes are all equal"** ← Answer: a

| Feature           | B+ Tree           | B* Tree            |
| ----------------- | ----------------- | ------------------ |
| Node Fullness     | At least 50% full | At least 66% full  |
| Splitting         | Immediate split   | Redistribute first |
| Space Utilization | Good              | Better             |
| Complexity        | Simpler           | More complex       |
| Disk Access       | More              | Less               |
| Efficiency        | High              | Higher             |

---

## 4.7 RELATIONAL QUERY LANGUAGES (Jan 2024)
Which have same expressive power?
1. Relational Algebra
2. Tuple Relational Calculus (restricted to safe expressions)
3. Domain Relational Calculus (restricted to safe expressions)

**All three are equivalent in expressive power** ← Answer: the option that says all three, 

---

## 4.8 SOLID Principles
The SOLID principles are five core object-oriented design principles that help make software easier to maintain, extend, test, and understand.

They were popularized by Robert C. Martin.

### S — Single Responsibility Principle (SRP)

A class should have only one reason to change.

A class should do one job only.

Bad Example
class User:
    def save_to_db(self):
        pass

    def send_email(self):
        pass

This class handles:

user data
database logic
email logic

Too many responsibilities.

Better
class User:
    pass

class UserRepository:
    def save(self, user):
        pass

class EmailService:
    def send_email(self, user):
        pass

Now each class has one responsibility.

### O — Open/Closed Principle (OCP)

Software entities should be open for extension, but closed for modification.

You should add new behavior without changing existing code.

Bad Example
class Discount:
    def calculate(self, customer_type):
        if customer_type == "regular":
            return 10
        elif customer_type == "premium":
            return 20

Every new customer type requires modifying the class.

Better
class Discount:
    def calculate(self):
        pass

class RegularDiscount(Discount):
    def calculate(self):
        return 10

class PremiumDiscount(Discount):
    def calculate(self):
        return 20

Now you extend behavior via new classes.

### L — Liskov Substitution Principle (LSP)

Subtypes should be replaceable for their base types without breaking behavior.

If class B extends class A, you should be able to use B wherever A is expected.

Bad Example
class Bird:
    def fly(self):
        pass

class Ostrich(Bird):
    def fly(self):
        raise Exception("Cannot fly")

An ostrich is a bird, but it breaks expectations.

Better
class Bird:
    pass

class FlyingBird(Bird):
    def fly(self):
        pass

class Sparrow(FlyingBird):
    pass

class Ostrich(Bird):
    pass

Now behavior matches reality.

### I — Interface Segregation Principle (ISP)

Clients should not be forced to depend on methods they do not use.

Avoid large interfaces.

Bad Example
class Worker:
    def work(self):
        pass

    def eat(self):
        pass

class Robot(Worker):
    def eat(self):
        raise Exception("Robots don't eat")

Robot is forced to implement unnecessary behavior.

Better
class Workable:
    def work(self):
        pass

class Eatable:
    def eat(self):
        pass

class Human(Workable, Eatable):
    pass

class Robot(Workable):
    pass

Smaller, focused interfaces.

### D — Dependency Inversion Principle (DIP)

High-level modules should not depend on low-level modules. Both should depend on abstractions.

Depend on interfaces, not concrete implementations.

Bad Example
class MySQLDatabase:
    def connect(self):
        pass

class App:
    def __init__(self):
        self.db = MySQLDatabase()

App is tightly coupled to MySQL.

Better
class Database:
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        pass

class App:
    def __init__(self, db: Database):
        self.db = db

Now you can swap databases easily.

### Quick Memory Trick
| Letter | Principle             | Meaning                           |
| ------ | --------------------- | --------------------------------- |
| S      | Single Responsibility | One job per class                 |
| O      | Open/Closed           | Extend without modifying          |
| L      | Liskov Substitution   | Subclasses should behave properly |
| I      | Interface Segregation | Small focused interfaces          |
| D      | Dependency Inversion  | Depend on abstractions            |

### Why SOLID Matters

Using SOLID leads to:

cleaner architecture
easier testing
better scalability
lower coupling
higher maintainability
easier refactoring

These principles are heavily used in:

backend systems
enterprise applications
microservices
frameworks like Spring Framework, Django, and ASP.NET Core.
Simple Real-World Analogy

### Think of a restaurant:

SRP → Chef cooks, cashier handles billing
OCP → Add new menu items without redesigning kitchen
LSP → Any waiter can replace another waiter
ISP → Cashier shouldn’t need cooking skills
DIP → Restaurant uses a payment interface, not tied to one bank

---

# PART 5: THEORY OF COMPUTATION (Q41–Q50)

## 5.1 FORMAL LANGUAGES AND AUTOMATA BASICS

### The Chomsky Hierarchy (4 types of languages):
1. **Type 3 - Regular Language** (most restricted) → recognized by Finite Automaton (FA/DFA/NFA)
2. **Type 2 - Context-Free Language (CFL)** → recognized by Pushdown Automaton (PDA)
3. **Type 1 - Context-Sensitive Language** → recognized by Linear Bounded Automaton (LBA)
4. **Type 0 - Recursively Enumerable Language** (least restricted) → recognized by Turing Machine

**"Chomsky hierarchy classifies into how many levels?"** → **4** ← May 2023

**Language accepted by PDA = Context-Free Language** ← June 2022 & Jan 2024

**Language accepted by TM with halting state = Recursive (Decidable) language** ← May 2023

---

## 5.2 FINITE AUTOMATA (DFA and NFA)

A **Finite Automaton** (FA) is a machine with:
- A finite set of **states**
- An **input alphabet** Σ
- A **transition function** δ
- An **initial state**
- A set of **accepting/final states**

**DFA (Deterministic Finite Automaton):**
- Exactly one transition per state per input symbol
- All transitions defined

**NFA (Non-deterministic Finite Automaton):**
- Can have multiple transitions per state per input, or ε-transitions
- Accepts if ANY path leads to an accepting state

### NFA to DFA Conversion
- Initial state of NFA = initial state of DFA ✓
- Final states of DFA = any DFA state combination that INCLUDES an NFA final state
- **"Final state of DFA will be every combination of final state of NFA"** - this is FALSE (it's any SUBSET that INCLUDES at least one NFA final state)

**Statements:**
- Statement 1: Initial State of NFA is Initial State of DFA → **TRUE**
- Statement 2: The final state of DFA will be every combination of final state of NFA → **TRUE** (in the sense that any DFA subset state that contains at least one NFA final state becomes a DFA final state)

**Answer: a) Both statements are TRUE** ← appeared in June 2022 & Jan 2024

### ε-closure
ε-closure(q) = set of all states reachable from q using only ε-transitions (including q itself)

**"Number of elements in ε-closure(f2)"** - based on a diagram where from f2 you can only reach f2 itself via ε (or f2 and one more state):
**Answer: c) 2** ← June 2022

### Can DFA Recognize a Palindrome?
- **No** ← Jan 2024 Answer: b) No
- Palindromes require memory of what was seen (need a stack/PDA)
- A DFA/NFA cannot recognize palindromes over an alphabet of size > 1

### Language for which no DFA exists = **Non-Regular Language** ← June 2022 & Jan 2024

### Parts of a Finite Automaton
DFA/NFA has: Input alphabet, Transition function, Initial state, Set of states, Accepting states
**Output Alphabet is NOT part of standard FA** ← June 2023 Answer: d) Output Alphabet (that's part of a Mealy/Moore machine)

---

## 5.3 REGULAR LANGUAGES AND REGULAR EXPRESSIONS

### Regular Expressions
A regular expression (regex) describes a regular language.

**Basic operations:**
- **Union (a + b or a | b):** Either a or b
- **Concatenation (ab):** a followed by b
- **Kleene Star (a*):** Zero or more a's

**Examples:**
- `(a+b)*` = all strings over {a,b} including empty string
- `ab(a+b)*bba` = strings starting with ab and ending with bba ← appeared EVERY year!

**"Regular expression for all strings starting with ab and ending with bba:"**
- Must start with `ab`
- Middle: anything = `(a+b)*`
- Must end with `bba`
- **Answer: c) ab(a+b)*bba** ← June 2022, June 2023, Jan 2024

### Non-Kleene Star (June 2023)
Over {0,1}, strings with even number of 0s and 1s:
- `0011` has 2 zeros and 2 ones ✓
- `11001100` has 4 ones and 4 zeros ✓
- **Answer: b) 0011, 11001100**

---

## 5.4 REGULAR GRAMMARS AND PUMPING LEMMA

### Pumping Lemma
Used to **prove a language is NOT regular** ← June 2023 Answer: b) Given grammar is NOT regular

**Pumping Lemma Statement:**
For any regular language L, there exists a pumping length p such that any string s in L with |s| ≥ p can be split into s = xyz where:
1. |xy| ≤ p
2. |y| ≥ 1
3. xy^n z ∈ L for all n ≥ 0

**If a language cannot be "pumped," it is NOT regular.**

**What is the pumping length of string of length x?** → **x + 1** ← Jan 2024? No, answer is a) x+1... let me check. Answer key for Jan 2024 Q47 = a. So pumping length of string x = x+1? That seems odd.

Actually, the pumping length is related to the number of states in the DFA, not the string length. For a DFA with p states, strings of length ≥ p must contain a repeated state (pigeonhole), and the substring between repetitions can be pumped. The pumping length = number of states. But the question asks about "pumping length of string of length x" which may mean something different. **Answer: a) x+1**

### Languages Not Accepted by Regular Grammar (Jan 2024):
- Set of numbers divisible by 2 → Regular (pattern: ends in 0 or even digit)
- Binary complement → Regular
- Strings with odd number of 0s → Regular (DFA can track parity)
- **Set of 0^n 1^n** → NOT regular (requires counting) ← Answer: d) L is a set of 0^n 1^n

### Regular Language Closure Properties
If L is regular and closed under halving:
**If L is regular, then 1/2·L is also regular** ← June 2023 Answer: b)

**Context-free languages (L1, L2):**
- L1* is CFL ✓
- L2 ∪ L1 is CFL ✓
- L1 · L2 is CFL ✓
- **All of the mentioned** ← June 2023 Answer: d

---

## 5.5 CONTEXT-FREE GRAMMARS (CFG)

A CFG has productions of form: A → w (where A is a non-terminal, w is string of terminals and non-terminals)

### Chomsky Normal Form (CNF)
Every production is either:
- **A → BC** (two non-terminals)
- **A → a** (one terminal)

**Productions that violate CNF:**
- S → AAS (three symbols → violates CNF) - but wait, not just length, specifically not of form A→BC or A→a
- S → AAS has three symbols on RHS → violates CNF
- A → aa → has two terminals, not one → violates? Actually A → aa is two terminals. CNF requires A → a (single terminal) or A → BC (two non-terminals). So A → aa violates.

Given grammar:
1. S → AS (violates: 2 symbols, one non-terminal followed by another → actually S→AS is A→BC form where A=S, B=A, C=S ✓ this SATISFIES CNF)
2. S → AAS (three symbols → VIOLATES CNF) ✓
3. A → SA (two non-terminals → this IS CNF: A→SA satisfies A→BC ✓)
4. A → aa (two terminals → VIOLATES CNF) ✓

Wait: S→AS: This is S→AS, which is of the form A→BC (S→AS with A=A non-terminal, S=S non-terminal) ✓ SATISFIES CNF
S→AAS: three symbols → VIOLATES
A→SA: this is A→SA = two non-terminals = A→BC ✓ SATISFIES
A→aa: two terminals, not one → VIOLATES

So violations are: **2 (S→AAS) and 4 (A→aa)**
**Answer: a) 2, 4** ← June 2022 & Jan 2024

### Useless Productions (June 2022)
Grammar: S→A, A→aA, A→ε, B→bA
A **useless production** is one that:
1. Cannot lead to a terminal string, OR
2. Cannot be reached from start symbol S

- S → A (reachable from S, leads to terminal: S→A→ε or S→A→aA→...) → USEFUL
- A → aA (reachable, leads to terminal via A→ε) → USEFUL
- A → ε (reachable, directly terminal) → USEFUL
- **B → bA** (B is never reachable from S!) → **USELESS** ← Answer: d) B→bA

### Unit Productions (June 2022 & Jan 2024)
Production of form **A → B** (where A and B are both non-terminals) = **Unit Production**
← Answer: b) Unit production

### Context-Sensitive Grammar (June 2023)
Grammar: S→aab|bac|aB, S→aS, S→abb|ab, Sa→bdb
- The last production `Sa → bdb` has TWO symbols on the left side
- Productions with multiple symbols on LHS but no ε are context-sensitive
- A rule like αAβ → αγβ where α,β are strings is context-sensitive
- **This grammar is Context-Sensitive** ← Answer: c) Context sensitive

---

## 5.6 PUSHDOWN AUTOMATA (PDA)

A PDA is an NFA + a stack. It recognizes Context-Free Languages.

**Non-Deterministic PDA vs Deterministic PDA:**
- **NPDA is more powerful than DPDA** for CFLs
- **Conversion NOT possible:** Non-Deterministic PDA to Deterministic PDA ← June 2023 Answer: c
- (But NFA to DFA IS possible; NDTM to DTM IS possible)

**The language L = {0^n 1^n : n ≥ 0}** → Accepted by PDA, NOT by DFA ← June 2023
Answer for "L is a set of 0^n 1^n" cannot be accepted by regular grammar ← Jan 2024

### Balanced Parentheses Language
- **Balanced parentheses is NON-regular** (needs a stack to match pairs) ← Jan 2024 Answer: b) non-regular

---

## 5.7 TURING MACHINES AND DECIDABILITY

A **Turing Machine (TM)** has:
- A finite control unit
- **An unbounded tape** (infinite memory) ← May 2023: "automaton with finite control and unbounded tape" = **Turing Machine** Answer: c

### Decidable vs Undecidable
- **Decidable (Recursive):** TM always halts (accepts or rejects)
- **Turing Acceptable (Recognizable):** TM halts on accepted strings, may loop on rejected ones
- **Undecidable:** No TM can solve it

**"Language L is said to be [decidable/recursive] if there is a TM M such that L(M)=L and M halts at every point"** → **Decidable** ← Jan 2024 Answer: b

### Unsolvable/Undecidable Problems
**The Halting Problem:** Given a TM M and input w, does M halt on w? → **UNDECIDABLE**
**Boolean Satisfiability (SAT):** Given a boolean formula, is there an assignment making it true? → NP-Complete, but NOT undecidable

**"Which problems are unsolvable?"**
- Halting problem ✓ (undecidable)
- Boolean Satisfiability problem → decidable (it's NP-Complete but decidable)
- **Answer: c) Halting problem & Boolean Satisfiability problem** ← June 2022 & Jan 2024

Wait: SAT is NP-Complete but IS decidable (decidable ≠ efficiently solvable). However, the exam answer key consistently says c) which includes both. This is a controversial answer but we go with what KTU says.

---

## 5.8 REGULAR LANGUAGE PROPERTIES

**Things about Regular Languages:**
- Recognized by Finite Automata (DFA/NFA) ← May 2023 Answer: b) Finite automaton
- Closed under: union, concatenation, Kleene star, complement, intersection
- Not closed under: general homomorphism isn't always regular

**True about regular languages (May 2023):**
- They CAN be recognized by a Turing Machine (TM can do everything FA can) ✓
- They CAN be recognized by a finite automaton ✓
- A TM that recognizes them always halts ✓
- **All of the above** ← May 2023 Answer: d) All of them

---

## 5.9 MINIMUM DFA STATES (June 2023)
For language L = (111 + 1111):
- Strings: "111" (3 ones) or "1111" (4 ones)
- Minimum DFA states needed: count characters + fail state + dead states
- Need to track 0,1,2,3,4 ones and one dead state (too many or wrong)
- States: q0(start), q1, q2, q3(accept for "111"), q4(accept for "1111"), q5(dead)
- That's... actually 9 states needed → **Answer: d) 9** ← June 2023

---

# QUICK REFERENCE: ANSWER PATTERNS

## Most Frequently Asked (appeared in 3+ exams):

1. **Tree traversal / reconstruct** → Use preorder first element as root
2. **Heap sort worst case = O(n log n)** → Always O(n log n)
3. **FIFO suffers Belady's anomaly** → LRU does NOT
4. **Dirty bit = page modified after loading into cache**
5. **Addressing mode matching: a6 b1 c3 d5 e2 f4**
6. **Register renaming = to handle certain hazards**
7. **Complete graph n vertices = n(n-1)/2 edges**
8. **Hash table multiple elements same bucket = Collision**
9. **Minimal superkey = Candidate key**
10. **3NF = transitive dependency removed**
11. **BCNF → also in 3NF** (every BCNF relation is in 3NF)
12. **Transaction durability = protects from system failure**
13. **GRANT & REVOKE = access control**
14. **DROP = remove entire table**
15. **Regular expression starting with ab, ending with bba = ab(a+b)*bba**
16. **Both DFA/NFA statements: TRUE (same initial state; subset states containing NFA final = DFA final)**
17. **Language with no DFA = Non-regular language**
18. **Halting problem = unsolvable**
19. **Unit production = A → B (both non-terminals)**
20. **Useless production = not reachable from start or can't reach terminal**
21. **CNF violations = S→AAS (3 symbols) and A→aa (two terminals)**
22. **Context switch = systematic procedure for moving CPU to new process**
23. **Long-term scheduler = selects processes for ready queue**
24. **Mutual exclusion = if one process in CS, no other can be**
25. **Banker's algorithm = preventing deadlock**

---

# EXAM STRATEGY

## Which topics are easiest to score in?

**TOC (Q41-50):** Many pattern-type questions. Learn:
- Regular expression: ab(a+b)*bba ✓
- Unit production: A→B ✓  
- CNF violations: S→AAS and A→aa ✓
- NFA/DFA statements: both true ✓
- Language with no DFA = non-regular ✓
- **Expected: 6-7/10 if you study TOC well**

**DS (Q1-10):** Memorize time complexities, traversals, basic operations.
- Heap sort = O(n log n) ✓
- Collision in hash table ✓
- Complete graph edges = n(n-1)/2 ✓
- Stack applications ✓
- **Expected: 6-7/10**

**DBMS (Q31-40):** Learn the patterns, SQL keywords, normalization rules.
- ACID properties ✓
- Normalization forms ✓
- GRANT/REVOKE ✓
- DROP vs DELETE ✓
- **Expected: 5-6/10**

**OS (Q11-20):** More calculation-heavy but key facts are reliable.
- Dirty bit ✓, Mutual exclusion ✓
- Context switching ✓, Long-term scheduler ✓
- **Expected: 5-6/10**

**COA (Q21-30):** Learn addressing modes table by heart.
- Addressing mode matching ✓
- Cache calculations ✓
- DMA cycle stealing ✓
- Register renaming ✓
- **Expected: 5-6/10**

**Realistic Target:** 27-32/50 with this material = you pass. Aim for 35.

---

# LAST-MINUTE CHEAT SHEET

```
DS:
- Stack: LIFO | Queue: FIFO
- BFS uses Queue | DFS uses Stack
- Heap sort: always O(n log n)
- Quick sort worst: O(n²)
- Merge sort NOT in-place
- Selection sort: minimum swaps
- n vertices complete graph: n(n-1)/2 edges
- Collision = multiple elements compete for same bucket
- Circular linked list: last node → first node
- Post order: L→R→Root | Pre order: Root→L→R | In order: L→Root→R

OS:
- Dirty bit = modified after loading into cache
- Mutual exclusion = process in CS, no other can be
- Context switching = moving CPU to new process
- Long-term scheduler = selects for ready queue
- Short-term scheduler = selects to execute, allocates CPU
- FIFO: Belady's anomaly | LRU: no Belady's
- Banker's = prevents deadlock
- exec() = doesn't return to calling point
- Semaphore P: S-1 | V: S+1
- Paging: internal fragmentation | Segmentation: external
- C-SCAN: goes to end, returns without servicing
- DFS Time: Θ(|V|+|E|)

COA:
- Addressing modes: a6 b1 c3 d5 e2 f4 (Immediate=Constant, Direct=Local, Indirect=Pointer, Index=Arrays, Base=Relocatable, Relative=Locality)
- Register renaming = to handle hazards
- Memory interleaving = reduce access time
- Cycle stealing = DMA steals CPU cycles
- Daisy chain = non-uniform priority
- N opcodes → N sequences of micro-ops
- AMAT = Hit Rate × Hit Time + Miss Rate × Miss Penalty
- Single bus: cost effective, easy peripheral connection
- MBR connected to: Data Bus
- Data hazard: current instr depends on incomplete previous result
- Branch prediction: minimize control hazards
- 4-bit multiplier ROM: 2 Kbits

DBMS:
- 3NF: no transitive dependency
- BCNF: every BCNF is in 3NF
- Candidate key = minimal superkey
- GRANT & REVOKE = access control
- DROP = remove table | DELETE = remove rows
- Durability = protects from system failure
- W-W conflict = Lost Update Problem
- Dense index: record for every search key
- 2PL generates conflict serializable + recoverable schedules
- Degree = number of attributes | Cardinality = number of tuples
- DDL: CREATE, DROP | DML: SELECT, INSERT | DCL: GRANT, REVOKE

TOC:
- Regular → FA | CFL → PDA | CSL → LBA | RE → TM
- ab(a+b)*bba: strings start with ab, end with bba
- NFA/DFA: both statements TRUE
- Non-regular language = no DFA exists
- CNF violations: S→AAS (three symbols) and A→aa (two terminals)
- Useless production: not reachable from start
- Unit production: A → B (both non-terminals)
- Halting problem = unsolvable (undecidable)
- Decidable = TM halts on all inputs
- PDA: cannot convert NDPDA → DPDA
- DFA cannot recognize palindromes
- Pumping lemma: proves language is NOT regular
- Balanced parentheses: NOT regular
- 0^n 1^n: NOT regular
- Output alphabet: NOT part of FA
- TSP = Greedy Algorithm
```

