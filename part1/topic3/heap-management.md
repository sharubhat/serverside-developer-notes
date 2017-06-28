# Heap Management

## Need for a Generational Heap:

* Most objects die young. Hence they can be aged in nursery/young generation.
* Within young generation, objects are aged by moving them back and forth in survivor spaces\(S0 and S1\). The area where most allocations happen is called Eden Space.
* Only long lived objects are promoted to Old generation.

# Hotspot's traditional generational heap

Most new objects are created in Eden space. Once they are aged, they are moved to one of S1 or S2 depending on which one is currently marked as From space. Once From space gets filled, objects are aged and moved to To space and To and From get interchanged. The objects are moved back and forth between S1 and S2 until they reach a tenuring threshold. Once tenuring threshold is reached, the objects are promoted to old generation.

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

## Reclamation

### Throughput Collector

Throughput collector in old generation is multi-threaded. Entire heap is marked, swept and compacted in it's entirety. Old generation at a given point in time will have occupied space and free space. Lets say we have an object that can fit into free space and is ready for promotion, it gets promoted to free space. This goes on until old generation is full.

When old gen is full, it goes for Parallel Mark-Sweep and Compaction. During this, the heap is divided into regions based on number of GC threads. The compaction algorithm starts by compacting live objects to lower end of the heap. It does so by having a destination region and a source region. As destination becomes full or source becomes empty, new destination and source regions are selected. This compaction goes on until the heap is fully compacted.

### Mostly Concurrent Mark-Sweep Collector \(CMS collector\) - no compaction.

Old gen collection in CMS is multi-threaded, mostly concurrent marked and swept in entirety. There is no compaction in this algorithm. It uses a list called FreeList that maintains free space in old generation. The object being promoted is put into the free space it can fit in based on FreeList lookup and the list is updated accordingly. But this results in fragmentation of the heap and so a promotion failure can happen when there are a few free spaces but the object can not fit into any of the available space. More such failures lead to Concurrent Mode Failures.

Causes:

* Marking threshold is too high.
* Heap is too small. 
* High application mutation rate.  

Too many CMFs lead to Fallback Full Garbage Collection.This fallback is single threaded, fully compacting, stop-the-world garbage collection called full GC.



