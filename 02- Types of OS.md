# Operating System Lecture 2 - Types of Operating Systems

## Goals of Operating Systems

Before understanding types of OS, we need to know what goals were kept in mind while designing them:

### 1. Maximum CPU Utilization
- CPU should never sit idle when processes are available
- Example: If Process P1 goes to I/O operation, CPU should immediately start executing P2
- Goal: Keep CPU busy at all times

### 2. No Process Starvation
- Every process should get a chance to execute
- Problem scenario: If P1 has an infinite loop (while(1)), P2 and P3 would never get CPU time
- Solution: Operating system must ensure all processes get execution time

### 3. High Priority Job Execution
- OS should support priority-based execution
- Example: Antivirus scan when USB is inserted is a high-priority task
- High-priority jobs should preempt normal jobs when necessary

---

## Types of Operating Systems

### 1. Single Process OS

**Characteristics:**
- Only one job executes at a time
- Oldest type of OS
- Sequential execution: P1 → P2 → P3

**Drawbacks:**
- ❌ No maximum CPU utilization (if P1 goes to I/O, P2 cannot execute)
- ❌ Process starvation exists (if P1 is a big job, P2 and P3 wait indefinitely)
- ❌ No high-priority job execution

**Example:** MS-DOS

**Historical Context:** Software was developed according to available hardware capabilities at that time

---

### 2. Batch Processing OS

**How it works:**
- Multiple users submit jobs using **punch cards**
- Operator collects all jobs and sorts them based on requirements
- Jobs are divided into batches of similar types
- Each batch is submitted sequentially to CPU

**Process Flow:**
1. Users submit jobs via punch cards (physical cards with holes representing binary information)
2. Operator sorts jobs by requirements
3. Jobs grouped into batches (Batch-1: Job1, Job4 | Batch-2: Job2, Job5, Job7)
4. Batches executed sequentially

**Drawbacks:**
- ❌ No maximum CPU utilization (sequential execution within batches)
- ❌ Process starvation (both job and batch level)
- ❌ No high-priority job execution until current batch completes

**Example:** ATLAS

---

### 3. Multi-Programming OS

**Key Features:**
- Single CPU
- Multiple processes in **Ready Queue** (queue of processes ready to execute)
- **Context switching** when process goes to I/O or wait state

**How it works:**
- When P1 goes to I/O, CPU immediately switches to P2
- Creates virtual environment where CPU is always busy
- Processes don't wait for I/O completion of other processes

**Context Switching Explained:**

*Real-life analogy:* Studying Physics, then switching to Chemistry
- Close all Physics books and save bookmarks (save state)
- Open Chemistry books from where you left (restore state)

*In OS:*
1. Save P1's current context in **PCB (Process Control Block)**
   - Current position, call stack, all process information
2. Remove P1 from CPU
3. Restore P2's context from PCB
4. CPU starts working on P2

**Benefits:**
- ✅ Better CPU utilization
- ⚠️ Still has some starvation issues
- ⚠️ High-priority jobs still face delays

**Example:** THE

---

### 4. Multi-Tasking OS

**Key Concept:** Logical extension of Multi-Programming + **Time Sharing**

**Major Difference from Multi-Programming:**
- Doesn't wait for I/O to do context switching
- Uses **time quantum** (e.g., 100ms per process)
- After time quantum expires, CPU switches to next process regardless of I/O

**How it works:**
- P1 gets 100ms → P2 gets 100ms → P3 gets 100ms → repeat
- Even if P1 doesn't go to I/O, it's preempted after its time quantum

**Benefits:**
- ✅ Maximum CPU utilization (CPU never idle)
- ✅ Minimal process starvation (every process gets equal time slices)
- ✅ High-priority job execution (can interrupt via software interrupt)
- ✅ Increased responsiveness (all apps feel responsive)

**Modern Usage:** Most current operating systems are multi-tasking

**Example:** CTSS

---

### 5. Multi-Processing OS

**Key Feature:** **Multiple CPUs (CPU ≥ 1)**

**Characteristics:**
- Includes all features of multi-tasking (context switching, time sharing)
- Multiple CPUs/cores (modern CPUs have 4, 8, or more cores)
- Each core acts as a logical processor

**How it works:**
- CPU-1 executes P1, P2 with time sharing
- CPU-2 executes P3, P4 simultaneously
- OS decides which job goes to which CPU (process scheduling algorithms)

