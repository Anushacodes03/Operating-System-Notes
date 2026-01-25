# Operating Systems - System Calls (Lecture 5)

## Introduction

System calls are a fundamental mechanism in operating systems that enable user applications to interact with the kernel and access hardware resources.

## Recap: User Space vs Kernel Space

### Two Separate Spaces
- **User Space**: Where applications run (limited access)
- **Kernel Space**: Where OS core functions execute (full hardware access)
- These are distinct, separate areas with controlled switching between them

### Key Principle
- Applications run in user mode
- Actual hardware work is done by kernel
- Only kernel has direct access to hardware
- User space applications cannot directly access hardware

## What are System Calls?

### Definition
System calls are mechanisms using which a user program can request a service from the kernel for which it does not have the permission to perform.

### Purpose
- Provides an interface between user space and kernel space
- Enables user applications to interact with kernel space
- Allows controlled access to hardware resources
- **Only way** to switch between user mode and kernel mode

### Why System Calls are Necessary
- User and kernel spaces are separate areas
- Kernel space has hardware access
- User applications need system calls to work with hardware
- Required for: memory allocation, CPU cycles, I/O operations

## How System Calls Work

### Architecture
```
User Space
    ↓
System Call Interface (SCI)
    ↓
Kernel Space
    ↓
Hardware
```

### System Call Interface (SCI)
- Entry point to kernel space
- Maps user requests to kernel implementations
- Handles the switching mechanism

### Process Flow Example: Creating a Folder

#### GUI Method
1. Right-click → New Folder
2. Type "movies"
3. Folder created

#### CLI Method
```bash
mkdir movies
```

#### Behind the Scenes
1. User clicks "New Folder" or runs `mkdir` command
2. Request goes to System Call Interface (SCI)
3. SCI finds corresponding `mkdir` implementation in kernel
4. Kernel executes the implementation (written in C)
5. Kernel adds a new inode in the file system tree
6. New folder appears in GUI/file system
7. Control returns to user mode

### Mode Switching
- Uses **software interrupts** to switch between modes
- Software interrupt tells CPU to stop current work and handle the system call
- After kernel completes work, switches back to user mode

## System Call Implementation

### Language
- System calls are implemented in **C language**
- Low-level C that can directly access hardware
- User sees an interface to the C implementation

### Example: Process Execution (hello.exe)
1. User runs hello.exe in user mode
2. System call for execution is invoked
3. Switch to kernel mode via software interrupt
4. Kernel's process management creates the process
5. Memory allocated in RAM
6. I/O devices accessed if needed
7. Process created and information returned to user mode
8. Process visible in Task Manager/Activity Monitor

## Types of System Calls

### 1. Process Control
**Purpose**: Creating, managing, and terminating processes

**Examples**:
- `createprocess()` / `fork()` - Create new process
- `exitprocess()` / `exit()` - Exit/terminate process
- `WaitForSingleObject()` / `wait()` - Wait for process completion

**Key Concepts**:
- `fork()` creates child processes
- Every new process is a child of some parent process
- Root process (PID 0) is the first process when system boots

### 2. File Management
**Purpose**: Creating, accessing, and managing files

**Examples**:
- `open()` - Open a file
- `read()` - Read from file
- `write()` - Write to file
- `close()` - Close file
- `chmod()` - Change file permissions/mode
- `chown()` - Change file ownership
- `umask()` - Set file creation mask

**Features**:
- Read/write operations
- Repositioning (read from specific position, not just start)
- Security and permissions management

### 3. Device Management
**Purpose**: Managing I/O devices

**Examples**:
- `read()` - Read from device
- `write()` - Write to device
- `ioctl()` - I/O control operations
- Get/set device attributes
- Attach/detach devices

### 4. Information Maintenance
**Purpose**: Managing system information

**Examples**:
- `getpid()` - Get process ID
- `alarm()` - Set alarm
- `sleep()` - Sleep for specified time
- `date()` - Get date and time

**Usage**: Manages information about processes, devices, time, and dates

### 5. Communication Management
**Purpose**: Inter-Process Communication (IPC)

**Examples**:
- `pipe()` - Create pipe for message passing
- `shmget()` - Shared memory operations
- `mmap()` - Map/unmap devices in memory

**IPC Methods**:
- Message passing (using pipes)
- Shared memory
- Remote devices (LAN communication)

## Practical Example: Shell Script Demonstration

### Script Creation (hello.sh)
```bash
#!/bin/bash
file=true
while $file; do
    echo "Hello Code Help"
    sleep
done
```

### System Calls Involved

#### File Creation Phase
1. **File Management**: `open()` - Create/open hello.sh
2. **File Management**: `write()` - Write script content
3. **File Management**: Save file to desktop

#### Execution Phase
1. **Process Control**: `fork()` - Create child process for hello.sh
2. **Process Control**: Execute the script
3. **Information Management**: `ps -a` - Display process information and PID
4. **Process Control**: `getpid()` - Retrieve process ID

#### Termination Phase
```bash
kill -9 [PID]
```
- **Process Control**: `kill()` system call
- Switches to kernel mode
- Kernel stops CPU work on that PID
- Process terminated

### Process Information
- **PID**: Process ID (unique identifier)
- **PPID**: Parent Process ID
- Every process has a parent except the root process

## Important Commands

### Process Management
- `ps -a` - List all processes
- `kill -9 [PID]` - Force kill process
- `man [command]` - Manual/help for commands

### File Operations
- `mkdir [name]` - Make directory
- `chmod` - Change file permissions
- `chown` - Change file ownership

## Key Takeaways

1. System calls are the **only** way to switch from user to kernel mode
2. All system calls are implemented in **C language**
3. System Call Interface (SCI) acts as the **entry point** to kernel space
4. **Software interrupts** facilitate mode switching
5. User mode has limited access; kernel mode has full hardware access
6. Different types of system calls handle different OS functions
7. Multiple system calls may execute for a single user operation

## Homework

1. Research all mentioned system calls
2. Understand what each system call does
3. Practice using system calls in terminal
4. Read manual pages using `man [command]`
5. Focus on understanding the working rather than memorizing names

## Signal Types (for kill command)
- Signal 3: QUIT
- Signal 9: KILL (force)
- Signal ABORT: Abort process
- And others (read `man kill` for complete list)

---

**Note**: This lecture covered fundamental concepts of system calls. Understanding these concepts is crucial for technical interviews at product-based companies and for deeper OS knowledge.