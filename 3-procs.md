### Lecture 3: Processes and Interprocess Communication (IPC)

---

#### **1. Process Concept**

- A **process** is a program in execution, forming the basis of computation.
- **Program vs. Process:**
  - A **program** is a passive entity (e.g., a file on disk).
  - A **process** is an active entity that includes:
    - Program code (text section)
    - Current activity (program counter, registers)
    - Stack (temporary data like function parameters)
    - Data section (global variables)
    - Heap (dynamically allocated memory)

**Example:** Running multiple instances of a web browser creates multiple processes.

**Process States:**
1. **New:** Process is being created.
2. **Running:** Instructions are being executed.
3. **Waiting:** Process is waiting for an event (e.g., I/O completion).
4. **Ready:** Process is waiting to be assigned to a processor.
5. **Terminated:** Process has finished execution.

**Key Structure:** **Process Control Block (PCB)**
- Contains process state, program counter, CPU registers, memory allocation, and other data.

---

#### **2. Process Scheduling**

The OS must efficiently manage CPU use:
- **Scheduling Queues:**
  - **Job Queue:** All processes in the system.
  - **Ready Queue:** Processes in memory, ready to execute.
  - **Device Queues:** Processes waiting for I/O devices.
- **Schedulers:**
  - **Long-term Scheduler:** Determines which processes enter the ready queue (controls multiprogramming).
  - **Short-term Scheduler:** Allocates CPU to a process.
  - **Medium-term Scheduler:** Temporarily removes processes from memory (swapping).

---

#### **3. Operations on Processes**

1. **Process Creation:**
   - Parent process creates children, forming a tree.
   - Examples in UNIX:
     - `fork()`: Creates a new process.
     - `exec()`: Replaces process memory with a new program.

2. **Process Termination:**
   - A process ends with an `exit()` system call.
   - The parent can terminate child processes using `abort()`.

---

#### **4. Interprocess Communication (IPC)**

**Cooperating Processes:** Processes that share information or resources for:
- Information sharing
- Speedup of computation
- Modularity
- Convenience

**IPC Models:**
1. **Shared Memory:**
   - Processes share a memory region.
   - Example: Producer-Consumer Problem using a bounded buffer.

2. **Message Passing:**
   - Processes exchange messages via operations like `send()` and `receive()`.

**Communication Variants:**
- **Direct Communication:** Processes explicitly name each other.
- **Indirect Communication:** Messages are sent through mailboxes (ports).

---

#### **5. Communication in Client-Server Systems**

Techniques include:
1. **Sockets:** Endpoint for communication, identified by an IP address and port.
2. **Remote Procedure Calls (RPCs):** Abstract procedure calls between networked systems.
3. **Pipes:**
   - Ordinary Pipes: Unidirectional communication requiring a parent-child relationship.
   - Named Pipes: Bidirectional, no parent-child relationship needed.
4. **Remote Method Invocation (RMI):** Java-based mechanism similar to RPCs.

---

### **Interactive Questions**
1. **What are the main states of a process, and what happens in each state?**

   <details>
   <summary>Answer</summary>
   States include:<br>
   - New: Process is created.<br>
   - Running: Instructions are executed.<br>
   - Waiting: Waiting for an event.<br>
   - Ready: Waiting for CPU allocation.<br>
   - Terminated: Process execution ends.<br>
   </details>

2. **How do `fork()` and `exec()` work in process creation?**

   <details>
   <summary>Answer</summary>
   `fork()` creates a new process as a copy of the parent. `exec()` replaces the new process's memory with a new program.
   </details>

3. **What is the difference between shared memory and message passing in IPC?**

   <details>
   <summary>Answer</summary>
   Shared memory allows processes to communicate by accessing the same memory region, while message passing involves sending and receiving messages via the OS.
   </details>

---

### **Multiple-Choice Quiz**

1. **What is a process?**
   - A. A program stored on disk
   - B. A program in execution
   - C. A user interface for execution
   - D. A type of operating system

   <details>
   <summary>Answer</summary>
   B. A program in execution
   </details>

2. **Which scheduler controls the degree of multiprogramming?**
   - A. Short-term scheduler
   - B. Long-term scheduler
   - C. Medium-term scheduler
   - D. None of the above

   <details>
   <summary>Answer</summary>
   B. Long-term scheduler
   </details>

3. **What is the purpose of `exec()` in UNIX?**
   - A. Create a new process
   - B. Replace process memory with a new program
   - C. Terminate a process
   - D. Manage process scheduling

   <details>
   <summary>Answer</summary>
   B. Replace process memory with a new program
   </details>

4. **Which IPC mechanism uses a bounded buffer?**
   - A. Message passing
   - B. Shared memory
   - C. Sockets
   - D. Remote Procedure Call

   <details>
   <summary>Answer</summary>
   B. Shared memory
   </details>
