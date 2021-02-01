# GraphDP
GraphDP is an efficient storage system towards high throughput of concurrent graph processing jobs, it can be integrated into existing out-of-core graph processing systems to reduce the storage and data access overhead. GraphDP uses a novel dynamic I/O scheduling strategy, which enables the graph data to be loaded in an optimal I/O mode and effectively reduces the redundant data loaded into the memory and cache. Meanwhile, GraphDP preferentially stores frequently accessed graph data in the memory via an efficient caching mechanism, which further reduces the data access overhead.

## Integrate with out-of-core graph processing system
Take GridGraph as an example:

### Compilation
The requirements and the compiled method are same as the original systems. To compile:
```
make
```
### Preprocessing
The original graph data needs to be partitioned into the grid format for GridGraph:
```
./bin/preprocess -i [input path] -o [output path] -v [vertices] -p [partitions] -t [0=unweighted, 1=weighted]
```
The graph partitions need to be further logically labeled into chunks:
```
./bin/Preprocessing [path]  [cache size in MB] [graph size in MB] [memory budget in GB]
```
### Running Applications
We submit concurrent jobs(PageRank, WCC, BFS, SSSP) through the concurrent_jobs file:
```
./bin/concurrent_jobs [path] [number of submissions] [number of iterations] [start vertex id] [cache size in MB] [graph size in MB] [memory budget in GB]
```