2020-01-28 | 11:03

### Using Networks in Distributed Systems 

#### Problems with using networks in DS:
- unreliable 
    - trace packets 
    - ways in which network is unreliable
        - drop packets
        - flip bits 
        - duplicate packets 
        - out of order packets
        - incorrect dest, i.e. routing problems 
- latency
    - async 
- bandwidth not infinite 
- network is not secure 
    - checksum 
- topology fixed 
    - naming 
- network admin (diff people)
    - interfacing 
    - written by different people 
- transport is not free 
    - packeting has overhead (acks/counters etc.) i.e metadata 
    - encryption/decryption is not free 
- network is not homogeneous
    - all factors can have diff properties 

#### Desirable Properties

##### Name Resolution (lookup/add database system)
- quick 
    - hashmap?
    - multi level cache 
- consistent 
    - expiration queries at multiple levels 
- reliable 
    - multilevel (hierarchy)
- secure 
    - certificates 
- scale 
    - multilevel (hierarchy)
    - load balancing
