2020-02-06 | 10:38 

### Load balancing schemes 

- LB based on client name 
    - assumptions 
        - names are uniformly distributed 
            - hash the names!
        - all servers are same 
        - clients are trying to get to the same resource 
- LB randomly 
    - what distribution 
- LB using round robin 
    - server takes roughly same amounts of time to process requests
        - use weighted to handle differently-abled servers
        - use history to remove nodes from rounds
- if server is slow
    - duplicate requests, have servers talk to each other
    - progress reports, dynamically readjust LB scheme

- hash names and mod with servers (aka Consistent Hashing, see. maglev, 
shiv/proxygen)
    - problem with this is that 
        - if servers enter or leave everyone has move to different servers 
    - fix: use a fixed range for hashing and have servers partition this range 
        - if new servers join, then only those clients who were in that partition 
        have to move 
        - note: wrap around in effect (circular range)
    - imbalance (?)
        - add more servers! (easy but expensive) 
        - duplicates of servers (virtually but same physical hardware)
