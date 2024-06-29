# PDF3 - Paralleism


Understanding the differences between coarse-grained, fine-grained, simultaneous multithreading (SMT), and superscalar architectures involves exploring their distinct approaches to processing instructions and managing computational resources. Here are the key points for each:

### Coarse-Grained Multithreading

**Advantages:**
1. **Simplicity:** Easier to implement compared to fine-grained and SMT.
2. **Reduced Context Switching Overhead:** Since the switching happens at a higher granularity, there's less frequent context switching which can reduce overhead.
3. **Effective Use of Pipeline:** When one thread stalls, another can be executed, thus keeping the pipeline busy.

**Disadvantages:**
1. **Lower Resource Utilization:** During thread switching, resources might be underutilized as the switching happens at the end of a process or block of instructions.
2. **Latency:** Higher latency in switching between threads since it happens less frequently compared to fine-grained multithreading.

### Fine-Grained Multithreading

**Advantages:**
1. **Higher Resource Utilization:** By switching between threads more frequently (often every clock cycle), resources are used more efficiently.
2. **Reduced Latency in Pipeline Stalls:** Frequent switching helps in hiding latencies due to pipeline stalls, thus keeping the execution units busy.

**Disadvantages:**
1. **Complex Implementation:** Requires more complex hardware to manage the frequent switching.
2. **Increased Overhead:** More frequent context switching can increase the overhead.

### Simultaneous Multithreading (SMT)

**Advantages:**
1. **Maximizes Resource Usage:** Allows multiple threads to be executed simultaneously within a single CPU core, leading to higher utilization of CPU resources.
2. **Improved Throughput:** Can significantly increase the throughput of the system as multiple instructions from different threads are executed in parallel.
3. **Latency Hiding:** Similar to fine-grained multithreading, SMT can hide latencies more effectively.

**Disadvantages:**
1. **Complexity:** Very complex to implement due to the need to manage multiple threads and ensure they don't interfere with each other.
2. **Resource Contention:** Threads may compete for the same resources, leading to potential contention and reduced performance.
3. **Security Concerns:** Increased complexity can lead to security vulnerabilities, such as side-channel attacks (e.g., Spectre and Meltdown).

### Superscalar

**Advantages:**
1. **Instruction-Level Parallelism:** Can execute multiple instructions simultaneously, increasing the instruction throughput.
2. **Higher Performance:** By dispatching multiple instructions to different execution units in a single cycle, performance is significantly enhanced.
3. **Dynamic Scheduling:** Can dynamically schedule instructions out of order to maximize resource usage and minimize stalls.

**Disadvantages:**
1. **Complexity and Cost:** The hardware required to manage multiple pipelines and handle out-of-order execution is complex and expensive.
2. **Power Consumption:** Higher power consumption due to increased hardware complexity.
3. **Diminishing Returns:** Beyond a certain point, adding more execution units yields diminishing returns due to instruction dependencies and the difficulty of finding sufficient parallelism.

### Summary

- **Coarse-Grained Multithreading**: Simpler, lower resource utilization, less frequent switching.
- **Fine-Grained Multithreading**: Higher resource utilization, frequent context switching, more complex.
- **Simultaneous Multithreading (SMT)**: Maximizes resource usage, complex, potential for resource contention and security issues.
- **Superscalar**: High instruction throughput, complex and costly, diminishing returns beyond a certain level of parallelism.

Each approach has its own set of trade-offs and is suitable for different types of applications and workloads.


Thread-level parallelism (TLP) and instruction-level parallelism (ILP) are two strategies for improving the performance of processors by parallelizing workloads, but they operate at different levels and have distinct characteristics. Here's a detailed comparison of TLP and ILP, including their advantages and disadvantages:

### Thread-Level Parallelism (TLP)

**Definition:**
TLP refers to the ability of a processor to execute multiple threads or processes concurrently. This can be achieved through techniques such as multithreading (e.g., SMT, coarse-grained, fine-grained) and multi-core processors.

**Advantages:**
1. **Higher Throughput:** Multiple threads can be executed simultaneously, increasing overall system throughput.
2. **Better Resource Utilization:** By running multiple threads, processors can keep more of their execution units busy, especially when some threads are stalled due to waiting for data or other resources.
3. **Latency Tolerance:** TLP can help hide latencies by switching to other threads when one is waiting for I/O operations or memory access.
4. **Scalability:** Multi-core architectures can be scaled by adding more cores to handle additional threads.

**Disadvantages:**
1. **Complexity:** Managing multiple threads requires complex hardware and software support, including scheduling, synchronization, and context switching.
2. **Resource Contention:** Multiple threads might compete for shared resources such as caches, memory, and I/O bandwidth, leading to contention and potential performance degradation.
3. **Overhead:** Thread management introduces overhead in terms of context switching and synchronization, which can affect performance if not managed efficiently.

### Instruction-Level Parallelism (ILP)

**Definition:**
ILP refers to the ability of a processor to execute multiple instructions from a single thread simultaneously. This is typically achieved through techniques like pipelining, superscalar execution, and out-of-order execution.

