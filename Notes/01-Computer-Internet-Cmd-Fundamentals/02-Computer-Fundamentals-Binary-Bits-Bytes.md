# Computer Fundamentals: Binary, Bits, Bytes & Data-Size Units

## 1. Binary Number System

### Definition
The **binary number system** is a base-2 number system that uses only two digits: `0` and `1`.

Computers use binary to represent and process digital information.

- `0` can represent a LOW or OFF state.
- `1` can represent a HIGH or ON state.

These are simplified logical representations; the actual electrical implementation depends on the hardware.

### Decimal vs. Binary

| Number System | Base | Digits Used |
|---|---:|---|
| Binary | 2 | 0, 1 |
| Decimal | 10 | 0–9 |
| Hexadecimal | 16 | 0–9, A–F |

### Binary Place Values

Each position represents a power of 2, starting from the right with \(2^0\).

| Position | \(2^7\) | \(2^6\) | \(2^5\) | \(2^4\) | \(2^3\) | \(2^2\) | \(2^1\) | \(2^0\) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Value | 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |

### Example: Convert Binary to Decimal

Convert `1011` to decimal:

$$
\begin{aligned}
1011_2 &= 1(2^3)+0(2^2)+1(2^1)+1(2^0)\\
&=8+0+2+1\\
&=11_{10}
\end{aligned}
$$

Therefore, $(1011)_2=(11)_{10}$.

### Example: Convert Decimal to Binary

Convert decimal `13` to binary by repeatedly dividing by 2:

| Division | Quotient | Remainder |
|---|---:|---:|
| 13 ÷ 2 | 6 | 1 |
| 6 ÷ 2 | 3 | 0 |
| 3 ÷ 2 | 1 | 1 |
| 1 ÷ 2 | 0 | 1 |

Read the remainders from bottom to top.

**Result:** $(13)_{10}=(1101)_2$

---

## 2. Bit (Binary Digit)

### Definition
A **bit** is the smallest basic unit of digital information. It can hold one of two values: `0` or `1`.

The word *bit* comes from *binary digit*.

### Examples
- `0` = 1 bit
- `1` = 1 bit
- `101` = 3 bits
- `10110101` = 8 bits

### Where Bits Are Used
- Network transmission speeds
- Binary data representation
- Digital communication
- Data encoding and compression
- Computer memory and storage systems

### Important Notation
- `b` = bit
- `B` = byte

**Remember:** A lowercase `b` and an uppercase `B` mean different things.

---

## 3. Byte

### Definition
A **byte** is a unit of digital information consisting of 8 bits in modern computing.

$$
1\text{ Byte}=8\text{ bits}
$$

### Example

The binary sequence:

`01000001`

contains 8 bits, or 1 byte.

Under ASCII and UTF-8, this byte represents the character `A`.

### Common Units

| Unit | Symbol | Size |
|---|---|---:|
| Bit | b | 1 bit |
| Byte | B | 8 bits |
| Kilobyte | KB | 1,000 bytes |
| Megabyte | MB | 1,000 KB |
| Gigabyte | GB | 1,000 MB |
| Terabyte | TB | 1,000 GB |

The table uses decimal (SI) units. Binary units are defined separately below.

---

## 4. Decimal vs. Binary Data-Size Units

There are two commonly used measurement systems.

### A. Decimal Units (SI)

These use powers of 1,000 and are commonly used by storage manufacturers and network providers.

| Unit | Symbol | Exact Size |
|---|---|---:|
| Kilobyte | KB | \(10^3\) bytes = 1,000 bytes |
| Megabyte | MB | \(10^6\) bytes = 1,000,000 bytes |
| Gigabyte | GB | \(10^9\) bytes |
| Terabyte | TB | \(10^{12}\) bytes |

### B. Binary Units (IEC)

These use powers of 1,024.

| Unit | Symbol | Exact Size |
|---|---|---:|
| Kibibyte | KiB | \(2^{10}\) bytes = 1,024 bytes |
| Mebibyte | MiB | \(2^{20}\) bytes = 1,048,576 bytes |
| Gibibyte | GiB | \(2^{30}\) bytes |
| Tebibyte | TiB | \(2^{40}\) bytes |

