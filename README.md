##OSSA MID - EXAM

1.  **Question:** Consider the following C program: `for(i=0; i<N; i++) { pid=fork(); }`. For N=5, How many child processes are created when the program is executed?
    *   **Options:** a. 31, b. 32, c. 16, d. 15, e. None of the above
    *   **Answer:** a. 31
    *   **Explanation:** Each `fork()` call creates a child process which also continues the loop from its current state. The number of *total* processes (parent + all children/descendants) becomes 2^N after N iterations. The number of *newly created child* processes is 2^N - 1. For N=5, this is 2^5 - 1 = 32 - 1 = 31.

---

2.  **Question:** In Unix, Which system call creates the new process?
    *   **Options:** a. fork, b. create, c. new, d. none of the mentioned
    *   **Answer:** a. fork
    *   **Explanation:** The `fork()` system call is the standard mechanism in Unix-like operating systems to create a new process, which is a near-duplicate of the calling (parent) process.

---

3.  **Question:** How many processes are created from the following C program?
    ```c
    #include <stdio.h>
    #include <unistd.h> // Added for fork/pid_t
    int main() {
        for(int i=0; i<10; i++) {
            int pid = fork();
            if(pid == 0) { // Child process
                printf("child\n");
                return 0; // Child exits immediately
            } else { // Parent process
                printf("parent\n");
                // Parent continues loop
            }
        }
        return 0;
    }
    ```
    *(Note: Image showed handwritten "1024" but code structure dictates otherwise)*
    *   **Answer:** 10 child processes are created (plus the original parent). Total processes involved over time: 11. Total running simultaneously diminishes as children exit.
    *   **Explanation:** The parent process loops 10 times. In each iteration, it creates one child process using `fork()`. Crucially, the child process immediately executes `return 0;` and exits. It does *not* continue the loop. Therefore, only the original parent process completes all 10 iterations, creating exactly 10 child processes. The handwritten "1024" (2^10) would apply if the child processes *also* continued to loop and fork, which they don't due to the `return 0;` in the `if(pid == 0)` block.

---

4.  **Question:** Consider the following statements and select the most appropriate answer:
    A) Synchronization is sharing system resources in a way that concurrent processes share a common memory space.
    B) The synchronization problem arise in processes.
    *   **Options:** a. Both statements are true, b. Statement B is true, c. Both statements are not true, d. Statement A is true
    *   **Answer:** a. Both statements are true
    *   **Explanation:** Statement B is fundamentally true; concurrency issues (requiring synchronization) arise when multiple processes access shared resources. Statement A is a slightly simplified but generally correct description; synchronization mechanisms are used to manage access to shared resources, and shared memory is a primary context where this is needed.

---

5.  **Question:** A process can be terminated due to:
    *   **Options:** a. Normal exit, b. Fatal error, c. Killed by another process, d. All of the above
    *   **Answer:** d. All of the above
    *   **Explanation:** A process can end its execution normally when finished, terminate abnormally due to an unrecoverable error, or be explicitly terminated by another process (usually with appropriate permissions) or the operating system.

---

6.  **Question:** What is interprocess communication?
    *   **Options:** a. communication within the process, b. communication between two process, c. communication between two threads of same process, d. none of the mentioned
    *   **Answer:** b. communication between two process
    *   **Explanation:** Interprocess Communication (IPC) refers specifically to the mechanisms that allow separate, distinct processes to exchange data and coordinate their activities. Communication within a single process (e.g., between its threads) uses different, often simpler, methods.

---

7.  **Question:** Choose the correct statement.
    *   **Options:** a. Program is a process in execution, b. Stack of a given process contains the global variables, c. Program Code of a process is also known as the Data Section, d. Program becomes a process when executable file is loaded into main memory
    *   **Answer:** d. Program becomes a process when executable file is loaded into main memory.
    *   **Explanation:** A program is a static set of instructions (an executable file). A process is a dynamic instance of a program being executed. This transition occurs when the OS loads the program code and data into memory and allocates necessary resources (like a Process Control Block). Option A reverses the definition. Option B is incorrect; the stack holds local variables and function call information. Option C is incorrect; program code resides in the text/code section, while the data section holds global/static variables.

---

8.  **Question:** Which one of the following error will be handled by the operating system?
    *   **Options:** a. lack of paper in printer, b. connection failure in the network, c. inefficient use of resouces, d. all of the above
    *   **Answer:** d. all of the above
    *   **Explanation:** The OS manages hardware devices and must handle errors reported by them (like printer status). It manages network interfaces and handles network stack errors. While it doesn't directly fix "inefficient use," it manages resource allocation and must handle consequences like resource exhaustion, often triggered by inefficient use.

---

9.  **Question:** Instead of starting a new thread for each task to execute concurrently, the task can be passed to ______.
    *   **Options:** a. a process, b. a thread pool, c. a thread queue, d. None of these
    *   **Answer:** b. a thread pool
    *   **Explanation:** A thread pool is a common concurrency pattern where a fixed number of worker threads are created upfront. Tasks are submitted to a queue, and these existing threads pick up tasks from the queue, avoiding the overhead of creating and destroying a thread for every single task.

---

10. **Question:** An un-interruptible unit is known as:
    *   **Options:** a. Single, b. Atomic, c. Static, d. None of these
    *   **Answer:** b. Atomic
    *   **Explanation:** In computing, an atomic operation is one that appears to the rest of the system to occur instantaneously. It cannot be interrupted part-way through; it either completes fully or doesn't happen at all, ensuring consistency in concurrent environments.

---

11. **Question:** Select the correct number of processes created by the following code:
    ```c
    #include <stdio.h>
    #include <unistd.h> // Added for fork
    int main() {
        fork();
        fork();
        fork();
        fork();
        printf("hello\n");
        return 0;
    }
    ```
    *   **Options:** a. 5 child processes, b. 4 child processes and 1 parent process, c. 15 child processes and 1 parent process, d. 16 child processes
    *   **Answer:** c. 15 child processes and 1 parent process
    *   **Explanation:** Each `fork()` doubles the number of active processes.
    *   Start: 1 process (original parent)
    *   After 1st fork: 2 processes
    *   After 2nd fork: 4 processes
    *   After 3rd fork: 8 processes
    *   After 4th fork: 16 processes
    *   These 16 processes consist of the original parent process and 15 child/descendant processes created through the series of forks. All 16 will eventually execute the `printf`.

