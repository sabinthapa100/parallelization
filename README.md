This is about parallelization -- to acheive performance in the current computing hardwares!

My reference is this: https://education.molssi.org/parallel-programming/


Introduction: What is Parallelization?

Most strategies for speeding up code focus on efficiency—writing better algorithms or using faster languages to reduce the total amount of work a computer has to do. Parallelization takes a different approach: instead of reducing the workload, it divides that work among multiple processing units (CPUs or GPUs) that labor simultaneously.

Think of it like building a house. A single worker might take a year to finish the job, but ten workers—if managed well—could finish it in a fraction of the time.

The Core Principles:
While the concept is simple, the execution involves a few key constraints:
1. The "Ideal" Speedup: If a task takes $t$ hours on one processor, the goal is for it to take $t/n$ hours on $n$ processors.
2. The Coordination Tax: Parallelization doesn’t actually reduce the total work; in fact, it often adds work because the processors must communicate and coordinate with one another.
3. Amdahl’s Law: This principle reminds us that a program can only go as fast as its most stubborn "serial" part (the tasks that simply cannot be split up). In general, if a calculation takes t hours to run in serial (that is, on a single processing unit, which can be either CPU or GPU or VPU or TPU), it will take at least t/n hours to run on n processing units; this principle is more formally expressed through Amdahl’s law. 

A primary goal of parallelization is to ensure that the actual parallelized runtimes are as close to the ideal runtime of t/n as possible.

These are the types of parallelization:

1. Distributed-Memory (Processes): Runs multiple independent instances of an executable across different cores; offers high scalability but requires more memory as each process maintains its own data copy.
2. Shared-Memory (Threads): Utilizes multiple threads within a single memory allocation; this is highly memory-efficient but limited to a single node since all threads must access the same RAM.
3. Vectorization (SIMD): Leverages "Single Instruction, Multiple Data" hardware to perform one operation on multiple data points simultaneously; primarily managed by the compiler to optimize core-level performance.
4. Heterogeneous Computing: Offloads specific parts of a calculation from the CPU to specialized accelerators like GPUs or FPGAs to increase processing speed. 

Here, I have three folders where I will work on those things in details for my practice: cuda (heterogenous), sharedmem (openMP) and distmem (mpi4py or mpi)


