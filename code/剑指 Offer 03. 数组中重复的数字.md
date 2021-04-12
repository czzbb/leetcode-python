# 剑指 Offer 03. 数组中重复的数字
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/

找出数组中重复的数字。  
在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

**示例 1：**
```
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
```

## 思路
* 与[287. 寻找重复数](https://github.com/czzbb/leetcode-python/blob/master/code/0287-%E5%AF%BB%E6%89%BE%E9%87%8D%E5%A4%8D%E6%95%B0.md)相似
* 将数组中的元素当作索引，将索引对应的值变为负
* 如果碰到索引的值是负数的话，说明这个索引之前出现过，返回这个索引
* 但这里`ind`会出现`0`，因此要特殊处理

## 代码
```python
class j3_Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        flag = False # flag表示0是否出现过
        for i in range(len(nums)):
            ind = abs(nums[i])
            if nums[ind]<0: # 如果对应元素小于零，说明出现过
                return ind
            else: # 没出现过
                nums[ind] *= -1
                if nums[ind] == 0:
                    if flag: return 0
                    else: flag = True
```
