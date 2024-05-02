# Memory Management
## Author: Rohan Singh
This module contains notes for memeory management for reference types or pointers. Pointers are references to objects.

**Recursive types** are types that include a reference to an object of the same type (example linkedlists).

---
## Memory Management Issues
Here are some memeory management issues:  
  - **Dangling Pointers:** an active pointer to memory that has been deallocated.  
  - **Memory Leak:** allocated memory with no pointers to it.  
  - **Segmentation Violation:** accessing memory outside the valid address space.

### Segmentation Violation
Segmentation Violation referes to  accessing memory outside the valid address space, this is very common in languages like C. This can very easily be solved by simply not allowing pointer arithmentic or pointer typecasting.


### Dangling Pointers
Dangling pointers refer to an active pointer to memory that has been deallocated. This is only possible in languages that permit explicit memory deallocation. This problem can be solved using two techniques: **tombstones** and **lock & key**.

**Tombstone:** In tombstones, instead of allocating memory directly to a pointer, it instead points to a tombstone and a tombstone points to memory. On deallocation the tombstone is marked with an illegal flag.

**Lock & Key:** In lock and key, each pointer is a pair (address, key). Each allocated memory starts with a lock value and on accessing the memory, the "key" of the pointer must match the "lock" value of the address. On deallocation, the "lock" value of the address is invalid.

---

## Memory Leaks
This refers to having allocated memory with no pointers to it. There are two ways of handling this problem **reference counters** and **passive garbage collection**. 

**Reference Counters:** in this we simply create a count for the number of references that an object in memory has. The memory is deallocated as soon as the reference count of the object goes to 0.

**Passive Garbage Collection:** in passive garbage collection, when the program runs out of memory, we stop the program to look for pieces of memroy that has no pointers to it and any such memory is deallocated. Unlike reference counters there is no constant update to the counts.

### Mark and Sweep
This is a procedure to find unused memory locations that is used in passive garbage collection. These are the steps in this procedure:  
  1) All of the allocated memory locations are marked as "unused".  
  2) Do DFS on the stack and mark all of the variables from the pointers as "still used".  
  3) Deallocate any memory marked as unused.

