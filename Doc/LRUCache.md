
## LRUCache ##
===

### 什么是 LRU ###
---

[LRU Cache](http://baike.baidu.com/link?url=axLw9G-1uuyndDPpTwTnAuktgy1kSRm1vb_2o5nWuy04gOXUjHFjJ4mM0rgxNRJ3)是一个Cache的置换算法，含义是“最近最少使用”，把满足“最近最少使用”的数据从Cache中剔除出去，并且保证Cache中第一个数据是最近刚刚访问的，因为这样的数据更有可能被接下来的程序所访问。

LRU的应用比较广泛，最基础的内存页置换中就用了，对了，这里有个概念要清楚一下，Cache不见得是CPU的高速缓存的那个Cache，这里的Cache直接翻译为缓存，就是两种存储方式的速度有比较大的差别，都可以用Cache缓存数据，比如硬盘明显比内存慢，所以常用的数据我们可以Cache在内存中。


### LRU基本算法描述 ###

---

前提：

- 由于我只是简单实现一下这个算法，所以数据都用int代替，下一个版本会改成模板形式的，更加通用。

要求：

- 只提供两个接口，一个获取数据getValue(key),一个写入数据putValue(key,value)
- 无论是获取还是写入数据，当前这个数据要保持在最容易访问的位置
- 缓存数量有限，最长时间没被访问的数据应该置换出缓存

算法：

为了满足上面几个条件，实际上可以用一个双向链表来实现，每次访问完数据（不管是获取还是写入），调整双向链表的顺序，把刚刚访问的数据调整到链表的最前方，以后再访问的时候速度将最快。

为了方便，提供一个头和一个尾节点，不存具体的数，链表的基本形式如下面的这个简单表述

Head <===> Node1 <===> Node2 <===> Node3 <===> Near

OK，就这么些，比较简单，实现起来也不难，用c++封装一个LRUCache类，类提供两个方法，分别是获取和更新，初始化类的时候传入Cache的节点数。

[http://blog.csdn.net/ygrx/article/details/11105755](http://blog.csdn.net/ygrx/article/details/11105755)