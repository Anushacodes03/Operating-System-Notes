# Lecture 8: Types of Storage

## Introduction
- **Topic**: Types of Storage in PC
- **Instructor**: Lakshay

## What is Storage?
Storage is where:
- Files are stored
- Data is stored
- Instructions are stored

## Hierarchical Structure of Storage

The storage hierarchy from closest to CPU to farthest:

```
1. Register (closest to CPU)
2. Cache
3. Main Memory (RAM)
4. Disk (Secondary Storage)
```

---

## 1. Register
- **Location**: Closest component to CPU
- **Definition**: Smallest unit of storage
- **Function**: CPU works directly on registers
- **Structure**: Array-type structure containing 0s and 1s
- **How it works**: 
  - PC works on 0/1 (high voltage or low voltage)
  - All instructions are fetched into registers
  - CPU works directly on them

---

## 2. Cache
- **Level**: Second level of storage
- **Purpose**: Additional memory used to store data temporarily
- **Contents**: Instructions and data that are frequently needed by CPU
- **How it works**:
  - OS identifies repetitive instructions/data in a program
  - Instead of fetching from main memory repeatedly, keeps them closer to CPU
  - Stores particular instructions that are used multiple times
  - Example: Sorting algorithms executed multiple times, repetitive data operations
- **Advantage**: 
  - Access time is less than main memory
  - Less costly to access than main memory
  - Makes overall program execution faster

---

## 3. Main Memory (RAM)
- **Function**: Where processes reside
- **Operation**: CPU contacts main memory to get instructions
- **Relationship with Secondary Memory**: 
  - Programs are stored in secondary memory
  - Brought to main memory for execution
  - Then processed by CPU

---

## 4. Secondary Memory (Hard Disk, SSD)
- **Contents**: 
  - Files
  - Media
  - Programs
  - Projects
- **Process Flow**: 
  - Program (in secondary memory) → Main Memory → Process (execution)
- **Types**: 
  - Hard Disk
  - SSD (fastest among secondary storage)

---

## Classification of Storage

### Primary Memory
1. Register
2. Cache
3. Main Memory (RAM)

### Secondary Memory
- Various types of disks
- SSD (fastest)
- Hard Disk

---

## Comparison of Storage Types

### 1. Cost (Manufacturing)

| Storage Type | Cost Level | Reason |
|-------------|-----------|---------|
| **Register** | Most expensive | Made of transistors, uses silicon and rare metals, closest to CPU, built with best materials for speed |
| **Cache** | Cheaper than register, costlier than main memory | - |
| **Main Memory** | Moderate | - |
| **Secondary Storage** | Cheapest | 1TB hard disk: ₹3000-4000, while 1GB RAM: ₹2000-3000 |

### 2. Access Speed

**Fastest to Slowest:**
1. Register (fastest)
2. Cache
3. Main Memory
4. Secondary Storage (slowest)

### 3. Storage Size

**Smallest to Largest:**
1. **Register**: 32-bit or 64-bit
2. **Cache**: Few KBs
3. **Main Memory**: GBs
4. **Secondary Storage**: TBs (1TB - 2TB)

**Why this pattern?**
- Cost factor: Making 1TB register/cache would require enormous money
- Practical limitations based on manufacturing costs

### 4. Volatility

**Volatile (Data lost on shutdown):**
- Register
- Cache
- Main Memory (RAM)
- Processes vanish after PC shutdown

**Non-volatile (Data persists):**
- Secondary Storage (Hard Disk, SSD)
- Data doesn't flush off after shutdown

---

## Summary Table

| Feature | Register | Cache | Main Memory | Secondary Storage |
|---------|----------|-------|-------------|-------------------|
| **Position** | Closest to CPU | 2nd level | 3rd level | Farthest from CPU |
| **Cost** | Highest | High | Moderate | Lowest |
| **Speed** | Fastest | Fast | Moderate | Slowest |
| **Size** | 32/64 bits | KBs | GBs | TBs |
| **Volatility** | Volatile | Volatile | Volatile | Non-volatile |
| **Purpose** | Direct CPU operations | Temporary storage of frequent data/instructions | Process execution | Long-term file storage |

---

## Key Takeaways

1. Storage devices form a **hierarchy** based on proximity to CPU
2. **Closer to CPU** = Faster access + Higher cost + Smaller size
3. **Trade-off exists** between speed, cost, and storage capacity
4. **Primary memory is volatile**, secondary memory is non-volatile
5. **Cache optimization** by OS improves program performance by storing repetitive instructions/data

---

## Additional Notes

- **Sponsor**: Crio - Project-driven platform for learning technical skills (SDE, QA profiles)
- Features: Practical projects, APIs, DevOps, Selenium with Java
- Offers placement guarantee program and 1-week free trial

---

*End of Lecture 8*
