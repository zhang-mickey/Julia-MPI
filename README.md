# Julia-MPI

## Performance metric

### speedup
```
Speedup =(Time on 1 CPU)/(Time on p CPUs)
```
can speedup be super linear?(yes) (theoretically speedup can never exceed the number of processing elements p)
Because the parallel version may perform less work than a sequential algorithm.
Two examples
(1)Negative search overhead
more processing units gives overall more registers per subtask,memory hit patterns, simply better.
如果需要搜索一个教室所有的学生（一个 m*n 的矩阵），需要按列将每个学生都搜索一遍，如果安排m个处理器，每个搜索一行，可能我们要找到人就在最后一行第一个，那么一下子就找到了。当然考虑最坏的情况，speedup还是p倍，但是平均情况会好很多。
(2)Better caching behavior
a random process that searches space for a result is now divided into 1024 searchers covering more space at once so finding the solution faster is more probable. 
如果用顺序算法只有一个处理器，很可能大部分数据都存在main memory里面了，而如果用很多个处理器，我们可以将所有的数据直接存在 cashe里面！基本就不需要花时间读取了。
### Amdahl's law
<img width="442" alt="image" src="https://github.com/zhang-mickey/Julia-MPI/assets/145342600/05657f3f-0585-4294-bc13-b47d326e2608">



### Efficiency
Efficiency =speedup/p

## Parallel machines and architecture
### Processor organizations
* Diameter * (maximum distance)
Bisection width(minimum number of edges that should be removed to split the graph into 2-almost-equal halves)
mesh
binary tree
hypercube
### Types pf parallel machines
#### Processor arrays
Instructions can operate on vectors
communicate with other PEs through a network
#### Shared-Memory Multiprocessors
#### Distributed-Memory Multicomputers
Processors communicate by sending messages over a network
##  Parallel Algorithm
### Barnes-Hut
### ASP
### IDA*
#### Approaches
##### TDS(Transposition Driven Scheduling)
efficiently handles so-called transposition tables on distributed-memory systems.
use  asynchronous communication and message aggregation
obtain far better performance than partition and replicate the tables
</br>
The problem of efficiently sharing transposition tables in distributed search.
why asynchronous communication works well than replication and partitioning to distribute these tables
### parallelizing the traininf process
wxplain the difference and optimizations to scale up DL
#### Data parallelism
Training data is split over the compute nodes
All compute nodes have identical copy of the DL model
Advantage:
Scales well for compute-intensive operations
</br>
disadvandage: 

</br>
Synchronization bottleneck, need large batches
</br>
Model must fit in memory on each node-data parallelism fails if the model is too big for 1 node
#### Model parallelism
Each node has different part of the DL model(split the model [Reinforcement Learning +Reduced memory footprint])-Output signal is propagated to node with next layer
disadvandage:Heavy communication; little parallelism(stalling)
