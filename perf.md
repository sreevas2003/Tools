# perf

**What is perf?**

👉 perf tells you WHERE the CPU time is going.

- Which function
- Which line
- Which kernel or user code

is consuming CPU.

👉 perf = CPU microscope

**2️⃣ Why perf is VERY IMPORTANT**

Questions:

- Which process?
- Which function?
- User space or kernel?
- Why slow?

👉 Only perf answers this

**3️⃣ Where perf is used**

| Area           | Why                      |
| -------------- | ------------------------ |
| Linux servers  | High CPU debugging       |
| Embedded Linux | Boot time optimization   |
| Kernel dev     | Scheduler, drivers       |
| Performance    | Hotspot analysis         |
| Interviews     | Advanced Linux profiling |

4️⃣ How perf works (Simple idea)

- CPU generates samples
- Samples capture instruction pointer
- perf counts where CPU spends time
- Reports top functions

**Install & Check perf**
```
sudo apt install linux-tools-common linux-tools-generic
perf --version
```
**MOST BASIC command**
```
perf stat ls
```
**Output example:**
```
 Performance counter stats for 'ls':

  1,234,567 cycles
    456,789 instructions
         123 cache-misses
```
**Meaning (simple)**

| Term         | Meaning               |
| ------------ | --------------------- |
| cycles       | CPU clock cycles used |
| instructions | Instructions executed |
| cache-misses | Slow memory access    |

**Real CPU Profiling (MOST IMPORTANT)**
```
perf top
```
**What it shows**

<img width="531" height="140" alt="image" src="https://github.com/user-attachments/assets/f2abcd93-6f6d-405d-8a7f-ae1a3e766172" />

**Meaning:**

- process_data() → main CPU hog
- memcpy() → memory-heavy
- schedule() → kernel scheduling cost

👉 Now you know WHAT to optimize

**User vs Kernel CPU**

- Shared Object = vmlinux → kernel
- .so or app name → user space

**9️⃣ Record & Analyze (Professional Way)**

Step 1: Record
```
perf record ./myapp
```
Step 2: Report
```
perf report
```

You’ll see:
```
40%  process_data
20%  parse_packet
10%  memcpy
```

**🔟 Hands-on Lab (Do this)**

Create CPU load
```
// cpu_burn.c
#include <stdio.h>
int main() {
    while(1);
}
```

Compile:
```
gcc cpu_burn.c -o cpu_burn
```

Profile:
```
perf top ./cpu_burn
```
✔️ You’ll see main consuming CPU
👉 This is real profiling, not guessing.

**1️⃣1️⃣ perf stat (Compare performance)**
```
perf stat ./cpu_burn
```
Optimize code → run again → compare numbers.

Used in:

- Compiler optimization
- Algorithm comparison

**1️⃣2️⃣ perf record on running PID**
```
perf record -p <PID>
```
Example:
```
perf record -p 1234
perf report
```

**1️⃣3️⃣ perf for Kernel & Drivers**
```
perf top -k
```
Shows:

- Interrupt handlers
- Scheduling
- Kernel hotspots

**perf vs htop vs iotop**

| Tool  | Answers             |
| ----- | ------------------- |
| htop  | Who uses CPU        |
| iotop | Who uses disk       |
| perf  | Where CPU time goes |

**perf in Boot Time Optimization**
```
perf record -a sleep 10
perf report
```

Used to find:

- Slow drivers
- Init delays
- Kernel bottlenecks

========================================================
FILE NAME: perf_interview_questions.txt
TOPIC: Linux CPU Profiler - perf
LEVEL: Beginner to Advanced
========================================================

1. What is perf?

perf is a Linux performance analysis tool used to profile CPU usage and identify where execution time is spent at function and instruction level.

--------------------------------------------------------

2. Why is perf important in Linux performance debugging?

perf helps identify CPU hotspots, inefficient code paths, and kernel or user-space bottlenecks that cannot be seen using tools like top or htop.

