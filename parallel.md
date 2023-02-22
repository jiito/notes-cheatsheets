# Parallel 


## ISPC

`export` indecates that the function should be made available to C++

`uniform` indicates that the variable has the same value for all the concurrently-executing programs. **All values passed to the the application must be uniform**

`foreach` specifies parallel iteration over n-dimensional data

ISPC's execution model is SPMD-- which means the program compiles down to run in parallel across the elements of the SIMD unit. 