### Lecture 9: Virtual Memory

---

#### **1. Introduction to Virtual Memory**
Virtual memory separates user logical memory from physical memory, allowing:
- Partial program execution without loading the entire process into memory.
- **Benefits:**
  - Supports larger programs than physical memory size.
  - Enables more efficient multitasking.
  - Reduces I/O operations for loading/swapping processes.

**Example:** A system can execute a 1GB process on a machine with only 512MB of RAM using virtual memory.

---

#### **2. Demand Paging**
Demand paging is a lazy-loading strategy:
- **How it Works:**
  - Pages are brought into memory only when required.
  - Unreferenced pages remain on disk, reducing I/O operations.

- **Key Components:**
  - **Page Table Valid-Invalid Bit:**
    - `Valid (v)`: Page in memory.
    - `Invalid (i)`: Page not in memory → **Page Fault**.

---

#### **3. Page Fault Handling**
A **page fault** occurs when a referenced page is not in memory:
1. OS checks the page table.
2. If the reference is valid, the page is loaded into a free frame.
3. Update the page table and restart the interrupted instruction.

---

#### **4. Copy-on-Write (COW)**
- Allows processes to share memory pages.
- When a write occurs, a new copy of the page is created for the writing process.
- Efficiently supports process creation (`fork()`), as only modified pages are copied.

---

#### **5. Page Replacement**
When memory is full, a page replacement algorithm selects a page to replace:
- **Basic Steps:**
  1. Locate the desired page on disk.
  2. Find a free frame or select a victim frame.
  3. If the victim frame is modified, write it to disk.
  4. Load the desired page and update page tables.

**Common Algorithms:**
1. **FIFO (First-In, First-Out):** Replaces the oldest page.
   - **Belady’s Anomaly:** Adding more frames can increase page faults.
2. **Optimal:** Replaces the page not needed for the longest future period.
   - Used for theoretical benchmarking.
3. **LRU (Least Recently Used):** Replaces the least recently accessed page.
   - Common and practical, though slightly expensive to implement.
4. **Second-Chance:** A FIFO variation using reference bits to decide replacement.

---

#### **6. Allocation of Frames**
- **Fixed Allocation:** Equal or proportional frame allocation.
- **Priority Allocation:** Higher-priority processes get more frames.
- **Global vs. Local Replacement:**
  - **Global:** Any frame can be replaced.
  - **Local:** Only a process's allocated frames are replaced.

---

#### **7. Thrashing**
Thrashing occurs when a process spends more time swapping pages in and out than executing:
- **Causes:**
  - Insufficient frames for the working set.
  - High page-fault rate.
- **Solution:** Reduce the degree of multiprogramming or use working set models to manage frame allocation.

---

#### **8. Working-Set Model**
- Tracks the set of pages actively used by a process.
- **Parameters:**
  - **Δ (window size):** Determines the locality of reference.
  - **WSS (Working-Set Size):** Total number of pages in the working set.

---

#### **9. Page-Fault Frequency (PFF)**
- Directly adjusts frames based on the page-fault rate:
  - **Low fault rate:** Remove frames.
  - **High fault rate:** Add frames.

---

#### **10. Memory-Mapped Files**
- Maps file content directly into the virtual memory address space.
- Enables efficient file I/O by treating file contents as part of process memory.

---

### **Interactive Questions**

1. **What is the role of the valid-invalid bit in demand paging?**

   <details>
   <summary>Answer</summary>
   The valid-invalid bit indicates whether a page is in memory (`valid`) or not (`invalid`), helping detect page faults.
   </details>

2. **Explain how Copy-on-Write (COW) works during process creation.**

   <details>
   <summary>Answer</summary>
   COW allows parent and child processes to share pages in memory until one process modifies a page, triggering a copy operation.
   </details>

3. **What is the difference between global and local page replacement?**

   <details>
   <summary>Answer</summary>
   Global replacement selects a frame from any process, while local replacement only uses a process’s allocated frames.
   </details>

---

### **Multiple-Choice Quiz**

1. **Which of the following best describes thrashing?**
   - A. Low CPU utilization due to frequent I/O operations.
   - B. A process running out of disk space.
   - C. Too many processes executing concurrently.
   - D. Insufficient memory for kernel operations.

   <details>
   <summary>Answer</summary>
   A. Low CPU utilization due to frequent I/O operations.
   </details>

2. **Which page replacement algorithm guarantees the lowest page-fault rate?**
   - A. FIFO
   - B. Optimal
   - C. LRU
   - D. Second-Chance

   <details>
   <summary>Answer</summary>
   B. Optimal
   </details>

3. **What happens during a page fault?**
   - A. A process is terminated.
   - B. A page is swapped from memory to disk.
   - C. The required page is loaded into memory.
   - D. All processes are suspended.

   <details>
   <summary>Answer</summary>
   C. The required page is loaded into memory.
   </details>

4. **In the working-set model, what does Δ represent?**
   - A. The page-fault rate.
   - B. The process's memory limit.
   - C. The working-set window.
   - D. The total number of frames in memory.

   <details>
   <summary>Answer</summary>
   C. The working-set window.
   </details>
