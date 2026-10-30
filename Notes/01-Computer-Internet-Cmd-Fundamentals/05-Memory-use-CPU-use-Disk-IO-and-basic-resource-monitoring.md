# Linux Fundamentals: Memory Usage, CPU Usage, Disk I/O & Resource Monitoring

## 1. Introduction to Resource Monitoring

**Resource monitoring** means observing how a computer uses its hardware and operating-system resources while programs are running.

The four important areas are:

1. **CPU usage** — how much processing work the CPU is doing.
2. **Memory usage (RAM)** — how much physical memory applications and the operating system are using.
3. **Disk I/O** — how quickly data is read from or written to storage.
4. **System load and resource pressure** — whether the system is struggling to keep up with its workload.

Resource monitoring is an essential skill for developers and system administrators. It helps diagnose slow applications, excessive memory consumption, high CPU usage, and storage bottlenecks.

### Why developers need it

Imagine your ASP.NET Core web application becomes slow.

| Symptom | Possible Cause |
|---|---|
| CPU usage stays near 100% | Expensive computation, inefficient code, or excessive processing |
| Available memory becomes very low | Memory leak, too many processes, or large data structures |
| Disk activity stays high | Heavy database queries, logging, or large file operations |
| System becomes unresponsive | Resource exhaustion or multiple bottlenecks |
| Application crashes unexpectedly | Out-of-memory condition, unhandled errors, or another failure |

**Important:** A high resource reading does not automatically mean something is wrong. You need to understand the workload and compare resource usage with normal behavior.

---

## 2. Understanding CPU Usage

### 2.1 What is CPU usage?

CPU usage indicates how much of the CPU's available processing capacity is being used during a period of time.

For example:

- **0–10%:** Light processing activity.
- **30–60%:** Moderate activity.
- **80–100%:** Heavy activity.

These ranges are only rough examples. High usage can be perfectly normal during compilation, machine-learning workloads, or video rendering.

### 2.2 CPU cores and utilization

A CPU may have multiple logical CPUs, including cores and hardware threads.

On a machine with 8 logical CPUs, a single-threaded program can fully occupy one logical CPU while total system CPU usage appears around 12.5%, depending on the monitoring tool's calculation.

This explains why a program may be CPU-bound without showing 100% total system usage.

### 2.3 Check CPU information

```bash
lscpu
```

Displays CPU architecture, logical CPU count, core information, and other hardware details.

To see the number of logical CPUs:

```bash
nproc
```

### 2.4 Monitor CPU usage with `top`

```bash
top
```

The interactive process monitor displays CPU activity, memory usage, and running processes.

Useful controls:

- Press `P` to sort by CPU usage.
- Press `M` to sort by memory usage.
- Press `q` to quit.

The CPU summary may contain categories such as:

| Category | Meaning |
|---|---|
| `us` | Time spent running user-space processes |
| `sy` | Time spent in the kernel |
| `id` | Idle CPU time |
| `wa` | Time the CPU is idle while I/O is outstanding |
| `st` | Time taken by a hypervisor from a virtual CPU, when applicable |

A high `wa` value can indicate storage or I/O delays, although it must be interpreted alongside other metrics.

### 2.5 Monitor CPU usage with `htop`

```bash
htop
```

`htop` provides a more visual, interactive view of processes and system resource usage. It may need to be installed first.

On Omarchy or another Arch-based system:

```bash
sudo pacman -S htop
```

Use the package manager appropriate to your Linux distribution.

### 2.6 Check CPU usage with `ps`

```bash
ps -eo pid,comm,%cpu,%mem --sort=-%cpu | head
```

This displays processes sorted by CPU usage, with the highest values first.

To inspect a specific process:

```bash
ps -p PID -o pid,comm,%cpu,%mem
```

Replace `PID` with the actual process ID.

### 2.7 Common causes of high CPU usage

- Infinite loops or inefficient algorithms.
- Too many concurrent tasks.
- Excessive serialization or data processing.
- Repeated database result processing in application code.
- Background jobs consuming processing capacity.
- Compilation or machine-learning workloads.

### 2.8 Practical CPU test

Run a harmless CPU-intensive command:

```bash
yes > /dev/null
```

In another terminal, run:

```bash
top
```

You should see the `yes` process consuming CPU.

Stop the test by finding its terminal and pressing `Ctrl+C`. If necessary, locate the process with `pgrep -a yes` and stop only the process you started.

**Do not leave this test running unnecessarily.**

---

## 3. Understanding Memory Usage (RAM)

### 3.1 What is RAM?

