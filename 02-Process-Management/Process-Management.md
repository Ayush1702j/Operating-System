# Process Management

## Operating System – Unit II

Process Management is one of the most important functions of an Operating System. It controls the creation, execution, scheduling, synchronization, and termination of processes.

---

# Unit II Topics

- Process Concept
- Process States
- Process Control Block (PCB)
- Context Switching
- Process Scheduling
- Schedulers
- Operations on Processes
- Inter-Process Communication (IPC)
- Shared Memory
- Message Passing
- Producer-Consumer Problem

---

# What is a Process?

A **process** is a program that is currently executing.

- Program = Passive entity
- Process = Active entity
- Multiple processes can run simultaneously in modern operating systems.

Example:

A browser can have multiple processes for different tabs.

---

# Process in Memory

A process consists of several memory sections.

| Section | Purpose |
|---------|---------|
| Text | Program instructions |
| Data | Global variables |
| Heap | Dynamic memory |
| Stack | Function calls and local variables |

```text
+-----------+
| Stack     |
+-----------+
| Heap      |
+-----------+
| Data      |
+-----------+
| Text      |
+-----------+
```

---

# Process States

A process moves through different states during execution.

```text
New
 ↓
Ready
 ↓
Running
 ↓
Waiting
 ↓
Ready
 ↓
Running
 ↓
Terminated
```

## Five Process States

### 1. New

Process has just been created.

### 2. Ready

Waiting for CPU allocation.

### 3. Running

Currently executing on CPU.

### 4. Waiting

Waiting for I/O or another event.

### 5. Terminated

Execution has completed.

---

# Process Control Block (PCB)

Every process has a **PCB**, which stores all information required to manage it.

## PCB Contents

- Process ID (PID)
- Process State
- Program Counter
- CPU Registers
- Priority
- Scheduling Information
- Memory Information
- Accounting Information
- I/O Information

```text
+-------------------+
| Process ID        |
| State             |
| Program Counter   |
| CPU Registers     |
| Priority          |
| Memory Info       |
| I/O Status        |
+-------------------+
```

---

# Context Switching

Context switching happens when the CPU changes from one process to another.

## What Happens?

1. Save current process information into PCB.
2. Select another process.
3. Load new process information.
4. Resume execution.

```text
Process A
    ↓ Save PCB
Operating System
    ↓ Load PCB
Process B
```

## Why Context Switch?

- Multitasking
- Interrupt Handling
- User/Kernel switching

---

# Steps of Context Switch

1. Save CPU registers.
2. Update PCB.
3. Move process to appropriate queue.
4. Select next process.
5. Update memory structures.
6. Restore CPU registers.
7. Resume execution.

---

# Process Scheduling

Scheduling decides which process gets CPU time.

## Objectives

- Maximize CPU utilization
- Improve responsiveness
- Reduce waiting time
- Increase throughput

---

# Scheduling Queues

```text
Job Queue
    ↓
Ready Queue
    ↓
CPU
    ↓
I/O Queue
```

### Job Queue

Contains all processes.

### Ready Queue

Contains processes waiting for CPU.

### Device Queue

Contains processes waiting for I/O.

---

# Types of Schedulers

| Scheduler | Purpose |
|-----------|---------|
| Long-Term | Selects jobs from disk |
| Short-Term | Allocates CPU |
| Medium-Term | Swaps processes |

---

## Long-Term Scheduler

- Controls multiprogramming.
- Selects jobs from storage.
- Runs less frequently.

## Short-Term Scheduler

- Selects next process.
- Runs very frequently.
- Must be fast.

## Medium-Term Scheduler

- Performs swapping.
- Removes and restores processes.

```text
Memory
   ↓ Swap Out
Disk
   ↑ Swap In
Memory
```

---

# CPU-Bound vs I/O-Bound Processes

| CPU-Bound | I/O-Bound |
|-----------|-----------|
| More CPU work | More I/O work |
| Long CPU bursts | Short CPU bursts |
| Less waiting | More waiting |

A good scheduler balances both types.

---

# Process Representation in Linux

Linux represents every process using a `task_struct`.

Important fields include:

- PID
- State
- Time Slice
- Parent Process
- Child Process
- Open Files
- Memory Structure

---

# Process Creation

Processes are created dynamically.

### Parent Process

Creates another process.

### Child Process

Newly created process.

This forms a **process tree**.

```text
init
 ├── bash
 │    ├── ps
 │    └── emacs
 ├── sshd
 └── kthreadd
```

---

# UNIX Process Creation

UNIX uses three important system calls.

## fork()

