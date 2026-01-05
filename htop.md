# htop 
**🔹 What htop is**

* htop stands for **Hisham's top**, named after its original author, Hisham H. Muhammad
* htop is an interactive process viewer.
* htop is an interactive, real-time process & system monitor for Linux. 

It answers:

- Which process is using CPU?

- Which process is eating RAM?

- Is the system overloaded?

**2️⃣ Install htop**
```
sudo apt update
sudo apt install htop
```
verify :-
```
htop --version
```

**3️⃣ Launch & First Look**
```
htop
```
**Screen Layout (Very Important)**

<img width="686" height="166" alt="image" src="https://github.com/user-attachments/assets/7591477a-9977-46ee-a7c0-d3ab4aac1445" />

<img width="1133" height="747" alt="image" src="https://github.com/user-attachments/assets/73fd6cb5-202a-4254-8164-77257b7e4ff7" />

**4️⃣ Understanding CPU Bars (Core-Level)**

CPU Colors

| Color  | Meaning         |
| ------ | --------------- |
| Green  | User processes  |
| Red    | Kernel (system) |
| Blue   | Low priority    |
| Orange | IRQ / SoftIRQ   |

**5️⃣ Memory Breakdown (Interview Favorite)**
| Field | Meaning                    |
| ----- | -------------------------- |
| MEM   | Used RAM (excluding cache) |
| BUFF  | Block device buffers       |
| CACHE | Page cache                 |
| SWAP  | Swap usage                 |

**6️⃣ Process States (Very Important)**

| State | Meaning                             |
| ----- | ----------------------------------- |
| R     | Running                             |
| S     | Sleeping                            |
| D     | Uninterruptible sleep ⚠️ (I/O wait) |
| Z     | Zombie                              |
| T     | Stopped                             |

👉 D-state processes = disk / driver issue

**7️⃣ Essential Keyboard Shortcuts (Must Know)**

| Key   | Action                  |
| ----- | ----------------------- |
| `F1`  | Help                    |
| `F2`  | Setup (columns, meters) |
| `F3`  | Search                  |
| `F4`  | Filter                  |
| `F5`  | Tree view 🌳            |
| `F6`  | Sort by column          |
| `F9`  | Kill process            |
| `F10` | Quit                    |
| `u`   | Show user processes     |

**1️⃣2️⃣ Embedded / Kernel Debugging Use-Cases**

| Scenario     | What to check              |
| ------------ | -------------------------- |
| Board hangs  | D-state processes          |
| High load    | CPU bar + load average     |
| App slow     | Tree view + per-thread CPU |
| Memory leak  | RES growing continuously   |
| Driver issue | High kernel (red) CPU      |

**1️⃣3️⃣ htop vs top (Interview Table)**

| Feature       | top     | htop |
| ------------- | ------- | ---- |
| Mouse support | ❌       | ✅    |
| Tree view     | ❌       | ✅    |
| Per-core CPU  | ❌       | ✅    |
| Kill from UI  | Hard    | Easy |
| Customization | Limited | High |

**1️⃣4️⃣ Mini Hands-On Lab (Do This)**

Step 1: Create CPU load
```
yes > /dev/null &
```
Step 2: Observe in htop
```
htop
```
Step 3:

- Sort by CPU
- Identify yes
- Kill it using F9


# htop Interview Questions & Answers (Top 30)


========================================================
FILE NAME: htop_interview_questions.txt
TOPIC: Linux Performance Tool - htop
LEVEL: Beginner to Advanced
========================================================

1. What is htop?
htop is an interactive, real-time process monitoring tool for Linux. It is an enhanced version of the top command with better UI, per-core CPU visibility, and interactive process control.

--------------------------------------------------------

2. How is htop different from top?
htop provides a color-coded interface, per-CPU core usage, tree view of processes, mouse support, and easier process killing and sorting compared to top.

--------------------------------------------------------

3. How do you start htop?
By typing the command:
htop

--------------------------------------------------------