---

12. **Question:** What is the purpose of the dual-mode operation?
    *   **Options:** a. Set an interrupt after specific period, b. A system call changes mode to kernel, return from call resets it to user, c. Provides ability to distinguish system is running user code or kernel code, d. Allows OS to protect itself and other system components.
    *   **Answer:** d. Allows OS to protect itself and other system components. (Option c is also related and describes the mechanism).
    *   **Explanation:** Dual-mode operation (User Mode and Kernel Mode) is a fundamental protection mechanism. Privileged instructions (like modifying hardware registers, managing memory, disabling interrupts) can only be executed in Kernel Mode. User applications run in User Mode with restricted privileges. This prevents user programs from interfering with the OS or other processes, thus protecting the system's integrity and stability. Option (c) describes *how* it works, but (d) describes the *purpose*.

---

13. **Question:** Storage systems organized in a hierarchy are, Select one:
    *   **Options:** a. Registers, Speed, Cost, b. Cost, Volatility, Caching, c. Caching, I/O handling, Speed, d. Speed, Cost, Volatility
    *   **Answer:** d. Speed, Cost, Volatility
    *   **Explanation:** The memory hierarchy (registers, cache, main memory, secondary storage) is characterized by trade-offs across these key attributes. Higher levels (like registers) are faster, more expensive per bit, and typically volatile (lose data when power is off). Lower levels (like disk) are slower, cheaper per bit, and non-volatile.

---

14. **Question:** RPC provides a(an) ______ on the client side, a separate one for each remote procedure.
    *   **Options:** a. identifier, b. process identifier, c. name, d. stub
    *   **Answer:** d. stub
    *   **Explanation:** In Remote Procedure Call (RPC), the client-side stub acts as a local representative (proxy) for the remote procedure. It packages (marshals) the arguments, sends the request over the network, receives the response, and unpacks (unmarshals) the results, making the remote call appear like a local one to the client program.

---

15. **Question:** For real time operating systems, interrupt latency should be:
    *   **Options:** a. minimal, b. zero, c. dependent on the scheduling, d. maximum
    *   **Answer:** a. minimal
    *   **Explanation:** Interrupt latency is the time between an interrupt occurring and the system starting to execute the corresponding interrupt service routine. In real-time systems, which must respond to events within strict deadlines, minimizing this latency is critical for predictability and responsiveness. Zero latency is practically impossible.

---

16. **Question:** Consider the following C program and select the correct output:
    ```c
    #include <stdio.h>
    #include <unistd.h> // Added for fork/pid_t
    int main() {
        int value = 120;
        int pid;
        pid = fork();
        if (pid == 0) { // Child
            value += 20;
            printf("Child: value = %d\n", value);
        } else { // Parent
            value -= 20;
            printf("Parent: value = %d\n", value);
        }
        return 0;
    }
    ```
    *   **Options:** a. Child: value = 140 Parent: value = 120, b. Child: value = 140 Parent: value = 100, c. Child: value = 120 Parent: value = 100, d. The answer cannot be obtained...
    *   **Answer:** b. Child: value = 140 Parent: value = 100
    *   **Explanation:** When `fork()` is called, the child process gets a *copy* of the parent's address space, including the variable `value`.
    *   The child process executes the `if(pid==0)` block, changing its copy of `value` to 120 + 20 = 140.
    *   The parent process executes the `else` block, changing its *own separate* copy of `value` to 120 - 20 = 100.

---

17. **Question:** In a computer system structure, what links the User Interface and OS Services?
    *   **Options:** a. I/O operations, b. System calls, c. Interrupt Service Routines (ISRs), d. Communication policies
    *   **Answer:** b. System calls
    *   **Explanation:** User applications (including user interfaces like shells or graphical environments) cannot directly access hardware or core OS functions. They request these services (like file access, process creation, network communication) from the OS kernel through a well-defined interface known as the system call interface.

---

