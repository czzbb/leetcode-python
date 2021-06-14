# 剑指 Offer 59 - I. 滑动窗口的最大值
**难度:Hard**
## 题目
原文链接：https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/

给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

**示例:**
```
输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
输出: [3,3,5,5,6,7] 
解释: 

  滑动窗口的位置                最大值
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
 
```

## 代码
```python
class j59_1_Solution(object):
    # 同239
    # 建立单调队列，用双向队列实现
    def maxSlidingWindow(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        n = len(nums)
        # 特殊情况
        if n*k == 0:return []
        if k==1: return nums
        #
        d = deque()#双向队列
        ans = []
        def input_deque(ind):
            # 单调队列满了
            if d and ind-d[0] == k:
                d.popleft()
            # 出队比i小的
            while d and nums[d[-1]]<nums[ind]:
                d.pop()
            # 入队
            d.append(ind)
        # 先入队前k-1个
        for i in range(k-1):
            input_deque(i)
        #
        for i in range(k-1,len(nums)):
            input_deque(i)
            ans.append(nums[d[0]])
        return ans
```