**Additional Benefits:**
- ✅ Even better CPU utilization
- ✅ Less starvation
- ✅ **Increased reliability**: If CPU-1 fails, CPU-2 continues working
- ✅ True parallel processing

**Example:** Windows

---

### 6. Distributed OS (Loosely Coupled OS)

**Architecture:**
- One OS managing multiple CPUs and memories
- Systems connected over network (Internet/LAN)
- Different systems in different physical locations

**How it works:**
- Multiple autonomous computers interconnected
- Jobs distributed across different systems
- P1 → Computer 1, P2 → Computer 2, P3 → Computer 3
- Each computer may have different capabilities (low-end, high-end, with/without GPU)

**Use Case Example:**
- Online coding platforms (LeetCode, CodeChef)
- Code submitted is executed on available Linux machines
- Whichever system is free gets the work

**Key Terms:**
- Loosely coupled
- Autonomous
- Interconnected computers
- Multiple users and resources

---

### 7. Real-Time OS (RTOS)

**Key Requirements:**
- Zero error tolerance
- High accuracy (to decimal points)
- Real-time computation
- Deterministic behavior

**Where Used:**
- ✈️ **Flight Control Systems** - Air Traffic Control (ATC)
- ⚛️ **Nuclear Plants** - Critical industrial applications
- 🏭 **Industrial Automation**
- 🏥 **Medical Equipment**
- Any system where human lives depend on accuracy

**Characteristics:**
- Error-free computation mandatory
- Real-time processing
- Highly reliable and predictable

---

## Summary Table

| OS Type | CPU Count | Key Feature | CPU Utilization | Starvation | Example |
|---------|-----------|-------------|----------------|------------|---------|
| Single Process | 1 | One process at a time | ❌ Low | ❌ High | MS-DOS |
| Batch Processing | 1 | Jobs in batches | ❌ Low | ❌ High | ATLAS |
| Multi-Programming | 1 | Context switching on I/O | ⚠️ Medium | ⚠️ Medium | THE |
| Multi-Tasking | 1 | Time sharing | ✅ High | ✅ Low | CTSS |
| Multi-Processing | Multiple | Multiple CPUs | ✅ Very High | ✅ Very Low | Windows |
| Distributed | Multiple (networked) | Networked systems | ✅ High | ✅ Low | Cloud systems |
| Real-Time | Varies | Zero error tolerance | ✅ High | ✅ Low | ATC systems |

---

## Important Interview Concepts

### Most Important Types (Focus Areas):
1. **Single Process OS**
2. **Batch Processing OS**
3. **Multi-Programming OS**
4. **Multi-Tasking OS**
5. **Multi-Processing OS**

### Key Differences to Remember:

**Multi-Programming vs Multi-Tasking:**
- Multi-Programming: Context switch only on I/O
- Multi-Tasking: Context switch based on time quantum (time sharing)

**Multi-Tasking vs Multi-Processing:**
- Multi-Tasking: Single CPU with time sharing
- Multi-Processing: Multiple CPUs

### Context Switching:
- Process of saving one process state and loading another
- Uses PCB (Process Control Block) to store/restore process information
- Involves saving: current position, call stack, process state, registers

---

## Key Terminology

**Ready Queue:** Queue containing all processes that are ready to execute and waiting for CPU time

**Punch Card:** Physical card with holes representing binary information, used in early computing for job submission

**PCB (Process Control Block):** Data structure that stores all information about a process

**Time Quantum:** Fixed time slice allocated to each process in time-sharing systems

**Context Switching:** The process of saving the state of a currently running process and loading the state of another process

**Process Starvation:** Situation where a process never gets CPU time to execute

---

## Historical Note

**Development Philosophy:**
- Software is always developed according to hardware capabilities
- Cannot create software first and then build hardware for it
- Hardware limitations drive software design
- OS evolution has been incremental and gradual

---

## Homework

Find and comment additional examples for:
- Distributed OS
- Real-Time OS (RTOS)

---

## Visual Summary

```
Evolution of Operating Systems:

Single Process → Batch Processing → Multi-Programming → Multi-Tasking → Multi-Processing
     ↓                ↓                   ↓                  ↓                ↓
  One job         Batches of          Context            Time            Multiple
  at a time       similar jobs        Switching          Sharing          CPUs

                                    ↓                      ↓
                              Distributed OS         Real-Time OS
                           (Network of systems)    (Critical systems)
```

---

*Notes from Code Help - Operating Systems Series Lecture 2*  
*Instructor: Lakshay (Code Help)*