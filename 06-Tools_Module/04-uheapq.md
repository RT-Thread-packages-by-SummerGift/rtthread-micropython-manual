# **uheapq** – 堆排序算法

`uheapq` 模块提供了堆排序相关算法，堆队列是一个列表，它的元素以特定的方式存储。

更多内容可参考 [heapq](https://docs.python.org/3/library/heapq.html?highlight=heapq#module-heapq)  。

`函数`

- uheapq.heappush(heap, item)  
  把 item 推到 heap。

- uheapq.heappop(heap)  
  从 heap 弹出第一个元素并返回。 如果是堆时空的会抛出 IndexError。

- uheapq.heapify(x)  
  将列表 x 转换成堆。

----------