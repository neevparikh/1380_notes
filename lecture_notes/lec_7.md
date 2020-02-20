2020-02-20 | 10:36


### Vector clocks (continued)

Tophat question

S1 -e1-----------------e2------------------------>>-e5-----------------e6------
    [1, 0]             [2, 0]                   |  [3, 2]             [4, 2]   
                                                |
                                                | (server talks)
                                                |
                                                |
S2 --------------------e3------------------e4->>-----------e7------------------
                       [0, 1]              [0, 2]         [0, 3]                                   



### Distributed Hash Tables

- Peer to peer system (P2P)
    - each client stores some parts of the data 
    - each part is like a chunk/object 
    - nodes can enter and exit as they please; no central authority 
        - needs redundancy as chunks can disappear
    - e.g. Tapestry 
    - terminology for tapestry
        - root
            - server that has key, ID 
        - publish
            - put stuff (k, obj) into the database
        - route table
            - what every node stores in the tapestry network
            - see structure
                - can always use your own ID, so something in every row/col (?)
            - every hop gets you one digit closer to the required destination
                - log(N) tries only (I think)
                - if the closest server doesn't have it, wait for new publish
            - we can have no node with required key 
        - we will use base 4


#### Routing Table Structure 

+---------+---------+---------+---------+---------+
|         |    0    |    1    |    2    |    3    |                    
+---------+---------+---------+---------+---------+
|   xxxx  |  0122   |  1302   |  2310   |  3333   |  Stores one matching addr
|   1xxx  |  ----   |  ----   |  ----   |  1302   |  per col for that x.
|   13xx  |  1302   |  ----   |  ----   |  ----   |                    
|   130x  |  ----   |  ----   |  1302   |  ----   |                    
+---------+---------+---------+---------+---------+
 has root
 ID per
 digit


#### Pseudocode for routing
    - lookup(k, step)
    - overlap = prefix(k, my-id)
    - row = step 
    - col = k.index(overlap)
    - while not node = route-table.index(row, col)
        - step += 1 
        - if step == full
            - look for k in hashmap 
            - return val or err
        - try again 
    - node.lookup(k, step + 1)
