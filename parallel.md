# Parallel 

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