**Random Access Memory (RAM)** is the fast working memory used by running applications and the operating system.

When an application starts, it generally loads code and data into memory so the CPU can access them efficiently.

Examples of memory-consuming activities:

- Opening many browser tabs.
- Running an IDE.
- Starting a database server.
- Loading a large dataset into Python.
- Running multiple web applications simultaneously.

RAM is volatile: its contents are generally lost when the machine loses power.

### 3.2 Memory terminology

| Term | Meaning |
|---|---|
| Total | RAM available to the operating system |
| Used | Memory currently reported as used by the tool |
| Free | Memory that is currently unused |
| Available | An estimate of memory that can be used by new applications without swapping heavily |
| Cache | Memory used to keep useful data readily available |
| Swap | Disk-backed space that can hold memory pages when needed |

**Important:** Linux intentionally uses otherwise-unused RAM for filesystem caching. Therefore, low `free` memory does not necessarily mean the system is running out of memory.

For a quick health check, pay attention to **available memory** and swap activity, not just the `free` column.

### 3.3 Check RAM with `free`

```bash
free -h
```

The `-h` option displays values in human-readable units.

Example output:

```text
               total        used        free      shared  buff/cache   available
Mem:             23Gi       8.0Gi       2.0Gi       500Mi        13Gi        14Gi
Swap:             8Gi       512Mi       7.5Gi
```

These are illustrative values, not measurements from your computer.

Interpretation:

- `total`: memory visible to the operating system.
- `used`: memory currently accounted for as used.
- `free`: completely unused memory.
- `buff/cache`: buffers and cache.
- `available`: estimated memory available for new applications.
- `Swap used`: amount of swap currently occupied.

A system with little free RAM can still be healthy if available memory remains sufficient and swapping is limited.

### 3.4 Monitor memory with `top`

```bash
top
```

Press `M` to sort processes by memory usage.

Useful columns include:

- `RES`: resident physical memory currently associated with a process.
- `VIRT`: virtual address space associated with a process.
- `%MEM`: percentage of physical memory associated with the process, according to the tool's accounting.

**Do not treat `VIRT` as actual RAM consumption.** It can include mapped files, reserved address space, and other virtual memory that is not resident in physical RAM.

### 3.5 Find memory-heavy processes

```bash
ps -eo pid,comm,%mem,rss --sort=-rss | head
```

`RSS` is resident set size, typically reported in KiB by `ps`. It estimates the physical memory currently resident for a process, but shared pages mean it should not be treated as an exact measurement of memory uniquely owned by that process.

### 3.6 Check swap

```bash
swapon --show
```

Shows configured swap devices or files.

```bash
free -h
```

Shows how much swap is currently used.

Using some swap is not automatically a problem. However, sustained heavy swapping can make a system slow because storage is much slower than RAM.

### 3.7 What is an out-of-memory (OOM) condition?

An **out-of-memory condition** occurs when the system cannot satisfy memory demands under its current constraints. Linux may invoke an OOM killer to terminate selected processes to protect the system.

Inspect kernel messages when investigating suspected OOM events:

```bash
sudo journalctl -k -b | grep -i -E 'out of memory|oom|killed process'
```

Depending on system configuration, logs may be incomplete or access may be restricted.

### 3.8 Memory leaks

A **memory leak** occurs when a program retains memory it no longer needs, causing memory consumption to grow unnecessarily over time.

For example, a web application might keep adding request data to a collection without removing old entries.

Possible warning signs:

- Memory usage grows steadily.
- Restarting the application temporarily reduces memory consumption.
- The application slows down or crashes as memory pressure increases.

High memory usage alone does not prove a leak. A large workload or intentional caching may explain it.

---

## 4. Understanding Disk I/O

### 4.1 What is disk I/O?

**Disk I/O (Input/Output)** refers to reading data from storage and writing data to storage.

Storage may include an SSD, HDD, USB drive, or another block device.

Examples:

- Reading a database table.
- Saving application logs.
- Installing software packages.
- Loading a large dataset.
- Copying files.
- Writing database transactions.

### 4.2 Important disk I/O metrics

| Metric | Meaning |
|---|---|
| Read throughput | Amount of data read per second |
| Write throughput | Amount of data written per second |
| IOPS | Number of input/output operations per second |
| Latency | Time taken for an I/O operation to complete |
| Queue depth | Number of I/O requests waiting or in progress |
| Utilization | How busy the device is according to the monitoring tool |

High throughput does not always mean poor performance. A storage device can be transferring data quickly and efficiently.

