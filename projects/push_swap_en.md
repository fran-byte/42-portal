---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting push_swap)

### 📌 Objective:

Design and implement an efficient sorting algorithm using a **limited set of stack operations**, with the goal of sorting integers using the **fewest number of moves possible**.

---

### 🧱 What Is `push_swap`?

- It receives a list of unordered integers via command-line arguments.
- It outputs to `stdout` a **series of instructions** that sort the numbers using only the allowed operations.
- ✅ **It must not print the numbers**, only the instructions.

---

## 🛠️ Allowed Operations

You can only use the following operations (assembler-style):

| **Instruction** | **Description**                                                                 |
|-----------------|----------------------------------------------------------------------------------|
| `sa`            | Swap the first two elements at the top of stack A.                              |
| `sb`            | Swap the first two elements at the top of stack B.                              |
| `ss`            | Perform `sa` and `sb` simultaneously.                                           |
| `pa`            | Push the first element from stack B onto the top of stack A.                    |
| `pb`            | Push the first element from stack A onto the top of stack B.                    |
| `ra`            | Rotate all elements of stack A up by one.                                       |
| `rb`            | Rotate all elements of stack B up by one.                                       |
| `rr`            | Perform `ra` and `rb` simultaneously.                                           |
| `rra`           | Reverse rotate stack A (last element becomes first).                            |
| `rrb`           | Reverse rotate stack B.                                                         |
| `rrr`           | Perform `rra` and `rrb` simultaneously.                                         |

---

## 🎯 Final Goal

You must build a sorting algorithm that:

* ✅ Correctly sorts any list of **unique integers**.
* ✅ Uses **only** the allowed operations.
* ✅ Is **efficient** (fewer than 700 moves for 100 numbers).
* ✅ Is **robust** (handles errors, invalid input, etc.).

---

## ⚙️ Sorting Algorithm Structure

The algorithm can be broken down into **three main phases**:

---

### 🔁 Phase 1: Push Elements from A to B

1. **Initial setup:**
   - Push the first two elements from A to B unconditionally.

2. **Target node in B:**
   - For each number in A, find a “target node” in B: the smallest number in B that is larger than the current number.
   - If no such number exists, the target is the largest number in B.

3. **Cost calculation:**
   - For each number in A, calculate how many moves are needed to bring it to the top of A and its target to the top of B.

4. **Select cheapest move:**
   - Push the number from A to B that has the **lowest insertion cost**.

5. **Repeat:**
   - Continue until only **three numbers remain in A**.

---

### 🧮 Phase 2: Sort the Remaining 3 Elements in A

1. **Three-number algorithm:**
   - If the three elements aren’t in order:
     - Rotate the largest to the bottom.
     - Swap the top two if necessary.

---

### 🔁 Phase 3: Push Elements Back from B to A

1. **Find the target node in A:**
   - For each number in B, find the largest number in A that is smaller.
   - If none exists, the target is the smallest number in A.

2. **Cost calculation:**
   - Calculate how many moves are needed to bring both the number and its target to the tops of their stacks.

3. **Push the cheapest:**
   - Move the number from B to A with the **lowest cost**.

4. **Repeat:**
   - Until B is empty.

---

### 🔄 Final Phase: Rotate to Smallest

- Once all numbers are in A, **rotate A** until the smallest number is on top.

---

## 🧪 Example Execution

### Input:
```bash
./push_swap 2 7 5 4 3 6 1
````

### Step-by-step:

1. **Initial Stack A:**

```
A (top to bottom):
2
7
5
4
3
6
1
```

2. **Push 2 to B:**

```
A       B
7       2
5
4
3
6
1
```

3. **Push 7 to B:**

```
A       B
5       7
4       2
3
6
1
```

4. **Repeat until only 3 remain in A**

5. **Sort the 3 elements in A**

6. **Push from B to A using the minimum cost algorithm**

7. **Rotate A to bring the smallest number on top**

Final result:

```
A (sorted):
1
2
3
4
5
6
7

B: (empty)
```

---

## 📚 Useful Resources

* `man 3 atoi`
* `man 2 write`
* `man 3 malloc`
* [Wikipedia: Stack (data structure)](https://en.wikipedia.org/wiki/Stack_%28abstract_data_type%29)
* [Push\_swap visualizer (GitHub)](https://github.com/o-reo/push_swap_visualizer)

---

## 🧠 Practical Tips

* Start by handling input and validating arguments (no duplicates, only valid integers).
* Use a `t_stack` struct with `prev` / `next` pointers to manage stacks efficiently.
* Implement helper functions like `is_sorted`, `stack_len`, `get_min` early.
* Print stack contents during development to debug.
* Separate responsibilities clearly: cost, target node, best move.
* Create test scripts for 3, 5, and 100+ elements.
* Make it work first — then focus on optimization.

---
