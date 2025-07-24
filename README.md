### 1. Introduction to Operating Systems

**Q1: What are the basic functions of an operating system?**  
**A:** An OS manages hardware and software resources, providing services like:  
- **Process Management**: Creating, scheduling, and terminating processes.  
- **Memory Management**: Allocating and deallocating memory to processes.  
- **File Management**: Handling file creation, deletion, and access.  
- **I/O Management**: Coordinating input/output devices.  
- **Security**: Protecting system resources and user data.

**Q2: Differentiate between batch, multiprogramming, and time-sharing systems.**  
**A:**  
- **Batch Systems**: Jobs are grouped and processed sequentially without user interaction (e.g., punch card systems).  
- **Multiprogramming Systems**: Multiple programs reside in memory, and the CPU switches between them to maximize utilization.  
- **Time-Sharing Systems**: Multiple users share the CPU through time slices, enabling interactive computing (e.g., UNIX).

**Q3: What are the advantages of time-sharing systems over batch systems?**  
**A:** Time-sharing systems allow multiple users to interact with the system simultaneously, reduce response time, and improve resource utilization compared to batch systems, which process jobs sequentially without interactivity.

---

### 2. Operating System Organization

**Q4: Explain the difference between processor and user modes.**  
**A:**  
- **Processor Mode (Kernel Mode)**: The CPU executes privileged instructions, accessing all hardware and system resources (e.g., kernel operations).  
- **User Mode**: The CPU runs user applications with restricted access to prevent unauthorized system modifications.

**Q5: What is the role of a kernel in an operating system?**  
**A:** The kernel is the core of the OS, managing hardware, processes, memory, and I/O. It handles system calls, interrupts, and resource allocation, acting as a bridge between applications and hardware.

**Q6: What are system calls? Provide examples.**  
**A:** System calls are interfaces for user programs to request OS services. Examples:  
- `fork()`: Creates a new process.  
- `read()`: Reads data from a file.  
- `exec()`: Executes a new program.

**Q7: What are system programs, and how do they differ from system calls?**  
**A:** System programs are utility software (e.g., compilers, file managers) that provide a user-friendly interface to OS functions. System calls are low-level interfaces used by programs to interact directly with the kernel.

---

### 3. Process Management

**Q8: What is a process, and how does it differ from a program?**  
**A:** A process is an executing program with its own memory, registers, and state. A program is a passive entity (code), while a process is active and managed by the OS.

**Q9: Describe the system view of a process and its resources.**  
**A:** The system views a process as an entity with:  
- **Program Counter**: Tracks the next instruction.  
- **Registers**: Store temporary data.  
- **Memory**: Code, data, and stack segments.  
- **Resources**: Files, I/O devices, and CPU time allocated by the OS.

**Q10: What is a process hierarchy?**  
**A:** A process hierarchy is a tree-like structure where a parent process creates child processes (e.g., using `fork()`). Child processes inherit attributes from the parent and form a hierarchy (e.g., init process in UNIX).

**Q11: What are threads, and what are common threading issues?**  
**A:** Threads are lightweight processes sharing the same memory space within a process. Issues include:  
- **Race Conditions**: Multiple threads accessing shared data concurrently.  
- **Deadlocks**: Threads waiting for each other’s resources.  
- **Thread Synchronization**: Coordinating thread execution using locks or semaphores.

---

### 4. Process Scheduling

**Q12: List and explain scheduling criteria.**  
**A:**  
- **CPU Utilization**: Maximize CPU usage.  
- **Throughput**: Number of processes completed per unit time.  
- **Turnaround Time**: Total time from submission to completion.  
- **Waiting Time**: Time spent in the ready queue.  
- **Response Time**: Time from submission to first response.

**Q13: Differentiate between preemptive and non-preemptive scheduling.**  
**A:**  
- **Preemptive**: The OS can interrupt a running process to allocate CPU to another (e.g., Round Robin).  
- **Non-Preemptive**: A process runs to completion or voluntarily releases the CPU (e.g., FCFS).

**Q14: Explain long-term, short-term, and medium-term scheduling.**  
**A:**  
- **Long-Term Scheduler**: Decides which jobs enter the ready queue (controls degree of multiprogramming).  
- **Short-Term Scheduler**: Allocates CPU to processes in the ready queue (fast, frequent).  
- **Medium-Term Scheduler**: Swaps processes in and out of memory to manage resource contention.

