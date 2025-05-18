---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting Philosophers)

### 📌 Objective:

This project focuses on **concurrent programming**. It challenges you to solve a classic computer science problem that teaches how to efficiently and safely manage **shared resources** across multiple threads. The key concepts are **concurrency**, **synchronization**, and the use of **threads** and **mutexes**.

A group of philosophers alternates between three activities: **eating**, **thinking**, and **sleeping**. Their access to the necessary resources (forks) is limited, and the solution lies in ensuring that each philosopher can complete their cycles **without conflicts or deadlocks**.

---

## 🔹 2. The Dining Philosophers Problem

Originally proposed by **Edsger Dijkstra**, it's a classic metaphor in concurrent programming: several processes (philosophers) must coordinate to access limited shared resources (forks), while avoiding **deadlocks**, **starvation**, or **race conditions**.

### 📅 Problem Setup

* Five philosophers sit at a round table.
* Each philosopher alternates between **eating**, **thinking**, and **sleeping**.
* There are five forks, one between each pair of philosophers.
* To eat, a philosopher needs **both the left and right fork**.
* After eating, they think, then sleep, and repeat the cycle.

Problems arise if synchronization isn't handled properly:

### 🔒 Key Issues

* **Deadlock**: Every philosopher grabs one fork and waits indefinitely for the other.
* **Starvation**: Some philosophers never get to eat because others monopolize the forks.
* **Race conditions**: Multiple philosophers attempt to access the same fork simultaneously, causing data inconsistencies.

---

## 🔹 3. Theoretical Concepts

This project introduces two critical tools for concurrency:

### 🔢 Threads

* A thread is the smallest unit of execution.
* Threads share memory/resources of the parent process, making them lightweight but prone to shared state issues.
* Each philosopher is an independent thread.

In C, you'll use **POSIX Threads (pthreads)**:

* `pthread_create` → Create a new thread.
* `pthread_join` → Wait for a thread to finish.
* `pthread_exit` → End a thread cleanly.
* Use `usleep` to simulate delays.

### ⏳ Context Switching

* Threads don't truly run in parallel (unless using multiple cores).
* The OS switches between them rapidly.
* Proper **synchronization** is key.

### 🔐 Mutexes (Mutual Exclusion)

* Mutexes prevent simultaneous access to shared resources.
* Each fork is protected by a mutex.

Key functions:

* `pthread_mutex_init`
* `pthread_mutex_lock`
* `pthread_mutex_unlock`
* `pthread_mutex_destroy`

Philosophers must:

* Lock the two required fork mutexes to eat.
* Unlock them when finished.

---

## 🔹 4. Solution Strategies

### 🔎 Ordered Resource Acquisition

* Some philosophers pick up the left fork first, others the right.
* This reduces risk of circular waits.

### ❌ Limit Concurrent Eaters

* Only allow (N - 1) philosophers to attempt to eat at the same time.

### 🔼 Fork Hierarchy

* Assign an order to forks.
* Philosophers must always pick up the lower-numbered fork first.

---

## 📃 Project Structure

### Description:

The **Philosophers** project simulates the dining philosophers problem using threads and mutexes.

### File Structure:

```
philosophers/
├── philo.c               // Main entry, argument validation
├── philo_utils.c         // Time, string-to-int, sleep utils
├── philo_start.c         // Simulation setup and start
├── philo_create.c        // Philosopher routine (eat, sleep, think)
├── philo_monitor_deaths.c // Starvation monitoring
├── philo.h               // Header with structs, constants, and prototypes
```

![Diagram](../../img/milestone_3/philo.png)

---

## 📈 Core Features

### 📊 Argument Validation

* Requires 4 or 5 args: number\_of\_philosophers, time\_to\_die, time\_to\_eat, time\_to\_sleep, \[meals\_required]
* All must be positive integers.

### ⚖️ Simulation Initialization

* Forks (mutexes) and philosophers are initialized.
* A thread is created per philosopher.

### 🤔 Philosopher Lifecycle

* `take_forks`: lock left/right forks
* Eat → sleep → think
* One-philosopher case is handled specially.

### 🔎 Death Monitoring

* `monitor_deaths`: independent thread
* Checks if any philosopher exceeded `time_to_die` without eating
* If so, logs and terminates simulation

### ⚖️ Synchronization

* Mutexes ensure exclusive fork access
* Print messages are also mutex-protected to avoid overlapping

---

## 🔴 `philo_monitor_deaths.c` Summary

### Function: `monitor_deaths`

* Continuously checks the time since each philosopher's last meal
* If `time_since_last_meal > time_to_die`:

  * Print death message
  * Stop simulation

Mutexes protect shared access to `last_meal` to avoid race conditions.

---

## 📝 Test Cases

Inside `philo_start.c`:

```c
// No one should die:
./philo 5 800 200 200
./philo 5 600 150 150
./philo 4 410 200 200
./philo 100 800 200 200
./philo 105 800 200 200
./philo 200 800 200 200

// A philosopher should die:
./philo 1 800 200 200
./philo 4 310 200 100
./philo 4 200 205 200

// Error cases:
./philo -5 600 200 200
./philo 4 -5 200 200
./philo 4 600 -5 200
./philo 4 600 200 -5
./philo 4 600 200 200 -5

// Memory leak check:
valgrind --leak-check=full --track-origins=yes --show-leak-kinds=all ./philo
```

---

## 💡 Valgrind

Always use **Valgrind** to detect memory leaks and ensure proper memory management:

```bash
valgrind --leak-check=full --track-origins=yes --show-leak-kinds=all ./philo 5 800 200 200
```

---
