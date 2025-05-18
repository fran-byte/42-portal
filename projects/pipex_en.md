---
layout: default
title: "fran-byte 42 Madrid"
---

## 🔹 1. Prerequisites (Before Starting pipex)

### 📌 Objective:

Recreate the behavior of **shell pipes (`|`) and input/output redirections**, using system calls in C. Your program must **execute two commands in sequence**, redirecting input and output to files, and **connecting them via a pipe**.

---

## 🔧 What Does `pipex` Do?

It executes two chained commands, managing their input/output flow:

```bash
./pipex infile cmd1 cmd2 outfile
