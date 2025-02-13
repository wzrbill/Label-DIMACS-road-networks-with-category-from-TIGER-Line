### Purpose: 
The purpose of this notebook is to attach category of each edge of DIMACS road networks.
### Source: 
We use TIGER/Line dataset from DIMACS to attach categories to edges
Please find detailed description of road category from [Census](https://www2.census.gov/geo/tiger/TIGER1992/Documentation/APPENDXE.txt)
### Approach: 
   * 1. We first download target road network from 
    http://www.diag.uniroma1.it/challenge9/download.shtml, NY for the rest of description.
    
   * 2. Then we download all the TIGER/Line from 
       http://www.diag.uniroma1.it/challenge9/data/tiger/, and we merge them into USA_ALL.tmp for reference.
       merge.cpp can be found at "Merging of two or more files" on the same webpage,
       and compile it to 'merge.out' before running
       
   * 3. We use USA_ALL.tmp as dictionary to guide the labeling process of target road network, and
       save it as USA-road-l.NY.gr in the format of DIMACS.

   * 4. We rebalance the number of labels by first sort labels by descending order of their frequencies.
        And then we merge them by set the interval as $s$ and $e = math.floor(s+\frac{(len(key_lis) - i -1 )}/{l_size} + 1)$


### File Format
TIGER/Line file format
```c++
The format of the uncompressed file is very simple. It is a whitespace-separated list of numbers:
- Number of nodes
- For each node:
 id
 longitude
 latitude
- Number of edges
- For each edge:
 id of the source node
 id of the target node
 travel time
 spatial distance in meters
 road category
```
Fragment of data from TIGER/Line NY.tmp
```c++
716215
0 -73894888 42697724
1 -73765666 42635380
2 -73765927 42635158
3 -73766842 42634190
4 -73766953 42634206
5 -73769565 42634679
...
897451
0 0
0 0 41
1 2
81.543055103891703084 32.617222041556701129 41
3 4
23.118078201258498439 9.2472312805033993754 41
4 5
549.78593925117002073 219.91437570046801397 41
5 6
143.27298033774900432 57.309192135099699783 41
6 7
...
```
Fragment of data from road network NY.gr
```c++
c 9th DIMACS Implementation Challenge: Shortest Paths
c http://www.dis.uniroma1.it/~challenge9
c TIGER/Line graph USA-road-d.NY
c
p sp 264346 733846
c graph contains 264346 nodes and 733846 arcs
c
a 1 2 803
a 2 1 803
a 3 4 158
a 4 3 158
a 5 6 774
a 6 5 774
a 7 8 1531
...
```

### WorkFlow:
 download merge.cpp from http://www.diag.uniroma1.it/challenge9/data/tiger/merge.cpp
 ```c++
 - Data preparation with merge.out already compiled
   - pullFromTigerLine()
   |
   - pullFromDIMACS()
   |
   - unzipTigerLine_Road()
   |
   - mergetmps2USAALL()
   |
   : Return: Now we have USA_ALL.tmp

 - Label given graph
   |
   -: Description: Given graph from Dimacs like NY, 
      we label it with coor2id_dict and edge2wc_dict,
      and output to USA-road-l.NY.gr
   |
   - labelGivenGr_with_USA_ALL()
   |
   -: Write as: USA-road-l.NY.gr
```
