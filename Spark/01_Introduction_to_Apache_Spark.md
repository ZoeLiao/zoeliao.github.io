# 1. Introduction to Apache Spark: A Unified Analytics Engine 

## What is Apache Spark
- Apache Spark is a unified engine designed for large-scale distributed data processing.
- It borrowed the idea from Hadoop Map-Reduce, but enhance the system by make it:
    - highly fault tolerant
    - embarrassingly parallel
    - faster by supporting in-memory storage for intermediate results between iterative and interactive map and reduce computations
        - Because of lacking efficient data sharing, Hadoop is not good at:
            - Iterative Jobs (迭代式運算), e.g., ML
            - Iteractive Analyst (交互式分析), e.g., Markov matrix
    - offer easy and composable APIs in multiple languages as a programming model:
        - ML: MLlib
        - SQL for interactive queries: Spark SQL
        - stream processing: Structured Streaming
        - graph processing: GraphX
    - support other workloads in a unified manner 

### History
- 2009: Designed by RAD Lab (UC Berkeley)
- 2014: Apache Spark 1.0 was released.

## The 4 Design Philosophy Centers of Spark 

### 1. Speed
- DAG scheduler and query optimizer:
    - construct an efficient computational graph that can usually be decomposed into tasks that are executed in parallel across workers on the cluster. 
- Tungsten:
    - Its physical execution engine, Tungsten, uses whole-stage code generation to generate compact code for execution.
- With all the intermediate results retained in memory and its limited disk I/O, this gives it a huge performance boost.

### 2. Ease of Use
- Resilient Distributed Dataset (RDD, 彈性分散式資料集):
    - Is a set of partitions (*splits* in Hadoop) 
    - supports 2 type of operations that you can use to build big data applications in familiar languages:
        - 1. Transformations: is a lazy function that produces new RDD from the existing RDDs. 
        - 2. Actions: give non-RDD values which are stored to drivers or to the external storage system. 

### 3. Modularity (模塊化)
- Spark operations can be applied across many types of workloads and expressed in any of the supported programming languages: Scala, Java, Python, SQL, and R.

### 4. Extensibility
- Spark focuses on its fast, parallel computation engine rather than on storage.
- Spark decouple *storage* and *compute*, so you can read data stored in myriad sources, and process it all in memory.

### 5. Unified Analytics
- Spark replaces all the separate batch processing, graph, stream, and query engines with a unified stack of components that addresses diverse workloads under a single distributed fast engine.
