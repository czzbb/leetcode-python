# 剑指 Offer 46. 把数字翻译成字符串
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

**示例 1:**
```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```


## 代码
```python
class j46_Solution:
    # 动态规划
    # 如果s[i-2:i]为10-25的数，则 dp[i] = dp[i-1] + dp[i-2]；否则 dp[i] = dp[i-1]
    def translateNum(self, num: int) -> int:
        s  = str(num)
        pre_two, pre_one = 1, 1# 初始值
        for i in range(2, len(s)+1):
            if '10'<=s[i-2:i]<='25':
                pre_two, pre_one = pre_one, pre_one+pre_two
            else:
                pre_two, pre_one = pre_one, pre_one
        return pre_one
```
