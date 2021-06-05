# 剑指 Offer 45. 把数组排成最小的数
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

**示例 1:**
```
输入: [10,2]
输出: "102"
```
**示例 2:**
```
输入: [3,30,34,5,9]
输出: "3033459"
```

## 代码
```python
class j45_Solution:
    # 和179题相同。
    # 179求最大，这里求最小
    def minNumber(self, nums: List[int]) -> str:
        def cmp1(x, y):
            if x+y<y+x:return -1
            return 1
        ans = ''.join(sorted(map(str, nums), key = cmp_to_key(cmp1)))
        return ans
```
