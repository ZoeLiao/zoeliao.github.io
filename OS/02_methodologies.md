# Ch2. Methodologies

## 2.1 Terminology
- **IOPS**
    -  Input/output operations per second is a measure of the rate of data transfer operations.
    - For disk I/O, IOPS refers to reads and writes per second.
- **Throughput**
    - The rate of work performed.
- **Response Time**
    - The time for an operation to complete
- **Latency**
    - A measure of time an operation spends waiting to be serviced
- **Utilization**
    - For resources that service requests, utilization is a measure of how busy a resource is, based on how much time in a given interval it was actively performing work.
- **Saturation**
    - The degree to which a resource has queued work it cannot service.
- **Bottleneck**
    - In systems performance, a bottleneck is a resource that limits the performance of the system. Identifying and removing systemic bottlenecks is a key activity of systems performance.
- **Workload**
    - The input to the system or the load applied is the workload.
    - For a database, the workload consists of the database queries and commands sent by the clients. 
- **Cache**
    - A fast storage area that can duplicate or buffer a limited amount of data, to avoid communicating directly with a slower tier of storage, thereby improving performance.
    - For economic reasons, a cache is often smaller than the slower tier.

## 2.2 Models
### 2.2.1 System Under Test (SUT)
- Input (workload) -> System Under Test (affected by Perturbations 擾動?) -> Resulting Performance
- It is important to be aware that perturbations (interference) can affect results, including those caused by scheduled system activity, other users of the system, and other workloads. 

### 2.2.2 Queueing System
- arrival -> Queue -> service center -> departure
- Example: disks

## 2.3 Concepts
### 2.3.1 Latency
- Definition: the time spent waiting before an operation is performed
- Example:
    - DNS latency, TCP connection latency (TCP handshake), TCP data transfer time.

### 2.3.2 Time Scales
- To compare time

### 2.3.3 Trade-Offs
- High-Performance, On-Time, Inexpensive

### 2.3.4 Tuning Efforts
- Performance tuning is most effective when done closest to where the work is performed.

### 2.3.5 Level of Appropriateness
- Whether it is suitable dependes on situation

### 2.3.6 When to Stop Analysis
- When you’ve explained the bulk of the performance problem 
- When the potential ROI is less than the cost of analysis
- When there are bigger ROIs elsewhere.

### 2.3.7 Point-in-Time Recommendations
- The performance characteristics of environments change over time, due to the addition of more users, newer hardware, and updated software or firmware.
- Performance recommendations, especially the values of tunable parameters, are valid only at a specific point in time.
- When changing tunable parameters, it can be helpful to store them in a version control system with a detailed history. (You may already do something similar when using configuration management tools such as Puppet, Salt, Chef, etc.)

### 2.3.8 Load vs. Architecture
- An performance issues may due to
    - problems of loed
    - problems of applications

### 2.3.9 Scalability
- The performance of the system under increasing load is its scalability
- At the begining, it may be linear. However, when it reaches *knee point*, throughput profile departs from linear scalability, as contention for the resource increases. For example, whan a component reaches 100% utilization: the saturation point. It may also occur when a component approaches 100% utilization and queueing begins to be frequent and significant.

### 2.3.10 Metrics
Common types of system performance metrics include:
- Throughput: Either operations or data volume per second
- IOPS: I/O operations per second
- Utilization: How busy a resource is, as a percentage
- Latency: Operation time, as an average or percentile 

- Overhead
    - observer effect: Performance metrics are not free, it can negatively affect the performance of the target of measurement
- Issues
    - metrics can be confusing, complicated, unreliable, inaccurate, and even plain wrong (due to bugs). 
