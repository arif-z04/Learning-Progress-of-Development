# Computer Fundamentals: CPU, RAM, Storage, Processes & Threads

## 1. CPU (Central Processing Unit)

### Definition
The **CPU** is the main processing unit of a computer. It executes machine instructions and performs arithmetic, logical operations, and other computations.

### Main Components and Concepts
- **Core:** An execution unit inside a CPU. Multiple cores can execute tasks in parallel.
- **Clock Speed:** The rate at which a CPU clock cycles, measured in GHz. Higher clock speed does not always mean better overall performance.
- **Cache:** Small, fast memory inside or close to the CPU that stores frequently needed data.
- **Instruction:** An operation that the CPU can execute.

### Example
```csharp
int price = 100;
int quantity = 5;
int total = price * quantity;
```

When this program runs, the CPU executes the instructions required to calculate `total`.

### When CPU Performance Matters
- Complex calculations
- Large data processing
- Machine learning
- Encryption and compression
- Inefficient algorithms and loops

### Linux Commands
```bash
lscpu
top
```

- `lscpu`: Displays CPU information.
- `top`: Monitors running processes and resource usage.

---

## 2. RAM (Random Access Memory)

### Definition
**RAM** is the computer's temporary working memory. It stores the program instructions and data currently needed by running applications.

### Characteristics
- Volatile: Data is generally lost when power is removed.
- Fast: Much faster than persistent storage.
- Temporary: Used while programs are running.
- Limited capacity: Running applications compete for available memory.

### Example
When you open VS Code:
1. VS Code's files remain stored on your SSD.
2. The operating system loads the required program data into RAM.
3. The CPU executes instructions using the required data.

### What Happens When RAM Is Insufficient?
The operating system may reclaim cached memory, compress memory, or use swap space on storage. Excessive swapping can significantly slow down the computer.

### Linux Command
```bash
free -h
```

Important columns:
- `total`: Total memory available to Linux.
- `used`: Memory currently in use, calculated according to the tool's accounting.
- `free`: Completely unused memory.
- `buff/cache`: Memory used for buffers and caches.
- `available`: Estimated memory available for new applications without significant swapping.
- `Swap`: Disk-backed memory used when needed.

**Note:** Low `free` memory does not necessarily mean a problem. Linux uses otherwise-available RAM for caching.

---

## 3. Storage

### Definition
**Storage** is the persistent location where a computer saves its operating system, applications, source code, documents, and database files.

### Types
- **HDD (Hard Disk Drive):** Uses spinning magnetic disks.
- **SSD (Solid-State Drive):** Uses flash memory and is generally faster than an HDD.

### Characteristics
- Non-volatile: Data normally remains after shutdown.
- Stores files and installed applications.
- Has a finite capacity.
- Performance affects file access, database operations, application startup, and builds.

### Example
In a web application:
- Source code is stored on the SSD.
- Database files are stored persistently on storage.
- Frequently used data may be cached in RAM.
- The CPU executes the instructions needed to process requests.

### Linux Commands
```bash
df -h
lsblk
```

- `df -h`: Displays filesystem space usage.
- `lsblk`: Lists block devices and partitions.

**Important:** `df -h` checks filesystem capacity, not RAM usage.

---

## 4. Processes

### Definition
A **program** is a set of instructions stored in a file. A **process** is a running instance of a program managed by the operating system.

A process has its own virtual address space and operating-system-managed resources. It may contain one or more threads.

### Examples
- A running VS Code instance
- A running web browser
- An ASP.NET Core backend
- A MySQL database server

### PID (Process ID)
A **PID** is an identifier assigned to a process by the operating system.

### Linux Commands
```bash
ps aux
```
Lists running processes and information such as CPU and memory usage.

```bash
pgrep -a dotnet
```
Searches for processes matching `dotnet` and displays their command lines.

```bash
ps -p 1 -o pid,comm,args
```
Displays information about process 1.

```bash
top
```
Provides an interactive view of running processes and resource consumption.

