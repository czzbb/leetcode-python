# 剑指 Offer 61. 扑克牌中的顺子
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

**示例 1:**
```
输入: [1,2,3,4,5]
输出: True
```
**示例 2:**
```
输入: [0,0,1,2,5]
输出: True
```

## 代码
```python
class j61_Solution:
    # 顺子满足两个条件：
    # 1. 除0外不会出现重复数字
    # 2. 最大值-最小值<5
    def isStraight(self, nums: List[int]) -> bool:
        mini, maxi = 14, -1
        seen = set()
        for num in nums:
            if num:
                if num in seen:return False
                seen.add(num)
                mini = min(mini, num)
                maxi = max(maxi, num)
        return maxi-mini <5
```
