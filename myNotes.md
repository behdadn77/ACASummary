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

# PDF 6 Dynamic Branch Prediction


### Dynamic Branch Prediction
Schemes: 
Dynamic branch prediction is based on two
interacting mechanisms:

**Branch Outcome Predictor:**

To predict the direction of a branch (i.e. taken or not
taken).
* Branch Target Predictor:
To predict the branch target address in case of taken
branch.

These modules are used by the Instruction Fetch
Unit to predict the next instruction to read in the I
cache.

If branch is not taken
PC is incremented.

If branch is taken
BTP gives the target address

### Branch Target Buffer
Branch Target Buffer (Branch Target Predictor)
is a
cache storing the predicted branch target address
for the next instruction after a branch
•
We access the BTB in the IF stage using the
instruction address of the fetched instruction (a
possible branch) to index the cache.

The predicted target address is expressed as PC
relative


### Branch History Table
Branch
History
Table
(or
Branch
Prediction
Buffer):

Table
containing
1 bit for
each
entry
that
says
whether
the
branch
was
recently
taken
or
not
.

Table
indexed
by the
lower
portion
of the
address
of the
branch
instruction
.

Prediction
:
hint
that
it
is
assumed
to be
correct
, and
fetching
begins
in the
predicted
direction
.

If
the
hint
turns
out to be
wrong
, the
prediction
bit
is
inverted
and
stored
back. The pipeline
is
flushed
and the
correct
sequence
is
executed
.

The
table
has
no
tags
(
every
access
is
a hit) and the
prediction
bit
could
has
been
put
there
by
another
branch
with the
same
low

order
address
bits:
but
it
does
not
matter
.
The
prediction
is
just a
hint



#### A misprediction occurs when

The
prediction
is
incorrect
for
that
branch
, or
 
The
same
index
has
been
referenced
by
two
different
branches
, and the
previous
history
refers
to the
other
branch
 
To solve
this
problem
it
is
enough
to
increase
the
number
of
rows
in the BHT or to use a
hashing
function
(
such
as
in
GShare
)


## 2 bit Branch History Table
The prediction must miss twice before it is
changed.

**In a loop branch, at the last loop iteration, we
do not need to change the prediction.**

For each index in the table, the 2 bits are used
to encode the four states of a finite state
machine



## n-bit Branch History Table
•
Generalization: n-bit saturating counter for each
entry in the prediction buffer.

The counter can take on values between 0 and 2^n-1

When the counter is greater than or equal to one-half of
its maximum value (2^n-1), the branch is predicted as
taken.

Otherwise, it is predicted as untaken.
•
As in the 2-bit scheme, the counter is incremented
on a taken branch and decremented on an untaken
branch.
•
Studies on n-bit predictors have shown that 2-bit
predictors behave almost as well.

## Correlating Branch Predictors

BHT predictors use only the recent behavior of
a single branch to predict the future behavior of
that branch.

Basic Idea: the behavior of recent branches are
correlated, that is the recent behavior of other
branches rather than just the current branch
(we are trying to predict) can influence the
prediction of the current branch.


Branch predictors that use the behavior of other
branches to make a prediction are called
Correlating Predictors
or
2-level Predictors.

Example a (1,1) Correlating Predictors means a
1-bit predictor with 1-bit of correlation: the
behavior of last branch is used to choose
among a pair of 1-bit branch predictors.



***I skipped a lot of parts that are maybe important***


## GA Predictor

The Branch History Table (BHT) and Global History Register with Global Prediction (GAg) are both techniques used for dynamic branch prediction in computer architecture, but they operate differently and have distinct characteristics. Here’s a comparison between the two:

### Branch History Table (BHT)

**Description:**
- A BHT is a simple table used for branch prediction where each entry in the table corresponds to a branch instruction. It records the outcomes (taken or not taken) of recent executions of that branch.

**Operation:**
- Each entry typically consists of a counter or a set of bits that are updated based on the actual outcome of the branch instruction. For example, a 2-bit counter can represent four states to indicate how likely a branch is to be taken.

**Advantages:**
- **Simplicity:** Easy to implement and understand.
- **Local Prediction:** Works well for branches that have a consistent behavior pattern.

**Disadvantages:**
- **Limited Context:** Only considers the history of individual branches, which may not capture complex patterns or correlations with other branches.
- **Storage Requirements:** Requires a table entry for each branch, which can be large for programs with many branches.

### Global History Register with Global Prediction (GAg)

**Description:**
- GAg uses a global history register (GHR) that records the outcomes of the most recent branches (usually as a shift register) and a global pattern history table (PHT) indexed by this global history.

**Operation:**
- The GHR is a single register that captures the history of the last N branches (regardless of which branch instruction they were).
- The PHT is indexed using the GHR, and it stores the prediction for the combination of recent branch outcomes.
- This method leverages the global branch history to make predictions, capturing more complex patterns across different branches.

**Advantages:**
- **Global Context:** Takes into account the outcomes of multiple branches, potentially improving prediction accuracy for branches that are correlated.
- **Captures Complex Patterns:** More effective for programs where branch outcomes are interdependent.

**Disadvantages:**
- **Complexity:** More complex to implement than a simple BHT.
- **Longer History Management:** Managing and updating the global history register can be more challenging.
- **Potential for Conflicts:** Multiple branches may map to the same entry in the PHT, causing aliasing and reducing prediction accuracy.

