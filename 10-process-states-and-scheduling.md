# OS Lecture 10: Process States and Scheduling

## Overview
This lecture covers process states, their life cycle, and the different types of schedulers and queues in operating systems.

---

## Process State

**Definition:** The current status/stage of a process throughout its lifecycle, stored in the Process Control Block (PCB).

### Five States of a Process

1. **New State**
   - Process is being created
   - Program is being converted into a process
   - State written in PCB: "NEW"

2. **Ready State**
   - Process is created and loaded into memory
   - Located in the ready queue
   - Ready for execution, only needs CPU allocation
   - Multiple processes can exist in ready queue (multiprogramming)

3. **Running State**
   - Process has been allocated CPU
   - Currently being executed
   - Only one process per CPU core

4. **Waiting State**
   - Process is waiting for I/O completion
   - Cannot proceed until I/O operation finishes
   - Also called blocked state

5. **Terminated State**
   - Process execution is complete
   - Process no longer exists in memory
   - Resources are deallocated

---

## Process Life Cycle

```
[Disk/Pool] → NEW → READY → RUNNING → TERMINATED
                       ↑        ↓
                       |     WAITING
                       └────────┘
```

### State Transitions

1. **New → Ready:** Process creation complete, moved to ready queue
2. **Ready → Running:** CPU scheduler allocates CPU to the process
3. **Running → Waiting:** Process requires I/O operation
4. **Running → Ready:** Time quantum expires (time slice finished)
5. **Running → Terminated:** Process execution completes
6. **Waiting → Ready:** I/O operation completes (NOT directly to running)

### Important Notes:
- When a process completes I/O, it returns to **ready queue**, NOT running state
- Scheduler decides when the process gets CPU again based on priority and scheduling algorithm
- Software interrupts are used to move processes back to ready queue when time quantum expires

---

## Types of Queues

### 1. Job Queue
- Contains all processes in **new state**
- Processes waiting to be admitted to ready queue
- Largest pool of processes

### 2. Ready Queue
- Contains processes in **ready state**
- Processes loaded in memory, waiting for CPU
- Number of processes governed by degree of multiprogramming

### 3. Waiting Queue
- Contains processes in **waiting state**
- Processes waiting for I/O completion
- Multiple processes can wait simultaneously

---

## Types of Schedulers

### 1. Job Scheduler (Long-Term Scheduler - LTS)

**Function:**
- Picks processes from job pool (disk)
- Converts programs to new state
- Moves them to ready queue

**Characteristics:**
- **Low frequency** operation
- Checks job pool at longer intervals (e.g., every 1 minute)
- More "lazy" compared to CPU scheduler
- Higher idle time between executions

**Responsibility:**
- Controls **degree of multiprogramming**
- Determines how many processes can be in ready queue at once

### 2. CPU Scheduler (Short-Term Scheduler - STS)

**Function:**
- Picks processes from ready queue
- Dispatches them to CPU for execution
- Uses scheduling algorithms to determine order

**Characteristics:**
- **High frequency** operation
- Checks constantly (every few milliseconds)
- Minimal idle time
- Ensures CPU is never idle

**Working:**
- Continuously monitors CPU status
- Immediately schedules new process when CPU becomes free
- Works with dispatcher to allocate CPU

### 3. Dispatcher

**Function:**
- Module that actually provides CPU to the selected process
- Performs context switching
- Transfers control to the process

---

## Why Different Names?

### Long-Term Scheduler (LTS)
- Called "long-term" because of **lower frequency**
- Operates with longer time gaps between executions
- Example: Checks job pool every 1 minute

### Short-Term Scheduler (STS)
- Called "short-term" because of **higher frequency**
- Operates almost continuously
- Immediately responds when CPU becomes free
- Ensures minimal CPU idle time

---

## Degree of Multiprogramming

**Definition:** Maximum number of processes that can exist in ready queue simultaneously

**Controlled by:** Job Scheduler (Long-Term Scheduler)

**Example:** If degree = 5, maximum 5 processes can be in ready queue at time t=0

---

## Example Scenario

### Initial State:
- Ready Queue: P1, P2, P3

### Execution Flow:

1. **t=0:** CPU scheduler selects P3
   - P3 moves to running state
   - Ready Queue: P1, P2

2. **t=1:** P3 requests I/O
   - P3 moves to waiting state
   - CPU becomes free
   - CPU scheduler immediately selects P2
   - Ready Queue: P1

3. **t=2:** P2 moves to running state
   - P2 requests I/O
   - P2 moves to waiting state
   - CPU scheduler selects P1

4. **t=3:** P3 completes I/O
   - P3 returns to **ready queue** (not running!)
   - Ready Queue: P3
   - P1 continues running

5. **Later:** P3 gets scheduled again based on algorithm and priority

---

## Key Takeaways

1. Process state is stored in PCB
2. Five states: New, Ready, Running, Waiting, Terminated
3. Processes returning from I/O go to ready queue, not directly to running
4. Three types of queues: Job, Ready, Waiting
5. Job Scheduler (LTS) controls degree of multiprogramming
6. CPU Scheduler (STS) ensures minimal CPU idle time
7. Frequency difference: STS >> LTS
8. Software interrupts handle time quantum expiration

---

## Summary Diagram

```
                    Job Scheduler (LTS)
                           ↓
[Job Queue] → [New] → [Ready Queue] → [Running] → [Terminated]
                           ↑              ↓
                           |         [Waiting Queue]
                           └──────────────┘
                      
                    CPU Scheduler (STS)
                           ↑
                      Dispatcher
```

---

**End of Lecture 10**