18. **Question:** Given processes A(Arrival=0, Burst=8), B(1, 5), C(5, 2), D(7, 3). Use round-robin (quantum=3ms), context switch=0.2ms. Compute average waiting time.
    *   **Options:** a. 5.51ms, b. 5.15ms, c. 20.6ms, d. 9.0ms, e. 4.8ms
    *   **Calculated Answer:** 7.65 ms
    *   **Explanation:**
        *   A runs (0-3), remaining 5. Queue: B. CS (3-3.2)
        *   B runs (3.2-6.2), remaining 2. Queue: A, C. CS (6.2-6.4)
        *   A runs (6.4-9.4), remaining 2. Queue: C, D, B. CS (9.4-9.6)
        *   C runs (9.6-11.6), done. Queue: D, B, A. CS (11.6-11.8)
        *   D runs (11.8-14.8), done. Queue: B, A. CS (14.8-15)
        *   B runs (15-17), done. Queue: A. CS (17-17.2)
        *   A runs (17.2-19.2), done. Queue: Empty.
        *   Wait A = (6.4-3) + (17.2-9.4) - 1 = 3.4 + 7.8 - 1 = 10.2 (Start times 0, 6.4, 17.2. First burst doesn't wait. Second wait = 6.4-3 = 3.4. Third wait = 17.2-9.4=7.8. Total 11.2) Wait A = (6.4-0) + (17.2-9.4) - 8 = 6.4 + 7.8 - 8 = 6.2? Let's use Wait = Turnaround - Burst. CT_A=19.2, CT_B=17, CT_C=11.6, CT_D=14.8. TT_A=19.2, TT_B=16, TT_C=6.6, TT_D=7.8. Wait A=19.2-8=11.2, Wait B=16-5=11, Wait C=6.6-2=4.6, Wait D=7.8-3=4.8. Avg Wait = (11.2+11+4.6+4.8)/4 = 31.6/4 = 7.9ms.
        *   *Re-calculating carefully:*
        *   0.0: A arrives (Q: A)
        *   0.0: A runs [3] -> A(5) (Q: )
        *   1.0: B arrives (Q: B)
        *   3.0: A preempted (Q: B, A) CS(0.2)
        *   3.2: B runs [3] -> B(2) (Q: A)
        *   5.0: C arrives (Q: A, C)
        *   6.2: B preempted (Q: A, C, B) CS(0.2)
        *   6.4: A runs [3] -> A(2) (Q: C, B)
        *   7.0: D arrives (Q: C, B, D)
        *   9.4: A preempted (Q: C, B, D, A) CS(0.2)
        *   9.6: C runs [2] -> C(0) (Q: B, D, A) FINISH C @ 11.6
        *   11.6: CS(0.2)
        *   11.8: B runs [2] -> B(0) (Q: D, A) FINISH B @ 13.8
        *   13.8: CS(0.2)
        *   14.0: D runs [3] -> D(0) (Q: A) FINISH D @ 17.0
        *   17.0: CS(0.2)
        *   17.2: A runs [2] -> A(0) (Q: ) FINISH A @ 19.2
        *   CT: A=19.2, B=13.8, C=11.6, D=17.0
        *   TT: A=19.2-0=19.2, B=13.8-1=12.8, C=11.6-5=6.6, D=17.0-7=10.0
        *   WT: A=19.2-8=11.2, B=12.8-5=7.8, C=6.6-2=4.6, D=10.0-3=7.0
        *   Avg WT = (11.2 + 7.8 + 4.6 + 7.0) / 4 = 30.6 / 4 = 7.65 ms.
    *   **Note:** None of the provided options match the calculated average waiting time of 7.65 ms.

---

19. **Question:** The most optimal scheduling algorithm is:
    *   **Options:** a. FCFS - First come First served, b. SJF - Shortest Job First, c. RR - Round Robin, d. None of these
    *   **Answer:** b. SJF - Shortest Job First
    *   **Explanation:** Shortest Job First (SJF) scheduling (specifically, its preemptive version, Shortest Remaining Time First - SRTF) is proven to be optimal in terms of minimizing the average waiting time for a given set of processes. Its drawback is the need to know future CPU burst times.

---

20. **Question:** What is the function of the long-term scheduler?
    *   **Options:** a. It selects which process has to be brought into the ready queue, b. It selects which process has to be executed next and allocates CPU, c. It selects which process to remove from memory by swapping, d. None of these
    *   **Answer:** a. It selects which process has to be brought into the ready queue
    *   **Explanation:** The long-term scheduler (or job scheduler) selects processes from a job pool (on disk) and loads them into main memory to join the ready queue. It controls the degree of multiprogramming. Option (b) describes the short-term (CPU) scheduler, and (c) describes the medium-term scheduler (related to swapping).

---

21. **Question:** Attributes of a thread are...
    *   **Options:** a. Program Counter (PC), ID, Stack, CPU Registers, b. Program Counter (PC), Heap, Stack, CPU Registers, c. Program Counter (PC), ID, Stack, Text Section, d. Program Counter (PC), ID, Stack, Data Section
    *   **Answer:** a. Program Counter (PC), ID, Stack, CPU Registers
    *   **Explanation:** Each thread within a process needs its own execution context. This includes a program counter (to track its instruction pointer), a set of CPU registers, a stack (for local variables and function calls), and a unique thread ID. Threads within the same process share the code (text) section, data section, and heap.

---

22. **Question:** Given processes A(Arrival=0, Burst=7), B(2, 4), C(4, 1), D(5, 5). Apply round-robin (quantum = 3 milliseconds) scheduling considering the context switching time as 0.1 milliseconds. Compute the average waiting time.
    *   **Options:** a. 35.1 ms, b. 35.21ms, c. 8.67ms, d. 8.77ms, e. 7.775
    *   **Calculated Answer:** 7.425 ms
    *   **Explanation:**
        *   0.0: A arrives (Q: A)
        *   0.0: A runs [3] -> A(4) (Q: )
        *   2.0: B arrives (Q: B)
        *   3.0: A preempted (Q: B, A) CS(0.1)
        *   3.1: B runs [3] -> B(1) (Q: A)
        *   4.0: C arrives (Q: A, C)
        *   5.0: D arrives (Q: A, C, D)
        *   6.1: B preempted (Q: A, C, D, B) CS(0.1)
        *   6.2: A runs [3] -> A(1) (Q: C, D, B)
        *   9.2: A preempted (Q: C, D, B, A) CS(0.1)
        *   9.3: C runs [1] -> C(0) (Q: D, B, A) FINISH C @ 10.3
        *   10.3: CS(0.1)
        *   10.4: D runs [3] -> D(2) (Q: B, A)
        *   13.4: D preempted (Q: B, A, D) CS(0.1)
        *   13.5: B runs [1] -> B(0) (Q: A, D) FINISH B @ 14.5
        *   14.5: CS(0.1)
        *   14.6: A runs [1] -> A(0) (Q: D) FINISH A @ 15.6
        *   15.6: CS(0.1)
        *   15.7: D runs [2] -> D(0) (Q: ) FINISH D @ 17.7
        *   CT: A=15.6, B=14.5, C=10.3, D=17.7
        *   TT: A=15.6-0=15.6, B=14.5-2=12.5, C=10.3-4=6.3, D=17.7-5=12.7
        *   WT: A=15.6-7=8.6, B=12.5-4=8.5, C=6.3-1=5.3, D=12.7-5=7.7
        *   Avg WT = (8.6 + 8.5 + 5.3 + 7.7) / 4 = 30.1 / 4 = 7.525 ms.
        *   *Recalculating... Wait Times: A starts at 0, runs 0-3. Resumes 6.2. Wait = (6.2-3)=3.2. Resumes 14.6. Wait = (14.6-9.2)=5.4. Total A wait = 3.2+5.4 = 8.6. B starts 3.1. Wait=(3.1-2)=1.1. Resumes 13.5. Wait=(13.5-6.1)=7.4. Total B wait = 1.1+7.4 = 8.5. C starts 9.3. Wait=(9.3-4)=5.3. Total C wait=5.3. D starts 10.4. Wait=(10.4-5)=5.4. Resumes 15.7. Wait=(15.7-13.4)=2.3. Total D wait=5.4+2.3=7.7. Avg WT = (8.6 + 8.5 + 5.3 + 7.7) / 4 = 30.1 / 4 = 7.525 ms.*
    *   **Note:** Closest option is e. 7.775, but the calculated result is 7.525 ms. There might be a slight variation in handling context switch time or preemption timing, but 7.775 is the most plausible intended answer among the choices.

---

23. **Question:** Which one of the following cannot be scheduled by the kernel?
    *   **Options:** a. Kernel level thread, b. User level thread, c. Process, d. None of the mentioned
    *   **Answer:** b. User level thread
    *   **Explanation:** The OS kernel schedules entities it is aware of and manages, which include processes and kernel-level threads. User-level threads are managed entirely within a user process by a thread library; the kernel is typically unaware of their existence and cannot schedule them individually. It schedules the process that contains them.

---

24. **Question:** In priority scheduling algorithm, when a process arrives at the ready queue, its priority is compared with the priority of:
    *   **Options:** a. All processes, b. Currently running process, c. Init process, d. Parent process
    *   **Answer:** b. Currently running process
    *   **Explanation:** In *preemptive* priority scheduling (the common interpretation unless stated otherwise), when a new process arrives, its priority is compared to the process currently executing on the CPU. If the new process has higher priority, the currently running process is preempted, and the new process is scheduled. In non-preemptive priority, comparison happens only when the CPU becomes free.

---

25. **Question:** Which of the following system call transforms executable binary file into a process?
    *   **Options:** a. system(), b. getpid(), c. fork(), d. exec()
    *   **Answer:** d. exec()
    *   **Explanation:** The `exec()` family of system calls replaces the current process's image (code, data, stack, heap) with a new one loaded from the specified executable binary file. This is how a program is typically run after being created via `fork()`. `fork()` creates a copy, `exec()` transforms it.

---

26. **Question:** Select the most appropriate answer by considering the following C program:
    ```c
    #include <stdio.h>
    #include <unistd.h>
    int main() {
        int pid = fork();
        if (pid == 0) { // Child
            printf("Hello\n");
        } else { // Parent
            sleep(100); // Parent sleeps for a long time
        }
        return 0; // Both exit
    }
    ```
    *   **Options:** a. A never ending loop, b. None of the above, c. A zombie process, d. An orphan process
    *   **Answer:** c. A zombie process
    *   **Explanation:** The child process prints "Hello" and then exits almost immediately by executing `return 0;`. The parent process, however, enters a long `sleep(100)`. Since the parent hasn't waited for the child (using `wait()` or `waitpid()`), the exited child process enters the zombie state. Its process table entry remains until the parent eventually wakes up and reaps it (or the parent exits itself). It's not an orphan because the parent is still alive, just sleeping.

---

27. **Question:** Choose the correct statement.
    *   **Options:** a. Ready Queue contains all the processes in the system which are newly created, b. Long-term scheduler selects which process should be sent out from the ready queue to the CPU, c. Short-term scheduler is invoked very frequently, d. CPU-bound process spends more time doing computations; therefore it's having many CPU bursts
    *   **Answer:** c. Short-term scheduler is invoked very frequently
    *   **Explanation:** The short-term (CPU) scheduler selects the next process to run on the CPU from the ready queue. This decision happens frequently (e.g., on time slice expiration, I/O completion, system calls), typically on the order of milliseconds. Option A is wrong (Ready Queue holds processes ready to run, not just new). Option B describes the short-term scheduler, not long-term. Option D is incorrect; CPU-bound processes have *few*, *long* CPU bursts.

---

28. **Question:** If all processes are I/O bound, the ready queue will almost always be ______ and the Short term Scheduler will have a ______ to do.
    *   **Options:** a. empty, little, b. empty, lot, c. full, little, d. full, lot
    *   **Answer:** a. empty, little
    *   **Explanation:** I/O-bound processes use the CPU for very short bursts and then block waiting for I/O. Consequently, they spend most of their time in the waiting state, not the ready queue. This leaves the ready queue mostly empty, and the short-term (CPU) scheduler has fewer processes to choose from, hence less work ("little to do").

---

29. **Question:** Given processes A(Arrival=0, Burst=8), B(1, 5), C(5, 2), D(8, 1). Compute average waiting time for round-robin (quantum=3) scheduling. (Assume context switch time = 0 if not specified).
    *   **Options:** a. 8 seconds, b. 4 seconds, c. 6 seconds, d. 24 seconds, e. None of the above
    *   **Calculated Answer:** 6.0 seconds/ms
    *   **Explanation:**
        *   0: A runs [3] -> A(5) (Q: B)
        *   3: B runs [3] -> B(2) (Q: A)
        *   5: C arrives (Q: A, C)
        *   6: A runs [3] -> A(2) (Q: C, B)
        *   8: D arrives (Q: C, B, D)
        *   9: C runs [2] -> C(0) (Q: B, D, A) FINISH C @ 11
        *   11: B runs [2] -> B(0) (Q: D, A) FINISH B @ 13
        *   13: D runs [1] -> D(0) (Q: A) FINISH D @ 14
        *   14: A runs [2] -> A(0) (Q: ) FINISH A @ 16
        *   CT: A=16, B=13, C=11, D=14
        *   TT: A=16, B=12, C=6, D=6
        *   WT: A=16-8=8, B=12-5=7, C=6-2=4, D=6-1=5
        *   Avg WT = (8+7+4+5)/4 = 24/4 = 6.0
    *   **Note:** Option 'c' matches the calculated result.

---

30. **Question:** Switching the CPU to another Process requires to save state of the old process and loading new process state is called as:
    *   **Options:** a. Process Blocking, b. Context Switch, c. Time Sharing, d. Process loading, e. None of the above
    *   **Answer:** b. Context Switch
    *   **Explanation:** This is the definition of a context switch. The OS saves the execution context (registers, PC, etc.) of the currently running process and restores the context of the next process scheduled to run.

---

31. **Question:** Select the most correct average turnaround time for preemptive shortest job first scheduling. Processes: A(Arrival=1, Burst=7), B(3, 3), C(6, 2), D(7, 5).
    *   **Options:** a. 5.75 seconds, b. 5.25 seconds, c. 5.5 seconds, d. 5 seconds
    *   **Calculated Answer:** 7.0 seconds/ms
    *   **Explanation:** Preemptive SJF (Shortest Remaining Time First - SRTF):
        *   0: Idle
        *   1: A arrives, runs A(7)
        *   3: B arrives (BT=3), A remaining=5. B has shorter burst. Preempt A. Run B. A(5) B(3)
        *   6: B finishes. CT_B=6. C arrives (BT=2). Compare A(5) and C(2). Run C. A(5) C(2)
        *   7: D arrives (BT=5). C remaining=1. Run C. A(5) C(2) D(5)
        *   8: C finishes. CT_C=8. Compare A(5) and D(5). Tie-break (FCFS). Run A. A(5) D(5)
        *   13: A finishes. CT_A=13. Run D. D(5)
        *   18: D finishes. CT_D=18.
        *   CT: A=13, B=6, C=8, D=18
        *   TT: A=13-1=12, B=6-3=3, C=8-6=2, D=18-7=11
        *   Avg TT = (12 + 3 + 2 + 11) / 4 = 28 / 4 = 7.0
    *   **Note:** None of the provided options match the calculated average turnaround time of 7.0.

---

32. **Question:** Consider the following set of processes with their arrival time, priority, and burst time. If the preemptive priority scheduling algorithm (smaller integer has higher priority) is used, compute the average waiting time. Processes: A(Arrival=0, Priority=3, Burst=6), B(2, 2, 4), C(5, 2, 2), D(7, 1, 4).
    *   **Options:** a. 3 seconds, b. 3.75 seconds, c. 4 seconds, d. 4.45 seconds, e. None of the above
    *   **Answer:** b. 3.75 seconds
    *   **Explanation:** Preemptive Priority (lower number = higher priority):
        *   0: A arrives (P=3), runs A(6)
        *   2: B arrives (P=2). B has higher priority. Preempt A. Run B. A remaining=4. B(4)
        *   5: C arrives (P=2). B running (P=2). Tie-break (FCFS). B continues. A(4) B(4) C(2)
        *   6: B finishes. CT_B=6. Compare A(P=3) and C(P=2). Run C. A(4) C(2)
        *   7: D arrives (P=1). D has highest priority. Preempt C. Run D. A(4) C remaining=1. D(4)
        *   11: D finishes. CT_D=11. Compare A(P=3) and C(P=2). Run C. A(4) C(1)
        *   12: C finishes. CT_C=12. Run A. A(4)
        *   16: A finishes. CT_A=16.
        *   CT: A=16, B=6, C=12, D=11
        *   TT: A=16-0=16, B=6-2=4, C=12-5=7, D=11-7=4
        *   WT: A=16-6=10, B=4-4=0, C=7-2=5, D=4-4=0
        *   Avg WT = (10 + 0 + 5 + 0) / 4 = 15 / 4 = 3.75

---

33. **Question:** In a computer system, assume that ten processes arrive every minute, and there are normally 8 processes in the queue. Compute the average waiting time per process by Little's formula.
    *   **Options:** a. 8 seconds, b. 0.8 seconds, c. 4.8 seconds, d. 48 seconds, e. None of the above
    *   **Answer:** d. 48 seconds
    *   **Explanation:** Little's Law states L = λ * W, where L is the average number of items in the system/queue, λ is the average arrival rate, and W is the average time spent in the system/queue.
    *   Here, L = 8 processes (in the queue).
    *   λ = 10 processes per minute.
    *   We want W (average waiting time).
    *   W = L / λ = 8 processes / (10 processes/minute) = 0.8 minutes.
    *   Convert to seconds: 0.8 minutes * 60 seconds/minute = 48 seconds.

---

34. **Question:** Why does the system select a new process to run?
    a) When process switches from running to waiting state.
    b) Switches from running to ready state.
    c) Switches from waiting to ready state.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only a) and b) are correct, d. All are correct, e. None of the above
    *   **Answer:** c. Only a) and b) are correct.
    *   **Explanation:** The CPU scheduler *must* select a new process (or re-select the same one if it's the only one ready) whenever the currently running process leaves the CPU. This happens when the process blocks for I/O (running -> waiting, case a) or when it is preempted, for example, by a timer interrupt or a higher-priority process arriving (running -> ready, case b). When a process moves from waiting to ready (case c), it becomes eligible to run, but this doesn't necessarily force an immediate rescheduling unless the CPU is idle or the newly ready process causes preemption.

---

35. **Question:** What is the ready state of a process?
    *   **Options:** a. When process is scheduled to run after some execution, b. When process is unable to run until some task has been completed, c. When process is using the CPU, d. When process is ready to execute an IO operation, e. None of the above
    *   **Answer:** a. When process is scheduled to run after some execution (This option is poorly worded, but implies waiting for CPU).
    *   **Explanation:** The Ready state signifies that a process has all the resources it needs to run *except* the CPU. It is loaded in main memory and is waiting for the CPU scheduler to allocate the CPU to it. Option (b) describes the Waiting/Blocked state. Option (c) describes the Running state. Option (d) usually precedes entering the Waiting state.

---

36. **Question:** When the currently running process is suspended & a new process will be selected to run by the scheduler, then the currently running process must be saved in its PCB and restore the status from the PCB this process is called as:
    *   **Options:** a. Interrupting, b. Preempting, c. Scheduling, d. Context switching, e. Dispatching
    *   **Answer:** d. Context switching
    *   **Explanation:** The process described – saving the state (context) of one process and loading the state of another – is the definition of a context switch. Scheduling is the decision-making process, dispatching is the act of giving control to the selected process, interrupting/preempting are events that might trigger scheduling/context switching.

---

37. **Question:** Consider the following statements regarding the processes and threads:
    a) Processes creation is faster than thread creation.
    b) Inter thread communication is much faster than the inter process communication.
    c) User level threads are slower than the kernel level threads.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only b) and c) are correct, d. All are correct, e. None of the above
    *   **Answer:** b. Only b) is correct
    *   **Explanation:** (a) Thread creation is significantly lighter-weight and faster than process creation because it doesn't involve duplicating the entire address space. (b) Threads within the same process share memory, allowing very fast communication through shared variables. IPC typically involves kernel mediation (system calls, copying data), which is slower. (c) User-level thread context switches can be faster than kernel-level ones (no mode switch), but if one user-level thread blocks on a system call, the entire process might block (depending on kernel support). The performance comparison isn't universally "slower". Statement (b) is the most consistently true advantage.

