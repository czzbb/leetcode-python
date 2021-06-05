# 剑指 Offer 50. 第一个只出现一次的字符
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

**示例:**
```
s = "abaccdeff"
返回 "b"

s = "" 
返回 " "
```

## 代码
```python
class j50_Solution:
    # 哈希表：key为字母，value表示其是否出现1次
    def firstUniqChar(self, s: str) -> str:
        dic = {}
        for c in s:
            dic[c] = c not in dic
        for c in s:
            if dic[c]:return c
        return ' '
```
