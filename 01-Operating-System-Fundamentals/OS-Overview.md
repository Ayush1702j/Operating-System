# Operating System Overview

## Unit 1 – Introduction to Operating System

An **Operating System (OS)** is system software that acts as an interface between the user and computer hardware. It manages hardware resources and provides services that allow applications to run efficiently.

---

# Operating System Goals

- Execute user programs.
- Make the computer system easy to use.
- Use hardware resources efficiently.

---

# Computer System Structure

A computer system has four main components:

1. **Hardware**
   - CPU
   - Memory
   - Input/Output Devices

2. **Operating System**
   - Controls and manages hardware resources.

3. **Application Programs**
   - Web Browser
   - Compiler
   - Database
   - Games

4. **Users**
   - Humans
   - Other Computers

---

# Operating System as a Resource Allocator

The operating system:

- Manages all system resources.
- Allocates CPU time.
- Controls memory.
- Coordinates hardware usage.
- Prevents improper use of the computer.

---

# Basic Functions of Operating System

## 1. Memory Management

- Allocates memory to different processes.
- Keeps track of memory usage.
- Frees memory after process completion.

## 2. Process Management

A **process** is a program in execution.

The OS:

- Creates processes.
- Schedules CPU time.
- Terminates completed processes.

## 3. File Management

The operating system can:

- Create files
- Delete files
- Open files
- Save files
- Organize directories

## 4. Device Management

The OS communicates with hardware using **device drivers**.

Examples:

- Keyboard
- Mouse
- Printer
- Disk Drive

## 5. Security Management

The operating system protects the system using:

- Authentication
- Authorization
- Access Control
- Encryption

---

# Storage Management

Storage management includes:

- Creating files
- Organizing directories
- Managing secondary storage
- Backing up data

---

# I/O Subsystem

The Input/Output subsystem hides hardware complexity from users.

It performs:

- Buffering
- Caching
- Spooling
- Device Driver Management

---

# Types of Operating Systems

## 1. Batch Operating System

Jobs are grouped into batches and executed without user interaction.

### Advantages

- Better throughput
- Less idle time

### Example

IBM OS/360

---

## 2. Multiuser Operating System

Multiple users can use the same computer simultaneously.

### Advantages

- Resource sharing
- Cost effective
- Centralized management

### Challenges

- Security risks
- Performance issues

---

## 3. Multitasking Operating System

Allows multiple tasks to run on a single CPU.

Performance depends on:

- CPU speed
- Number of cores
- RAM size
- Program size

---

## 4. Multiprocessor Operating System

Uses multiple processors for parallel execution.

### Features

- Load balancing
- Faster processing
- Better scalability

### Examples

- Linux SMP
- Windows Server
- Solaris

---

## 5. Embedded Operating System

Designed for specific hardware with limited resources.

### Features

- Small memory footprint
- High reliability
- Specialized I/O support

### Examples

- Embedded Linux
- TinyOS
- Contiki

---

## 6. Real-Time Operating System (RTOS)

Executes tasks within strict time limits.

### Hard Real-Time

Missing deadlines causes system failure.

**Examples**

- Flight control systems
- Missile guidance systems

### Soft Real-Time

Small delays are acceptable.

**Examples**

- Video streaming
- Web servers
- Online transactions

---

# Operating System Structures

## Layered Structure

The operating system is divided into multiple layers.

```text
User
 ↓
Applications
 ↓
Operating System
 ↓
Hardware
```

### Advantages

- Modular
- Easy maintenance

---

## Monolithic Kernel

All services run inside kernel space.

### Pros

- Fast
- Efficient

### Cons

- One bug can crash the entire operating system.

### Examples

- Linux
- UNIX

---

## Microkernel

Only essential services remain inside the kernel.

Other services run in user space.

### Pros

- Secure
- Reliable
- Easy to extend

### Cons

- More communication overhead

### Examples

- QNX
- Minix

---

## Hybrid Kernel

Combines monolithic and microkernel features.

### Examples

- Windows
- macOS

---

# Kernel Comparison

| Feature | Monolithic | Microkernel | Hybrid |
|---------|------------|-------------|---------|
| Speed | Fast | Slower | Moderate |
| Reliability | Lower | Higher | Higher |
| Extensibility | Difficult | Easy | Moderate |

---

# System Calls

A **system call** is the mechanism through which a user program requests services from the operating system.

```text
User Program
      ↓
     API
      ↓
 System Call
      ↓
 Operating System Kernel
```

System calls are the **only way** user programs communicate with the kernel.

---

# Common Types of System Calls

## Process Control

- Create process
- Execute process
- Terminate process
- Wait for process

## File Management

- Open file
- Read file
- Write file
- Delete file

## Device Management

- Request device
- Release device
- Read device
- Write device

## Information Management

- Get time
- Set attributes

## Communication

- Send messages
- Receive messages
- Create communication links

---

# Key Takeaways

- The operating system acts as a bridge between users and hardware.
- It manages CPU, memory, files, storage, and devices.
- Different operating systems are designed for different purposes.
- System calls allow programs to communicate with the kernel.
- Modern operating systems use layered, monolithic, microkernel, or hybrid architectures.
