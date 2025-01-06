# Processes in Operating Systems

### Concept
- A **process** is an **active** entity.
- A **program** is a **passive** entity.

#### Process in Memory Layout:
```
max
    stack   -> local variables, function parameters, return values/addresses
      |
      v

      ^
      |
    heap    -> dynamically allocated variables
    data     -> global & static variables
    text     -> code
0
```

---

### Process States and Transitions

| **State Transition**        | **Reason**                     |
|-----------------------------|---------------------------------|
| **new → ready**            | Admission                      |
| **ready → running**         | Scheduler dispatch             |
| **running → ready**         | (Timed) interrupt              |
| **running → terminated**   | Exit or exception              |
| **running → waiting**       | I/O or event wait              |
| **waiting → ready**         | I/O or event completion        |

- When a process is **ready** to take the CPU, it resides in the **ready queue**.
- When a process is **running**, it is **owning the CPU**.

---

### Process Control Block (PCB)
- A **data structure** to track information about each process.
- Stores:
  - **Process state**: (waiting, running, etc.).
  - **Program counter**: Address of the next instruction.
  - **CPU register values**: Ensures a process resumes execution with the correct state.
  - **Scheduling information**: Priority, scheduling policies.
  - **Memory management information**: Memory allocations.
  - **Accounting information**: CPU usage time, total execution time.

---

### Process Transition Steps
1. When a process (e.g., `P0`) is interrupted, the kernel saves its state (PCB0).
2. The kernel selects the next process (e.g., `P1`).
3. The kernel reloads the state of `P1` (PCB1) from memory (kernel address space).

- **Idle Time**: The time the kernel executes instead of user processes. The CPU is not idle during this period, but it appears idle to users.

---

### Threads
- A **thread** is a lightweight subprocess.
- Applications can be single-threaded or multi-threaded.
- For multi-threaded applications, the PCB is maintained on a **per-thread basis**.

---

### OS Queues
- **Job queue**: List of all system processes.
- **Ready queue**: Maintains processes ready to execute.
- **Device queue**: Specific to each device; holds processes waiting for I/O.

---

### Schedulers
- **Short-term scheduler**: Selects the next process to execute from the ready queue.
  - Invoked frequently.
- **Long-term scheduler**: Determines which processes to bring into the ready queue.
  - Focuses on maintaining a balance between CPU-bound and I/O-bound processes.
  - Invoked infrequently.

#### Process Types
- **CPU-bound process**: Long CPU bursts, low I/O activity (e.g., scientific calculations).
  - Example: `|cpu...|io|cpu...|`
- **I/O-bound process**: Short CPU bursts, high I/O activity (e.g., interactive applications).
  - Example: `|io..|cpu|io..|cpu|io...|`

#### Medium-term Scheduler
- Performs **swapping** (moving processes between memory and disk):
  - **Swap out**: Move process from memory to disk.
  - **Swap in**: Bring process back from disk to memory.
  - Used when memory is full or to balance CPU-bound and I/O-bound processes.

---

### Context Switching
- The kernel's mechanism to switch the CPU from one process to another.
- Steps:
  1. Save the PCB (registers, program counter) of the previous process.
  2. Load the PCB of the next process.
- **Context Switching Overhead**: Takes time (e.g., ~1ms, which equals a million CPU cycles on a 1 GHz processor).

---

### Foreground and Background Processes
- Originated from resource constraints (low memory, limited computation power).
- **Foreground process**: Typically one at a time.
- **Background processes**: Multiple, with limited computations (e.g., notifications).

---

### Process Creation and Termination (POSIX Implementation)
- **Process Table**: Stores details of all processes.
- **PID**: Unique process identifier.

#### Process Creation
1. **Parent creates child process**:
   - The child can inherit resources from the parent or obtain them from the OS.
2. **Resource inheritance**:
   - **Shared resources**: Parent and child share resources.
   - **Partitioned resources**: Parent divides resources between itself and the child.
3. Parent and child can execute **concurrently**, or the parent can **wait** for the child to complete.

#### POSIX System Calls
- **fork()**:
  - Creates a child process.
  - Returns:
    - `>0`: Child PID (in the parent process).
    - `0`: In the child process.
    - `<0`: Failure to create the child process.
  - The child duplicates the parent's memory.
  - Execution continues in both parent and child after `fork()`.
- **exec()**:
  - Replaces the child process with a new program.
  - Example: Replace the child process with a binary file and its arguments.
- **wait()**:
  - Suspends the parent process until the child completes.
  - Prevents **zombie processes**.
- **exit()**:
  - Terminates a process.
  - Deallocates resources and returns a status to the parent.

#### Zombie Processes
- A child process that has terminated but still occupies an entry in the process table.
- Occurs when the parent does not call `wait()` to clean up.

#### Orphan Processes
- A child process whose parent has terminated.
- Adopted by the **init()** process (PID=1) in most systems.

#### Summary
- **fork()**: Create a duplicate child process.
- **exec()**: Replace process memory with a new program.
- **wait()**: Suspend parent until child finishes.
- **exit()**: Terminate process and release resources.
- **Zombie**: Child terminated but not cleaned up.
- **Orphan**: Parent terminated, child continues execution.

---

### Inter-Process Communication (IPC)
- **Message Passing**:
  - Processes communicate via the kernel using system calls.
  - Messages are exchanged through kernel-managed message queues.
- **Shared Memory**:
  - Processes share a memory block created by one process.
  - Faster than message passing, but susceptible to cache coherence issues.
- **Cache Coherence Problem**:
  - In multi-processor systems, stale data in cache can delay updates to shared memory.

---

### Producer-Consumer Problem
- **Bounded Buffer**: Limited size buffer.
- **Unbounded Buffer**: Infinite size buffer (theoretical).
- Practical Implementation:
  - Producer increments buffer index: `in = (in + 1) % buffer_size;`
  - Consumer decrements buffer index: `out--;`
  - Check buffer full: `if ((in + 1) % buffer_size == out) wait();`

---

### Other IPC Methods
- **Direct Communication**:
  - Processes communicate directly.
  - Example: `send(pid, msg)`.
- **Indirect Communication**:
  - Communication via mailboxes.
  - Example: `send(mid, msg)`.
- **Message Passing Modes**:
  - **Blocking (Synchronous)**:
    - Sender waits until the message is received.
    - Receiver waits until a message is available.
  - **Non-Blocking (Asynchronous)**:
    - Sender continues without waiting.
    - Receiver checks for messages periodically or uses timeouts.
- **Sockets**:
  - Endpoints for communication identified by IP address and port number.
  - Communication occurs between pairs of sockets.
- **Remote Procedure Call (RPC)**:
  - Allows function calls across a network.
  - Steps:
    1. Pack (marshal) data.
    2. Unpack data.
    3. Execute remotely.
    4. Return results.
- **Pipes**:
  - **Ordinary Pipes**: Unidirectional; data flows from parent (writer) to child (reader).
  - **Named Pipes**: Bidirectional; no parent-child relationship required.
