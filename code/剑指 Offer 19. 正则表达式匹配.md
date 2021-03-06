# 剑指 Offer 19. 正则表达式匹配
**难度:Hard**
## 题目
原文链接：https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/

给你一个字符串 s 和一个字符规律 p，请你来实现一个支持 '.' 和 '*' 的正则表达式匹配。
* '.' 匹配任意单个字符
* '*' 匹配零个或多个前面的那一个元素  
所谓匹配，是要涵盖 整个 字符串 s的，而不是部分字符串。

**说明:**
* s 可能为空，且只包含从 a-z 的小写字母。
* p 可能为空，且只包含从 a-z 的小写字母，以及字符 . 和 *。

**示例 1:**
```
输入:
s = "aa"
p = "a"
输出: false
解释: "a" 无法匹配 "aa" 整个字符串。
```
**示例 2:**
```
输入:
s = "aa"
p = "a*"
输出: true
解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。
```
**示例 3:**
```
输入:
s = "ab"
p = ".*"
输出: true
解释: ".*" 表示可匹配零个或多个（'*'）任意字符（'.'）。
```
**示例 4:**
```
输入:
s = "aab"
p = "c*a*b"
输出: true
解释: 因为 '*' 表示零个或多个，这里 'c' 为 0 个, 'a' 被重复一次。因此可以匹配字符串 "aab"。
```
**示例 5:**
```
输入:
s = "mississippi"
p = "mis*is*p*."
输出: false
```

## 思路
同[10. 正则表达式匹配](https://github.com/czzbb/leetcode-python/blob/master/code/0010-%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%E5%8C%B9%E9%85%8D.md)

**方法一**
* 难点在于如何匹配 `*`
* 没有 `*` 时，就是匹配当前字符，再匹配后面的字符
* 有 `*` 时，考虑两种情况，只要有一种成立就行，用 `or`连接
  1. 匹配，（这里我们只考虑匹配一次，并保留当前字符，这样在下一次匹配中还能再匹配）
  2. 不匹配， 即 `*` 表示使用`0`次当前字符
* 使用该算法会有重复子问题，因此可以用字典记录或者使用dp算法

**方法二**
* 将上述方法改为`dp`
* `dp[i][j]`表示 `s[i:]` 是否和 `p[j:]`匹配；因此从后往前遍历
* 初始条件: 空匹配串`p`不能匹配除了空字符以外的子串`s`即：`dp[:][n] = False， dp[m][n] = True`
* 注意非空 `p` 可以匹配空 `s`，例如（`'a*'`可以匹配`''`），因此`i`从`m`开始遍历
## 代码
**方法一**
```python
class a10_Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        if not p: return not s
        flag = bool(s) and p[0] in [s[0],'.'] # 当前字符是否匹配
        if len(p)>1 and p[1] == '*': # 如果当前字符后面是 *，则考虑两种情况
            return flag and self.isMatch(s[1:], p) or self.isMatch(s, p[2:])
        else: # 没有*，就要匹配当前字符，和后面的字符
            return flag and self.isMatch(s[1:], p[1:])
```
**方法二**
```python
class a10__Solution(object):
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        m, n  = len(s), len(p)
        dp = [[False]*(n+1) for _ in range(m+1) ]
        dp[-1][-1] = True #
        for i in range(m, -1, -1):
            for j in range(n-1, -1, -1):
                flag = i < m and p[j] in[s[i], '.']
                if j+1<n and p[j+1] == '*':
                    dp[i][j] = flag and dp[i+1][j] or dp[i][j+2]
                else:
                    dp[i][j] = flag and dp[i+1][j+1]
        return dp[0][0]
```
