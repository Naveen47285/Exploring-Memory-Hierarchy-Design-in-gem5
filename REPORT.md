# Assignment 3: Exploring Memory Hierarchy Design in gem5

**Course:** MSCS-531 – Computer Architecture  
**Student:** Naveen Nallani  
**Date:** November 2025  

---

## Part 1 – Understanding Memory Hierarchy Design

### Introduction
Memory hierarchy organizes data storage into layers based on speed, cost, and capacity. It ensures faster access to frequently used data while maintaining large, inexpensive storage for less frequently used information. This layered design minimizes average access time and optimizes system performance.

### 1. Memory Hierarchy Design and Its Characteristics
According to GeeksforGeeks (2025), memory hierarchy is structured from CPU registers down to secondary storage and is based on the principle of locality. Each level offers a trade-off between speed, capacity, and cost. Registers and cache provide fast access for frequently used data, while DRAM and secondary storage handle larger datasets with slower access times. As we move down the hierarchy, capacity increases and cost per bit decreases. This balance is vital for system throughput and efficiency.

### 2. Advanced Cache Optimization
Modern caches use prefetching, victim caches, and cache partitioning to reduce miss rates. Prefetching predicts future memory requests, victim caches store recently evicted lines, and partitioning allocates cache space to specific cores or workloads. These techniques maximize throughput by reducing latency.

### 3. Virtual Memory and Virtual Machines
Virtual memory allows each process to use its own virtual address space, translated to physical memory via page tables and a Translation Lookaside Buffer (TLB). When space runs out, page-replacement algorithms like LRU and CLOCK determine which pages to swap. Hypervisors extend this mechanism to virtual machines, mapping guest virtual memory to host physical memory for process isolation and resource efficiency.

### 4. Cross-Cutting Issues and Emerging Trends
Memory hierarchy design balances cost, power, and complexity. Key trends include Compute Express Link (CXL) for shared memory pools, persistent memory for non-volatile storage, AI-assisted cache management, and NUMA-aware scheduling to minimize cross-socket latency.

---

## Part 2 – Implementing and Analyzing Cache Configurations in gem5

### Environment Setup
- **gem5 Version:** 25.0.0.1  
- **Architecture:** x86  
- **Host OS:** Ubuntu 22.04 LTS  
- **Program:** Static Hello World binary  

**Build and Run**
```bash
cd ~/gem5
scons build/X86/gem5.opt -j4
cd ~/exploring-memory-hierarchy-design
gcc hello.c -static -o hello
~/gem5/build/X86/gem5.opt ~/gem5/configs/deprecated/example/se.py -c ~/exploring-memory-hierarchy-design/hello
