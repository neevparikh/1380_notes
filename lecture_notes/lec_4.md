2020-02-04 | 10:35 

### What to do when messages fail

- Retry the message 
    - how long to wait
        - constant 
        - random 
        - previous history 
        - exponential back-off
    - retry assumptions 
        - Synchronous model 
            - client -> server time is bounded 
            - server response time is bounded 
                - network is fine
            - clock drift is bounded
                - times of server & client are synced periodically
        - Byzantine model 
            - nodes can lie to you 
- Other options 
     - response mandatory 
     - ID / timestamps 
         - hash the data 
         - include ID of previous message 
     - use only idempotent (see lec 3) operations 
     - send response before doing processing
     - allow rollback 

- RPC semantics (what is necessary to guarantee semantic)
    - 1 or more tries (at least once)
        - retry 
    - 1 or 0 tries (at most once) - can have bugs
        - retry 
        - logging (detect duplicate)
    - 1 only (exactly once)
        - retry
        - logging
        - and more

- Load balancing 
    - things we want 
        - have expected queues be proportional to resources
            - robustness to changing resources
            - redistribution based on state
        - (history | workload | ground truth) -> load distribution 
        - consistency for load balancing
