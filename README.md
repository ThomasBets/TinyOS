# TinyOS-3 Project

TinyOS-3 is a simulated operating system kernel supporting independent, multithreaded processes, with a focus on priority scheduling and inter-process communication. 
This project is implemented in C (C11 standard) and designed to run on Linux using the GCC compiler. 
It aims to manage the resources of a virtual machine environment efficiently, demonstrating key operating system functionalities in a simplified form.

## Table of Contents
- [Introduction](#introduction)
- [Features](#features)
- [Implementation Details](#implementation-details)
  - [Multilevel Feedback Queue Scheduler](#multilevel-feedback-queue-scheduler)
  - [Multithreading System Calls](#multithreading-system-calls)
  - [Inter-process Communication (Pipes and Sockets)](#inter-process-communication-pipes-and-sockets)
  - [System Information Output](#system-information-output)
- [Getting Started](#getting-started)
- [Development and Collaboration](#development-and-collaboration)

## Introduction
TinyOS-3 allows the scheduling and management of independent processes by sharing the CPU core time efficiently. The kernel takes full control over process lifecycle—creating, scheduling, and terminating them as required. TinyOS-3 will manage resources of a virtual machine environment, resembling characteristics of embedded systems in industries like gaming consoles, industrial tools, and communication devices.

The project is developed in C11 to maintain compatibility with classic C standards, while utilizing useful extensions provided by the C11 standard.

## Features
- **Basic Kernel**: A simple program structure with all "programs" embedded as executable functions within the main memory.
- **Scheduling Algorithm**: Implements a multilevel feedback queue (MFQ) scheduler for improved interactivity.
- **Multithreading**: Adds multithreading capabilities to processes using custom system calls.
- **Inter-Process Communication (IPC)**: Supports process communication via pipes and local sockets.
- **System Compatibility**: Uses Linux libraries (e.g., `malloc`, `free`, `printf`) to ease memory management and input/output operations.

## Implementation Details

### Multilevel Feedback Queue Scheduler
The default scheduling uses a Round-Robin approach with a First-In-First-Out (FIFO) queue. To enhance interactivity, TinyOS-3 will implement the **Multilevel Feedback Queue (MFQ)** scheduling algorithm:
  - Processes are assigned priority levels based on their execution behavior.
  - New threads enter a medium-priority queue initially.
  - Processes consuming their quantum lower in priority; those releasing CPU voluntarily increase in priority.
  - Priority inversion handling adjusts thread priorities when higher-priority threads are blocked by lower-priority threads waiting on resources (e.g., mutex locks).

### Multithreading System Calls
TinyOS-3 supports multithreaded processes with system calls defined in `tinyos.h`:
- `CreateThread`: Initializes a new thread within a process.
- `ThreadSelf`, `ThreadJoin`, `ThreadExit`, `ThreadDetach`: Manage thread lifecycle and synchronization.

Each thread is managed with a separate control block for better organization and efficiency.

### Inter-process Communication (Pipes and Sockets)
Two primary mechanisms of IPC are implemented:
  - **Pipes**: Provides a unidirectional data channel between threads, suitable for synchronized data transfer.
  - **Sockets**: Allows local inter-process communication in a manner similar to network sockets. System calls such as `Socket`, `Connect`, `Listen`, `Accept`, and `Shutdown` provide a familiar interface for creating and managing socket-based communication.

### System Information Output
The `OpenInfo` system call allows user programs to access and print real-time system data, including active process information and resource usage.

## Getting Started
### Prerequisites
- **Linux** operating system.
- **GCC Compiler** with C11 support.

### Compilation
To compile TinyOS-3:
```bash
gcc -std=c11 -o tinyos3 tinyos3.c -pthread
