### Lecture 8: Main Memory

---

#### **1. Introduction to Memory Management**
Memory management ensures efficient utilization of the computer's main memory while providing a logical abstraction for processes.

- **Key Concepts:**
  - Programs must be loaded into memory to execute.
  - Main memory (RAM) is the only directly accessible storage for the CPU.
  - Memory is managed using various hardware and software techniques to ensure protection and efficient allocation.

---

#### **2. Address Binding**
- **Stages of Binding:**
  1. **Compile Time:** Absolute addresses are generated if memory location is known beforehand.
  2. **Load Time:** Relocatable addresses are generated, adjusted during loading.
  3. **Execution Time:** Binding occurs dynamically; the process can be moved during execution.

- **Logical vs. Physical Addresses:**
  - **Logical Address:** Generated by the CPU; also called a virtual address.
  - **Physical Address:** Actual location in memory.

- The **Memory Management Unit (MMU)** maps logical to physical addresses at runtime.

---

#### **3. Swapping**
Swapping temporarily moves a process out of main memory to a **backing store** and brings it back later.

- **Key Points:**
  - Helps run more processes than can fit in physical memory.
  - **Roll Out, Roll In:** Swapping based on process priority.
  - Modern systems minimize swapping due to performance concerns.

---

#### **4. Contiguous Memory Allocation**
- Memory is divided into contiguous sections.
- **Dynamic Storage Allocation Strategies:**
  1. **First-Fit:** Allocates the first hole that fits.
  2. **Best-Fit:** Allocates the smallest suitable hole.
  3. **Worst-Fit:** Allocates the largest hole.

- **Fragmentation:**
  - **External Fragmentation:** Sufficient memory exists, but it's not contiguous.
  - **Internal Fragmentation:** Allocated memory exceeds process needs.

---

#### **5. Segmentation**
Segmentation divides programs into logical units like code, data, and stack.

- **Logical Address:** Consists of a segment number and an offset.
- **Segment Table:** Maps segments to physical memory.
  - Contains the **base** (starting address) and **limit** (size) of each segment.

**Advantages:**
  - Matches the programmer's logical view of memory.
  - Facilitates code sharing and protection.

---

#### **6. Paging**
Paging divides both physical and logical memory into fixed-size blocks:
- **Frames:** Physical memory blocks.
- **Pages:** Logical memory blocks.

- **Address Translation:**
  - Logical address consists of a **page number** and an **offset**.
  - Page tables map logical pages to physical frames.

**Advantages:**
  - Eliminates external fragmentation.
  - Enables efficient memory usage.

**Challenges:**
  - **Page Table Overhead:** Large page tables may require hierarchical or hashed structures.
  - **Internal Fragmentation:** Last frame may not be fully used.

---

#### **7. Structure of the Page Table**
Techniques to handle large page tables:
1. **Hierarchical Paging:** Breaks down page tables into multiple levels.
2. **Hashed Page Tables:** Uses a hash table to store mappings.
3. **Inverted Page Tables:** Tracks physical pages instead of logical ones, reducing memory overhead.

---

#### **8. Examples of Architectures**
- **Intel 32/64-bit Architectures:** Support both segmentation and paging.
- **ARM Architecture:** Primarily uses paging with extensions for memory protection and virtualization.

---

### **Interactive Questions**

1. **What is the difference between logical and physical addresses?**

   <details>
   <summary>Answer</summary>
   Logical addresses are generated by the CPU during program execution, while physical addresses refer to the actual location in memory.
   </details>

2. **How does paging reduce external fragmentation?**

   <details>
   <summary>Answer</summary>
   By dividing memory into fixed-size frames and pages, any available frame can be used for a page, eliminating the need for contiguous memory blocks.
   </details>

3. **Why might hierarchical paging be used instead of a flat page table?**

   <details>
   <summary>Answer</summary>
   Hierarchical paging reduces memory overhead by breaking large page tables into smaller, more manageable levels.
   </details>

---

### **Multiple-Choice Quiz**

1. **What is the main advantage of paging over contiguous memory allocation?**
   - A. It simplifies address translation.
   - B. It eliminates external fragmentation.
   - C. It improves memory access speed.
   - D. It requires less hardware support.

   <details>
   <summary>Answer</summary>
   B. It eliminates external fragmentation.
   </details>

2. **Which of the following is NOT a stage of address binding?**
   - A. Compile Time
   - B. Load Time
   - C. Execution Time
   - D. Runtime Allocation

   <details>
   <summary>Answer</summary>
   D. Runtime Allocation
   </details>

3. **In segmentation, what does the segment table store?**
   - A. Logical addresses
   - B. Base and limit of segments
   - C. Page numbers and offsets
   - D. Process control information

   <details>
   <summary>Answer</summary>
   B. Base and limit of segments
   </details>

4. **Which of the following is true about inverted page tables?**
   - A. They map logical to physical addresses directly.
   - B. They track physical frames instead of logical pages.
   - C. They eliminate the need for translation lookaside buffers (TLBs).
   - D. They increase memory usage for large address spaces.

   <details>
   <summary>Answer</summary>
   B. They track physical frames instead of logical pages.
   </details>