4. What information does htop display by default?
It displays CPU usage per core, memory usage, swap usage, load average, running processes, CPU%, memory%, runtime, and command name.

--------------------------------------------------------

5. What do the CPU colors in htop represent?
Green: User-space processes  
Red: Kernel-space processes  
Blue: Low-priority processes  
Orange/Yellow: IRQ and softIRQ processing

--------------------------------------------------------

6. What does high red CPU usage indicate?
High red CPU usage indicates heavy kernel activity, often due to drivers, interrupts, or kernel threads.

--------------------------------------------------------

7. What is RES memory in htop?
RES (Resident Set Size) is the actual physical RAM currently used by a process.

--------------------------------------------------------

8. What is VIRT memory?
VIRT is the total virtual memory allocated to a process, including shared libraries, mapped files, and swapped memory.

--------------------------------------------------------

9. What does SHR memory mean?
SHR is shared memory used by a process, such as shared libraries.

--------------------------------------------------------

10. What is the difference between MEM and CACHE?
MEM is actual application memory usage. CACHE is memory used by Linux for file caching, which can be freed if needed.

--------------------------------------------------------

11. What does process state 'D' mean?
D state means uninterruptible sleep, usually waiting for I/O operations like disk or driver responses.

--------------------------------------------------------

12. Why are D-state processes dangerous?
They cannot be killed easily and often indicate disk I/O issues or buggy kernel drivers.

--------------------------------------------------------

13. What is a zombie process in htop?
A zombie process (state Z) has finished execution but still exists because its parent has not collected its exit status.

--------------------------------------------------------

14. How do you kill a process using htop?
Select the process and press F9, then choose the signal (SIGTERM or SIGKILL).

--------------------------------------------------------

15. What is SIGTERM vs SIGKILL?
SIGTERM (15) requests graceful termination.  
SIGKILL (9) forcefully terminates the process without cleanup.

--------------------------------------------------------

16. How do you sort processes in htop?
Press F6 and select a column such as CPU%, MEM%, or TIME.

--------------------------------------------------------

17. How do you filter processes in htop?
Press F4 and type the process name to filter.

--------------------------------------------------------

18. What is tree view in htop?
Tree view shows parent-child relationships between processes, useful for debugging forked or multi-threaded applications.

--------------------------------------------------------

19. How do you enable tree view?
Press F5.

--------------------------------------------------------

20. How can htop help in debugging performance issues?
It helps identify CPU hogs, memory leaks, I/O waits, runaway threads, and kernel-heavy processes in real time.

--------------------------------------------------------

21. How do you monitor multi-core CPU usage?
htop shows a separate bar for each CPU core at the top.

--------------------------------------------------------

22. What is load average in htop?
Load average represents the number of processes waiting for CPU or I/O over 1, 5, and 15 minutes.

--------------------------------------------------------

23. What does high load average but low CPU usage indicate?
It usually indicates I/O bottlenecks or blocked processes.

--------------------------------------------------------

24. How do you change process priority in htop?
Use F7 to increase priority and F8 to decrease priority (nice value).

--------------------------------------------------------

25. What permissions are required to kill all processes?
Root or sudo privileges are required to kill system or other user processes.

--------------------------------------------------------

26. Can htop replace perf or ftrace?
No. htop is for monitoring. perf and ftrace are for detailed profiling and kernel tracing.

--------------------------------------------------------

27. Is htop suitable for embedded Linux systems?
Yes. htop is commonly used on embedded Linux boards for real-time debugging and performance monitoring.

--------------------------------------------------------

28. Where is htop configuration stored?
In the user's home directory under:
~/.config/htop/htoprc

--------------------------------------------------------

29. What does TIME+ column indicate?
It shows the total CPU time consumed by a process since it started.

--------------------------------------------------------

30. When should htop be the first tool you use?
When the system feels slow, hangs, overheats, or behaves unexpectedly, htop is usually the first diagnostic tool.

========================================================
END OF FILE
========================================================

