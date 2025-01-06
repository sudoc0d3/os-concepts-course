# OS Structure

This chapter discusses:

- Services an operating system provides to users, processes, and other systems
- Various ways of structuring an operating system (OS)
- How OSs are installed and customized
- How OSs boot

---

## Services

**Services** are accessed using *system calls*, which invoke the corresponding Interrupt Service Routine (ISR). Examples include:

- **User Interface (UI)**: Command-line interfaces (CLI) or graphical user interfaces (GUI)
- **Program Execution**: Loading, running, and terminating programs
- **I/O Operations**: Accessing and controlling input/output devices
- **File System Manipulation**: Reading, writing, creating, and deleting files and directories
- **Communication**: Enabling processes to exchange information
- **Error Detection**: Monitoring the system to detect and report errors
- **Resource Allocation**: Managing CPU cycles, memory, and I/O devices
- **Accounting**: Tracking resource usage for optimization and billing
- **Protection and Security**: Ensuring authorized access and secure communication

---

## System Calls

### Overview

- A **system call** is a *special function call* that allows user programs to request services from the OS.
- **APIs** (Application Programming Interfaces) are abstractions that wrap multiple system calls.
- **POSIX** (Portable Operating System Interface) is a standard API for UNIX-based operating systems.
- The **system call interface** acts as the intermediary between the application program and the actual system call.
- **Standard library functions** are typically implemented as system calls.

### Parameter Passing

- Parameters are passed by placing them in memory and passing the address of the first parameter to a register.
  - This addresses the issue of limited parameters due to the finite number of registers.
- The *caller* (usually the program) pushes the parameters.
- The *callee* (the OS) pops the parameters.

### System Programs

- System programs belong to the OS but are not part of the kernel.
- They involve many system calls and include:
  - **File managers** and **text editors**: Launched by users to perform tasks requiring system calls.
  - **Background services/daemons/subsystems**: Often launched at boot time by the system, though some can be started by the user after boot.

---

## OS Design and Implementation

### Design

- **User goals** differ from **system/developer goals**.
- **Policy** determines *what* will be done.
- **Mechanism** determines *how* to do it.
- Mechanisms should be flexible enough to allow changes in policy due to hardware advancements.

### Implementation

- Most OS cores are written in C/C++ rather than assembly due to:
  - Application of software engineering principles (e.g., productivity, readability, and maintainability).
  - Portability across architectures.
  - Compiler optimizations.
- Some system programs may be written in scripting languages for simplicity.

---

## OS Structuring Approaches

### 1. Simple/Monolithic

A single, large kernel that contains all OS functionality.

- **Pros**:
  - High performance.
- **Cons**:
  - Difficult to maintain and debug.
- **Memory Shape**:
  ```
  [     |   kernel  |       ]
  ```

### 2. Layered Approach

Services are organized into layers, where a service in one layer can only call services in the layer directly below it.

- **Pros**:
  - Easier development and debugging.
  - Aligned with software engineering principles.
- **Cons**:
  - Difficulty in assigning certain services to specific layers.
  - Overhead in inter-layer communication.
- **Memory Shape**:
  ```
  [      |   kernel  |       ]
  ```
  *(Similar to monolithic, but structured differently in code)*

### 3. Microkernel

A minimal kernel with only essential services. All other services run in user mode outside the kernel. Communication between services occurs through **messages** via the kernel.

- **Pros**:
  - Increased stability: Failures in user-mode services do not crash the kernel.
  - Less frequent recompilation: Drivers and services outside the kernel are updated independently.
  - Enhanced security: Smaller kernel reduces vulnerabilities.
  - Improved portability.
- **Cons**:
  - Overhead due to message passing.
- **Memory Shape**:
  ```
  [    | sv1 | |sv2|     |kernel|    | sv3 |     ]
  ```

### 4. Modular Approach

Kernel allows other services to be dynamically loaded as *modules*, essentially extensions to the kernel.

- **Pros**:
  - Lower memory usage.
  - Flexibility: Modules can communicate directly with each other.
- **Cons**:
  - Overhead in loading modules at runtime.
- **Memory Shape**:
  ```
  [   |sv1| |sv2| |sv3| | kernel |     ]
  ```

### 5. Hybrid Approach

Combines multiple approaches to address diverse needs. Most modern OSs use a hybrid model due to evolving requirements.

- Some OSs are designed based on or inspired by other OSs.
