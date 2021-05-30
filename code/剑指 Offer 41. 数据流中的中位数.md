# 剑指 Offer 41. 数据流中的中位数
**难度:Hard**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，
```
[2,3,4] 的中位数是 3
[2,3] 的中位数是 (2 + 3) / 2 = 2.5
```
设计一个支持以下两种操作的数据结构：  
* void addNum(int num) - 从数据流中添加一个整数到数据结构中。
* double findMedian() - 返回目前所有元素的中位数。

**示例 1：**
```
输入：
["MedianFinder","addNum","addNum","findMedian","addNum","findMedian"]
[[],[1],[2],[],[3],[]]
输出：[null,null,null,1.50000,null,2.00000]
```
**示例 2：**
```
输入：
["MedianFinder","addNum","findMedian","addNum","findMedian"]
[[],[2],[],[3],[]]
输出：[null,null,2.00000,null,2.50000]
```

## 代码
```python
class j41_MedianFinder:
    # 同295
    # 使用两个堆各存一半。较大的一半用小堆顶，较小的一半用大堆顶。这样可以整体可以看成是有序的对半折。（好好理解）
    # 这里规定：较大的一半的个数会大于等于较小的一半
    def __init__(self):
        """
        initialize your data structure here.
        """
        self.big = [] # 较大的一半，用小堆顶
        self.small = [] # 较小的一半，用大堆顶

    def addNum(self, num: int) -> None:
        # 放入一边时，要先放另一边。
        if len(self.big) == len(self.small): # 个数相同，往大的放
            heapq.heappush(self.small, -num) # 先放小的
            heapq.heappush(self.big, -heapq.heappop(self.small)) # 再放大的
        else: # 否则，往小的放，保持平衡
            heapq.heappush(self.big, num)
            heapq.heappush(self.small, -heapq.heappop(self.big))

    def findMedian(self) -> float:
        return self.big[0] if len(self.big) != len(self.small) else (self.big[0]-self.small[0])/2
```
