# Lecture 9: Process Management - Introduction

## Course Information
- **Lecture Number:** 9
- **Topic:** Process Management Fundamentals
- **Instructor:** Lakshay

---

## Table of Contents
1. [What is a Process?](#what-is-a-process)
2. [Program vs Process](#program-vs-process)
3. [Process Creation Steps](#process-creation-steps)
4. [Process Architecture in Memory](#process-architecture-in-memory)
5. [Process Attributes](#process-attributes)
6. [Process Control Block (PCB)](#process-control-block-pcb)
7. [Common Memory Errors](#common-memory-errors)

---

## What is a Process?

### Definition
**Process:** A program under execution

- Process is a unit of work done by the computer
- It's how the OS executes user programs
- Process is the active entity, while program is passive

### Simple Analogy
- **Program:** Like an app in your phone's storage (e.g., TikTok app file)
- **Process:** When you tap the app and it starts running in RAM

---

## Program vs Process

### Program
- **Definition:** Code/data ready to execute
- **Location:** Resides on disk
- **State:** Passive/Static
- **Example:** A .exe file, GTA game file on your computer

### How Programs are Created
1. Write code in a text file (e.g., `.cpp` file)
2. Give it to the compiler
3. Compiler creates an executable
4. This executable is the **program**

### Process
- **Definition:** Program under execution
- **Location:** Loaded in RAM (memory)
- **State:** Active/Dynamic
- **Created by:** Operating System

---

## Process Creation Steps

The OS follows **5 main steps** to convert a program into a process:

### Step 1: Load Program and Static Data to Memory
- Program code is loaded from disk to RAM
- **Static data** is also loaded
  - Static data = Data used for initialization
  - Example: `char *name = "Lakshay"` or `int a = 0`
  - This data is written in the program and copied when process is created

### Step 2: Allocate Stack at Runtime
- **Stack** is allocated for:
  - Local variables
  - Function arguments
  - Return values
  - Function call management
- Used during function calls and recursive operations

### Step 3: Allocate Heap
- **Heap** is allocated for:
  - Dynamic memory allocation at runtime
  - Memory allocated using `malloc()` or `new`
  - Runtime memory requirements

### Step 4: I/O Tasks Setup
- In Unix systems, I/O descriptors are created:
  1. **Input handle** - for receiving input
  2. **Output handle** - for writing output
  3. **Error handle** - for error handling (e.g., `stderr` in C++)

**Example in C++:**
```cpp
fprintf(stderr, "error message");
```

### Step 5: Start Execution from main()
- OS hands control to `main()` function
- Process gets control of CPU and memory
- Process begins execution

**Why main()?**
- OS only knows about `main()` function
- Every C++ program starts execution from `main()`

### Return Value Significance
- `return 0` → Successful execution
- Other values (e.g., `-1`) or `exit()` → Error or abnormal termination
- OS uses this to determine if process executed successfully

---

## Process Architecture in Memory

When a process is loaded in memory, it has the following structure:

```
High Memory Address
+------------------+
|      Stack       |  ← Function calls, local variables
|        ↓         |     (grows downward)
|                  |
|   (Free Space)   |  ← Space for growth
|                  |
|        ↑         |
|       Heap       |  ← Dynamic allocation (grows upward)
+------------------+
|      Data        |  ← Global & static variables
+------------------+
|      Text        |  ← Compiled code (instructions)
+------------------+
Low Memory Address
```

### Memory Sections Explained

#### 1. Text Section
- Contains compiled code
- Machine instructions
- The actual executable code
- **Note:** You can view this by opening an executable in notepad (shows weird characters)

#### 2. Data Section
- Contains:
  - Global variables
  - Static data
- Accessible across modules/functions

#### 3. Heap
- Used for dynamic memory allocation
- Grows upward (towards higher memory addresses)
- Allocated using `malloc()`, `new`, etc.
- Must be manually freed in C++ (automatic in Java)

#### 4. Stack
- Used for function call management
- Grows downward (towards lower memory addresses)
- Contains:
  - Local variables
  - Function parameters
  - Return addresses

### Why Stack and Heap are Far Apart?
- Allows both to grow without immediate collision
- Provides sufficient space for program execution

---

## Common Memory Errors

### 1. Stack Overflow
**Cause:**
- Excessive recursive calls without proper base case
- Stack grows too large and reaches heap

**How it happens:**
1. Function called recursively
2. Each call creates new stack frame
3. Variables stored for each level
4. No exit condition → infinite growth
5. Stack touches heap → **Stack Overflow**

**Solution:**
- Always write proper base cases in recursion
- Ensure recursion has exit condition
- Unbind stack by returning from recursive calls

### 2. Out of Memory / Memory Insufficient Error
**Cause:**
- Continuous heap allocation without deallocation
- Memory leaks
- Heap grows and touches stack

**How it happens:**
1. Allocate memory on heap repeatedly
2. Never free the allocated memory
3. Heap keeps growing
4. Eventually touches stack → **Out of Memory**

**Solution:**
- Deallocate memory after use (in C++)
- Use `free()` or `delete` appropriately
- Avoid memory leaks

---

## Process Attributes

OS maintains a **Process Table** to manage all processes. Each entry is called a **Process Control Block (PCB)**.

### Process Table Structure
```
Process Table
+----+----+----+----+
| P1 | P2 | P3 | P4 | ...
+----+----+----+----+
  ↓    ↓    ↓    ↓
 PCB  PCB  PCB  PCB
```

- Each process has a unique PCB
- OS recognizes processes through their PCB
- PCB is a data structure storing all process information

---

## Process Control Block (PCB)

PCB is a data structure that contains **all information** about a process.

### PCB Components

#### 1. Process ID (PID)
- **Unique identifier** assigned by OS
- Used to differentiate between processes
- Example: Process #23, Process #24, etc.

#### 2. Program Counter (PC)
- Tracks current instruction being executed
- Points to the address of next instruction
- **Working:**
  ```
  while (process not finished) {
      1. Fetch instruction at PC
      2. PC++  (increment)
      3. Execute instruction
  }
  ```
- Starts at 0 and increments with each instruction
- Essential for knowing which instruction to execute next

#### 3. Process State
- Stores current state of the process
- States include: New, Ready, Running, Waiting, Terminated
- (Will be covered in detail in next lecture)

#### 4. Priority
- Determines process scheduling priority
- Used by CPU scheduler
- Higher priority processes get CPU first

#### 5. CPU Registers
Contains values of various CPU registers:
- **SP:** Stack Pointer
- **BP:** Base Pointer
- **CR:** Control Registers
- Other general-purpose registers

**Why store registers?**
- During context switching, current register values must be saved
- When process gets CPU again, restore previous state
- Ensures process continues from where it left off

#### 6. Open File List
- List of files currently opened by the process
- File descriptors
- File handles

#### 7. Device Descriptors
- List of I/O devices being used
- Device handles
- I/O related information

---

## Context Switching (Brief Overview)

### What happens during context switching?

1. **Process P1 running** → Time quantum ends or goes to wait state
2. **Save P1's state:**
   - All register values saved to P1's PCB
   - Program counter saved
   - All current state information preserved
3. **Load P2's state:**
   - Restore register values from P2's PCB
   - Restore program counter
   - Resume P2 execution
4. **When P1 gets CPU again:**
   - Restore all saved values from PCB
   - Continue from where it left off

**Key Point:** PCB stores everything temporarily during context switching

---

## Key Takeaways

1. **Program** (disk) → **Process** (memory) transformation done by OS
2. **5 steps** in process creation: Load, Stack allocation, Heap allocation, I/O setup, Execution
3. **Process memory** has 4 sections: Text, Data, Heap, Stack
4. **PCB** contains all process information
5. **Program Counter** tracks current instruction
6. **Context switching** uses PCB to save/restore process state
7. Stack and Heap grow towards each other
8. Always handle recursion and memory allocation carefully

---

## Important Notes

- Process is recognized by OS through its PCB
- Every process has a unique Process ID
- Stack overflow and Out of Memory are common programming errors
- Return value from `main()` indicates success/failure to OS
- Understanding PCB is crucial for understanding process management

---

## Next Lecture Preview
- Detailed discussion on **Process States**
- State transitions
- Process lifecycle

---

## Study Tips
1. Google unfamiliar terms and concepts
2. Understand the "easy way" first, then dive into technical details
3. Practice visualizing process architecture
4. Understand the relationship between program, process, and PCB
5. Try to relate concepts to real-world programming experience

---

*End of Lecture 9*
