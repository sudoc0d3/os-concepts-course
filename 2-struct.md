### Lecture 2: Operating-System Structures

---

#### **1. Operating System Services**
Operating systems provide services for both users and the system itself. These services are categorized into:

1. **User-Centric Services:**
   - **User Interface (UI):** 
     - Command-Line Interface (CLI)
     - Graphical User Interface (GUI)
     - Touchscreen interfaces
   - **Program Execution:** OS loads programs into memory and manages their execution.
   - **I/O Operations:** Manages interaction with devices like keyboards, disks, etc.
   - **File-System Manipulation:** Includes creating, deleting, reading, writing, and searching files and directories.
   - **Communications:** Allows processes to exchange information via shared memory or message passing.
   - **Error Detection:** Identifies and handles errors in hardware, software, and user programs.

2. **System-Centric Services:**
   - **Resource Allocation:** Distributes CPU cycles, memory, and I/O devices among processes.
   - **Accounting:** Tracks resource usage by users and programs.
   - **Protection and Security:** Controls access to resources and defends against threats.

---

#### **2. User Operating System Interface**
1. **CLI (Command-Line Interface):**
   - Users input commands, which are interpreted and executed by the system.
   - Examples include UNIX shells like Bourne Shell and Windows Command Prompt.
2. **GUI (Graphical User Interface):**
   - Users interact with icons, windows, and menus.
   - Examples: Microsoft Windows GUI and macOS Aqua.
3. **Touchscreen Interfaces:**
   - Designed for devices without traditional input devices.
   - Actions are based on touch gestures and virtual keyboards.

---

#### **3. System Calls**
System calls are the interface between user applications and the OS. Key points include:
- **Access through APIs:** Most system calls are accessed via high-level APIs like Win32, POSIX, or Java API.
- **Parameter Passing:** Parameters for system calls are passed using registers, blocks in memory, or stacks.

**Example:** A system call sequence to copy a file includes opening the file, reading its content, writing it to a new file, and closing both files.

---

#### **4. Types of System Calls**
1. **Process Control:** Create, terminate, load, execute, and manage processes.
2. **File Management:** Open, close, read, write, and delete files.
3. **Device Management:** Attach, detach, read, and write to devices.
4. **Information Maintenance:** Get and set time, date, and system attributes.
5. **Communications:** Manage message passing or shared memory between processes.
6. **Protection:** Control access permissions and enforce security.

---

#### **5. System Programs**
These provide a development and execution environment. They include:
- File manipulation tools (e.g., copy, delete).
- Programming language support (e.g., compilers, interpreters).
- Communication utilities.
- Background services like error logging and scheduling.

---

#### **6. Operating System Design and Implementation**
Key considerations:
- **Separation of Policy and Mechanism:** Policies decide "what," mechanisms determine "how."
- **Implementation Languages:** OS core in C/C++, with assembly for lower levels.

---

#### **7. Operating System Structure**
Common structures include:
1. **Simple Structure:** Minimal layers, e.g., MS-DOS.
2. **Layered Approach:** OS is divided into hierarchical layers.
3. **Microkernel:** Moves essential functions to user space for flexibility.
4. **Modules:** Object-oriented design, used in Linux and Solaris.
5. **Hybrid Systems:** Combines multiple approaches, e.g., macOS and Windows.

---

#### **8. System Boot**
- The **bootstrap loader** initializes the system, loads the OS kernel, and starts execution.
- Tools like GRUB can manage multiple boot configurations.

---

### **Interactive Questions**
1. **What are the main services provided by an operating system?**

   <details>
   <summary>Answer</summary>
   Services include user interfaces, program execution, I/O operations, file manipulation, communication, and error detection.
   </details>

2. **Why are APIs preferred over direct system calls?**

   <details>
   <summary>Answer</summary>
   APIs provide a high-level, user-friendly abstraction, making it easier for developers to write programs without dealing with system call complexities.
   </details>

3. **What is the advantage of a microkernel structure?**

   <details>
   <summary>Answer</summary>
   Microkernels are easier to extend, port, and secure as they have less code running in kernel mode.
   </details>

---

### **Multiple-Choice Quiz**

1. **Which of the following is NOT a type of system call?**
   - A. Process control
   - B. File manipulation
   - C. Command-line interpretation
   - D. Communications

   <details>
   <summary>Answer</summary>
   C. Command-line interpretation
   </details>

2. **What is the purpose of the bootstrap loader?**
   - A. To manage I/O devices
   - B. To initialize hardware and load the kernel
   - C. To execute user programs
   - D. To allocate resources

   <details>
   <summary>Answer</summary>
   B. To initialize hardware and load the kernel
   </details>

3. **Which OS structure uses a modular approach for flexibility?**
   - A. Simple Structure
   - B. Layered Approach
   - C. Microkernel
   - D. Modules

   <details>
   <summary>Answer</summary>
   D. Modules
   </details>
