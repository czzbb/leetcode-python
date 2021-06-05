# 剑指 Offer 48. 最长不含重复字符的子字符串
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

**示例 1:**
```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```
**示例 2:**
```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```
**示例 3:**
```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

## 代码
```python
class j48_Solution:
    # 同3
    # 滑动窗口
    # 使用dic记录窗口中的元素和个数
    # 如果新加元素c使得dic[c] >1;则缩小窗口直到dic[c] == 1
    def lengthOfLongestSubstring(self, s: str) -> int:
        dic = defaultdict(int)
        l = r = 0
        max_ = 0
        while r<len(s):
            c = s[r]
            r += 1
            dic[c]+=1
            while dic[c]>1:#如果窗口中有元素个数不为1，缩小窗口直到个数为1
                d = s[l]
                l+=1
                dic[d] -= 1
            # 此时窗口中元素个数都为1，求最值
            max_ = max(max_, r-l)
        return max_
```
