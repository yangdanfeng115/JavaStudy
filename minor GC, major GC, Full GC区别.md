在 Java 的垃圾回收机制中，Minor GC、Major GC 和 Full GC 是三种不同的垃圾回收操作。它们的区别在于清理的区域、触发条件以及对应用性能的影响。

# 1. Minor GC

Minor GC 是针对 新生代（Young Generation） 的垃圾回收。

## 特点：

回收范围：只清理新生代中的 Eden 区和 Survivor 区，不涉及老年代。

触发条件：当 Eden 区满 时触发 Minor GC。

回收过程：标记出新生代中不可达的对象。

回收不可达对象。

存活的对象会被移动到 Survivor 区；在 Survivor 区中存活次数超过一定阈值（MaxTenuringThreshold）的对象，会晋升到老年代。

停顿时间：短暂停顿，因为新生代通常较小，回收速度快。

频率：发生频繁，因为新生代是对象分配的主要区域，容易填满。

# 2. Major GC

Major GC 是针对 老年代（Old Generation） 的垃圾回收。

## 特点：

回收范围：主要清理老年代，不会清理新生代。

触发条件：当老年代空间不足（如新生代中晋升的对象导致老年代内存紧张）时触发 Major GC。

回收过程：标记老年代中的不可达对象。回收不可达对象，释放老年代的内存。

停顿时间：相对较长，因为老年代的对象数量较多，且通常是长生命周期对象。

频率：较低，通常发生在老年代堆积了大量长生命周期对象时。

# 3. Full GC

Full GC 是一次 全面的垃圾回收，会清理整个堆内存，包括新生代、老年代，以及元空间（Metaspace）。

## 特点：

回收范围：清理整个堆（新生代 + 老年代），并可能涉及元空间。

触发条件：

老年代内存不足时，垃圾回收器无法通过 Minor GC 或 Major GC 解决内存压力。

系统内存紧张，JVM 需要释放更多空间。

显式调用 System.gc()，可能会触发 Full GC（取决于垃圾回收器）。

JVM 运行中可能会触发 Full GC 来整理内存碎片。

## 回收过程：
先执行 Minor GC 清理新生代。

然后执行 Major GC 清理老年代。

如果有元空间碎片问题，也可能涉及元空间的清理。

停顿时间：最长的停顿时间，因为它需要清理整个堆内存，涉及更多区域和对象。

频率：应尽量减少 Full GC 的触发，因为它会对应用性能产生显著影响。

## 三者对比总结

![Alt text](https://github.com/yangdanfeng115/JavaStudy/blob/main/images/comparation%20in%20minor%20GC%20major%20GC%20and%20full%20GC.png))

## 性能优化建议

### 减少 Minor GC 频率：

优化对象创建，减少短命对象的数量。

增大新生代（通过 -Xmn 或 -XX:NewSize 配置新生代大小）。

### 减少 Major GC 的停顿：

通过调整 Survivor 区大小（-XX:SurvivorRatio）或晋升阈值（-XX:MaxTenuringThreshold），控制晋升到老年代的对象数量。

增加堆内存大小（-Xmx）。

### 减少 Full GC 的触发：

避免显式调用 System.gc()。

使用合适的垃圾回收器（如 G1 GC 或 ZGC）来减少 Full GC 的影响。

优化程序，减少长生命周期对象的创建。