--------------------------------------------------------

3. What kind of problems does perf solve?

High CPU usage, slow applications, kernel performance issues, scheduling overhead, and inefficient algorithms.

--------------------------------------------------------

4. How is perf different from htop?

htop shows which process uses CPU, while perf shows which functions and code paths consume CPU time.

--------------------------------------------------------

5. What is CPU profiling?

CPU profiling is the process of measuring where and how much CPU time is spent during program execution.

--------------------------------------------------------

6. Does perf require code modification?

No, perf works using hardware and software performance counters without modifying application code.

--------------------------------------------------------

7. What is perf stat used for?

perf stat provides overall performance statistics such as CPU cycles, instructions executed, cache misses, and context switches.

--------------------------------------------------------

8. Give an example of perf stat usage.

perf stat ./myapp

--------------------------------------------------------

9. What is perf top?

perf top shows real-time CPU usage at function level, similar to top but for code execution hotspots.

--------------------------------------------------------

10. What information does perf top display?

Function name, CPU overhead percentage, binary or library name, and whether execution is in user or kernel space.

--------------------------------------------------------

11. What is perf record?

perf record captures CPU execution samples over time and stores them for offline analysis.

--------------------------------------------------------

12. How do you analyze perf record data?

Using the command perf report.

--------------------------------------------------------

13. What is perf report?

perf report displays recorded profiling data in a readable format, showing CPU time spent per function.

--------------------------------------------------------

14. How do you profile a running process using perf?

Using perf record -p <PID>.

--------------------------------------------------------

15. Can perf profile kernel code?

Yes, perf can profile kernel functions, drivers, interrupts, and scheduler behavior.

--------------------------------------------------------

16. How does perf distinguish between user space and kernel space?

By identifying symbols from user binaries and the kernel image (vmlinux).

--------------------------------------------------------

17. What are hardware performance counters?

Special CPU registers that count low-level events such as cycles, instructions, cache misses, and branch mispredictions.

--------------------------------------------------------

18. What is a CPU hotspot?

A function or code section that consumes a significant percentage of CPU time.

--------------------------------------------------------

19. What does high cache-miss count indicate?

Poor memory locality or inefficient data access patterns causing performance degradation.

--------------------------------------------------------

20. What is the role of sampling in perf?

perf periodically samples the instruction pointer to statistically determine where CPU time is spent.

--------------------------------------------------------

21. What is the difference between sampling and tracing?

Sampling captures periodic snapshots, while tracing records every event, making sampling lighter and faster.

--------------------------------------------------------

22. Can perf be used on production systems?

Yes, perf is commonly used on production systems with low overhead when used carefully.

--------------------------------------------------------

23. What permissions are required to use perf?

Root privileges or appropriate perf_event permissions are required, especially for kernel profiling.

--------------------------------------------------------

24. How is perf used in boot time optimization?

By profiling kernel and user-space execution during boot to identify slow drivers and services.

--------------------------------------------------------

25. What does perf top showing schedule() indicate?

Excessive context switching or task contention in the system.

--------------------------------------------------------

26. What is vmlinux in perf output?

vmlinux is the uncompressed Linux kernel image containing kernel symbols.

--------------------------------------------------------

27. Can perf profile multi-threaded applications?

Yes, perf can profile CPU usage across multiple threads and processes.

--------------------------------------------------------

28. How does perf help in embedded Linux systems?

It identifies CPU-heavy drivers, inefficient application loops, and kernel overhead on resource-constrained systems.

--------------------------------------------------------

29. What is the main limitation of perf?

It requires kernel support and matching kernel tools, and interpretation requires understanding of system internals.

--------------------------------------------------------

30. Explain perf in one sentence.

perf is a Linux profiling tool that identifies exactly where CPU time is spent in applications and the kernel.

========================================================
END OF FILE
========================================================

