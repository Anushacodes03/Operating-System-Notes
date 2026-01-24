# Operating System - Lecture 4
## Components of Operating System

---

## Table of Contents
1. [Main Components of OS](#main-components-of-os)
2. [User Space](#user-space)
3. [Kernel](#kernel)
4. [Functions of Kernel](#functions-of-kernel)
5. [Types of Kernels](#types-of-kernels)
6. [Interprocess Communication (IPC)](#interprocess-communication-ipc)

---

## Main Components of OS

An Operating System consists of two main components:

### 1. User Space
- Area where user applications are executed
- Provides convenient environment for developers to run apps
- **Does NOT have direct access to hardware**

### 2. Kernel
- Has direct access to underlying hardware
- Acts as intermediary between user space and hardware

```
┌─────────────────┐
│   User Space    │ ← User Applications
├─────────────────┤
│     Kernel      │ ← Hardware Access
├─────────────────┤
│    Hardware     │
└─────────────────┘
```

---

## User Space

### What is User Space?

User Space is the environment where users interact with the system. It includes:

#### 1. GUI (Graphical User Interface)
- Visual interface with desktop, icons, start menu
- Users interact using mouse and clicks
- Examples: Windows Desktop, macOS Finder

#### 2. CLI (Command Line Interface)
- Text-based interface where users type commands
- Examples:
  - **Windows:** PowerShell
  - **macOS/Linux:** Terminal

### GUI vs CLI Example

**Creating a New Folder:**

| Method | Action |
|--------|--------|
| GUI | Right-click → New Folder |
| CLI | `mkdir foldername` |

> **Note:** GUI buttons internally call CLI commands (e.g., "New Folder" button uses `mkdir` command)

### Functions of User Space

1. Provides convenient environment to run user applications
2. Interacts with the kernel
3. Acts as interface layer between user and system

---

## Kernel

### What is Kernel?

- **Heart of the Operating System**
- Most important component of OS
- First component to load during system startup
- Directly interacts with hardware
- Executes commands from user space

### How Kernel Works

**Example: Executing a Shell Script**

```bash
./HelloWorld.sh
```

**Flow:**
1. User executes command in CLI (User Space)
2. Request goes to Kernel
3. Kernel requests CPU for computation cycles
4. CPU performs computation
5. Result ("Hello World") is displayed

---

## Functions of Kernel

### 1. Process Management

**Responsibilities:**
- Process creation and termination
- Process and thread scheduling
- Context switching
- Time switching
- Process synchronization
- Inter-process communication

**Goals:**
- Maximum CPU utilization
- Handle process priorities
- Prevent process starvation

### 2. Memory Management

**Responsibilities:**
- Memory allocation and deallocation
- Free space management
- Track vacant memory areas
- Manage RAM efficiently

**Example:**
- System has 2GB RAM
- Kernel allocates memory to processes
- Keeps track of free and occupied spaces
- Deallocates memory when process terminates

### 3. File Management

**Responsibilities:**
- Create and delete files
- Directory management
- Maintain hierarchical structure (tree structure)

**Directory Structure Example (Linux):**

```
Root (/)
├── Lakshay/
│   ├── OS/
│   ├── ABCD/
│   └── lakshay.txt
└── Ramesh/
```

> **Real-world Application:** This is where tree data structures are used in practice!

### 4. I/O Management

**Responsibilities:**
- Manage and control all I/O operations
- Handle I/O devices (USB, game controllers, etc.)
- Device notifications
- Provide access methods for devices

**Example:**
- Plug in a pen drive
- Kernel detects the device
- Notifies user space
- Provides access through GUI (e.g., "My Computer")

**Three Important I/O Operations:**
1. **Spooling** - Queue data between jobs (e.g., print spooling)
2. **Buffering** - Store data temporarily for near-future use (e.g., YouTube buffering)
3. **Caching** - Store frequently accessed data

---

## Types of Kernels

### 1. Monolithic Kernel

**Definition:** All kernel functions are present in the kernel itself.

**Structure:**
```
┌─────────────────────────────┐
│       User Space            │
├─────────────────────────────┤
│         Kernel              │
│  ┌─────────────────────┐   │
│  │ Process Management  │   │
│  │ Memory Management   │   │
│  │ File Management     │   │
│  │ I/O Management      │   │
│  └─────────────────────┘   │
├─────────────────────────────┤
│         Hardware            │
└─────────────────────────────┘
```

**Advantages:**
- ✅ Fast communication between kernel components
- ✅ Efficient performance (everything is centralized)

**Disadvantages:**
- ❌ Bulky kernel size
- ❌ Less reliable (if one component fails, entire kernel can crash)

**Examples:**
- Linux
- Unix
- MS-DOS

---

### 2. Micro Kernel

**Definition:** Only core functions in kernel, rest in user space.

**Structure:**
```
┌─────────────────────────────┐
│       User Space            │
│  ┌─────────────────────┐   │
│  │ File Management     │   │
│  │ I/O Management      │   │
│  └─────────────────────┘   │
├─────────────────────────────┤
│         Kernel              │
│  ┌─────────────────────┐   │
│  │ Process Management  │   │
│  │ Memory Management   │   │
│  └─────────────────────┘   │
├─────────────────────────────┤
│         Hardware            │
└─────────────────────────────┘
```

**Core Functions in Kernel:**
- Process Management (CPU-related)
- Memory Management (RAM-related)

**Functions in User Space:**
- File Management
- I/O Management

**Advantages:**
- ✅ Less bulky
- ✅ More reliable and stable (reduced risk of kernel crash)

**Disadvantages:**
- ❌ Reduced performance
- ❌ High overhead due to frequent switching between user and kernel mode

**Why Performance Decreases:**
- Frequent context switching between user mode and kernel mode
- Every switch has a cost
- More overhead = lower performance

**Examples:**
- L4 Linux
- Symbian OS (used in old Nokia phones)
- MINIX

---

### 3. Hybrid Kernel

**Definition:** Combines advantages of both Monolithic and Micro kernels.

**Structure:**
```
┌─────────────────────────────┐
│       User Space            │
│  ┌─────────────────────┐   │
│  │ File Management     │   │
│  └─────────────────────┘   │
├─────────────────────────────┤
│         Kernel              │
│  ┌─────────────────────┐   │
│  │ Process Management  │   │
│  │ Memory Management   │   │
│  │ I/O Management      │   │
│  └─────────────────────┘   │
├─────────────────────────────┤
│         Hardware            │
└─────────────────────────────┘
```

**Functions in Kernel:**
- Process Management
- Memory Management
- I/O Management

**Functions in User Space:**
- File Management

**Advantages:**
- ✅ Improved speed (reduced switching overhead)
- ✅ Increased stability
- ✅ Best of both worlds
- ✅ Uses speed and design of monolithic kernel
- ✅ Uses modularity and stability of micro kernel

**Examples:**
- macOS
- Windows NT
- Windows 7/10

---

### Other Kernel Types

**4. Nano Kernel**
**5. Exo Kernel**

> **Note:** These are less important from interview perspective. Study them for comprehensive understanding.

---

## User Mode vs Kernel Mode

### Definitions

**User Mode:**
- CPU executes user-space operations
- Limited hardware access
- Where user applications run

**Kernel Mode:**
- CPU executes kernel operations
- Full hardware access
- Privileged operations allowed

### Mode Switching

**How Switching Happens:**
- Through **Software Interrupts**

**What is a Software Interrupt?**
- Asynchronous notification to OS
- Generated by software (not hardware)
- Tells OS to stop current work and do something else

**Example:**
```
User executes: mkdir newfolder

Flow:
1. User Mode (typing command)
2. Press Enter
3. → Software Interrupt
4. → Switch to Kernel Mode
5. → File Management creates directory
6. → Switch back to User Mode
7. → Display confirmation
```

---

## Interprocess Communication (IPC)

### What is IPC?

**Interprocess Communication** - Method for processes to communicate with each other.

### Why is IPC Needed?

- Processes run in isolation (separate resources, memory)
- Sometimes processes need to share data
- Example: File Management (user space) needs to communicate with Memory Management (kernel space)

---

### IPC Methods

#### 1. Shared Memory

**Concept:** Create a common memory space that both processes can access.

```
Process P1          Shared Memory          Process P2
    ↓                    ↓                      ↑
  Write              [1, 2, 3]               Read
```

**How it Works:**
1. P1 writes data to shared memory
2. P2 reads data from shared memory
3. Communication achieved!

#### 2. Message Passing

**Concept:** Establish a direct communication channel between processes.

```
Process P1 ←────[Direct Pipe/Channel]────→ Process P2
```

**How it Works:**
- OS provides system calls for message passing
- Direct channel established between processes
- Messages sent through protocol calls

---

## Key Takeaways

### Components Summary

| Component | Access Level | Role |
|-----------|-------------|------|
| User Space | No hardware access | User applications, GUI/CLI |
| Kernel | Full hardware access | Core OS functions |

### Kernel Functions

1. **Process Management** - Create, schedule, synchronize processes
2. **Memory Management** - Allocate/deallocate RAM
3. **File Management** - Create/delete files, maintain directory structure
4. **I/O Management** - Manage devices and I/O operations

### Kernel Types Comparison

| Kernel Type | Performance | Reliability | Size | Examples |
|-------------|-------------|-------------|------|----------|
| Monolithic | High ⚡ | Low | Large | Linux, Unix |
| Micro | Low | High ✅ | Small | Symbian OS, MINIX |
| Hybrid | Medium-High ⚡ | High ✅ | Medium | macOS, Windows |

### IPC Methods

- **Shared Memory** - Common memory space
- **Message Passing** - Direct communication channel

---

## Important Interview Questions

1. **What are the main components of OS?**
   - User Space and Kernel

2. **What are the functions of Kernel?**
   - Process, Memory, File, and I/O Management

3. **Difference between Monolithic and Micro Kernel?**
   - Monolithic: All functions in kernel (fast but bulky)
   - Micro: Core functions in kernel (reliable but slower)

4. **How do processes in user space and kernel space communicate?**
   - Through IPC (Shared Memory or Message Passing)

5. **What is the difference between User Mode and Kernel Mode?**
   - User Mode: Limited access, user applications
   - Kernel Mode: Full hardware access, privileged operations

---

## Glossary

- **GUI** - Graphical User Interface
- **CLI** - Command Line Interface
- **IPC** - Interprocess Communication
- **Context Switching** - Switching between processes/modes
- **Software Interrupt** - Signal to OS to perform specific task
- **Spooling** - Queue data between jobs
- **Buffering** - Temporary data storage
- **Caching** - Store frequently accessed data

---

**Lecture:** OS Lecture 4  
**Topic:** Components of Operating System  
**Channel:** Code Help by Lakshay