### Why Are There Two Systems?

Computers use binary internally, but powers of 1,000 are convenient for standardized decimal measurements.

Historically, KB, MB, and GB were often used informally for binary-sized quantities too. The IEC units KiB, MiB, and GiB remove that ambiguity.

**Important:** `GB` and `GiB` are not exactly the same size.

---

## 5. Bits vs. Bytes in Network Speeds

Internet speeds are commonly measured in bits per second, while file sizes are commonly measured in bytes.

| Measurement | Meaning |
|---|---|
| bps | Bits per second |
| Kbps | Kilobits per second |
| Mbps | Megabits per second |
| Gbps | Gigabits per second |
| KB/s | Kilobytes per second |
| MB/s | Megabytes per second |

### Example: Download Speed

Suppose your internet connection is rated at 80 Mbps.

Convert megabits to megabytes per second:

$
\frac{80\text{ megabits/s}}{8}
=10\text{ megabytes/s}
$

The theoretical maximum is approximately **10 MB/s**, before accounting for protocol overhead, network conditions, and other factors.

### Important Formula

$$
\text{Bytes}=\frac{\text{Bits}}{8}
$$

$$
\text{Bits}=\text{Bytes}\times8
$$

---

## 6. Why Does a 512 GB SSD Show Less Capacity?

Suppose an SSD is advertised as 512 GB.

The manufacturer uses decimal units:

\[
512\text{ GB}=512,000,000,000\text{ bytes}
\]

Convert this to GiB:

\[
\frac{512,000,000,000}{1,073,741,824}
\approx476.84\text{ GiB}
\]

Therefore, the operating system may report approximately 476.8 GiB before accounting for partitions, filesystem metadata, and reserved space.

**This difference is mainly due to unit conventions, not missing storage.**

---

## 7. Data Sizes in Software Development

Understanding data sizes helps when building websites, APIs, databases, and applications.

### Common Examples
- A text file may occupy a few KB.
- A compressed image may occupy hundreds of KB or several MB.
- A video can occupy hundreds of MB or multiple GB.
- A database backup can occupy GB or more.
- RAM usage is commonly displayed in MiB or GiB.

Actual sizes depend on content, encoding, compression, and file format.

### Why Developers Need This Knowledge
- Estimating file uploads and downloads
- Configuring API upload limits
- Planning server storage
- Understanding network bandwidth
- Optimizing images and other assets
- Estimating memory usage
- Calculating backup and database sizes

---

## 8. Linux Commands for Data Sizes

### Check Filesystem Capacity

```bash
df -h
```

Shows filesystem capacity and usage using human-readable units.

### Check Directory Sizes

```bash
du -sh ~/Downloads
```

Shows the total disk space attributed to the Downloads directory.

### Check Individual File Sizes

```bash
ls -lh
```

Lists files with human-readable sizes.

### Check Memory

```bash
free -h
```

Displays RAM and swap statistics in human-readable units.

**Note:** The `-h` option means human-readable. The exact unit labels depend on the command and its implementation.

---

## 9. Quick Revision

| Term | Definition |
|---|---|
| Binary | Base-2 number system using 0 and 1 |
| Bit | One binary digit |
| Byte | 8 bits |
| KB | 1,000 bytes |
| KiB | 1,024 bytes |
| MB | 1,000,000 bytes |
| MiB | 1,048,576 bytes |
| GB | 1,000,000,000 bytes |
| GiB | 1,073,741,824 bytes |
| Mbps | Megabits per second |
| MB/s | Megabytes per second |

### Key Points to Remember
1. Computers represent digital information using binary.
2. A bit is a single binary digit.
3. One byte contains 8 bits.
4. Decimal units use powers of 1,000.
5. Binary units use powers of 1,024.
6. Network speeds use bits per second; file sizes commonly use bytes.
7. Divide bits by 8 to convert to bytes.
8. A 512 GB drive corresponds to approximately 476.84 GiB before filesystem overhead.

