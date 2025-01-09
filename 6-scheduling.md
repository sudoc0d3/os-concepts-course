### Lecture 6: CPU Scheduling

---

#### **1. Introduction to CPU Scheduling**
CPU scheduling is a core aspect of multiprogramming operating systems, where the CPU is shared among multiple processes to maximize efficiency.

- **CPU–I/O Burst Cycle:** 
  - Processes alternate between CPU execution and I/O waits.
  - CPU burst distribution is critical for scheduling algorithms.

---

#### **2. Scheduling Criteria**
Key metrics to evaluate CPU scheduling:
1. **CPU Utilization:** Keep the CPU as busy as possible.
2. **Throughput:** Number of processes completed per time unit.
3. **Turnaround Time:** Total time taken for a process from submission to completion.
4. **Waiting Time:** Time spent by a process in the ready queue.
5. **Response Time:** Time from request submission to first response (important in time-sharing).

---

#### **3. Scheduling Algorithms**

##### **a. First-Come, First-Served (FCFS)**
- Processes are executed in the order of arrival.
- **Advantages:** Simple to implement.
- **Disadvantages:** 
  - May lead to the **convoy effect** where short processes wait for long ones.
- **Example:**
  Processes: P1 (24ms), P2 (3ms), P3 (3ms)
  - Average waiting time: \( (0 + 24 + 27) / 3 = 17 \) ms.

---

##### **b. Shortest-Job-First (SJF)**
- Selects the process with the shortest next CPU burst.
- **Optimal for average waiting time.**
- **Two Variants:**
  - **Non-preemptive:** Once a process starts, it cannot be preempted.
  - **Preemptive (Shortest Remaining Time First - SRTF):** Preempts if a new process has a shorter burst.

**Example:**
Processes: P1 (7ms), P2 (4ms), P3 (1ms), P4 (4ms)
- Average waiting time (Preemptive): \( (9 + 1 + 0 + 5) / 4 = 3.75 \) ms.

---

##### **c. Priority Scheduling**
- Processes are assigned priorities, and the CPU is allocated to the highest-priority process.
- **Problem:** Starvation for low-priority processes.
- **Solution:** **Aging**, where priorities increase with time.

---

##### **d. Round Robin (RR)**
- Processes are executed for a fixed **time quantum** in a cyclic order.
- **Advantages:** 
  - Reduces starvation.
  - Suitable for time-sharing systems.
- **Performance depends on quantum size:**
  - Small quantum -> High overhead.
  - Large quantum -> Similar to FCFS.

**Example:**
Processes: P1 (24ms), P2 (3ms), P3 (3ms)
- Time Quantum: 4ms.
- Average waiting time: \( (6 + 4 + 7) / 3 = 5.66 \) ms.

---

##### **e. Multilevel Queue Scheduling**
- **Ready queue partitioned** into separate queues (e.g., foreground and background).
- **Fixed Priority Scheduling:** May lead to starvation.
- **Time Slice Scheduling:** Each queue gets a percentage of CPU time.

##### **f. Multilevel Feedback Queue**
- Processes can move between queues based on behavior (e.g., aging).
- Parameters include:
  - Number of queues.
  - Scheduling algorithms for each queue.
  - Rules for upgrading/demoting processes.

---

#### **4. Multiple-Processor Scheduling**
- **Homogeneous Processors:** All processors can run any process.
- **Symmetric Multiprocessing (SMP):** Each processor is self-scheduling.
- **Processor Affinity:** Process prefers to run on the same processor to optimize cache usage.

**Load Balancing:**
- **Push Migration:** Redistributes tasks periodically from overloaded CPUs.
- **Pull Migration:** Idle CPUs pull tasks from busy ones.

---

#### **5. Algorithm Evaluation**
- **Deterministic Modeling:** Evaluates algorithms using a predefined workload.
- **Queueing Models:** Uses probabilistic models to predict system behavior.
- **Simulations:** Accurate but resource-intensive.
- **Implementation:** Most accurate, as algorithms are tested in real environments.

---

### **Interactive Questions**

1. **What is the convoy effect in FCFS scheduling?**

   <details>
   <summary>Answer</summary>
   The convoy effect occurs when shorter processes must wait for a longer process to complete, leading to inefficient CPU utilization.
   </details>

2. **How does Round Robin scheduling handle starvation?**

   <details>
   <summary>Answer</summary>
   By assigning a fixed time quantum and cycling through processes, all processes get CPU time, reducing the risk of starvation.
   </details>

3. **What are the key differences between preemptive and non-preemptive SJF scheduling?**

   <details>
   <summary>Answer</summary>
   Preemptive SJF (SRTF) allows a new process with a shorter burst to preempt the current one, while non-preemptive SJF completes the current process before switching.
   </details>

---

### **Multiple-Choice Quiz**

1. **Which scheduling algorithm minimizes average waiting time for a set of processes?**
   - A. FCFS
   - B. SJF
   - C. Priority Scheduling
   - D. Round Robin

   <details>
   <summary>Answer</summary>
   B. SJF
   </details>

2. **What is the main disadvantage of Priority Scheduling?**
   - A. High complexity
   - B. Starvation of low-priority processes
   - C. High context switch overhead
   - D. None of the above

   <details>
   <summary>Answer</summary>
   B. Starvation of low-priority processes
   </details>

3. **What does the dispatcher do in CPU scheduling?**
   - A. Selects the next process to execute.
   - B. Allocates memory to processes.
   - C. Gives control of the CPU to the selected process.
   - D. Monitors CPU usage.

   <details>
   <summary>Answer</summary>
   C. Gives control of the CPU to the selected process.
   </details>

4. **What is the effect of a very large time quantum in Round Robin scheduling?**
   - A. Increases context switch overhead.
   - B. Reduces starvation but increases waiting time.
   - C. Makes it behave like FCFS.
   - D. Improves CPU utilization significantly.

   <details>
   <summary>Answer</summary>
   C. Makes it behave like FCFS.
   </details>
