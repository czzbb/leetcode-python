# 剑指 Offer 66. 构建乘积数组
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/

给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

**示例:**
```
输入: [1,2,3,4,5]
输出: [120,60,40,30,24]
```

## 代码
```python
class j66_Solution(object):
    # 同238
    # 除自身以外元素的乘积 = 左边的乘积 * 右边的乘积
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        l = [1]*n # 记录元素左侧的乘积
        r = [1]*n # 记录元素右侧的乘积
        for i in range(1, n):
            l[i] = l[i-1]*nums[i-1]
        for i in range(n-2, -1, -1):
            r[i] = r[i+1]*nums[i+1]
        return [l[i]*r[i] for i in range(n)]
class j66__Solution(object):
    # 与上述方法相同，只是化简了下
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        n = len(nums)
        ans = [1] * n
        #
        for i in range(1, n):
            ans[i] = ans[i-1] * nums[i-1]
        # base 表示右边的乘积
        base = 1
        for i in range(n-2, -1, -1):
            base *= nums[i+1]
            ans[i] *= base
        return ans
```
