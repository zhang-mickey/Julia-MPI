## Floyd's Sequential algorithm
main idea:dp
### parallel
<img width="856" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/29190e83-5c09-42a4-adf2-a5119f2809bd">
</br>
<img width="798" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/980fe54b-af3c-404d-85bc-976f70f63655">

</br>
<img width="815" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/a4a729a5-eaa5-4f88-aa66-f4c698c1ac47">

</br>
<img width="811" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/01f2db19-3264-4abe-af91-875d183ddfc6">

</br>

##
In MPI, a communicator represents a group of processes that can communicate with each other. 
(MPI.COMM_WORLD from Julia) is a built-in communicator that represents all processes available in the MPI program. 

The rank of a processor is a unique (integer) identifier assigned to each process within a communicator. It allows processes to distinguish and address each other in communication operations.

## collective communication

MPI.Gather: Gathers data from all processes to a single process.
Each rank sends a message to the root rank (the root rank also sends a message to itself). The root rank receives all these values in a buffer (e.g. a vector).
<img width="327" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/642caac5-3a67-4342-a5a5-51759b1c68ea">

</br>

MPI.Scatter: Distributes data from one process to all processes.
<img width="324" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/d73681b8-b89c-48aa-9dd7-6649ba516d0f">

</br>
MPI.Bcast: Broadcasts data from one process to all processes.
<img width="344" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/280e0699-66cf-44f4-ba35-fad7cce33a02">

</br>
MPI.Barrier: Synchronizes all processes.

It is a good practice to not using the built-in communicators directly, and use a copy instead with MPI.Comm_dup. 

## point to point communication
Point-to-point communications are two-sided: there is a sender and a receiver.

The tag value used in MPI.Send and MPI.Recv! must match
MPI.ANY_TAG is particularly useful when you want to receive messages from different tags without specifying a fixed tag value or when you want to have flexibility in handling different message types.


```
x = 10
@assert x > 0  # This will not raise an error

x = -5
@assert x > 0  # This will raise an AssertionError because x is not positive

```
```
arr = rand(1:100, 1000000)  # create a random array with a million elements

time_taken = @elapsed begin
    sort(arr)
end

println("Time taken to sort the array: $time_taken seconds")

```
```
function my_function(arr)
    @inbounds for i in 1:length(arr)
        # Access elements without bounds checking
        println(arr[i])
    end
end
```

## 
https://docs.julialang.org/en/v1/manual/performance-tips/
##
https://juliaparallel.org/MPI.jl/stable/
##
You will perform experiments on DAS-5. 

Assignment will be graded taking into consideration your
efficiency results under the following case:

4 compute nodes/workers with 1 MPI process per node, with N= 3200 and
R=5 will give you up to 0.15
</br>
<img width="634" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/49c06055-ae59-42a6-8f10-efdd23639502">

</br>
<img width="744" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/6c0ac98e-06e7-43f0-80f8-2ea5f71f6724">

</br>
<img width="793" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/c586a2a6-65a2-4f88-825a-68ad0d031d99">

</br>
<img width="673" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/09a00c3b-c125-48a1-9e9e-79651408a5f2">
</br>
<img width="614" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/e7bd52a6-9bc9-4905-a853-8df34b068650">
</br>
<img width="535" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/923ed76d-7b61-409d-bf10-38edb58fa9e9">
</br>
<img width="621" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/3e471801-0302-4cad-b7eb-c796e606a7a5">
</br>
<img width="648" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/d19d1464-b44f-482a-9e97-c16640edeede">
</br>
基于MPI的并行化Floyd算法
