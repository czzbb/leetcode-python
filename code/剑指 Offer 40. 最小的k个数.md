# 剑指 Offer 40. 最小的k个数
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/

输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

**示例 1：**
```
输入：arr = [3,2,1], k = 2
输出：[1,2] 或者 [2,1]
```
**示例 2：**
```
输入：arr = [0,1,2,1], k = 1
输出：[0]
```

## 代码
```python
class j40_Solution(object):
    # top k 的问题一般都用：1.优先队列（堆） 2. 快排
    # 堆排序：时间O(nlogk)，空间O(k) ;快排：时间O(n), 空间O(1);
    # 但是快排需要修改原数组；并且快排不适合处理数据流的问题，因为需要一次性读入。
    # 类似 215
    # 使用堆排序完成优先队列
    def getLeastNumbers(self, arr, k):
        """
        :type arr: List[int]
        :type k: int
        :rtype: List[int]
        """
        if k == 0:return []
        hp = [-x for x in arr[:k]]# 大堆顶
        heapq.heapify(hp)
        for i in arr[k:]:
            if i < -hp[0]: #如果新元素比最大的元素小
                heapq.heappop(hp)
                heapq.heappush(hp, -i)
        return [-x for x in hp]
```
```python
class j40__Solution:
    # 借助快排的思想
    def getLeastNumbers(self, arr: List[int], k: int) -> List[int]:
        if k == 0:return []
        self.quicksort(arr, 0, len(arr)-1, k)
        return arr[:k]

    def quicksort(self, arr, l, r, k):
        if l<r:
            mid = self.partition(arr, l, r)
            if mid == k:return  # 刚好，就不用排序了，返回
            if mid < k: # 还不够，排右边的
                self.quicksort(arr, mid+1, r, k)
            else:   # 多了，排坐标的
                self.quicksort(arr, l, mid-1, k)

    def partition(self, arr, l, r):
        # 一次快排的函数
        # 类似快慢指针，i是慢指针
        i = l+1
        for j in range(l+1, r+1):
            if arr[j]<arr[l]:
                arr[j], arr[i] = arr[i], arr[j]
                i+=1
        arr[i-1], arr[l] = arr[l], arr[i-1]
        return i-1
```
