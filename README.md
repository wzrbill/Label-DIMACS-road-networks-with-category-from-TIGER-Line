### Purpose: 
The purpose of this notebook is to attach category of each edge of DIMACS road networks.
### Source: 
We use TIGER/Line dataset from DIMACS to attach categories to edges
### Approach: 
   * 1. We first download target road network from 
    http://www.diag.uniroma1.it/challenge9/download.shtml, NY for the rest of description.
    
   * 2. Then we download all the TIGER/Line from 
       http://www.diag.uniroma1.it/challenge9/data/tiger/, and we merge them into USA_ALL.tmp for reference.
       merge.cpp can be found at "Merging of two or more files" on the same webpage,
       and compile it to 'merge.out' before running
       
   * 3. We use USA_ALL.tmp as dictionary to guide the labeling process of target road network, and
       save it as USA-road-l.NY.gr in the format of DIMACS.

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