### Summary Table

| **Aspect**                   | **Branch History Table (BHT)**                                      | **Global History Register with Global Prediction (GAg)**               |
|------------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|
| **History Type**             | Local to each branch                                                | Global across all branches                                             |
| **Storage**                  | Table indexed by branch address                                      | Global History Register (GHR) and Pattern History Table (PHT)          |
| **Prediction Basis**         | Recent outcomes of individual branches                              | Combined recent outcomes of multiple branches                          |
| **Complexity**               | Simple                                                              | More complex                                                           |
| **Accuracy**                 | Good for independent branches                                       | Higher for interdependent branches                                     |
| **Implementation**           | Straightforward                                                     | Requires management of global history and handling potential aliasing  |
| **Advantages**               | Simple, easy to implement, effective for consistent branch patterns | Captures global patterns, potentially more accurate for correlated branches |
| **Disadvantages**            | Limited context, large storage for many branches                    | Complex, potential aliasing issues, more challenging to implement       |

In essence, while BHT focuses on individual branch histories, GAg leverages a global approach to capture broader execution patterns, which can improve prediction accuracy in scenarios with interdependent branches.


# PDF 7 - Instruction Level Parallelism
Pipeline performance
•
Pipeline CPI =
Ideal pipeline CPI
+
Structural
Stalls
+
Data Hazard Stalls
+
Control Stalls

Ideal pipeline CPI
: measure of the maximum
performance attainable by the implementation

* Structural hazards
: HW cannot support this
combination of instructions

* Data hazards
: Instruction depends on result of prior
instruction still in the pipeline

* Control hazards
: Caused by delay between the
fetching of instructions and decisions about changes
in control flow (branches, jumps, exceptions)

Hazards limit performance
* Structural
: need more HW resources
* Data
: need forwarding, compiler scheduling
* Control
: early evaluation & PC, delayed branch, predictors




## Complex Pipelining

Pipelining becomes complex when we want high performance in the
presence of:
Long latency or partially pipelined floating

point units
Multiple function and memory units
Memory systems with variable access time
Precise exception

## Issues in Complex Pipeline Control

* Structural conflicts at the execution stage if some FPU or memory
unit is not pipelined and takes more than one cycle
Structural conflicts at the write

* back stage
due to variable
latencies of different functional units


* Out of order write hazards due to variable latencies of different FUs

### Complex In Order Pipeline
**Delay writeback so all
operations have same latency
to WB stage**
Instructions commit in order, simplifies
precise exception implementation

### The following checks need to be made before the Issue
stage can dispatch an instruction
>
Is the required function unit available?
>
Is the input data available? RAW
>
Is it safe to write the destination? WAR/WAW
>
Is there a structural conflict at the WB stage?

## Getting higher performance
**In a pipelined machine, actual CPI is derived as:**

```
CPIpipe=CPIideal+Structural_stalls+Data_hazard_stalls+Control_stalls
```

Reduction of any right-hand term reduces
CPI
pipe
(increase Instructions Per Clock–IPC)

**Technique to increase
CPI
pipe
could create further
problems with hazards**

To reach higher performance (for a given technology)
–
more parallelism must be extracted from the program



Dependences must be detected and solved, and
instructions must be ordered (
scheduled
)
so as to
achieve highest parallelism of execution compatible
with available resources.



**If two instructions are dependent, they cannot execute
in parallel: they must be executed in order or only
partially overlapped**




## Name Dependences

**when 2 instructions use the same
register or memory location (called name), but there is no flow of
data between the instructions associated with that name**

> Antidependence
: when j writes a register or memory location that
instruction
i
reads. The original instructions ordering must be
preserved to ensure that
i
reads the correct value.

> Output Dependence
:
when
i
and j write the same register or
memory location. The original instructions ordering must be
preserved to ensure that the value finally written corresponds to j.


* Name dependences are not true data dependences,
since there is no value (no data flow) being transmitted
between instructions.
* If the name (register number or memory location) used
in the instructions could be changed, the instructions do
not conflict.
* Dependences through memory locations are more
difficult to detect (“
memory disambiguation
”
problem),
since two addresses may refer to the same location but
can look different.
* Register renaming can be more easily done.
* Renaming can be done either statically by the compiler
or dynamically by the hardware.



## Data Dependences and Hazards

A data/name dependence can potentially generate
a data hazard (RAW, WAW, or WAR), but the actual
hazard and the number of stalls to eliminate the
hazards are a property of the pipeline.
* RAW hazards correspond to true data dependences.

* WAW hazards correspond to output dependences

* WAR hazards correspond to
antidependences



**Dependences are a property of the program, while
hazards are a property of the pipeline**

## Control Dependences
**determines the ordering of
instructions**

* Instructions execution in program order to ensure
that an instruction that occurs before a branch is
executed before the branch.
* Detection of control hazards to ensure that an
instruction (that is control dependent on a branch) is
not executed until the branch direction is known.

control
dependence is not the critical property that must be
preserved.

## Program Properties
Program Properties

**Exception
behavior**
: Preserving exception
behavior
means that any changes in the ordering of instruction
execution must not change how exceptions are
raised in the program

**Data flow:** Actual flow of data values among
instructions that produces the correct results and
consumes them


