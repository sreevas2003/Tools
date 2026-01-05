# iotop
**1️⃣ What is iotop?**

👉 iotop shows which program is using the hard disk RIGHT NOW.

If your system feels:

- Slow
- Frozen
- Boot takes long
- Commands hang

**Where is iotop used?**

| Place          | Why             |
| -------------- | --------------- |
| Linux servers  | DB / log issues |
| Embedded Linux | SD card slow    |
| Boot analysis  | Slow startup    |
| Debugging      | System hangs    |
| Interviews     | Load avg vs CPU |

**How iotop works**

- Kernel tracks per-process disk read/write
- iotop shows it live
- Needs root access

**Install & Start** (First Practical Step)
```
sudo apt install iotop
```

Run:
```
sudo iotop
```

**⚠️ Must use sudo**

**What You See on Screen**

<img width="763" height="102" alt="image" src="https://github.com/user-attachments/assets/a72a0fea-2e21-4b0f-9deb-b089765aa0dd" />

| Column     | Simple meaning                       |
| ---------- | ------------------------------------ |
| DISK READ  | How fast process reads               |
| DISK WRITE | How fast process writes              |
| IO %       | How much time process waits for disk |
| SWAPIN %   | Memory swapped from disk             |
| COMMAND    | Program name                         |

👉 IO % near 100 = system feels frozen

**First Hands-On Experiment** (IMPORTANT)

**Step 1**: Open two terminals
**Terminal 1**
```
sudo iotop
```
**Terminal 2** (create disk write)
```
dd if=/dev/zero of=testfile bs=1M count=1000
```
**What you observe**

- dd appears in iotop
- High DISK WRITE
- High IO %

✔️ Now you understand what disk load looks like. (IMPORTANT)

**Only Show Processes Using Disk (Very Useful)**
```
sudo iotop -o
```

👉 Hides idle processes
👉 Shows only disk users

**Important Keys (Use Inside iotop)**

| Key | Meaning                      |
| --- | ---------------------------- |
| `o` | Only active disk processes   |
| `a` | Total disk usage since start |
| `q` | Quit                         |

**Save Output (Real Debugging Skill)**
```
sudo iotop -b -n 5 -o > disk_issue.txt
```

Later:
```
cat disk_issue.txt
```
**One-Line Interview Answers (Easy)**

- iotop shows per-process disk I/O usage
- High IO% means process waiting for disk
- Used when CPU is idle but system is slow
- Common in embedded Linux SD card issues



========================================================

FILE NAME: iotop_interview_questions.txt
TOPIC: Linux Disk I/O Monitoring - iotop
LEVEL: Beginner to Advanced

========================================================

1. What is iotop?

iotop is a Linux command-line tool used to monitor real-time disk read and write activity per process or thread.

--------------------------------------------------------

2. Why is iotop used?

iotop is used to identify which process is causing disk I/O bottlenecks when the system feels slow or unresponsive.

--------------------------------------------------------

3. When should you use iotop instead of htop?

When CPU usage is low but the system is slow due to disk read/write activity, iotop should be used.

--------------------------------------------------------

4. What type of problems does iotop help debug?

Disk bottlenecks, slow boot, excessive logging, swap usage, SD card wear, and I/O wait issues.

--------------------------------------------------------

5. Does iotop require root access?

Yes, iotop requires root or sudo privileges to access kernel I/O accounting data.

--------------------------------------------------------

6. Which kernel features are required for iotop?

CONFIG_TASKSTATS, CONFIG_TASK_DELAY_ACCT, and CONFIG_TASK_IO_ACCOUNTING must be enabled.

--------------------------------------------------------

7. What does the DISK READ column show?

It shows the current disk read speed of a process.

--------------------------------------------------------

8. What does the DISK WRITE column show?

It shows the current disk write speed of a process.

--------------------------------------------------------

9. What does the IO% column indicate?

IO% indicates the percentage of time a process is waiting for disk I/O to complete.

--------------------------------------------------------

10. What does high IO% mean?

High IO% means the process is blocked waiting for disk operations, often causing system lag.

--------------------------------------------------------

11. What does the SWAPIN% column indicate?

It shows the percentage of time a process spends swapping memory pages from disk.

--------------------------------------------------------

12. What does high SWAPIN% usually indicate?

Memory pressure or insufficient RAM rather than a pure disk performance issue.

--------------------------------------------------------

13. How do you start iotop?

By running the command sudo iotop.

--------------------------------------------------------

14. How do you show only processes doing disk I/O?

By using the command sudo iotop -o.

--------------------------------------------------------

15. What is batch mode in iotop?

Batch mode runs iotop without an interactive UI and prints output to the terminal or a file.

--------------------------------------------------------

16. How do you log disk I/O activity using iotop?

Using sudo iotop -b -n <count> -o > file.txt.

--------------------------------------------------------

17. What does the -n option do in iotop?

It specifies the number of iterations iotop should run in batch mode.

--------------------------------------------------------

18. What does accumulated mode in iotop mean?

It shows total disk I/O performed by processes since iotop was started.

--------------------------------------------------------

19. How do you enable accumulated mode?

By pressing the 'a' key while iotop is running.

--------------------------------------------------------

20. Can iotop show per-thread disk activity?

Yes, iotop can show disk I/O at the thread level using TID information.

--------------------------------------------------------

21. Why is iotop important in embedded Linux systems?

Embedded systems often use slow flash or SD cards, and iotop helps detect excessive writes that degrade performance.

--------------------------------------------------------

22. What is a common embedded Linux issue detected by iotop?

Continuous logging causing high disk writes and system freezes.

--------------------------------------------------------

23. What does it mean if load average is high but CPU usage is low?

Processes are likely blocked on I/O, which can be confirmed using iotop.

--------------------------------------------------------

24. Can iotop replace tools like perf or ftrace?

No, iotop is for disk I/O monitoring, while perf and ftrace are for CPU profiling and kernel tracing.

--------------------------------------------------------

25. How can iotop help during system boot analysis?

It identifies services or processes performing heavy disk I/O during boot.

--------------------------------------------------------

26. What filesystem issues can be identified using iotop?

Slow disks, excessive sync writes, journaling overhead, and filesystem contention.

--------------------------------------------------------

27. Does iotop work on all Linux systems?

It works only if the kernel supports required task accounting features.

--------------------------------------------------------

28. What command would you use to analyze disk I/O over SSH?

sudo iotop -b -o

--------------------------------------------------------

29. How do you exit iotop?

By pressing the 'q' key.

--------------------------------------------------------

30. In one sentence, explain iotop.

iotop identifies which processes are causing disk I/O delays and system slowdowns in Linux.


========================================================
END OF FILE
========================================================
