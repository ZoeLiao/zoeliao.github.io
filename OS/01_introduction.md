# Ch1. Introduction

## 1.1 Systems Performance
- Definition: studies the performance of an entire computer system:
    - single server: software + hardward
    - Distributed systems: multiple servers and applications
- Goal:
    - Improve the end-user experience by reducing:
        - latency
        - computing cost
            - eliminating inefficiencies,
            - improving system throughtput 
            - general tuning
- System performance studies full stack:
    - Full stack:
        - The entinre software stack from the application down to hardware

## 1.2 Roles
- System administrators
- SRE
- application developers
- network engineers
- data-base administrators 
- web administrators
- performance engineera

## 1.3 Activities
- Setting performance objectives and performance modeling for a future product.
- Performance characterization of prototype software and hardware.
- Performance analysis of in-development products in a test environment.
- Non-regression testing for new product versions.
- Benchmarking product releases.
- Proof-of-concept testing in the target production environment.
- Performance tuning in production.
- Monitoring of running production software.
- Performance analysis of production issues.
- Incident reviews for production issues.
- Performance tool development to enhance production analysis. 

## 1.4 Perspectives
- workload analysis
    - top-down
    - application developers
- resource analysis
    - bottom-up
    - role: system administrators

## 1.5 Performance Is Challenging
- 1. Subjective 主觀 
    - Performance is subjective
    - Subjective performance can be made objective by defining clear goals
- 2. Complexity
    - lack of an obvious starting point for analysis
    - cascading failure
        - untanlgle the relationships between components
    - Bottlenecks
    - complexity characteristic of the production workload, and hard to reproducible in a lab env
- 3. Multiple Causes
- 4. Mulitple Performance Issues
    - the performance analyst must quantify the magnitude of issues

## 1.6 Latency
- Definition: a measure of time spent waiting, and is an essential performance metric
- It can be ambiguous without qualifying terms

## 1.7 Observability
- Definition: understanding a system through observation, and classifies the tools that accomplish this 
- Tools:
    - Counters
    - Profiling
    - Tracing
- Not includes benchmark tools (modify the state of the system by performing a workload experiment)
    - because for production env, observability tools should be tried first wherever possible
- **Counters, Statistics, and Metrics**
    - Counters
        - hard-coded in the software, some of which are cumulative and always increment
    - Statistics
    - Metrics
        - a statistic that has been selected to evaluate or monitor a target
    - hierarchy:
        - counters (applications, kernel) -> statistics (performance tools, agents) -> metrics (performance monitoring UIs) -> alters (event processing)
- **Profiling** 
    - the use of tools that perform sampling, e.g., *flame graphs* 
- **Tracing**
    - event-based recording, where event data is captured and saved for later analysis or consumed on-the-fly for custom summaries and other actions.g
    - *tracepoints*: the linux technology for kernel static instrumentation
    - *user statically defined tracing (USDT)*: a static instrumentation technology for user-space software
- **Dynamic Instrumentation**
    -  creates instrumentation points after the software is running, by modifying in-memory instructions to insert instrumentation routines (like debuggers can insert a breakpoint on any functions)
    - 想像 debug 就是是在全黑的房間找問題，而 Dynamic Instrumentation 讓你可以拿手電筒指向任何你想找的地方
- **BPF**
    - originally stood for Berkeley Packet Filter, is powering the latest dynamic tracing tools for Linux

## 1.8 Experimentation
- benchmarking tools 
    - macro-benchmark: simulate a real-world workload
    - micro-benchmark: focus on a specific component, e.g., CPUs, disks, or networks
- Note:
    - On prod env, try observability first

## 1.9 Cloud Computing
- Try to save cost
- performance isloation

## 1.10 Methodologies
- Definition: A way to document the recommended steps for performing various tasks in systems performance

### Linux 60-second analysis checklist
- `uptime`: Load averages to identify if load is increasing or decreasing (compare 1-, 5-, and 15-minute averages).
- `dmesg -T | tail`: Kernel errors including OOM events.
- `vmstat -SM 1` (mac: `vm_stat`): System-wide statistics: run queue length, swapping, overall CPU usage.
- `mpstat -P ALL 1`: Per-CPU balance: a single busy CPU can indicate poor thread scaling.
- `pidstat 1`: Per-process CPU usage: identify unexpected CPU consumers, and user/system CPU time for each process.
- `iostat -sxz 1`: Disk I/O statistics: IOPS and throughput, average wait time, percent busy.
- `free -m`: Memory usage including the file system cache.
- `sar -n DEV 1`: Network device I/O: packets and throughput.
- `sar -n TCP,ETCP 1`: TCP statistics: connection rates, retransmits.
- `top`: Check overview.
