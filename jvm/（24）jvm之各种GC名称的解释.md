### Minor GC / Young GC

首先我们先来看最简单的名词，Minor GC / Young GC，这个非常好理解，我们都知道，“新生代” 也可以称之为 “年轻代”， 这两个名词是等价的。那么在年轻代中的Eden内存区域被占满之后，实际上就需要触发年轻代的gc，或者是新生代的 gc。

此时这个新生代gc，其实就是所谓的 “Minor GC”，也可以称之为 “Young GC”，这两个名词，相信我们就理解 了，说白了，就专门针对新生代的gc。

### Full GC？Old GC？傻傻分不清楚

一直是说老年代一旦被占满之后，就会触发老年代的gc，之前称呼这种GC为Full GC。

其实所谓的老年代gc，称之为“Old GC”更加合适一些，因为从字面意义上就可以理解，这就是所谓的老年代gc。

但是在这里之所以我们把老年代GC称之为Full GC，其实也是可以的，只不过是一个字面意思的多种不同的说法。

为了更加精准的表述这个老年代gc的含义，我们从现在开始，一律把老年代gc称之为Old GC，后续也如此定义。

所以在这里，务必捋清这个概念，在跟面试官聊的时候，如果说到所谓的老年代gc，为了避免歧义，建议大家用 Old GC来指代。

### Full GC

对于Full GC，其实这里有一个更加合适的说法，就是说Full GC指的是针对新生代、老年代、永久代的全体内存空间的垃圾回收，所以称之为Full GC。

从字面意思上也可以理解，“Full” 就是整体的意思，所以就是对JVM进行一次整体的垃圾回收，把各个内存区域的垃圾都回收掉。

但是说实话，不同的名词如何定义每个人都有自己的看法，有些人，包括我自己，平时有一定的习惯是把Full GC直接等价为Old GC的，也就是仅仅针对老年代的垃圾回收。

但是如果从字面意义上来理解，建议日后在外面跟别人交谈的时候，把Full GC理解为针对JVM内所有内存区域的 一次整体垃圾回收

### Major GC

还有一个名词是所谓的Major GC，这个其实一般用的比较少，他也是一个非常容易混淆的概念

有些人把Major GC跟Old GC等价起来，认为他就是针对老年代的GC，也有人把Major GC和Full GC等价起来，认为他是针对JVM全体内存区域的GC。

所以针对这个容易混淆的概念，建议大家以后少提。如果听到有人说这个Major GC的概念，大家可以问清楚，他到底是想说Old GC呢？还是Full GC呢？

### Mixed GC

Mixed GC是G1中特有的概念，其实说白了，主要就是说在G1中，一旦老年代占据堆内存的45%了，就要触发Mixed GC，此时对年轻代和老年代都会进行回收。这个概念很好理解，大家只要知道是G1中特有的名词即可。