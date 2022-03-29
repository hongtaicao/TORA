## Code
System requirements
```
make
g++
```

Download the repository, clean and compile the code

```
make clean
make main.exe
```

Comment out ``Line 25`` of ``algebra/basetype.hpp`` can turn on debug mode, which can produce detailed information. It is required to clean and compile again.

The debug-off mode can be used to reproduce time and space performance of the work. The debug-on mode provides detailed information, e.g., explanation of the configurations, the sizes of intermediate relations, the times of sharing relations

We also provide two compiled binary files ``main-v0.12.exe`` and ``main-v0.12-debug.exe``. They are compiled under a ``Little Endian x86_64 18.04.1-Ubuntu`` machine.

## Datasets
We provide datasets as a file ``dataset.zip``. It contains 7 out of 9 datasets used in the paper as text files. The missing datasets are ``roadca`` and ``Com-LJ`` because of the size limit.

We provide queries as a file ``query.zip``. It contains all queries used in the paper as text files.

## Example Experiments
Reproduce the time and space performance
```
./main.exe bs -d ./p2p.txt -q ./query/Directed3/1.txt
```

Example truncated output
```
...
2021_11_04-06_22_58 TimeCost 0.007 (s) LEAF_BUILDINGBLOCK filter_enable=false LEAF_BINARY_BLOCK case 0
2021_11_04-06_22_58 TimeCost 0.025 (s) TotalCost 0.032 (s) MatchCount 1531 TotalCost_OE 0.032 (s) ./query/Directed3/1.txt MatchOrder [0,1,2] OP_MASKMERGE
v0.12 stop logger: v0.12-detail.csv
v0.12 stop logger: v0.12-best.csv
...
```

Explanation
* The first line shows the time cost of constructing input relations, which is 0.007 second.
* The second line shows the optimization time + the execution time as  0.025 seconds. The total time cost is 0.032 seconds, which is 0.007 + 0.025

Turn off sharing
```
./main.exe bs -leaf 0 -format 3 -c "0,0,0,0;0,1,0,0;0,0,0,1;0,1,0,1" -ablation-share -share-off -d ./p2p.txt -q ./query/Directed3/1.txt
```

Example truncated output
```
...
2021_11_05-06_07_41 TimeCost 0.017 (s) LEAF_BUILDINGBLOCK filter_enable=false LEAF_TEXT_NEIGHBORLIST case 0
2021_11_05-06_07_41 TimeCost 0.019 (s) TotalCost 0.036 (s) MatchCount 1531 TotalCost_OE 0.036 (s) ./query/Directed3/1.txt MatchOrder [0,1,2] OP_MASKMERGE
v0.12 stop logger: v0.12-detail.csv
v0.12 stop logger: v0.12-best.csv
2021_11_05-06_07_41 Exit. 0.227 (s) total elapsed time
...
```

Turn off attribute structure order
```
./main.exe bs -leaf 0 -format 3 -c "0,0,0,0;0,1,0,0;0,0,0,1;0,1,0,1" -ablation-order -d ./p2p.txt -q ./query/Directed3/1.txt
```

Turn off the complement implementation
```
./main.exe bs -leaf 0 -format 3 -c "0,0,0,0;0,1,0,0;0,0,0,1;0,1,0,1" -ablation-complement -d ./p2p.txt -q ./query/Directed3/1.txt
```