---

38. **Question:** Calculate the average waiting time for Shortest Job First (non preemptive) algorithm. Processes: A(Arrival=0, Burst=6), B(1, 4), C(3, 5), D(5, 2), E(6, 4).
    *   **Options:** a. 6.4, b. 6.6, c. 5.0, d. 6.0, e. 5.2
    *   **Calculated Answer:** 5.4
    *   **Explanation:** Non-preemptive SJF:
        *   0: A arrives. Runs A (BT=6).
        *   1: B arrives (BT=4). A is running.
        *   3: C arrives (BT=5). A is running.
        *   5: D arrives (BT=2). A is running.
        *   6: A finishes (CT_A=6). E arrives (BT=4). Ready queue: B(4), C(5), D(2), E(4). Shortest is D. Run D.
        *   8: D finishes (CT_D=8). Ready queue: B(4), C(5), E(4). Shortest are B and E. Tie-break (FCFS). Run B.
        *   12: B finishes (CT_B=12). Ready queue: C(5), E(4). Shortest is E. Run E.
        *   16: E finishes (CT_E=16). Ready queue: C(5). Run C.
        *   21: C finishes (CT_C=21).
        *   CT: A=6, B=12, C=21, D=8, E=16
        *   TT: A=6, B=11, C=18, D=3, E=10
        *   WT: A=6-6=0, B=11-4=7, C=18-5=13, D=3-2=1, E=10-4=6
        *   Avg WT = (0 + 7 + 13 + 1 + 6) / 5 = 27 / 5 = 5.4
    *   **Note:** Option 'e' 5.2 is the closest to the calculated 5.4.

