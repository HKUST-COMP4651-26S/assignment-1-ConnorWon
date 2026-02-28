[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/aQEb8Lmc)
# COMP4651 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Saturday

---

### Name: Connor Yeeho Won
### Student Id: 21335056
### Email: cywon@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

**Measurement Tool:** Phoronix

**CPU Performance:** pts/compress-7zip test suite
- It tests CPU performance by calculating the throughput of the CPU (MIPS) while the system compresses and decompresses generated test data. There are no parameters to set for this test, so I just used the default settings. 
- The measurement result returned is MIPS (million instructions per second) which describes the throughput of the CPU.

**Memory Performance:** pts/ramspeed test suite
- It tests the memory performance by performing various memory operations. There are two parameters to set for the test suite: the memory operation (benchmark) and the type of data being operated on (type). I decided to select benchmark - average, type - floating point, because based on the uploaded results data for the test suite on openbenchmark.com, this run configuration has the least amount of variation in the test run results. 
- The measurement result returned is MB/s, which represents the throughput of data between Memory and the CPU.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` | 3630 MIPS Compression / 3095 MIPS Decompression | 10427.45 MB/s |
    | `t2.medium`  | 9487 MIPS Compression / 5814 MIPS Decompression | 18420.96 MB/s |
    | `c5d.large` | 7548 MIPS Compression / 4903 MIPS Decompression | 13756.43 MB/s |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` | 4770 Mbps      | 0.200 ms |
    | `m5.large` - `m5.large`   | 4950 Mbps      | 0.197 ms |
    | `c5n.large` - `c5n.large` | 4960 Mbps      | 0.148 ms |
    | `t3.medium` - `c5n.large` | 4850 Mbps      | 0.175 ms |
    | `m5.large` - `c5n.large`  | 2860 Mbps      | 0.560 ms |
    | `m5.large` - `t3.medium`  | 2750 Mbps      | 0.677 ms |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      | 37.0 Mbps      | 55.494 ms|
    | N. Virginia - N. Virginia | 4190 Mbps      | 0.223 ms |
    | Oregon - Oregon           | 4758 Mbps      | 0.171 ms |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
