# Parallelization for Scientific Computing  
**Author:** Sabin Thapa  
**Email:** sthapa3@kent.edu  
**Affiliation:** Kent State University  
**Status:** Learning, experimentation, and long-term skill development  
**Primary Reference:** https://education.molssi.org/parallel-programming/

---

## Motivation

Modern computing performance no longer comes primarily from faster clock speeds. Instead, performance gains arise from **parallel hardware**: multi-core CPUs, many-core GPUs, vector units, and distributed clusters.

This repository is my **hands-on learning space** for understanding and practicing **parallelization**, with a focus on **scientific and physics applications**. The intent is not to chase peak performance immediately, but to **build correct intuition first**, then apply these ideas to real research problems.

Typical physics use cases motivating this work include:
- Numerical simulations
- Monte-Carlo sampling
- Parameter sweeps
- Transport equations
- Lattice-based models
- Event-by-event calculations

This repository is intentionally incremental:  
> **learn → test → understand → apply**

---

## What Is Parallelization?

Most strategies for speeding up code focus on **efficiency**:
- Better algorithms
- Faster numerical methods
- Optimized data structures
- Lower-level languages

These approaches reduce the **total amount of work** the computer must perform.

**Parallelization takes a different approach.**

Instead of reducing the workload, it **divides the same workload among multiple processing units**—CPUs, GPUs, or accelerators—so that work is done **simultaneously**.

### A Simple Analogy

Building a house:
- One worker may take a year.
- Ten workers—if coordinated well—can finish much faster.

However, coordination itself takes effort.  
Parallel computing behaves the same way.

---

## Core Principles of Parallel Computing

While the idea of parallelization is simple, its execution is constrained by several fundamental principles.

---

### 1. Ideal Speedup

If a task takes time \( t \) to run on a single processing unit, the ideal runtime on \( n \) processing units is:

\[
t_{\text{ideal}} = \frac{t}{n}
\]

This represents the **best-case scenario** and serves as an upper bound on performance.

In practice, this ideal is rarely achieved.

---

### 2. The Coordination Tax

Parallelization does **not** reduce the total amount of work.  
In fact, it often **adds work**, due to:
- Communication between processors
- Synchronization and barriers
- Memory contention
- Data movement (especially CPU ↔ GPU)

This overhead is the **price paid** for parallel execution.

---

### 3. Amdahl’s Law (The Fundamental Limit)

Every real program contains some portion that **cannot be parallelized**.

If a fraction \( f \) of the program is strictly serial, the maximum achievable speedup on \( n \) processors is:

\[
S(n) = \frac{1}{f + \frac{1-f}{n}}
\]

This means:
- No matter how many processors are used,
- The serial portion ultimately limits performance.

> A parallel program is only as fast as its most stubborn serial section.

---

### Practical Goal

The goal of parallelization is **not perfect scaling**, but to ensure that actual runtimes approach the ideal \( t/n \) as closely as possible **within hardware and algorithmic constraints**.

---

## Types of Parallelization Explored Here

This repository focuses on the main parallel paradigms used in modern scientific computing.

---

### 1. Distributed-Memory Parallelism (Processes)

**Concept**
- Multiple independent processes
- Each process has its own memory space
- Communication via message passing

**Typical tools**
- MPI
- `mpi4py`

**Strengths**
- Excellent scalability
- Works across nodes and clusters

**Tradeoffs**
- Higher memory usage
- Explicit communication required

📁 **Folder:** `distmem/`

---

### 2. Shared-Memory Parallelism (Threads)

**Concept**
- Multiple threads operating within a single memory space
- All threads share the same RAM

**Typical tools**
- OpenMP
- Threading libraries

**Strengths**
- Memory efficient
- Fast communication between threads

**Tradeoffs**
- Limited to a single node
- Requires careful synchronization to avoid race conditions

📁 **Folder:** `sharedmem/`

---

### 3. Vectorization (SIMD)

**Concept**
- Single instruction applied to multiple data elements simultaneously
- Occurs at the CPU core level

**Typical tools**
- Compiler auto-vectorization
- NumPy / BLAS
- Explicit SIMD intrinsics (advanced)

**Strengths**
- Very high performance
- Minimal code changes in many cases

**Tradeoffs**
- Less direct programmer control
- Sensitive to data layout and memory access patterns

*(Often implicit inside examples rather than a standalone folder.)*

---

### 4. Heterogeneous Computing

**Concept**
- Offloading computation from CPUs to specialized accelerators
- GPUs, TPUs, or FPGAs

**Typical tools**
- CUDA
- GPU-accelerated Python libraries

**Strengths**
- Massive parallelism
- Excellent for dense numerical workloads

**Tradeoffs**
- Data transfer overhead
- Hardware-specific programming models

📁 **Folder:** `cuda/`

---

## Repository Structure

```text
parallelization/
│
├── distmem/        # Distributed memory (MPI / mpi4py)
│
├── sharedmem/      # Shared memory (OpenMP, threading)
│
├── cuda/           # Heterogeneous computing (GPU / CUDA)
│
└── README.md
