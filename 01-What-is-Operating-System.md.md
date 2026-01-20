# Operating System - Lecture 1 Notes

## Introduction
- This lecture covers the basics of Operating Systems
- Focus on understanding **why** OS exists before diving into **what** it is

---

## Why is an Operating System Necessary?

### Scenario: What happens without an OS?

**Example Setup:**
- Device components: CPU, Memory, GPU, Disk
- Apps to run: TikTok and PUBG

**Problems without OS:**

1. **Resource Exploitation/Hijacking**
   - When TikTok launches, it directly accesses all resources (CPU, memory, GPU, disk)
   - TikTok "hacks" all available resources
   - When you try to open PUBG, resources are unavailable
   - System hangs even though adequate resources exist
   - No mechanism to share resources between applications

2. **No Resource Management**
   - Apps cannot coexist
   - One app monopolizes all resources
   - Other apps cannot run simultaneously

---

## Main Functions of an Operating System

### 1. Resource Management (Resource Arbitration)

**How OS solves the problem:**
- OS acts as a layer between apps and hardware
- Allocates resources proportionally:
  - TikTok: 5% CPU, 10% Memory, 12% GPU
  - PUBG: 50% CPU, 50% Memory, 60% GPU
- Prevents any single app from monopolizing resources
- Enables multiple apps to run simultaneously

### 2. Acts as an Interface

**Bank Analogy:**
- **You** = User/Application
- **Bank Uncle** = Operating System (Interface)
- **Treasury** = Resources (CPU, GPU, Memory)

**How it works:**
- User doesn't directly access treasury (resources)
- Goes through the bank uncle (OS)
- OS manages the interaction between user and resources

**In OS terms:**
- User App ↔ OS (Interface) ↔ Resources (CPU, GPU, Memory, Disk)

### 3. Prevents Code Duplication (DRY Principle)

**DRY = Do Not Repeat Yourself**

**Problem without OS:**
- TikTok developer writes app logic + memory management code
- PUBG developer writes app logic + memory management code
- Same memory/resource management code repeated in every app
- Apps become bulky (50 MB → 750-850 MB)
- Violates DRY principle

**Solution with OS:**
- OS contains all resource and memory management code
- Developers only write application logic
- Apps remain lightweight
- Code reusability achieved

**Developer Benefits:**
- Focus only on app logic (e.g., weather forecasting)
- No need to worry about resource management
- Cleaner, simpler code

### 4. Provides Isolation and Protection

**Problem without OS:**
- Apps share memory without boundaries
- TikTok could write into PUBG's memory space
- Example: TikTok overwrites PUBG health from 100% → 0%
- Player dies unexpectedly
- Major security violation

**Solution with OS:**
- OS logically separates memory sections
- TikTok gets memory: 0 to X
- PUBG gets memory: X to Y
- Each app is unaware of others
- Memory protection enforced
- Isolation maintained

### 5. Hardware Abstraction

**What OS does:**
- Writes all hardware interaction code internally
- Hides complexity from developers
- Example: `malloc` or `new` for memory allocation
  - Developer requests 10 bytes
  - OS handles which memory sector to use
  - Developer doesn't need implementation details

**Benefits:**
- Underlying hardware complexity hidden
- Simple interface for developers
- Abstraction of hardware details

### 6. Controls Hardware Access

- User applications cannot directly access hardware
- All hardware access goes through OS
- OS mediates all hardware interactions
- Provides controlled, secure access

---

## Formal Definition of Operating System

> **An Operating System is a piece of software that manages all the resources of a computer system, both hardware and software, and provides an environment in which the user can execute his/her programs in a convenient and efficient manner.**

**Key aspects:**
- Manages hardware and software resources
- Provides execution environment
- Enables convenient and efficient program execution
- Hides underlying hardware complexity
- Acts as a resource manager

---

## Summary: Problems Without OS

1. **Resource Exploitation** - Apps hijack all resources
2. **Complex, Bulky Apps** - Every app contains resource management code
3. **No Memory Protection** - Apps can interfere with each other
4. **No Isolation** - Security vulnerabilities
5. **Inefficient Resource Usage** - Cannot run multiple apps

---

## Summary: Functions of OS

1. **Resource Management/Arbitration** - Fair allocation of resources
2. **Interface** - Bridge between hardware and applications
3. **Abstraction** - Hides hardware complexity
4. **Isolation & Protection** - Secure execution environment
5. **Hardware Access Control** - Mediated hardware access
6. **Efficient Program Execution** - Convenient development environment

---

## Key Takeaways

- OS is essential for modern computing
- Enables multitasking and resource sharing
- Simplifies application development
- Provides security and stability
- Acts as intermediary between hardware and software