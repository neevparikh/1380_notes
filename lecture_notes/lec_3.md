2020-01-30 | 10:52

### Improving performance (and other properties)

#### In Name Resolution 
- use caching to store frequent queries
    - multi level cache (have cache on client and on resolver)
- using a resolver (that can redirect you) is rather unsecure bc of lack of 
  using keys or something like that 
- geolocate the IP to determine the closest server 
    - also maybe ping servers to see temoral locality 

#### RPC stuff 
- RPC (remote procedure calls) 
- allow you to make calls over the network 
- serializes arguements and discovers required server 
- copies what pointer points to 
    - deepcopy if pointers are recursive 
    - otherwise, send an "address" to the calling server so when pointer is 
      dereferenced, the calling server is looked up using another RPC
- problems 
    - RPC could fail 
        - server or network could go down 
            - retry again 
        - request could go through then server goes down 
            - breaks consistency maybe (?)
    - address could point to invalid memory 
    - latency from network problems
        - async calls then (?)
- idempotent calls 
    - calling again doesn't change anything 
    - with failure, simply try again 
    - ex:   
        - read 
        - get 
    - not idempotent ex: 
        - write
        - add
