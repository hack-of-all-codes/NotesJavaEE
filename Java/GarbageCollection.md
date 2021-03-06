# Garbage Collection

## Garbage Collection Steps
* Marking
* Deletion
* Compacting (Optional)

## Generational Garbage Collection

**JVM Partitions the Heap:**
* Eden - new object are allocated here, minor GCs (stop-the-world event) cleans this up very frequently
* Survivor Space (S0/S1) - survived 1 minor GC, objects are swapped around between S1 and S2
* Tenured (Old Generation) -  survived X (threshold) minor GC are promoted here, still gets cleaned up when a major GC cleans up and compacts the space here
* Metaspace (Permanent Generation) - classes and methods, application metadata

**For Visualization:**
* run **jvisualvm**
* install the Visual GC plugin

![Visual VM](/Images/VisualVM.png)

## Command Line Switches
```
java -Xmx12m -Xms3m -Xmn1m -XX:PermSize=20m -XX:MaxPermSize=20m -XX:+UseSerialGC -jar Java2demo.jar
```
Switch            | Description
----------------- | ------------
-Xms              | Sets the initial heap size for when the JVM starts
-Xmx              | Sets the maximum heap size
-Xmn              | Sets the size of the Young Generation
-XX:PermSize      | Sets the starting size of the Permanent Generation
-XX:MaxPermSize   | Sets the maximum size of the Permanent Generation
-XX:+UseSerialGC  | Enable Serial Collector
-XX:+UseParallelGC| Enable Parallel Collector, use -XX:ParallelGCThreads=<desired number> to specify thread count

**-XX:+UseParallelGC**
* multi-threaded young generation collector
* single-threaded old generation collector
* single-threaded compaction

**-XX:+UseParallelOldGC**
* everything is multithreaded

## The Concurrent Mark Sweep (CMS) Collector
* cleans up the old/tenured generation parallel to application threads
* younger generation cleanup is still serial and stop-the-world
* does not do **compacting** for obvious reasons (thread safety)
* To enable the CMS Collector use:
```
-XX:+UseConcMarkSweepGC
```
* and to set the number of threads use:
```
-XX:ParallelCMSThreads=<n>
```

## The G1 (Garbage First) Garbage Collector
* single physical heap, split into regions

![GM Regions](/Images/G1Regions.png)
* easy to resize
* yough GCs are parallel


**Sources:**
* [Oracle: Garbage Collection Basics](http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)
* [Oracle: G1 Garbage Collector](http://www.oracle.com/technetwork/tutorials/tutorials-1876574.html)
* [Youtube/Oracle: G1 Garbage Collector Performance Tuning](https://www.youtube.com/watch?v=bhVzCIk3-Q4)
