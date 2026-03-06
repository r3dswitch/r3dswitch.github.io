This chapter introduces the fundamental concept of a **process** in operating systems - defined simply as a running program. Here's a summary of the key concepts:

## Core Problem and Solution

The OS faces the challenge of providing the illusion of many CPUs when only a few physical CPUs exist. It solves this through **CPU virtualization** using time sharing - rapidly switching between processes to create the appearance of concurrent execution.

## What is a Process?

A process consists of a program's **machine state** during execution:

- **Memory** (address space): Contains instructions and data
- **Registers**: Including special ones like program counter (PC) and stack pointer
- **I/O information**: Such as open files

## Process Lifecycle

**Creation**: The OS loads program code and static data from disk into memory, allocates stack and heap space, sets up I/O (like standard input/output), then jumps to the main() function.

**States**: Processes exist in three primary states:

- **Running**: Currently executing on CPU
- **Ready**: Prepared to run but not currently scheduled
- **Blocked**: Waiting for some event (like I/O completion)

## Process API

Operating systems provide interfaces to:

- Create new processes
- Destroy/kill processes
- Wait for process completion
- Suspend/resume processes
- Get process status information

## Implementation

The OS maintains **process lists** and **Process Control Blocks (PCBs)** - data structures that store each process's state information, including register contexts for context switching between processes.

## Design Philosophy

The chapter emphasizes separating **mechanisms** (low-level methods like context switching) from **policies** (high-level decisions like which process to run next), promoting modularity in OS design.

This abstraction allows users to run multiple programs simultaneously without worrying about CPU availability, forming the foundation for modern multitasking operating systems.