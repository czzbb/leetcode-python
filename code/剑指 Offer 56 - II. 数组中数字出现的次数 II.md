# 剑指 Offer 56 - II. 数组中数字出现的次数 II
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-ii-lcof/

在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。

**示例 1：**
```
输入：nums = [3,4,3,3]
输出：4
```
**示例 2：**
```
输入：nums = [9,1,7,9,7,9,7]
输出：1
```


## 代码
```python
class j56_2_Solution(object):
    # 同137
    # 使用位运算
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        # 记录每一位出现的次数
        counts = [0] * 32
        #
        for num in nums:
            for j in range(32):
                counts[j] += num & 1
                num >>= 1
        # m对应元素出现的次数
        m = 3
        #
        res = counts[31]%m
        for i in range(1, 32):
            res <<= 1
            res |= counts[31 - i] % m
        # 原因在于Python是动态类型语言，在这种情况下其会将符号位置的1看成了值，而不是当作符号“负数”
        return res - 2 ** 32 if res > 2 ** 31 - 1 else res
```
