# Garbage Collection in JavaScript

JavaScript utilizes automatic memory management through a process called garbage collection. This means developers typically do not need to manually allocate or deallocate memory, as is required in languages like C or C++. The JavaScript engine handles this automatically in the background. 
The core principle behind JavaScript's garbage collection is to identify and reclaim memory that is no longer reachable or "in use" by the program. The most common algorithm used for this is Mark-and-Sweep.
How Mark-and-Sweep Works:

- Marking Phase:
  - The garbage collector starts from a set of "root" objects (e.g., global variables, objects on the call stack)
    that are known to be reachable. It then traverses the object graph, marking all objects that can be reached
    from these roots as "active" or "in use." This process recursively marks all objects that are referenced
    directly or indirectly by reachable objects.
- Sweeping Phase:
  - After the marking phase, the garbage collector iterates through all objects in memory. Any objects that were
    not marked during the marking phase are considered "unreachable" or "garbage" and are then swept away (deallocated),
    freeing up their memory for future use.