Creates a child process.

## exec()

Replaces child memory with a new program.

## wait()

Parent waits until child finishes.

```text
Parent
   |
 fork()
  / \
Parent Child
        |
      exec()
        |
      exit()
        |
      wait()
```

---

# Example of fork()

```c
pid_t pid;

pid = fork();

if(pid == 0)
{
    printf("Child Process");
}
else
{
    wait(NULL);
    printf("Parent Process");
}
```

---

# Process Termination

A process ends using `exit()`.

Resources are released automatically.

## Reasons for Termination

- Normal completion
- Parent abort
- Resource limit exceeded
- Cascading termination

---

# Zombie Process

A zombie process has finished execution but still occupies a process table entry because its parent has not called `wait()`.

## Characteristics

- Execution completed
- PCB still exists
- Removed after parent reads exit status

---

# Orphan Process

An orphan process is a child whose parent has already terminated.

The operating system adopts it automatically.

---

# Multiprocess Architecture Example

Google Chrome uses multiple processes.

### Browser Process

- User interface
- Network
- Disk I/O

### Renderer Process

- HTML
- CSS
- JavaScript

### Plugin Process

Handles browser plugins separately.

Each browser tab can run as a separate process.

---

# Inter-Process Communication (IPC)

Processes communicate using IPC.

Two communication models exist.

1. Shared Memory
2. Message Passing

---

# Shared Memory

Processes share the same memory region.

### Advantages

- Very fast
- High performance

### Disadvantages

- Requires synchronization
- Can cause race conditions

```text
Process A
     ↕
Shared Memory
     ↕
Process B
```

---

# Producer-Consumer Problem

Two processes share a buffer.

- Producer creates data.
- Consumer uses data.

## Buffer Types

### Unbounded Buffer

No size limit.

### Bounded Buffer

Fixed buffer size.

```text
Producer → Buffer → Consumer
```

---

# Producer Code

```c
while(true)
{
    while(counter == BUFFER_SIZE);

    buffer[in] = nextProduced;
    in = (in + 1) % BUFFER_SIZE;
    counter++;
}
```

---

# Consumer Code

```c
while(true)
{
    while(counter == 0);

    nextConsumed = buffer[out];
    out = (out + 1) % BUFFER_SIZE;
    counter--;
}
```

---

# Message Passing

Processes exchange messages instead of sharing memory.

Two operations:

- send()
- receive()

```text
Process A
    |
 send()
    |
Message Queue
    |
receive()
    |
Process B
```

---

# Types of Communication

## Direct Communication

Processes communicate using each other's names.

Example:

```text
send(P, message)
receive(Q, message)
```

---

## Indirect Communication

Uses mailboxes (ports).

```text
send(Mailbox, message)
receive(Mailbox, message)
```

Multiple processes can share the same mailbox.

---

# Synchronization

Message passing can be:

### Blocking (Synchronous)

- Sender waits.
- Receiver waits.

### Non-Blocking (Asynchronous)

- Sender continues immediately.
- Receiver checks later.

---

# Buffering Types

| Type | Description |
|------|-------------|
| Zero | No waiting messages |
| Bounded | Limited capacity |
| Unbounded | Unlimited capacity |

---

# POSIX Shared Memory

Important functions:

```c
shm_open()
ftruncate()
mmap()
shm_unlink()
```

These create and manage shared memory segments.

---

# Windows Message Passing

Windows uses **ALPC (Advanced Local Procedure Call)**.

Communication uses:

- Connection Port
- Client Port
- Server Port
- Shared Memory

---

# Quick Revision

## Important System Calls

| System Call | Purpose |
|-------------|----------|
| fork() | Create child process |
| exec() | Load new program |
| wait() | Wait for child |
| exit() | Terminate process |

---

## PCB Quick Recall

- PID
- State
- Program Counter
- Registers
- Priority
- Memory Info
- I/O Info

---

## Process States Quick Recall

```text
New → Ready → Running → Waiting → Ready → Running → Terminated
```

---

# Interview Questions

1. What is a process?
2. Difference between program and process.
3. What is PCB?
4. Explain context switching.
5. What are process states?
6. Difference between Zombie and Orphan process.
7. Explain fork(), exec(), and wait().
8. What is IPC?
9. Difference between Shared Memory and Message Passing.
10. Explain Producer-Consumer Problem.

---

# Key Takeaways

- A process is an executing program.
- PCB stores all process information.
- Context switching enables multitasking.
- Scheduling decides CPU allocation.
- IPC allows processes to communicate.
- Shared memory is faster, while message passing is safer and easier to manage.
