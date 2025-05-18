---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting push_swap)

### 📌 Objective:

Design and implement an efficient sorting algorithm using a **limited set of stack operations**, aiming to sort numbers with the **fewest possible moves**.

---

### 🧱 What Is `push_swap`?

- Receives a list of unordered integers via command-line arguments.
- Outputs to `stdout` a **series of instructions** that sort the numbers using only the allowed operations.
- ✅ It **must not print the numbers**, only the instructions.

---

## 🛠️ Allowed Instructions

You can only use the following operations (assembler-style):

| **Instruction** | **Description**                                                                 |
|-----------------|----------------------------------------------------------------------------------|
| `sa`            | Swap the top two elements of stack A.                                           |
| `sb`            | Swap the top two elements of stack B.                                           |
| `ss`            | Apply `sa` and `sb` at the same time.                                           |
| `pa`            | Push the top element of B onto A.                                               |
| `pb`            | Push the top element of A onto B.                                               |
| `ra`            | Rotate all elements of A up by 1. First becomes last.                           |
| `rb`            | Rotate all elements of B up by 1.                                               |
| `rr`            | Apply `ra` and `rb` at the same time.                                           |
| `rra`           | Reverse rotate A: last element becomes first.                                   |
| `rrb`           | Reverse rotate B.                                                               |
| `rrr`           | Apply `rra` and `rrb` at the same time.                                         |

---

## 🎯 Final Objective

You must create a sorting algorithm that:

* ✅ Correctly sorts any list of **unique integers**.
* ✅ Uses **only** the allowed operations.
* ✅ Is **efficient** (less than 700 moves for 100 numbers).
* ✅ Is **robust** (handles errors, invalid input, etc.).

---

## ⚙️ Sorting Algorithm Overview

The sorting algorithm can be split into **three main phases**:

---

### 🔁 Phase 1: Move Elements from A to B

1. **Initial Setup:**
   - Push the first two elements from A to B without any condition.

2. **Target Node in B:**
   - For each element in A, find a “target” in B: the smallest number in B that is greater than the current number.
   - If none exists, the target is the largest number in B.

3. **Cost Calculation:**
   - For each element in A, calculate the cost of bringing it to the top of A and its target to the top of B.

4. **Select Cheapest Node:**
   - Move the element from A to B with the **lowest operation cost**.

5. **Repeat:**
   - Continue until only **three elements remain in A**.

---

### 🧮 Phase 2: Sort the Remaining 3 Elements in A

1. **Three Element Sort:**
   - If the 3 elements are not sorted:
     - Move the **largest number to the bottom** using rotation.
     - Swap the top two if needed to finish sorting.

---

### 🔁 Phase 3: Move Elements Back from B to A

1. **Find Target Node in A:**
   - For each element in B, find the biggest number in A that is smaller.
   - If none exists, the target is the smallest number in A.

2. **Calculate Cost:**
   - For each element in B, calculate the number of moves to bring it and its target into the right positions.

3. **Push the Cheapest Element:**
   - Move the element with the **lowest cost** back to A.

4. **Repeat:**
   - Continue until B is empty.

---

### 🔄 Final Adjustment: Rotate the Smallest to Top

- Once all elements are back in A, **rotate A** until the smallest number is at the top.

---

## 🧪 Example Execution

### Initial input:
```bash
./push_swap 2 7 5 4 3 6 1
