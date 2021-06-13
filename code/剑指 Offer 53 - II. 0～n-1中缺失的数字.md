# 剑指 Offer 53 - II. 0～n-1中缺失的数字
**难度:easy**
## 题目
原文链接：

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

**示例 1:**
```
输入: [0,1,3]
输出: 2
```
**示例 2:**
```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

## 代码
```python
class j53_2_Solution:
    # 异或操作，但时间为O(n)
    # 也可以用理想求和-实际求和。
    # 但一般有序，就要二分
    def missingNumber(self, nums: List[int]) -> int:
        ans = 0
        n = len(nums)
        for i in range(n+1):
            ans ^= i
        for i in range(n):
            ans ^= nums[i]
        return ans
class j53_2__Solution:
    # 二分法
    def missingNumber(self, nums: List[int]) -> int:
        l, r = 0, len(nums)-1
        while l<r:
            mid = (l+r)>>1
            if nums[mid] == mid: # 等于的情况一定不是解
                l = mid+1
            else:
                r = mid
        if nums[l] == l: l+=1 # 如果出现[0, 1, 2, 3]这样完整的，需要加1
        return l
class j53_2___Solution:
    # 数学
    def missingNumber(self, nums: List[int]) -> int:
        size = len(nums)
        sum_ = (size+1)*size//2
        return sum_-sum(nums)
```
