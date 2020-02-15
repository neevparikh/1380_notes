# Syncing between servers:

## Partial ordering vs total ordering
    * Total ordering says that we can correctly order every single message
        * very expensive (involves atomic clocks, and also inccurs a performance hit)
    * partial odering says that we can correctly order every message from a single client, however, we can't say anything about the order of events occuring on seperate machines
        * cheaper, however we loose the the ability to interact nicely between servers

## Causal Ordering -- a type of partial ordering
Logical clocks: have each server start a clock at zero and the increment it by 1 for each event. Then if it gets an event from another server then we also get the other servers logical clock and we set our to the max of their clock and ours
    * we don't actually use this but it's close.
    * Imagine we have server 1 with 5 event e11 ... e15
                             2 with 5 event e21 ... e25
      Now imagine that e23 is the same as e15. At this point server 2 updates it's logical clock to be 5 and keeps increments form there

Vector clock: What we actually use is a vector of these logical clocks $$x \in \R^n$$ where n is the number of servers. Each server starts with a full vector of zeros and increments it's index. When a new message is sent we perform the max operation piecewise along the vector (and also increment your index)

S1 -e1----e30-----e20-----e7-
                          ^ 
S2 -e5----e2--------------^--
          ^>>>\   >>>>>>>>^
      >>>/     >V>^
S3 -e21---------e3----------
Where e2 depends on e21,
      e3 depends on e2,
      e7 depends on e7

Logical clock
S1 -e1----e30-----e20-----e7-
    1     2       3       4
S2 -e5----e2-----------------
    1     2
S3 -e21---------e3----------
    1           3

Vector clock
S1 -e1--------e30-------e20-------e7-------
    [1, 0, 0] [2, 0, 0] [3, 0, 0] [4, 2, 2]
S2 -e5--------e2---------------------------
    [0, 1, 0] [0, 2, 1] 
S3 -e21-------e3---------------------------
    [0, 0, 1] [0, 2, 2] 

Note that with the Vector Clock, information only transfers when messages are sent. For example, S3 knows nothing about S1

Vector Clocks are hard to scale, but we're not going to talk about that yet
