# 剑指 Offer 56 - I. 数组中数字出现的次数
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/

一个整型数组 nums 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

**示例 1：**
```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```
**示例 2：**
```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```


## 代码
```python
class j56_1_Solution(object):
    # 同260
    # 位运算: 类似的题目有136，137，260，645
    # cnt 记录所有元素的异或和，最终会等于两个只出现一次的数的异或和
    # ind 记下第一个不同的位，并以此来将数组元素分为两组。
    # 两组内部进行异或和；由于相同的元素会分到同一组，异或后“消失”，并且两个只出现一次的数会分到不同组；
    # 因此两组数异或之后就剩下这两个只出现一次的数
    # 这一思想也可以运用到 645 题：使用 enumerate 函数

    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        cnt = 0
        for num in nums:
            cnt ^= num
        #
        ind = 1
        while cnt & ind == 0:
            ind <<= 1
        #
        a = b = 0
        for num in nums:
            if num & ind:
                a ^= num
            else:
                b ^= num
        return [a, b]
```