---

39. **Question:** If the kernel is single threaded, then any user level thread performing a blocking system call will :
    *   **Options:** a. cause the entire process to run along with the other threads, b. cause the thread to block with the other threads running, c. cause the entire process to block even if the other threads are available to run, d. cause the main thread to block and others are running, e. None of these
    *   **Answer:** c. cause the entire process to block even if the other threads are available to run
    *   **Explanation:** If the kernel is unaware of user-level threads (sees the process as a single thread of execution), and one user-level thread makes a blocking system call (like reading from the keyboard), the kernel blocks the *entire process*. It has no knowledge that other user-level threads within that process might be ready to run.

---

40. **Question:** Consider the following C program: `int value = 60; ... pid = fork(); ... else { value -= 20; printf("PARENT : value= %d\n", value); /* Line A */ } ...`. Select one:
    *   **Options:** a. PARENT < 40, b. PARENT = 60, c. PARENT = 80, d. PARENT = 20, e. None of the above
    *   **Answer:** e. None of the above (Calculated PARENT value is 40)
    *   **Explanation:** The parent process executes the `else` block. Its independent copy of `value` (initially 60) is modified: `value = value - 20`, so `value` becomes 40. Line A will print "PARENT : value= 40". Since 40 is not explicitly listed as an option, "None of the above" is the correct choice based on the calculation.

