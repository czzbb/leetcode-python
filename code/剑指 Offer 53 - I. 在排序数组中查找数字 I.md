# 剑指 Offer 53 - I. 在排序数组中查找数字 I
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/

统计一个数字在排序数组中出现的次数。

**示例 1:**
```
输入: nums = [5,7,7,8,8,10], target = 8
输出: 2
```
**示例 2:**
```
输入: nums = [5,7,7,8,8,10], target = 6
输出: 0
```

## 代码
```python
class j53_1_Solution(object):
    # 和34几乎相同，只是返回值不同
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if not nums:
            return [-1, -1]
        f = self.first(nums, target)
        if f == -1:
            return 0
        l = self.last(nums, target)
        return l-f+1

    def first(self, nums, target):
        l, r = 0, len(nums) - 1
        while l < r:
            mid = (l + r) >> 1
            if nums[mid] < target:
                l = mid + 1
            else:
                r = mid
        if nums[l] == target:
            return l
        else:
            return -1

    def last(self, nums, target):
        l, r = 0, len(nums) - 1
        while l < r:
            mid = (l + r + 1) >> 1# 这里是向上取整！！！！
            if nums[mid] > target:
                r = mid - 1
            else:
                l = mid
        # 先判断过了 first，因此一定有值
        return l
```
```python
class j53_1__Solution:
    # 可以通过找到 target最右侧的坐标，和target-1 最右侧的坐标（如果没有，就是第一个小于target的坐标）
    # 两者做差即可，这样只要一个二分。因为 last 函数对于不存在的target，会找到第一个小于target处
    def search(self, nums: List[int], target: int) -> int:
        if not nums: return 0
        return self.last(nums, target) - self.last(nums, target-1)

    def last(self, nums, target):
        if target<nums[0]:return -1 # 当nums中的值都大于target时，需要返回-1
        l, r = 0, len(nums)-1
        while l<r:
            mid = (l+r+1)>>1
            if nums[mid]>target:
                r = mid-1
            else:
                l = mid
        return l
```