**Advantages:**
1. **Increased Instruction Throughput:** By executing multiple instructions concurrently, ILP can significantly improve the performance of a single thread.
2. **Efficient Use of Execution Units:** Techniques like superscalar execution and out-of-order execution make effective use of the processor's execution units, minimizing idle time.
3. **Reduced Latency:** ILP techniques can help reduce the execution time of individual instructions, leading to lower overall latency for a single thread.

**Disadvantages:**
1. **Complex Hardware:** Implementing ILP requires sophisticated hardware mechanisms, such as multiple execution units, complex scheduling logic, and dependency checking, which increases design complexity and cost.
2. **Diminishing Returns:** Beyond a certain point, adding more parallel execution units yields diminishing returns due to instruction dependencies and limited parallelism in the instruction stream.
3. **Power Consumption:** The additional hardware required for ILP can lead to higher power consumption, which is a critical consideration for modern processors.

### Summary

- **TLP (Thread-Level Parallelism)**
  - **Focus:** Multiple threads/processes.
  - **Techniques:** Multithreading (SMT, coarse-grained, fine-grained), multi-core processors.
  - **Advantages:** Higher throughput, better resource utilization, latency tolerance, scalability.
  - **Disadvantages:** Complexity, resource contention, overhead.

- **ILP (Instruction-Level Parallelism)**
  - **Focus:** Multiple instructions from a single thread.
  - **Techniques:** Pipelining, superscalar execution, out-of-order execution.
  - **Advantages:** Increased instruction throughput, efficient use of execution units, reduced latency.
  - **Disadvantages:** Complex hardware, diminishing returns, power consumption.

### Practical Use Cases

- **TLP** is highly effective in environments where workloads can be divided into independent threads, such as server applications, parallel computing tasks, and multitasking operating systems.
- **ILP** is beneficial for improving the performance of individual applications and programs, particularly those that cannot easily be parallelized at the thread level, such as many legacy applications and single-threaded workloads.

Both TLP and ILP are essential for modern processors, and they are often used in combination to achieve optimal performance across a wide range of applications and workloads.


## Flynn Taxonomy (1966)
SISD: Single Instruction Single Data Uniprocessor systems

MISD: Multiple Instruction Single Data.
No practical configuration and no commercial
systems

SIMD: Single Instruction Multiple Data

Simple programming model, low overhead,
flexibility, custom integrated circuits

MIMD: Multiple Instruction Multiple Data
Scalable, fau## PDF3 - Paralleism


# PDF 4, 5 Branch Hazards and Static Branch Prediction Technique

Conditional Branch Instruction:
the branch is taken
only if the
condition
is satisfied.
The
branch target address (BTA)
is stored in the
Program Counter (PC)
instead of the address of the
next instruction in the sequential instruction stream



### Execution of conditional branches

stage MIPS pipeline

* Branch Outcome and Branch Target Address are ready
at the end of the EX stage (3
rd
stage)
* Conditional branches are solved when PC is updated
at the end of the ME stage (4
th
stage)


Control hazards reduce the performance from the
ideal speedup gained by the pipelining since they can
make it necessary to stall the pipeline


### Branch Hazards
To feed the pipeline we need to fetch a new
instruction at each clock cycle, but the branch
decision (to change or not change the PC) is taken
during the MEM stage.
This delay to determine the correct instruction to
fetch is called
Control Hazard or Conditional Branch
Hazard

### Forwarding
Data forwarding uses temporary results stored in the
pipeline registers instead of waiting for the write back
of results in the RF.
We need to add multiplexers at the inputs of ALU to
fetch inputs from pipeline registers to avoid the
insertion of stalls in the pipeline.


### Early Evaluation of the PC
MIPS processor compares registers, computes branch
target address and

With the branch decision made during ID stage, there
is a reduction of the cost associated with each branch
(branch penalty)
:
We need only
one
clock
cycle stall
after each branch
Or a
flush
of only
one
instruction following the branch



## Delayed Branch Technique
The MIPS compiler always schedules a branch
independent instruction after the branch.
The behavior of the delayed branch is the same
whether or not the branch is taken.

I understand. Here’s the table summarizing the three methods used to fill the branch delay slot: from the target of the branch, from the fall-through path, and from before the branch:

| **Method**                  | **Description**                                         | **Advantages**                             | **Disadvantages**                         |
|-----------------------------|---------------------------------------------------------|--------------------------------------------|-------------------------------------------|
| **From Target of the Branch**       | Move an instruction from the branch target into the delay slot.   | Efficient if the branch is taken; reduces wasted cycles.       | Ineffective if the branch is not taken; can complicate pipeline management. |
| **From Fall-Through Path**     | Move an instruction from the fall-through path (next sequential instruction) into the delay slot. | Utilizes the slot when the branch is not taken. | Ineffective if the branch is taken; needs careful selection to avoid hazards. |
| **From Before the Branch** | Move an instruction that appears before the branch into the delay slot.     | Simple and straightforward, no additional instructions needed. | Limited by dependencies and ordering constraints.       |

### Summary:

- **From Target of the Branch:** Best if the branch is frequently taken; may cause issues if not taken.
- **From Fall-Through Path:** Useful when the branch is rarely taken; limited use if the branch is usually taken.
- **From Before the Branch:** Simple to implement; constrained by instruction dependencies and ordering.