---

41. **Question:** Consider the following statements regarding OS structures:
    a) Module architecture is used by most of the modern Operating systems.
    b) Micro kernel provides better reliability.
    c) Layered architecture is less efficient.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only a) and b) are correct, d. All are correct, e. None of the above
    *   **Answer:** d. All are correct
    *   **Explanation:** (a) Modern OS like Linux, Windows, macOS heavily use loadable kernel modules, providing flexibility. (b) A key design goal of microkernels is improved reliability by moving services outside the kernel, so a failing service doesn't crash the whole OS. (c) Strictly layered architectures often incur performance overhead due to the need for requests to pass through multiple layers, making them potentially less efficient than more monolithic or modular designs for certain operations. All three statements represent generally accepted concepts in OS design.

---

42. **Question:** Which of the following are library function(s)?
    *   **Options:** a. waitpid(), b. fork(), c. read(), d. exec(), e. None of the above
    *   **Answer:** e. None of the above (in the sense they primarily wrap system calls)
    *   **Explanation:** While `waitpid()`, `fork()`, `read()`, and `exec()` are functions callable from C programs and are part of standard libraries (like libc), their core functionality is implemented via underlying operating system *system calls*. They act as wrappers or interfaces to these kernel services. If the question implies functions *without* a direct, essential system call counterpart, then none fit. If it simply means "part of a standard library", they all are, but that's usually not the distinction intended in OS courses.

---

43. **Question:** Calculate the average turnaround time for the Round robin algorithm with quantum=4ms. Processes: A(Arrival=0, Burst=7), B(1, 4), C(2, 1), D(4, 4). (Assume CS=0).
    *   **Options:** a. 18.20, b. 18.45, c. 18.35, d. 18.00, e. 18.25
    *   **Calculated Answer:** 9.5 ms
    *   **Explanation:**
        *   0: A runs [4] -> A(3) (Q: B, C)
        *   4: B runs [4] -> B(0) (Q: C, D, A) FINISH B @ 8
        *   8: C runs [1] -> C(0) (Q: D, A) FINISH C @ 9
        *   9: D runs [4] -> D(0) (Q: A) FINISH D @ 13
        *   13: A runs [3] -> A(0) (Q: ) FINISH A @ 16
        *   CT: A=16, B=8, C=9, D=13
        *   TT: A=16-0=16, B=8-1=7, C=9-2=7, D=13-4=9
        *   Avg TT = (16 + 7 + 7 + 9) / 4 = 39 / 4 = 9.75 ms.
        *   *Recalculating carefully:*
        *   0: A arr. Run A[4] -> A(3). Q: B C
        *   4: A preempt. B arr. D arr. Run B[4] -> B(0). Q: C D A. FINISH B @ 8.
        *   8: B finishes. Run C[1] -> C(0). Q: D A. FINISH C @ 9.
        *   9: C finishes. Run D[4] -> D(0). Q: A. FINISH D @ 13.
        *   13: D finishes. Run A[3] -> A(0). Q: . FINISH A @ 16.
        *   CT: A=16, B=8, C=9, D=13.
        *   TT: A=16, B=7, C=7, D=9.
        *   Avg TT = (16+7+7+9)/4 = 39/4 = 9.75 ms.
    *   **Note:** None of the provided options (all around 18) match the calculated average turnaround time of 9.75 ms. There might be an error in the question data or the options.

