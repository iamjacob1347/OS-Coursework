# Week 3: Application Selection for Performance Testing

## Application Selection Matrix

| Application | Type | Purpose | Why Chosen |
|-------------|------|---------|------------|
| **stress-ng** | CPU-intensive | Generates various types of CPU load | Can simulate different CPU workloads, and being lightweight |
| **memtester** | RAM-intensive | Tests system memory for errors and measures performance | Specifically designed for memory testing and can allocate and test specific amounts of RAM |
| **iozone3** | I/O-intensive | Filesystem benchmark tool | Can test different file sizes and access patterns |
| **iperf3** | Network-intensive | Network performance measurement tool | Can test different protocols and packet sizes |
| **nginx-light** | Server Application | Lightweight web server | Easy to start/stop for testing and can measure request/response performance |
| **htop** | Monitoring | Interactive process viewer | Colorful display and easier to read |
| **sysstat** | Monitoring | System performance tools collection | Performance data collection and can log metrics over time for analysis. |

**Selection Rationale:**
I chose these applications because they:
1. Cover all workload types required by the assignment
2. Are lightweight and won't overwhelm my virtual environment
3. Have clear measurement outputs for quantitative analysis
4. Are commonly used in industry for performance testing
5. Can be controlled for consistent testing

## Installation Documentation

SSH connection established from Workstation VM terminal

## Expected Resource Profiles

### stress-ng
- **Primary Resource:** CPU
- **Expected CPU Usage:** 90-100% on all specified CPU cores when active
- **Memory Usage:** Low to moderate (50-200MB for test processes)
- **Disk I/O:** Minimal (only logging if enabled)
- **Network Usage:** None
- **Test Command:** stress-ng --cpu 4 --timeout 60s

### memtester
- **Primary Resource:** System Memory (RAM)
- **Expected Memory Usage:** Configurable allocation (planned: 512MB, 1GB, 1.5GB tests)
- **CPU Usage:** Moderate (memory access patterns generation)
- **Disk I/O:** Potentially high if system swaps to disk (will monitor swap usage)
- **Network Usage:** None
- **Test Command:** memtester 1G 3 *(1GB for 3 iterations)*

### iozone3
- **Primary Resource:** Disk I/O
- **Expected Disk Activity:** High sequential and random read/write operations
- **CPU Usage:** Moderate (I/O scheduling, data processing)
- **Memory Usage:** Moderate (file buffer caching)
- **Network Usage:** None
- **Test File Sizes:** 100MB, 500MB, 1GB files for different test scales

### iperf3
- **Primary Resource:** Network Bandwidth
- **Expected Network Usage:** Maximum available bandwidth between VMs
- **CPU Usage:** Moderate (packet processing, TCP stack)
- **Memory Usage:** Low (socket buffers)

### nginx-light
- **Primary Resource:** Mixed (CPU for request processing, Network for data transfer)
- **Expected Baseline Usage (Idle):** 
  - CPU: <1%
  - Memory: 20-30MB
  - Network: Minimal
- **Expected Load Usage (Under Test):**
  - CPU: 10-30% depending on request rate
  - Memory: 30-50MB
  - Network: HTTP traffic on port 80

## 4. Monitoring Strategy

### Overall Approach
All monitoring will be performed remotely from the Workstation VM using SSH to execute monitoring commands on the Server VM. This simulates real-world server administration and avoids adding monitoring overhead to the Server VM during tests.

#### **Tools Used:**
- mpstat: CPU statistics (per-core breakdown)
- vmstat: Memory, processes, I/O, CPU activity
- iostat: Disk I/O statistics
- Manual logging: Screenshots and command output capture
