# OS Lecture 3: Multiprogramming, Multiprocessing, Multitasking & Multithreading

## Overview
This lecture covers the key differences between multiprogramming, multiprocessing, multitasking, and multithreading - a common interview topic in Operating Systems.

---

## What is a Program?

**Program**: An executable file containing instructions to execute specific jobs
- Written in text files (e.g., `.cpp` files)
- Collection of characters (code)
- Compiler compiles the code to create executable (`.exe`) file
- Compiled code is in bits/bytes format - only OS can read it
- Executable code is **platform dependent** (different for Mac, Windows, Linux)
- **Stored in disk** (secondary storage)

### Example
When you write a C++ program to find prime numbers:
1. Code written in `.cpp` file
2. Compiler compiles it
3. Creates `.exe` file
4. Double-clicking `.exe` opens the program (e.g., MS Paint)

---

## What is a Process?

**Process**: Program under execution
- When you double-click an `.exe` file, the program is brought into execution
- Program moves from disk to **RAM (primary memory)**
- CPU only works when program is in RAM
- **Process = Program loaded in memory and being executed**

### Key Points
- Program exists on disk (compiled code)
- Process exists in RAM (program in execution)
- CPU executes processes from RAM
- Each process runs as a single entity with its own memory block

---

## What is a Thread?

**Thread**: Lightweight process
- **Single sequence stream within a process**
- **Independent path of execution**
- Sub-process inside a main process
- Used to achieve **parallelism** within a process
- Enables independent work within a process

### Characteristics of Threads
1. Lightweight process
2. Can execute independently
3. Part of a parent process
4. Shares memory space with other threads of the same process
5. No isolation between threads (unlike processes)

---

## Thread Examples

### Example 1: Facebook Profile Storage
When using Facebook:
- **Main Process**: Takes user input, processes it, displays information
- **Thread (background)**: Stores data to cloud asynchronously
- Writing to cloud happens independently without user awareness
- Work is divided: main task + sub-task (cloud storage via thread)

### Example 2: JPG to PNG Converter

**Without Multithreading (Sequential)**:
- Logic can only process 100×100 pixels at a time
- Image is 100×200 pixels
- Break into Part A and Part B
- Process Part A → Output A1 (10 seconds)
- Process Part B → Output B1 (10 seconds)
- Concatenate A1 and B1
- **Total time: 20 seconds**

**With Multithreading (Parallel)**:
- Thread T1 processes Part A → Output A1
- Thread T2 processes Part B → Output B1
- Both execute simultaneously on different CPUs
- Concatenate A1 and B1
- **Total time: 10 seconds**
- **50% faster execution**

### Example 3: Text Editor
When typing in a text editor (MS Word, Notepad):
- **Thread 1**: Actual typing/input
- **Thread 2**: Spell checking
- **Thread 3**: Formatting
- **Thread 4**: Auto-save

Without multithreading, these would happen sequentially - you'd have to wait for spell check, formatting, and saving before continuing to type.

### Example 4: Web Browser Tabs
Google Chrome tabs:
- Each tab runs as a separate thread
- Single code base for tab functionality
- New tabs spawn new threads
- Allows multiple tabs to work simultaneously

---

## Multithreading Requirements

### CPU Core Requirements
- Multithreading requires **multiple CPU cores** for true parallel execution
- **Number of cores = Number of threads** (optimal)
- With single CPU: threads will context switch (no performance gain)
- Modern systems have multiple cores (latest Mac: 8 cores)

### Example
- **1 CPU core**: Can execute only 1 task at a time
- **2 threads on 1 core**: Will context switch between threads (no benefit)
- **2 threads on 2 cores**: True parallel execution (significant benefit)
- **Don't create more threads than available cores** - no benefit beyond hardware capacity

---

## Multitasking vs Multithreading

| Aspect | Multitasking | Multithreading |
|--------|--------------|----------------|
| **Concept** | Multiple processes sharing CPU time | Multiple threads within a single process |
| **Scope** | Between processes (P1, P2, P3) | Within a process (T1, T2, T3 of P1) |
| **CPUs Required** | 1 CPU (context switching) | ≥1 CPU (parallel execution needs multiple cores) |
| **Memory Isolation** | Yes - each process has separate memory | No - threads share same memory space |
| **Memory Protection** | Yes - OS ensures isolation | No - all threads use same memory block |
| **Scheduling** | Processes are scheduled on CPU | Threads are scheduled within process |
| **Context Switching** | Between different processes | Between threads of same process |
| **Memory Switching** | Required during context switch | Not required (same address space) |