---

44. **Question:** Which is not a service of the operating system?
    *   **Options:** a. File-system manipulation, b. Process communication, c. Resource allocation, d. Accounting of the resource usage, e. Virus detection
    *   **Answer:** e. Virus detection
    *   **Explanation:** File system management, Inter-Process Communication (IPC), allocating resources (CPU, memory, I/O devices), and keeping track of resource usage (accounting) are all core services provided by typical operating systems. Virus detection and removal are generally handled by separate utility programs or security software, although some OS might bundle basic versions.

---

45. **Question:** Which of the following are non-privileged instructions?
    *   **Options:** a. Setting the system time, b. Changing the base register value, c. Reading the system time, d. Erasing the memory content, e. Switch from kernel mode to user mode
    *   **Answer:** c. Reading the system time
    *   **Explanation:** Non-privileged instructions are those that can be executed safely in user mode without potentially harming the OS or other processes. Reading the system time is generally considered a safe, non-privileged operation. Setting the time (a), manipulating memory management registers (b), arbitrarily erasing memory (d), and explicitly controlling mode switches (e, although returning from kernel to user is normal) are typically privileged operations restricted to the kernel.

---

46. **Question:** A process which has just terminated but has yet to release its resources is called:
    *   **Options:** a. A suspended process, b. A zombie process, c. A blocked process, d. A terminated process, e. An orphan process
    *   **Answer:** b. A zombie process
    *   **Explanation:** When a process terminates, its execution stops, and most resources are released. However, its entry in the process table remains until the parent process reads its exit status using a `wait()` system call. This lingering, terminated-but-not-yet-reaped process is called a zombie. It consumes minimal resources (just the process table entry).

---

47. **Question:** Consider the following statements regarding sockets:
    A. Socket is a communication end point with IP address and port number.
    B. Each port number has 16 bits number.
    C. Port numbers below 1024 are already reserved for servers.
    D. Every client program needs a port number for the communication.
    Which of the following is correct:
    *   **Options:** a. Only A, is correct, b. Only B and C. are correct, c. Only A, and C. are correct, d. All are correct, e. None of the above
    *   **Answer:** d. All are correct
    *   **Explanation:** (A) Defines a socket endpoint. (B) Port numbers are indeed 16-bit unsigned integers (0-65535). (C) Ports 0-1023 are typically "well-known ports" reserved for standard system services/servers (requires privileges to bind). (D) While servers bind to well-known ports, client processes also need a port number (usually assigned dynamically by the OS from the ephemeral range) to establish their end of the communication link.

---

48. **Question:** Given the following set of processes with their arrival times and burst times: A(0, 8), B(1, 4), C(3, 5), D(5, 2), E(6, 4). Calculate the average waiting time for First Come First Serve algorithm.
    *   **Options:** a. 9.8, b. 7.8, c. 8.2, d. 8.6, e. 8.4
    *   **Answer:** c. 8.2
    *   **Explanation:** FCFS Execution Order: A -> B -> C -> D -> E
        *   A starts 0, finishes 8. Wait = 0.
        *   B starts 8, finishes 12. Wait = 8 - 1 = 7.
        *   C starts 12, finishes 17. Wait = 12 - 3 = 9.
        *   D starts 17, finishes 19. Wait = 17 - 5 = 12.
        *   E starts 19, finishes 23. Wait = 19 - 6 = 13.
        *   Avg WT = (0 + 7 + 9 + 12 + 13) / 5 = 41 / 5 = 8.2

---

49. **Question:** Given the following set of processes with their arrival times and burst times: A(0, 8), B(1, 4), C(3, 5), D(5, 2), E(6, 4). Calculate the average turnaround time for First Come First Serve algorithm.
    *   **Options:** a. 13.6, b. 13.2, c. 13.4, d. 13.0, e. 12.8
    *   **Answer:** e. 12.8
    *   **Explanation:** FCFS Execution Order: A -> B -> C -> D -> E
        *   A starts 0, finishes 8. TT = 8 - 0 = 8.
        *   B starts 8, finishes 12. TT = 12 - 1 = 11.
        *   C starts 12, finishes 17. TT = 17 - 3 = 14.
        *   D starts 17, finishes 19. TT = 19 - 5 = 14.
        *   E starts 19, finishes 23. TT = 23 - 6 = 17.
        *   Avg TT = (8 + 11 + 14 + 14 + 17) / 5 = 64 / 5 = 12.8

---

50. **Question:** The state of a process after it encounters an I/O instruction is,
    *   **Options:** a. Ready, b. Waiting, c. Idle, d. Run, e. New
    *   **Answer:** b. Waiting
    *   **Explanation:** When a running process initiates an I/O operation (e.g., reading from disk, waiting for network input), it cannot continue executing until the I/O completes. The OS moves the process from the Running state to the Waiting (or Blocked) state. Once the I/O finishes, the OS moves it back to the Ready state.

---

51. **Question:** Consider the following statements related to the Operating System:
    a) The main goal of SPOOLING is to maximize the utilization of IO devices and CPU.
    b) The main goal of the Multiprogramming is to maximize the CPU utilization.
    c) The main goal of the Time sharing system is to maximize the resource sharing.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only a) and c) are correct, d. All are correct, e. None of the above
    *   **Answer:** b. Only b) is correct
    *   **Explanation:** (a) SPOOLing (Simultaneous Peripheral Operations On-Line) helps overlap I/O of one job with computation of another, improving overall system utilization, but maximizing CPU/IO might not be its *sole* or *main* goal compared to decoupling slow I/O. (b) Maximizing CPU utilization by keeping the CPU busy with some process whenever possible is the primary goal of multiprogramming. (c) The primary goal of time-sharing systems is to provide good *response time* to multiple interactive users, which involves sharing resources, but maximizing sharing itself isn't the main objective compared to responsiveness.