### Why Processes Matter
- Running and managing applications
- Monitoring CPU and memory usage
- Debugging application failures
- Running web servers and databases
- Managing background tasks

---

## 5. Threads

### Definition
A **thread** is an execution path within a process. It represents a sequence of instructions that can be scheduled for execution by the operating system.

A process can contain multiple threads. Threads within the same process share its memory space and many resources, but each thread has its own execution state and stack.

### Example
A web server may handle multiple requests concurrently. Depending on the server architecture and workload, different threads may execute work, while asynchronous operations allow other work to proceed during I/O waits.

### Why Threads Matter
- Performing multiple tasks concurrently
- Handling work in the background
- Improving throughput for suitable workloads
- Making use of multiple CPU cores for parallel work

### Important C# Concept: `async` and `await`

```csharp
var doctors = await dbContext.Doctors.ToListAsync();
```

This code asynchronously waits for a database operation to complete.

- `async` and `await` do not automatically create a new thread.
- Asynchronous I/O allows a thread to be available for other work while waiting.
- CPU-intensive work may require different approaches, such as parallel processing, when appropriate.

---

## 6. Process vs. Thread

| Feature | Process | Thread |
|---|---|---|
| Definition | Running instance of a program | Execution path within a process |
| Memory | Has its own virtual address space | Shares process memory with sibling threads |
| Resources | Owns or manages process-level resources | Uses resources belonging to its process |
| Communication | Often needs inter-process communication | Can communicate through shared memory |
| Creation overhead | Generally higher | Generally lower |
| Failure impact | Often isolated from other processes | A fatal thread failure can affect the whole process |

**Remember:** One process does not mean one thread. A single ASP.NET Core process can manage many threads and concurrent requests.

---

## 7. Concurrency vs. Parallelism

### Concurrency
Multiple tasks make progress during overlapping periods. They do not necessarily execute at the same instant.

### Parallelism
Multiple tasks execute at the same time, typically on different CPU cores.

**Example:** A web server can handle concurrent requests while some are waiting for database responses. CPU-intensive tasks may execute in parallel if suitable execution resources are available.

---

## 8. How CPU, RAM, Storage, Processes, and Threads Work Together

Consider running an ASP.NET Core web application connected to a database.

1. **Storage:** Contains the application's files and persistent database data.
2. **RAM:** Holds active program data, objects, and cached information.
3. **Process:** The operating system runs the backend as a process.
4. **Threads:** The process contains threads that execute application work.
5. **CPU:** Executes instructions performed by those threads.
6. **Database I/O:** The application may request data from a database, which may access cached data or persistent storage.
7. **Response:** The backend sends the result back to the client.

These components interact continuously; this is a simplified model rather than a strict one-way sequence.

---

## 9. Quick Revision

| Concept | Main Purpose | Linux Command |
|---|---|---|
| CPU | Executes instructions | `lscpu`, `top` |
| RAM | Holds active data | `free -h` |
| Storage | Stores persistent data | `df -h`, `lsblk` |
| Processes | Represents running programs | `ps aux`, `pgrep` |
| Threads | Represents execution paths within processes | `top`, `ps -T -p PID` |

### Key Points to Remember
- CPU executes instructions.
- RAM temporarily holds active program data.
- Storage persistently stores files and data.
- A process is a running instance of a program.
- A thread is an execution path inside a process.
- A process can contain multiple threads.
- Concurrency and parallelism are related but different.
- `async`/`await` does not automatically create a new thread.
- Linux uses RAM for caching, so low free memory alone does not indicate a problem.

## 10. Practical Exercises

Run these commands in a Linux terminal:

```bash
lscpu
free -h
df -h
lsblk
ps aux
top
pgrep -a dotnet
```

Observe CPU details, memory usage, disk capacity, running processes, and resource consumption.

**Learning milestone:** Be able to explain how a web application uses CPU, RAM, storage, processes, and threads when handling an HTTP request.