**Q15: Describe First-Come-First-Serve (FCFS) scheduling with an example.**  
**A:** FCFS schedules processes in arrival order (non-preemptive).  
**Example**: Processes P1 (burst time: 10), P2 (5), P3 (8), arriving at time 0.  
- Order: P1 → P2 → P3.  
- Waiting times: P1 = 0, P2 = 10, P3 = 15.  
- Average waiting time = (0 + 10 + 15) / 3 = 8.33.

**Q16: Explain Shortest Job First (SJF) scheduling and its advantages.**  
**A:** SJF schedules the process with the shortest burst time first (can be preemptive or non-preemptive).  
**Advantages**: Minimizes average waiting time; optimal for non-preemptive scheduling.  
**Disadvantage**: Requires burst time prediction, may cause starvation for long jobs.

**Q17: What is Shortest Remaining Time First (SRTF)?**  
**A:** SRTF is preemptive SJF, where the process with the shortest remaining time is scheduled whenever a new process arrives or completes.  
**Example**: P1 (burst: 8, arrival: 0), P2 (4, 1), P3 (9, 2).  
- Schedule: P1 (0-1), P2 (1-5), P1 (5-12), P3 (12-21).  
- Avg. waiting time = (0 + 0 + 10) / 3 = 3.33.

**Q18: Describe Priority Scheduling.**  
**A:** Processes are scheduled based on priority (higher priority runs first). Can be preemptive or non-preemptive.  
**Issue**: Starvation of low-priority processes (solved by aging).

**Q19: Explain Round Robin (RR) scheduling with a time quantum.**  
**A:** RR assigns each process a fixed time slice (quantum) in a cyclic order.  
**Example**: Processes P1 (10), P2 (5), P3 (8), quantum = 4.  
- Schedule: P1 (0-4), P2 (4-8), P3 (8-12), P1 (12-16), P3 (16-20), P1 (20-22).  
- Avg. waiting time = (10 + 3 + 8) / 3 = 7.

**Q20: What is Multilevel Queue Scheduling?**  
**A:** Processes are divided into multiple queues with different priorities (e.g., system processes, user processes). Each queue has its own scheduling algorithm (e.g., RR for interactive, FCFS for batch).

**Q21: Explain Multilevel Feedback Queue Scheduling.**  
**A:** Processes move between queues based on behavior. Short jobs get higher priority; long jobs move to lower-priority queues. Prevents starvation and adapts to process types.

---

### 5. Process Synchronization

**Q22: What are concurrent processes, and why is synchronization needed?**  
**A:** Concurrent processes execute simultaneously, sharing resources. Synchronization prevents race conditions and ensures data consistency (e.g., updating shared variables).

**Q23: Define the critical section and its requirements.**  
**A:** A critical section is a code segment accessing shared resources. Requirements:  
- **Mutual Exclusion**: Only one process can execute in the critical section at a time.  
- **Progress**: Non-critical section processes cannot block others.  
- **Bounded Waiting**: Limited waiting time for processes.

**Q24: What are semaphores, and how are they used?**  
**A:** Semaphores are synchronization tools (integer variables) with `wait()` (decrement) and `signal()` (increment) operations.  
- **Binary Semaphore**: 0 or 1 for mutual exclusion.  
- **Counting Semaphore**: Manages multiple resource instances.  
**Example**: Producer-consumer problem uses semaphores to control buffer access.

**Q25: List methods for inter-process communication (IPC).**  
**A:**  
- **Pipes**: Unidirectional data flow between processes.  
- **Message Passing**: Processes exchange messages via send/receive.  
- **Shared Memory**: Processes access a common memory region.  
- **Signals**: Asynchronous notifications for events.

---

### 6. Deadlock

**Q26: Define deadlock and its necessary conditions.**  
**A:** Deadlock occurs when processes hold resources and wait for others, causing a standstill. Conditions:  
- **Mutual Exclusion**: Resources held exclusively.  
- **Hold and Wait**: Processes hold resources while waiting for others.  
- **No Preemption**: Resources cannot be forcibly taken.  
- **Circular Wait**: Processes form a circular chain, each waiting for the next’s resource.

