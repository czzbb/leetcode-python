# 剑指 Offer 39. 数组中出现次数超过一半的数字
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例 1:**
```
输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
输出: 2
```

## 代码
```python
class j39_Solution:
    # 同169
    # 摩尔投票法
    def majorityElement(self, nums: List[int]) -> int:
        cnt = 0
        for num in nums:
            if cnt == 0: ans = num
            cnt += 1 if ans == num else -1
        return ans
```
