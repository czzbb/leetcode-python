# 剑指 Offer 58 - I. 翻转单词顺序
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

**示例 1：**
```
输入: "the sky is blue"
输出: "blue is sky the"
```
**示例 2：**
```
输入: "  hello world!  "
输出: "world! hello"
解释: 输入字符串可以在前面或者后面包含多余的空格，但是反转后的字符不能包括。
```

## 代码
```python
class j58_1_Solution:
    # 同151
    def reverseWords(self, s: str) -> str:
        return ' '.join(reversed(s.split()))
class j58_1__Solution:
    # 不调用库函数
    # 使用双指针
    def reverseWords(self, s: str) -> str:
        ans = []
        l, r, size = 0, 0, len(s)
        while r<size:
            # 找到非空格，即单词的首字母ind（l）
            while r<size and s[r] == ' ':
                r += 1
            l = r
            # 走到单词尾部
            while r<size and s[r] != ' ':
                r+=1
            # 是一个有效的单词：因为若最后都是空格，则l == r
            if l != r:
                ans.append(s[l:r])
        return ' '.join(ans[::-1])
```
