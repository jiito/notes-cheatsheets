# Parallel 

## Definitions
**Full Duplex**: A communication channel that allows simultaneous transmission and reception of data. 
**Half Duplex**: A communication channel that allows only one direction of transmission at a time.


## Abstraction vs Implementation

## ISPC

`export` indecates that the function should be made available to C++

`uniform` indicates that the variable has the same value for all the concurrently-executing programs. **All values passed to the the application must be uniform**

`foreach` specifies parallel iteration over n-dimensional data

ISPC's execution model is SPMD-- which means the program compiles down to run in parallel across the elements of the SIMD unit. 

**Flow:**
1. A number of *ispc* programs start running in parallel
2. This group is called a **gang**

The *ispc* program typically describes the behavior of a single program instance. A gang of them executes together on different data.

```c
float func(float a, float b) {
     return a + b / 2.;
}
```
For example, the above function could be called in parallel on N different values of a and b. 

**It is exectued within the same hardware thread and context as the application that called it.** Instead, a gang is mapped to the SIMD lanes of the current processor.

### Control Flow 
Program instances can follow other paths than the ones in their gangs. 

### Parallel Programming Basics
**Creating a program:**
1. Indentify work that can be done in parallel
2. Partition the work amongst the computing resources 
3. Manage communication between the parallel programs
  - minimize communication to increase performance

#### Decomposition
*Breaking the computation into a collection of tasks*
The number of tasks sets the upper bound to the speedup 

For **Amdahls Law** we must have a high portion of the computation that can be parallelized.

#### Assignment
*Assigning tasks to computing resources*
- **Static assignment**: the tasks are assigned to the computing resources before the program starts (C++ threads)
- **Dynamic assignment**: the tasks are assigned to the computing resources during the program execution (ISPC Tasks)
Goals: 
- Minimize communication
- Good work load balance (load balancing)


Dynamic Assignment with ISPC Tasks:
- ISPC assigns tasks to worker threads
- Want to have more tasks than worker threads because this will overcome load imbalance

#### Orchestration 
*Managing communication between parallel programs*

**Barriers:** an all-to-all synchronization point. All threads must reach the barrier before any can continue.


## Link Layer 
*Responsible for sending and receiving frames*

- Does not discern meaning from the data (opaque)