**Q27: How can deadlocks be prevented?**  
**A:** Break one of the four conditions:  
- Use resource sharing to avoid mutual exclusion.  
- Require processes to request all resources at once (no hold and wait).  
- Allow preemption of resources.  
- Order resources to prevent circular wait.

**Q28: Explain deadlock avoidance with the Banker’s Algorithm.**  
**A:** The Banker’s Algorithm ensures a safe state by checking if granting a resource request leads to deadlock. It uses:  
- **Available**: Free resources.  
- **Allocation**: Resources assigned to processes.  
- **Need**: Resources still needed by processes.  
The algorithm simulates resource allocation to ensure a safe sequence exists.

**Q29: How are deadlocks detected and recovered?**  
**A:**  
- **Detection**: Use a resource allocation graph or Banker’s Algorithm to identify cycles.  
- **Recovery**: Terminate processes, preempt resources, or rollback to a safe state.

---

### 7. Memory Management

**Q30: Differentiate between physical and virtual address spaces.**  
**A:**  
- **Physical Address Space**: Actual memory locations in RAM.  
- **Virtual Address Space**: Logical addresses assigned to processes, mapped to physical memory by the OS.

**Q31: Explain fixed and variable partition memory allocation strategies.**  
**A:**  
- **Fixed Partitions**: Memory is divided into fixed-size partitions; each process fits in one partition (leads to internal fragmentation).  
- **Variable Partitions**: Memory is allocated dynamically based on process size (leads to external fragmentation).

**Q32: What is paging in memory management?**  
**A:** Paging divides memory into fixed-size pages (physical) and process address space into pages (logical). Pages are mapped via a page table, eliminating external fragmentation but causing internal fragmentation.

**Q33: What is segmentation?**  
**A:** Segmentation divides a process’s address space into logical segments (e.g., code, data, stack), each with a base address and length. It supports modular programming but may cause external fragmentation.

**Q34: Explain virtual memory and its benefits.**  
**A:** Virtual memory allows processes to use more memory than physically available by using disk storage (swap space). Benefits:  
- Runs large processes on limited RAM.  
- Enables multitasking and memory protection.  
- Simplifies memory management via demand paging.

---

### 8. File and I/O Management

**Q35: Describe the directory structure in file management.**  
**A:** Directory structures organize files hierarchically:  
- **Single-Level**: All files in one directory.  
- **Two-Level**: User-specific directories under a root.  
- **Tree-Structured**: Hierarchical directories with subdirectories.  
- **Acyclic Graph**: Allows file sharing via links.

**Q36: List common file operations.**  
**A:** Create, delete, read, write, append, rename, and open/close files.

**Q37: Explain file allocation methods.**  
**A:**  
- **Contiguous Allocation**: Files occupy consecutive blocks (fast access, external fragmentation).  
- **Linked Allocation**: Files use linked lists of blocks (no fragmentation, slow access).  
- **Indexed Allocation**: Files use an index block to store block pointers (supports large files, overhead for small files).

**Q38: What is disk management in the context of I/O?**  
**A:** Disk management involves:  
- **Formatting**: Preparing disks for use.  
- **Partitioning**: Dividing disks into logical units.  
- **Scheduling**: Optimizing disk access (e.g., FCFS, SSTF, SCAN).  
- **Error Handling**: Managing bad sectors and ensuring data integrity.

---

### Sample Problem-Solving Questions

**Q39: Given processes P1 (burst: 6, arrival: 0), P2 (4, 1), P3 (8, 2) in SJF scheduling, calculate the average waiting time.**  
**A:**  
- Non-preemptive SJF: P1 (0-6), P2 (6-10), P3 (10-18).  
- Waiting times: P1 = 0, P2 = 5, P3 = 8.  
- Avg. waiting time = (0 + 5 + 8) / 3 = 4.33.

**Q40: For a system with resources R1 (2 instances) and R2 (1 instance), and processes P1 (needs 1 R1, 1 R2) and P2 (needs 1 R1), apply the Banker’s Algorithm to check if allocating R1 to P2 is safe.**  
**A:**  
- **Available**: R1 = 1, R2 = 0 (after allocating R1 to P2).  
- **Need**: P1 (1 R1, 1 R2), P2 (0 R1, 0 R2).  
- No safe sequence exists (P1 cannot finish due to unavailable R2). Allocation is unsafe.
