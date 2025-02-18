# Garbage Collection 101: System Design Notes

This document summarizes key concepts, strategies, and trade-offs involved in garbage collection (GC) as discussed in the "Garbage Collection 101" video. It provides an overview of how modern programming languages manage memory automatically and how various GC algorithms and designs impact system performance and design.



## 1. Introduction

Garbage Collection (GC) is an automatic memory management technique that reclaims memory occupied by objects no longer in use by a program. Its effective use is crucial for preventing memory leaks, ensuring efficient resource utilization, and maintaining overall application performance.


## 2. Core Concepts

### 2.1 Memory Reclamation
- **Objective:** Automatically reclaim memory to prevent the gradual increase in memory usage, which can lead to slower performance, crashes, or failures.
- **Impact:** Proper memory management is essential for maintaining application responsiveness and stability.

### 2.2 Reachability and GC Roots
- **Reachability:** An object is considered reachable if it can be accessed directly or indirectly by the application. The garbage collector begins with a set of known starting points, known as **GC roots**, and traverses object references to determine which objects are still in use.
- **GC Roots:** These are typically:
  - Global variables
  - Stack references (local variables)
  - Static fields
- **How It Works:** 
  - The GC starts at the GC roots and follows pointers (references) to other objects.
  - Any object that is connected to a GC root through a chain of references is marked as reachable (alive).
  - Objects that are not reached during this traversal are deemed unreachable and considered garbage, making them eligible for collection.

![image](https://github.com/user-attachments/assets/1a08bb0b-0545-48c5-b4a7-758ca7e73f82)

## 3. Generational Garbage Collection

**Generational Garbage Collection** leverages the observation that most objects die young by dividing the heap into separate regions (generations) and collecting them at different frequencies.

### 3.1 Empirical Observation
- **Most objects die young:** The design is based on the observation that most objects have a short lifespan.

### 3.2 Memory Divisions
- **Young Generation:**
  - **Eden Space:** Where new objects are allocated.
  - **Survivor Space:** Objects that survive a collection in Eden are moved here.
- **Old Generation:** For objects that persist longer; collections occur less frequently but are more comprehensive.
- **Metaspace (Java-specific):** Stores class metadata to reduce memory footprint in large applications.

![image](https://github.com/user-attachments/assets/33aafad0-30dd-4e19-8cf3-a061f55c7077)


### 3.3 Language Variations
- **Java:** Typically divides memory into Young, Old, and Metaspace.
- **V8 (JavaScript Engine):** Uses a two-generation system.
- **.NET:** Often implements a three-generation system (generations 0, 1, and 2).



## 4. Garbage Collection Algorithms

### 4.1 Mark and Sweep Algorithm
- **Mark Phase:** Traverses all objects starting from the GC roots and marks the reachable objects.
- **Sweep Phase:** Reclaims memory occupied by unmarked (unreachable) objects.
- **Stop-the-World Pause:** The entire application is paused during the GC process, which can be disruptive especially with large heaps.

![image](https://github.com/user-attachments/assets/1627c231-ef24-4d58-856e-0c4b76e6ca33)

### 4.2 Tri-Color Marking (Incremental Approach)
- **Three Sets:**
  - **White:** Objects considered as potential garbage (unreachable).
  - **Gray:** Objects that are reachable but whose references have not been fully explored.
  - **Black:** Objects that are reachable and fully processed.
- **Benefit:** Allows for incremental marking, reducing long pauses by processing parts of the object graph while the application continues to run.


## 5. Language-Specific Implementations

### 5.1 Java
- **Algorithms:** Offers multiple GC algorithms like Serial, Parallel, CMS (Concurrent Mark Sweep), and G1.
- **Design Focus:** Balancing performance, latency, and scalability across various application types.

### 5.2 Python
- **Mechanism:** Combines reference counting with a cyclic garbage collector.
  - **Reference Counting:** Automatically deallocates objects when their reference count drops to zero.
  - **Cyclic Collector:** Handles circular references that reference counting alone cannot resolve.

### 5.3 Go
- **Approach:** Uses a concurrent mark-and-sweep collector.
- **Technique:** Employs a tricolor marking algorithm to allow GC to run concurrently with the application, minimizing pause times.


## 6. Challenges and Trade-offs

### 6.1 Performance Overhead
- **GC Cycles:** Can introduce unpredictable pauses, which may be problematic for latency-sensitive systems.
  
### 6.2 Memory Fragmentation
- **Fragmentation:** Some GC strategies can leave gaps in memory, which may slow down allocation over time.
- **Balancing Pools:** Efficient memory management involves maintaining a balance between used and free memory pools to minimize fragmentation.

### 6.3 Control and Predictability
- **Loss of Fine-Grained Control:** Garbage collection abstracts memory deallocation away from the developer, leading to less control over when and how memory is freed.
- **Implications:** Unpredictable GC pauses can affect the responsiveness of applications, particularly in real-time or interactive systems.


## 7. Additional Considerations in System Design

- **Balancing Latency and Throughput:** Different GC strategies offer trade-offs between minimizing pause times and maximizing overall throughput.
- **Concurrent vs. Stop-the-World:** Choosing between concurrent (incremental) and stop-the-world GC methods depends on the application's responsiveness requirements.
- **Application Profiling:** Understanding object lifecycles and allocation patterns is key to tuning GC performance and selecting the appropriate algorithm.


## 8. Conclusion

Understanding garbage collection is essential for designing robust, scalable, and efficient systems. By comprehending the various GC algorithms, their generational approaches, and their impact on performance and latency, system designers can make informed choices that align with the requirements of their applications.

*For ongoing insights into system design, consider subscribing to the system design newsletter mentioned in the source material.*

# Resources

[Byte Byte Go - Garbage Collection 101 Video](https://www.youtube.com/watch?v=3Kqal7QaCCM)
