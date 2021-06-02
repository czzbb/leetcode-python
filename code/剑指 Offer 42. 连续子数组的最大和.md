# 剑指 Offer 42. 连续子数组的最大和
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

**示例1:**
```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

## 代码
```python
class j42_Solution(object):
    # 同53
    # 前缀和，并记录最小值
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        maxsum = nums[0]
        minsum = 0 #
        sum_ = 0
        for i in nums:
            sum_ += i
            maxsum = max(maxsum, sum_ - minsum)
            minsum = min(minsum, sum_)
        return maxsum
```
```python
class j42__Solution(object):
    # 分治法
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return self.helper(nums, 0, len(nums)-1)
    def helper(self, nums, l, r):
        if l>r:
            return -float('inf')
        mid = (l+r)//2
        leftsum = self.helper(nums, l, mid-1)
        rightsum = self.helper(nums, mid+1, r)
        #
        sum_l = 0
        max_l = nums[mid]
        for i in range(mid, l-1, -1):
            sum_l += nums[i]
            max_l = max(sum_l, max_l)
        #
        sum_r = 0
        max_r = nums[mid]
        for i in range(mid, r+1):
            sum_r += nums[i]
            max_r = max(sum_r, max_r)
        return max(max(leftsum, rightsum),max_l+max_r-nums[mid])
```
```python
class j42___Solution:
    # 动态规划/可以看作是贪心算法
    # dp 表示以 num[i] 为结尾的子序列的最大和值：max（只有当前值，当前值+之前的和）
    def maxSubArray(self, arr: List[int]) -> int:
        ans = arr[0]
        dp = arr[0]
        for i in range(1, len(arr)):
            dp = max(dp+arr[i], arr[i])
            ans = max(ans, dp)
        return ans
```
