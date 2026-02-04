# OS Lecture 12: Process Scheduling Algorithms

## Overview
Process scheduling is a crucial part of process management in operating systems. The CPU scheduler determines which process from the ready queue gets CPU time.

---

## Process Scheduling Basics

### The Process Flow
1. **Long Term Scheduler (LTS)** provides processes to the ready queue
2. **Short Term Scheduler (STS)** dispatches processes from ready queue to CPU
3. Processes execute in CPU's run state
4. After time quantum or I/O, processes return to ready queue or waiting state

### Key Components
- **CPU Scheduler**: Selects which process to execute when CPU is idle
- **Dispatcher**: Gives control of the CPU to the selected process
- **Scheduling Algorithm**: Determines the selection process

---

## Types of Scheduling Algorithms

### 1. Non-Preemptive Scheduling
Once a process gets the CPU, it holds it until:
- Process terminates, OR
- Process goes to wait/I/O state

**Characteristics:**
- ❌ No time quantum
- ❌ No time sharing
- ❌ Higher process starvation
- ❌ Lower CPU utilization
- ✅ Less overhead

### 2. Preemptive Scheduling
Process releases CPU when:
- Process terminates, OR
- Process goes to wait/I/O state, OR
- **Time quantum expires** (goes back to ready queue)

**Characteristics:**
- ✅ Time sharing enabled
- ✅ Less starvation (every process gets a chance)
- ✅ Higher CPU utilization
- ❌ More overhead (frequent context switching)

---

## Comparison: Preemptive vs Non-Preemptive

| Aspect | Non-Preemptive | Preemptive |
|--------|----------------|------------|
| **Starvation** | More (CPU-intensive jobs block others) | Less (time sharing ensures fairness) |
| **CPU Utilization** | Lower | Higher |
| **Overhead** | Less | More (frequent process switching) |
| **Time Sharing** | No | Yes |

---

## Goals of CPU Scheduling Algorithms

### 1. **Maximum CPU Utilization**
- Keep CPU busy as much as possible
- Minimize idle time

### 2. **Minimum Turnaround Time (TAT)**
- Reduce total time from arrival to completion
- Execute processes as quickly as possible

### 3. **Minimum Wait Time**
- Reduce time process spends waiting for CPU
- Less waiting = less starvation

### 4. **Minimum Response Time**
- Reduce time from arrival to first CPU allocation
- Ensure processes start executing quickly

### 5. **Maximum Throughput**
- Maximize number of processes completed per unit time
- Measure of system efficiency

---

## Important Terminology

### Arrival Time (AT)
Time when process arrives at the ready queue

### Burst Time (BT)
Time required by process for execution (assuming no other processes exist)

### Completion Time (CT)
Time when process finishes execution completely

### Turnaround Time (TAT)
Total time from arrival to completion
```
TAT = CT - AT
```

### Wait Time (WT)
Time process spends waiting for CPU
```
WT = TAT - BT
```

### Response Time
Time from arrival to first CPU allocation

### Throughput
Number of processes completed per unit time

---

## FCFS (First Come First Serve) Algorithm

### Concept
- Simplest scheduling algorithm
- Process that arrives first gets CPU first
- Operates like a queue (FIFO)

### Example 1: Standard Order

| Process | Arrival Time | Burst Time |
|---------|-------------|------------|
| P1 | 0 | 20 |
| P2 | 1 | 2 |
| P3 | 1 | 2 |

**Gantt Chart:**
```
| P1 (0-20) | P2 (20-22) | P3 (22-24) |
```

**Calculations:**

| Process | CT | TAT (CT-AT) | WT (TAT-BT) |
|---------|----|-----------|-----------:|
| P1 | 20 | 20 | 0 |
| P2 | 22 | 21 | 19 |
| P3 | 24 | 23 | 21 |

**Average Wait Time = (0 + 19 + 21) / 3 = 13.33 units**

### Example 2: Optimized Order

| Process | Arrival Time | Burst Time |
|---------|-------------|------------|
| P2 | 1 | 2 |
| P3 | 1 | 2 |
| P1 | 0 | 20 |

**Gantt Chart:**
```
| P2 (0-2) | P3 (2-4) | P1 (4-24) |
```

**Calculations:**

| Process | CT | TAT (CT-AT) | WT (TAT-BT) |
|---------|----|-----------|-----------:|
| P2 | 2 | 1 | 0 |
| P3 | 4 | 3 | 1 |
| P1 | 24 | 24 | 2 |

**Average Wait Time = (0 + 1 + 2) / 3 = 1 unit**

---

## Convoy Effect

### Definition
When a process with higher burst time significantly impacts the average waiting time of other processes.

### Explanation
- If a CPU-intensive job (high BT) executes first, other jobs wait longer
- Poor resource management leads to increased waiting time
- Not limited to CPU - applies to any shared resource

### Impact
- Example 1: Average WT = 13.33 units (P1 first)
- Example 2: Average WT = 1 unit (shorter jobs first)
- **Placing long jobs first increases system-wide waiting time**

### Key Takeaway
> "If there is any process that has higher BT, it will have a major impact on average BT of rest processes"

---

## Key Interview Questions

1. **What is the difference between preemptive and non-preemptive scheduling?**
2. **Explain convoy effect with an example**
3. **What are the goals of CPU scheduling?**
4. **Calculate TAT, WT, CT for given processes using FCFS**
5. **Why does preemptive scheduling have more overhead?**

---

## Summary

- **Process scheduling** selects which process gets CPU time
- **Two types**: Preemptive (with time quantum) and Non-preemptive (without)
- **Goals**: Max CPU utilization, Min TAT/WT/Response time, Max throughput
- **FCFS**: Simplest algorithm but suffers from convoy effect
- **Convoy effect**: Long burst time processes block shorter ones
- **Preemptive scheduling** offers better CPU utilization but higher overhead

---

## Formulas Quick Reference

```
TAT (Turnaround Time) = CT - AT
WT (Wait Time) = TAT - BT
Average Wait Time = Sum of all WT / Number of processes
Throughput = Number of processes completed / Total time
```
