# OS Lecture 11 - Process Management

## Topics Covered
1. Swapping
2. Context Switching
3. Orphan Process
4. Zombie Process

---

## 1. Schedulers Overview

### Types of Schedulers

#### **LTS (Long Term Scheduler)**
- Also called **Job Scheduler**
- Works on **Job Queue** (in secondary storage)
- Creates **mix of processes**
- Balances I/O intensive and CPU intensive processes
- Prevents starvation by maintaining good process mix

#### **STS (Short Term Scheduler)**
- Also called **CPU Scheduler**
- Works on **Ready Queue**
- Dispatches processes to CPU based on scheduling algorithm

#### **MTS (Medium Term Scheduler)**
- Introduced later in modern OS
- Not present in classic OS
- Performs **swapping operations**

---

## 2. Swapping

### What is Swapping?

**Swapping** is the process of moving processes between main memory and secondary storage to manage memory efficiently.

### Why Swapping is Needed

- When degree of multiprogramming increases
- Memory becomes insufficient for all processes in ready queue
- Some processes are more memory-intensive
- Need to free up memory for active processes

### Process Flow

```
Ready Queue (P1, P2, P3, P4)
       ↓
P1, P2 are memory intensive → Memory full
       ↓
Swap Out P3, P4 → Swap Space (Secondary Storage)
       ↓
Memory freed → P1, P2 work properly
       ↓
P1 terminates → Space available
       ↓
Swap In P3, P4 from secondary storage
```

### Key Terms

- **Swap Out**: Moving processes from main memory to secondary storage
- **Swap In**: Moving processes from secondary storage back to main memory
- **Swap Space**: Area in secondary storage (SSD/HD) where swapped processes are stored
- Performed by **Medium Term Scheduler (MTS)**

### Important Points

- Partially executed processes are swapped out
- Process state/context is saved in swap space
- Secondary storage is larger and cheaper than RAM
- Reduces memory pressure on the system

---

## 3. Context Switching

### Definition

**Context Switching** is the process of saving the state of a currently running process and loading the state of another process to execute.

### Real-Life Example

Playing a game → Papa calls to get food from delivery boy → Pause game, save context → Get food → Resume game with saved context

### When Context Switching Occurs

1. Process goes to **wait state** (I/O operation)
2. Process **time quantum finishes** (in time-sharing systems)
3. Process needs to be preempted

### Process Control Block (PCB) Components

```
PCB Structure:
- Program Counter (PC)
- Registers
- Process State
- Process ID (PID)
- File Handles/Descriptors (FD)
```

### Context Switching Process

**Process P1 executing:**
1. Save current context of P1 in PCB1
   - Save register values
   - Save program counter (current instruction address)
   - Save process state
   - Save file descriptors

**Switch to Process P2:**
2. Restore context of P2 from PCB2
   - Load register values
   - Load program counter
   - Load process state
   - Restore file descriptors

### Important Characteristics

- **Pure Overhead**: No useful work done during context switching
- CPU executes kernel code for switching, not user processes
- All processes in ready queue are idle during switching
- **Speed depends on**:
  - Register performance
  - Memory speed (DDR2, DDR3, DDR4, etc.)
  - Different for different machines

---

## 4. Orphan Process

### Definition

An **Orphan Process** is a process whose parent process has terminated before the child process completes execution.

### How Orphan Process is Created

```
Parent Process (P1) - Running
       ↓ fork()
Child Process (P2) - Running
       ↓
P1 terminates (exception/no wait) → P2 becomes orphan
       ↓
OS adopts P2 → Init process becomes new parent
```

### Key Points

- **Init process**: First process in OS (PID = 1)
- When parent exits without waiting, child becomes orphan
- OS intelligently reassigns orphan process to **init process**
- Init process becomes the new parent
- Maintains process tree structure

### Process Hierarchy

```
Init (PID = 1)
  ↓
  P1 → P2 (child)
  
After P1 exits:
Init (PID = 1)
  ↓
  P2 (adopted)
```

### Best Practice

- Parent should call **wait()** for child processes
- Parent should wait for child to complete
- Prevents orphan process creation

### Live Example Scenario

```bash
Terminal (PID: 9161)
  ↓
  orphan.sh (PID: 9185)
    ↓
    sleep 200

After orphan.sh exits:
Terminal (PID: 9161)
sleep 200 (PPID: 1) ← Now parent is init
```

---

## 5. Zombie Process

### Definition

A **Zombie Process** (also called **Defunct Process**) is a process that has completed execution but still has an entry in the process table.

### How Zombie Process is Created

```
Parent (P1) - Running
       ↓ fork()
Child (P2) - Running
       ↓
P2 calls exit() → Execution complete
       ↓
Resources released BUT entry remains in process table
       ↓
P1 hasn't called wait() yet → P2 becomes ZOMBIE
       ↓
P1 calls wait() → Reads exit status → Entry removed
```

### Why Zombies are Problematic

1. **Process table exhaustion**: Each zombie occupies one entry
2. **Limited PID availability**: PIDs cannot be reused
3. **Resource leak**: If parent never calls wait()
4. **System degradation**: Too many zombies prevent new process creation

### Normal Process Flow

```
Parent creates child
       ↓
Child executes
       ↓
Child calls exit() → Releases resources
       ↓
Parent calls wait() → Reads exit status
       ↓
Entry removed from process table (Reaping)
       ↓
Parent exits
```

### Zombie Process Flow

```
Parent creates child
       ↓
Child executes
       ↓
Child calls exit() (2 minutes)
       ↓
Resources released, entry remains
       ↓
Parent calls wait() (5 minutes)
       ↓
Gap of 3 minutes → ZOMBIE state
```

### Key Characteristics

- **All resources released** except process table entry
- **Exit status preserved** for parent to read
- **Cannot be killed** with normal signals
- **Reaping**: Removing zombie from process table after parent reads exit status

### Live Example

```bash
Terminal (PID: 9161)
  ↓
  zombie.sh (PID: 9569)
    ↓
    Multiple sleep 1 processes (fork with &)
    
After 1 second:
- Sleep processes complete
- Entries remain (zombies)
- Parent still running (sleep 100)

After parent reads exit status:
- All zombie entries removed
- Process table cleared
```

---

## Summary Table

| Aspect | Orphan Process | Zombie Process |
|--------|---------------|----------------|
| **Definition** | Parent died before child | Child died, waiting for parent |
| **Parent Status** | Terminated | Still running |
| **Child Status** | Still running | Execution completed |
| **Resources** | Allocated | Released (except table entry) |
| **Solution** | Adopted by init | Parent calls wait() |
| **Problem** | None (OS handles) | Process table exhaustion |
| **Also Called** | - | Defunct Process |

---

## Important Commands

### Check for Zombie Processes
```bash
ps -al | grep Z
```

### View Process Tree
```bash
ps -ef
pstree
```

### Process Information
- **PID**: Process ID
- **PPID**: Parent Process ID
- **PPID = 1**: Parent is init process

---

## Key Takeaways

1. **Swapping** manages memory by moving processes to/from secondary storage
2. **Context Switching** is overhead but necessary for multitasking
3. **Orphan Processes** are adopted by init process automatically
4. **Zombie Processes** must be reaped by parent calling wait()
5. Good programming practice: Always call wait() for child processes
6. Process table is a limited resource - must be managed carefully

---

## Interview Important Points

- Difference between orphan and zombie processes
- How they are formed
- Which scheduler performs swapping (MTS)
- Context switching is pure overhead
- Init process (PID = 1) is the first process
- Zombie process reaping mechanism
- Process table exhaustion issues