---

## Thread Scheduling

Threads are scheduled based on **priority**:
- When process P1 gets CPU time, its threads (T1, T2) compete for execution
- Higher priority thread gets more CPU time
- If equal priority, default scheduling applies
- Priority is set when threads are spawned

### Example
- Process P1 allocated CPU time slot
- P1 has threads T1 (high priority) and T2 (low priority)
- T1 will get more execution time within P1's time slot

---

## Context Switching: Threads vs Processes

### Thread Context Switching
- **Faster** than process context switching
- No memory address space switching required
- Threads share same memory space
- CPU cache state **remains preserved**
- Previous cache data may be useful for other threads

### Process Context Switching
- **Slower** than thread context switching
- Memory address space must be switched
- Each process has isolated memory
- CPU cache must be **flushed**
- Cache data from previous process is not useful for next process

### Why the Difference?
**Threads**: Same process, same memory area → cache can be reused
**Processes**: Different processes, different memory → cache must be cleared

---

## Memory Management

### Process Memory Allocation
```
RAM Memory:
┌─────────────┐
│   Process P1│  ← Separate memory block
├─────────────┤
│   Process P2│  ← Separate memory block
├─────────────┤
│   Process P3│  ← Separate memory block
└─────────────┘
```
- Each process gets independent memory block
- OS ensures isolation and protection
- No interference between processes

### Thread Memory Allocation
```
Process P1 Memory Block:
┌─────────────────────┐
│  Thread T1          │
│  Thread T2          │  ← All threads share
│  Thread T3          │     same memory block
└─────────────────────┘
```
- All threads of a process share the same memory space
- No isolation between threads
- Can access same resources and variables

---

## Summary Table

| Feature | Multiprogramming | Multiprocessing | Multitasking | Multithreading |
|---------|-----------------|-----------------|--------------|----------------|
| **Definition** | Multiple programs in memory | Multiple CPUs/processors | Multiple processes sharing CPU | Multiple threads in a process |
| **CPUs** | 1 | >1 | 1 | ≥1 (multiple for benefit) |
| **Goal** | CPU utilization | Parallel processing | Time sharing | Parallelism within process |
| **Scope** | Programs | Processors | Processes | Threads |
| **Memory** | Separate | Separate | Separate (isolated) | Shared |

---

## Key Interview Points

### Questions You Should Be Ready For
1. **Difference between multitasking and multithreading**
2. **Difference between multiprogramming and multitasking**
3. **Difference between multiprocessing and multitasking**
4. **What is a thread? Why is it called lightweight process?**
5. **Thread vs Process context switching - which is faster and why?**
6. **Why is multithreading beneficial?**
7. **Can we do multithreading on single CPU? What happens?**

### Important Concepts to Remember
- **Program**: Executable file on disk
- **Process**: Program in execution (in RAM)
- **Thread**: Independent execution path within process
- **Isolation**: Exists between processes, NOT between threads
- **Context switching**: Faster for threads than processes
- **Memory**: Separate for processes, shared for threads
- **Cache**: Preserved for threads, flushed for processes

---

## Additional Notes

### Why Multithreading is Important
- Achieves parallelism in applications
- Improves performance on multi-core systems
- Better resource utilization
- Responsive user interfaces
- Background task processing

### Limitations
- Hardware dependent (needs multiple cores for true benefit)
- Shared memory can cause synchronization issues
- More complex to program correctly
- Debugging is harder than single-threaded programs

---

## Course Information
*This lecture is part of an Operating Systems course by Code Help. For more detailed study on process management and threading, refer to upcoming lectures.*

**Sponsored by**: Coding Ninjas - India's leading coding education platform
- In-depth OS course based on Linux
- 12+ hours of content
- 150+ practice problems
- 12+ projects
- One-on-one doubt sessions

---

*Note: Thread concepts will be revisited in the Process Management section for deeper understanding.*