---

52. **Question:** Consider the following statements regarding the processes scheduling:
    a) Short term scheduler is faster than the medium term scheduler.
    b) Context switching between kernel level threads are faster than the user level threads.
    c) Ready queue is implemented with first in first out policy.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only b) and c) are correct, d. All are correct, e. None of the above
    *   **Answer:** a. Only a) is correct
    *   **Explanation:** (a) The short-term scheduler runs very frequently (milliseconds) to select the next process for the CPU. The medium-term scheduler (involved in swapping) runs much less frequently. Therefore, the short-term scheduler operates "faster" in terms of invocation frequency. (b) Context switching between user-level threads within the same process is generally *faster* than switching between kernel-level threads because it doesn't require a trap to the kernel (mode switch). (c) The ready queue's policy depends entirely on the CPU scheduling algorithm being used; it can be FIFO (for FCFS), a priority queue, etc., not necessarily just FIFO.

---

53. **Question:** Consider the following statements regarding operating system:
    A. Most of the system calls are implemented using the assembly language and C language.
    B. Current operating systems are based on the modules concept.
    C. Modern operating systems are interrupt driven.
    D. Modern operating systems are Always real time.
    Which of the following is correct:
    *   **Options:** a) Only A, and B. are correct, b) Only A, B and C. are correct, c) Only A, and C. are correct, d) All are correct, e) None of the above
    *   **Answer:** b) Only A, B and C. are correct
    *   **Explanation:** (A) System calls and kernel code are typically written in C and performance-critical parts in Assembly. (B) Modularity (loadable modules) is a key feature of modern OS like Linux, Windows. (C) Operating systems fundamentally react to events, primarily signaled by interrupts (hardware, software, timer). (D) While Real-Time Operating Systems (RTOS) exist, general-purpose OS like Windows, Linux, macOS are *not* always real-time; they prioritize throughput or fairness over strict deadlines.

---

54. **Question:** Thread specific data is:
    *   **Options:** a. Not associated with any process, b. Has been modified by the thread but not yet updated to the parent process, c. Is generated by the thread independent of the threads process, d. Is copied and not shared with the other threads, e. None of the above
    *   **Answer:** d. Is copied and not shared with the other threads. (Referring to stack, registers, thread-local storage)
    *   **Explanation:** While threads share code, data, and heap within a process, each thread has its *own* private stack, its *own* set of CPU registers, and can have thread-local storage (TLS). This data constitutes the thread's unique execution context and is not directly shared or copied between threads (though they can communicate via shared heap/global data). Option (d) best captures the non-shared nature of a thread's core execution context relative to *other threads*.

---

55. **Question:** Which scheduler move the process from new state to ready state?
    *   **Options:** a. CPU scheduler, b. Long term scheduler, c. Short term scheduler, d. Medium term scheduler, e. None of the above
    *   **Answer:** b. Long term scheduler
    *   **Explanation:** The Long-Term Scheduler (or Job Scheduler) is responsible for selecting processes from the job pool (New state) and admitting them into the system by loading them into memory and placing them in the Ready state. It controls the degree of multiprogramming.

---

56. **Question:** Which is not a state of the process?
    *   **Options:** a. Blocked, b. New, c. Running, d. Ready, e. Privileged
    *   **Answer:** e. Privileged
    *   **Explanation:** New, Ready, Running, Waiting (Blocked), and Terminated are standard process states. Privileged (or Kernel) is an execution *mode* that the CPU operates in, not a state of the process itself. A process can be in the Running state while executing in either User Mode or Kernel Mode.

---

57. **Question:** Consider the following statements for interrupt handling:
    A. Run the interrupt service routine
    B. Save the current state in Process Control Block (PCB)
    C. Interrupt occurs
    D. Restore the state saved in PCB
    E. Consult the interrupt vector
    F. Locate the interrupt service routine
    Select the correct order for interrupt handling:
    *   **Options:** a. C, E, B, F, A, D, b. C, E, F, B, A, D, c. C, E, B, A, F, D, d. C, F, E, B, A, D, e. None of the above
    *   **Answer:** b. C, E, F, B, A, D
    *   **Explanation:** The typical sequence is:
        1.  (C) Interrupt occurs.
        2.  CPU finishes current instruction (usually).
        3.  (E) CPU uses the interrupt type/number to consult the interrupt vector table.
        4.  (F) The vector provides the starting address of the appropriate Interrupt Service Routine (ISR).
        5.  (B) Before jumping to the ISR, the CPU saves the current context (PC, registers, status) - often onto the kernel stack associated with the interrupted process (related to PCB).
        6.  (A) The CPU jumps to and executes the ISR.
        7.  (D) After the ISR finishes, the saved state is restored, allowing the interrupted process to resume.

---

58. **Question:** Consider the following statements related to the multiprocessing systems:
    a) Asymmetric multiprocessing system has the load unbalancing problem.
    b) Symmetric multiprocessing system has the access controlling problem with shared data.
    c) Processor affinity is the solution to the load unbalancing problem.
    *   **Options:** a. Only a) is correct, b. Only b) is correct, c. Only a) and b) are correct, d. All are correct, e. None of the above
    *   **Answer:** b. Only b) is correct
    *   **Explanation:** (a) Asymmetric multiprocessing (AMP) assigns specific tasks to specific processors; load balancing isn't its inherent design goal or problem in the same way as SMP. One processor (the master) might become a bottleneck. (b) Symmetric multiprocessing (SMP), where all processors are peers, requires careful synchronization mechanisms (locks, semaphores) to control access to shared data structures and prevent race conditions. This is a key challenge ("access controlling problem"). (c) Processor affinity (binding a process to a specific processor) is primarily used to improve cache performance by reducing cache invalidations. It can actually *hinder* load balancing because it prevents the scheduler from moving a process to an idle processor.