Likewise, high utilization does not by itself prove that a disk is the bottleneck. Consider latency, workload, queueing, and application response time together.

### 4.3 Check disk capacity with `df`

```bash
df -h
```

Displays filesystem capacity, used space, available space, and mount points.

Example:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p2  200G  120G   70G  64% /
```

The values above are illustrative.

Use this command to identify filesystems that are nearly full.

### 4.4 Check directory size with `du`

```bash
du -sh ~/Projects
```

Shows the total space used by a directory.

Check common directories:

```bash
du -sh ~/Downloads
du -sh ~/.cache
```

These commands help identify large directories in your home directory.

To find large files within a directory:

```bash
find ~/Projects -type f -size +500M -print
```

This lists files larger than 500 MB.

### 4.5 Identify storage devices

```bash
lsblk
```

Displays block devices, partitions, and mount points.

For filesystem information:

```bash
lsblk -f
```

### 4.6 Monitor disk I/O with `iostat`

```bash
iostat -xz 1
```

This reports extended CPU and device I/O statistics every second. It is provided by the `sysstat` package on many distributions.

Install it on Arch-based systems if needed:

```bash
sudo pacman -S sysstat
```

Important columns commonly include:

- `r/s`: read requests per second.
- `w/s`: write requests per second.
- `rMB/s` or `rkB/s`: read throughput, depending on the version.
- `wMB/s` or `wkB/s`: write throughput, depending on the version.
- `await`: average time for I/O requests to complete, usually in milliseconds.
- `%util`: time the device was busy processing I/O requests.

Column names vary by version. Check the command's manual for the exact definitions.

On modern SSDs and NVMe devices, `%util` should not be interpreted as a universal measure of maximum capacity. A device may handle parallel requests, and a high value does not independently prove a bottleneck.

### 4.7 Find processes doing disk I/O

```bash
sudo iotop
```

If installed and supported, `iotop` displays process-level I/O activity.

On Arch-based systems:

```bash
sudo pacman -S iotop
```

Permissions, kernel support, and the installed version can affect which details are available.

### 4.8 Disk space vs. disk I/O

These are two different problems:

- **Disk space problem:** The filesystem is running out of room.
- **Disk I/O problem:** Reads or writes are slow, excessive, or delayed.

A disk can have plenty of free space but still be slow. It can also be almost full while performing I/O quickly.

---

## 5. System Load and Resource Pressure

### 5.1 What is load average?

Linux load average summarizes the number of tasks that are running or waiting for CPU time, along with tasks in certain uninterruptible states, over three time windows.

View it with:

```bash
uptime
```

Example:

```text
load average: 1.20, 1.50, 1.70
```

The three numbers represent approximately the last 1, 5, and 15 minutes.

### 5.2 Interpret load average carefully

Load average is not the same as CPU usage.

On a system with 8 logical CPUs, a load average near 8 can indicate that the system has roughly as many tasks demanding CPU time as it has logical CPUs, but the exact interpretation depends on task states and workload.

On a system with 2 logical CPUs, a load average of 8 suggests substantially more queued or uninterruptible work relative to CPU capacity.

Use `nproc` to see the logical CPU count:

```bash
nproc
```

A high load average can arise from CPU contention or tasks waiting on I/O. Investigate with `top`, `free`, and I/O tools instead of relying on one number.

### 5.3 Check system uptime and load

```bash
uptime
```

Shows how long the system has been running, the number of users, and load averages.

### 5.4 Check memory pressure

On Linux systems that expose Pressure Stall Information (PSI):

```bash
cat /proc/pressure/cpu
cat /proc/pressure/memory
cat /proc/pressure/io
```

PSI helps show how much time tasks are delayed because CPU, memory, or I/O resources are contended.

These files may not exist or may provide limited information in some environments.

---

## 6. A Basic Resource-Monitoring Toolkit

You do not need dozens of tools to begin. Learn these commands first.

| Command | Main Purpose |
|---|---|
| `top` | Live CPU, memory, and process monitoring |
| `htop` | Interactive process and resource monitoring |
| `free -h` | RAM and swap overview |
| `ps` | Inspect processes and their resource usage |
| `uptime` | System load averages |
| `df -h` | Filesystem capacity |
| `du -sh PATH` | Directory space usage |
| `lsblk` | Storage devices and partitions |
| `iostat -xz 1` | CPU and storage I/O statistics |
| `iotop` | Process-level disk I/O, where supported |
| `vmstat 1` | Periodic CPU, memory, swap, and I/O-related statistics |

### Try `vmstat`

```bash
vmstat 1
```

Updates statistics approximately every second. The first report commonly summarizes activity since boot, while subsequent reports show activity over the sampling interval.

Useful fields can include:

- `r`: runnable processes.
- `b`: processes blocked waiting for certain resources.
- `si` and `so`: swap-in and swap-out activity.
- `bi` and `bo`: block input and output.
- `us`, `sy`, and `id`: CPU time categories.

Exact interpretation depends on the system and version. Press `Ctrl+C` to stop the command.

---

## 7. Practical Troubleshooting Workflow

Suppose your development laptop suddenly becomes slow while running VS Code, a browser, a database, and an ASP.NET Core application.

### Step 1: Get a quick overview

```bash
uptime
free -h
df -h
```

Check system load, available memory, swap usage, and filesystem capacity.

### Step 2: Find the busiest processes

```bash
top
```

Press `P` to sort by CPU, then `M` to sort by memory.

### Step 3: Inspect a suspicious process

```bash
ps -p PID -o pid,ppid,stat,%cpu,%mem,rss,comm
```

Replace `PID` with the actual process ID.

### Step 4: Investigate storage activity

```bash
iostat -xz 1
```

Look for high I/O latency or sustained activity that matches the time of the slowdown.

### Step 5: Inspect logs

For a systemd-managed application:

```bash
journalctl -u myapp.service -n 100
```

Replace `myapp.service` with the real service name.

### Step 6: Form a hypothesis and test it

Examples:

- High CPU: inspect algorithms, loops, background jobs, and request volume.
- Low available RAM with sustained swapping: identify memory-heavy processes.
- High I/O latency: investigate database operations, storage activity, and filesystem issues.
- Filesystem nearly full: find large files and logs before deleting anything.

### Step 7: Verify the result

Repeat the same measurements after making a change. Compare the results under a similar workload.

**Professional habit:** Measure first, identify the likely bottleneck, make one controlled change, and measure again.

---

## 8. Practical Lab

Complete these exercises in your Linux terminal.

### Task 1: Record Your Baseline

```bash
lscpu
nproc
uptime
free -h
df -h
lsblk
```

Record the logical CPU count, load average, available RAM, swap usage, and free filesystem space.

### Task 2: Monitor Processes

```bash
top
```

Identify:

- One process using CPU.
- One process using memory.
- The overall CPU idle percentage.

Exit with `q`.

### Task 3: Inspect Storage Usage

```bash
du -sh ~/Downloads
du -sh ~/.cache
```

Compare the sizes. Do not delete anything merely because it is large; determine what the data is used for first.

### Task 4: Observe CPU Activity

In one terminal:

```bash
yes > /dev/null
```

In another terminal:

```bash
top
```

Observe CPU usage, then press `Ctrl+C` in the first terminal.

### Task 5: Inspect I/O Statistics

If `sysstat` is installed:

```bash
iostat -xz 1
```

Observe the output while the system is idle, then while performing an ordinary file operation.

### Task 6: Build a Resource Snapshot

Run:

```bash
{
  date
  uptime
  free -h
  df -h
} > resource-snapshot.txt
```

Inspect the file:

```bash
cat resource-snapshot.txt
```

This creates a simple text report of your system's resource state at that moment.

---

## 9. Quick Revision

| Concept | Key Idea |
|---|---|
| CPU usage | How much processing capacity is being used |
| RAM | Working memory for running programs |
| Available memory | Estimate of memory available for new work |
| Swap | Disk-backed memory used to hold memory pages |
| Disk I/O | Reading and writing data on storage |
| IOPS | Number of storage operations per second |
| Latency | Time taken for an operation to complete |
| Load average | Summary of runnable and certain uninterruptible tasks |
| `top` | Live process and resource monitor |
| `free -h` | RAM and swap summary |
| `df -h` | Filesystem capacity |
| `du -sh` | Directory space usage |
| `iostat` | CPU and storage I/O statistics |
| `vmstat` | Periodic system performance statistics |
| PSI | Measures resource contention and stalls |

## 10. Learning Milestone

You should now be able to:

- Inspect CPU and memory usage in Linux.
- Distinguish free RAM from available RAM.
- Find CPU-heavy and memory-heavy processes.
- Check swap usage and filesystem capacity.
- Explain the difference between disk space and disk I/O.
- Monitor storage performance with `iostat`.
- Understand load average and basic resource pressure.
- Follow a structured workflow to diagnose a slow development machine.

**Remember:** No single metric explains every performance problem. Combine CPU, memory, disk I/O, process information, and application logs to build an accurate picture of system health.