-> Process can request, use and release resources
-> resources are partitioned into instances

-> 4 conditions of deadlock: 
1. Mutual Exclusion 2. Hold and Wait 3. No preemption 4. Circular Wait
-> request and asssignment edge in a resource-allocation graph
-> 3 ways to deal with deadlock problem
  1. Deadlock avoidance = stay in a safe state
  2. Deadlock prevention => ensure that at-least one condition is not met
  3. Enter, detect and recover from a deadlock
  
Deadlock Prevention = restrain the way requests are made by altering one of the 4 deadlock conditions

1. Mutual Exclusion = can't deny this property for non-shareable resources

2. Hold and Wait
    -> whenever a process requests a resource, it should not hold other resources
        Protocol 1: request and be allocated all resources before execution
        Protocol 2: request resources only when you have none, and release resources before requesting for additional resources
    -> disadvantages = low resource utilizationa and possible starvation

3. No preemption:
    -> Protocol 1: release all resources if it needs an unavailable resource
    -> Protocol 2: when resource is requested, check availability
                      if available, allocate
                      else preempt other process using this resource and allocate to the requesting process
    -> applied to resources whose states are easily saved and reused
    -> not generally applied to printers or tape drivers
    
    
4. Circular Wait = ordering of resource types
    -> each process requests resources in an increasing order of enumeration
    -> give priorities based on numbering.
    Eg: Process P1 is allocated resource R5. If P1 requests R3 and R4, which are numerically less than 5, it won't be granted.
  
  
Resource Allocation graph
-> used for single instance of a resource
-> request and assignment edge

**Deadlock Avoidance**
-> used for single instance of a resource
-> in addition to request and assignment edges, we have a claim-edge(dashed-line)
-> when requesting, claim edge -> request edge
-> when releasing, assignment edge -> clain edge

-> claim edges of resources should be in the resource allocation graph before beginning
-> request is granted only if conversion of request to assignment edge does not lead to cycle formation(needs cycle detection algorithm)
-> if cycle is found, unsafe state




!! Safe, unsafe state

Single instance of a resource type -> resource-allocation graph
Multiple instances of a resource type -> Banker's algorithm

Banker's algorithm
-> algo for deadlock avoidance
-> multiple instances
-> Safety Algorithm and resource-allocation algorihtm

Deadlock detection
-> detection algorithm
-> recovery scheme

-> in a system 


**Recovery from deadlock**
Possibility 1: inform operator and make them deal with it
Possibility 2: make system recover

How to break from deadlock:
Option 1: abort one or more processes in circular-wait
Option 2: preempt resources from one or more deadlocked processes

Abort processes methods:
Method 1: Abort all deadlocked processes
          -> expensive
Method 2: Abort one process at a time, until deadlock is eliminated
          -> overhead -> takes time for deadlock detection algo after each abortion
          
Aborting a process may not be easy
Eg: file updation, printing

Partial Termination method:
-> determine which process is to eliminated
-> abort processes according to minimum cost

Factors affecting abortion:
1. process priority
2. time process has taken and time it will need
3. number and type of resources
4. number of resources needed by process
5. number of processes to be terminated 
6. interactive or batch process


