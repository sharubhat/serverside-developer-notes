# Heap Management

## Need for a Generational Heap:

* Most objects die young. Hence they can be aged in nursery/young generation.
* Within young generation, objects are aged by moving them back and forth in survivor spaces\(S0 and S1\). The area where most allocations happen is called Eden Space.
* Only long lived objects are promoted to Old generation.

# Hotspot's traditional generational heap

Most new objects are created in Eden space. Once they are aged, they are moved to one of S1 or S2 depending on which one is currently marked as From space. Once From space gets filled, objects are aged and moved to To space and To and From get interchanged. So until one of them overflows, the objects are moved back and forth between S1 and S2.

# ![](/assets/IMG_4427.JPG)

## Hotspot's heap management

GC is responsible for allocations and reclamations.

Allocations: Mostly happen lock-free out of Thread Local Area Buffers \(TLABs\)

Reclamations happen after tracing live data from the root set.

GC root set: Refer to [Garbage collection roots](https://www.ibm.com/support/knowledgecenter/en/SS3KLZ/com.ibm.java.diagnostics.memory.analyzer.doc/gcroots.html)

Most allocations happen inside Eden region. Eden region is further divided into TLABs. Each thread has it's own TLAB space which promotes lock-free access.

As new objects get created, Eden space gets filled. When Eden region is completely full, there will be reclamation. During this reclamation, live objects are moved to survivor space.

### Generational Garbage Collector

We can have different GC algorithms for each generation. These algorithms are suited for the generations as well as GC goals - latency, throughput or memory footprint.

**Hotspots Young Generation Collectors**

Similar algorithms for young generation collectors. Young generation is always collected in entirety called monolithic reclamation and the collection is stop-the-world pause.

Collector employs parallel GC worker threads. These worker threads have their own work queue and they can also perform work stealing. 

Surviving objects are aged and collected in Survivor spaces. If there is an overflow, aged objects are tenured to old generation. The promotion of objects happen in promoting thread's local area buffers also known as Promotional LABs or PLABs.















