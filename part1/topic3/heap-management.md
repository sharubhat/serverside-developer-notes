# ![](/assets/IMG_4427.JPG)Hotspot Garbage Collector

## Need for a Generational Heap:

* Most objects die young. Hence they can be aged in nursery/young generation.
* Within young generation, objects are aged by moving them back and forth in survivor spaces\(S0 or From Space and S1 or To Space\). The area where most allocations happen is called Eden Space.
* Only long lived objects are promoted to Old generation.



