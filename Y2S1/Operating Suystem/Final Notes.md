# Deadlock and Starvation
### Deadlock
- when two or more process are blocked forever because each holds a resource and waits for another held by another process
- **Four Condition**
	- Mutual Exclusion
		- Resource is in non-sharable mode
	- Hold and Wait
		- A process hold one resource while waiting for another resource
	- No Preemption
		- Resources cannot be forcibly taken away
	- Circular Wait
		- Process A waits for Process B, B waits for C, and last process waits for A, forming a circular chain
- **Handle deadlock**
	- Prevention
		- Prevent occurrence of one condition
	- Avoidance
		- Avoid deadlock if it becomes probable
	- Detection
		- Detects deadlock when it occurs
	- Recovery
		- Resume system normalcy quickly and gracefully
### Starvation
- when one process waits indefinitely for a resource because it is never chosen to get it
### Difference
- Two or more process are blocked forever
- one or a few processes cannot get resources

# Parallel Processing
### Parallel Processing
- multiprocessing means 2 or more processors operate in parallel
- Benefit
	- increase reliability
		- if one processors fails, others take over
	- faster processing
		- instruction can be processed in parallel, two or more at a time
- Challenge
	- How to connect the processors into configuration
	- How to orchestrate their interaction
### Critical Region
- a section of a program that must complete its execution before other processes can access the shared resources it uses
- Importance
	- ensure mutual exclusion, one process cannot access the critical region while another is inside
- Lock-and-Key Mechanism
	- Synchronization is implemented as a lock-and-key arrangement
### Semaphore
- an integer value used to provide mutual exclusion
- many problems can be solved using binary semaphores, which takes values 0 or 1
- **Two operation (Wait and Signal)**
	- **wait** (s) also called P(s) or down(s)
		- if S <= 0, the process blocks (waits)
		- Otherwise, S is decremented by 1 and the process proceeds
	- **signals** (s) also called V(s) or up(s)
		- Unconditionally increments S by 1
		- wakes up a waiting process if any
### Readers and Writers
- **Readers**
	- only read existing data
	- many readers can be active at the same time
- **Writers**
	- modify existing data
	- must be carefully accommodated

# File Manager
- track where each file is stored
- determine where and how files will be stored
- **File Structure**
	- Field -> Record -> File -> Database
### File Organization
- **Sequential Record Organization**
	- Records stored and retrieved serially, one after another
	- Easy to implement
- **Direct File Organization**
	- Use direct access files, only on direct access storage devices
	- Fast record access
- **Indexed Sequential Record Organization**
	- Records stored sequentially
	- No collision
### Physical Storage Allocation
1. Contiguous Allocation
	- Records stored one after another
2. Linked Allocation
	- Files use any available disk storage space
3. Indexed Allocation
	- Allow direct record access

### Free-Space Management
1. **Bit Vector**
	- each block represented by 1 bit
		- 1 is free, 0 is allocated
2. **Linked List**
	- free blocks linked together
3. **Grouping**
	- store addresses of number of free blocks in the first free block
4. **Counting**