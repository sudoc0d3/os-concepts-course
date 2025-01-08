### Lecture 5: Process Synchronization

---

#### **1. Introduction and Background**
- **Concurrency in Processes:**
  - Multiple processes may execute simultaneously.
  - Processes may access shared data, leading to **data inconsistency**.

- **Critical Section Problem:**
  - Ensures that multiple processes accessing shared data do so without interference.
  - Example: **Producer-Consumer Problem**
    - Producers increment a buffer counter, while consumers decrement it.
    - If operations overlap (race conditions), the buffer counter may become inconsistent.

---

#### **2. The Critical-Section Problem**
The problem involves designing a protocol ensuring:
1. **Mutual Exclusion:** Only one process executes in the critical section at a time.
2. **Progress:** If no process is in the critical section, the next process must not be indefinitely postponed.
3. **Bounded Waiting:** A process must not wait indefinitely to enter its critical section.

**Structure of a Process:**
```c
do {
   entry_section();
   critical_section();
   exit_section();
   remainder_section();
} while (TRUE);
```

---

#### **3. Peterson’s Solution**
- Designed for two processes.
- Uses shared variables:
  - `turn`: Indicates whose turn it is.
  - `flag[]`: Indicates if a process is ready to enter its critical section.
- **Algorithm:**
```c
do {
   flag[i] = true;
   turn = j;
   while (flag[j] && turn == j);
   // critical section
   flag[i] = false;
   // remainder section
} while (true);
```
- Meets all three requirements: mutual exclusion, progress, and bounded waiting.

---

#### **4. Synchronization Hardware**
- Hardware instructions like `test_and_set` or `compare_and_swap` ensure atomicity.
- **`test_and_set` Example:**
```c
boolean test_and_set(boolean *target) {
   boolean rv = *target;
   *target = TRUE;
   return rv;
}
```
- **`compare_and_swap` Example:**
```c
int compare_and_swap(int *value, int expected, int new_value) {
   int temp = *value;
   if (*value == expected)
      *value = new_value;
   return temp;
}
```

---

#### **5. Mutex Locks**
- Simplest synchronization tool:
  - **acquire():** Locks the critical section.
  - **release():** Unlocks the critical section.
- Example:
```c
acquire() {
   while (!available);
   available = false;
}

release() {
   available = true;
}
```
- May cause **busy waiting**, hence called **spinlocks**.

---

#### **6. Semaphores**
- **Counting Semaphore:** Integer variable for synchronization, modified using:
  - `wait()` (decrement)
  - `signal()` (increment)
- Binary semaphores (value 0 or 1) function like mutex locks.
- **Example Usage:**
```c
P1: S1; signal(synch);
P2: wait(synch); S2;
```

**Avoiding Busy Waiting:**
Semaphore implementation includes:
- A **waiting queue**.
- Operations:
  - `block()`: Adds the process to the waiting queue.
  - `wakeup()`: Removes a process from the queue.

---

#### **7. Classic Synchronization Problems**
1. **Bounded-Buffer Problem:**
   - Use semaphores for mutual exclusion and buffer management.
2. **Readers-Writers Problem:**
   - Allows multiple readers or a single writer but not both.
   - Uses semaphores `rw_mutex` and `mutex` for synchronization.
3. **Dining-Philosophers Problem:**
   - Philosophers alternate between thinking and eating.
   - Use semaphores to manage chopstick access.

---

#### **8. Monitors**
- High-level synchronization construct.
- Combines data variables and procedures to ensure mutual exclusion.
- Example:
```c
monitor MonitorName {
   // shared variables
   procedure P1(...) { ... }
   procedure P2(...) { ... }
}
```

---

### **Interactive Questions**

1. **What are the three conditions of the Critical-Section Problem?**

   <details>
   <summary>Answer</summary>
   Mutual Exclusion, Progress, Bounded Waiting.
   </details>

2. **How does Peterson's Solution ensure mutual exclusion?**

   <details>
   <summary>Answer</summary>
   By using `flag` and `turn` variables to alternate access between processes and block simultaneous entry into the critical section.
   </details>

3. **What is the difference between a mutex lock and a semaphore?**

   <details>
   <summary>Answer</summary>
   A mutex lock is a binary lock for mutual exclusion, while a semaphore is a more general synchronization tool that can have any integer value.
   </details>

---

### **Multiple-Choice Quiz**

1. **What is the purpose of the `test_and_set` instruction?**
   - A. To swap memory values.
   - B. To test and set a lock atomically.
   - C. To compare two values.
   - D. To implement semaphores.

   <details>
   <summary>Answer</summary>
   B. To test and set a lock atomically.
   </details>

2. **Which problem does Peterson’s solution address?**
   - A. Process creation.
   - B. Process termination.
   - C. Critical section problem.
   - D. Interprocess communication.

   <details>
   <summary>Answer</summary>
   C. Critical section problem.
   </details>

3. **What type of semaphore allows values beyond 0 and 1?**
   - A. Binary semaphore.
   - B. Mutex lock.
   - C. Counting semaphore.
   - D. Test semaphore.

   <details>
   <summary>Answer</summary>
   C. Counting semaphore.
   </details>

4. **What is the main issue in the Dining Philosophers Problem?**
   - A. Mutual exclusion
   - B. Starvation and deadlock
   - C. Race condition
   - D. Resource allocation

   <details>
   <summary>Answer</summary>
   B. Starvation and deadlock
   </details>
