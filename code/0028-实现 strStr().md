# 28. 实现 strStr()
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/implement-strstr/

实现 strStr() 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  -1。

**示例 1:**
```
输入: haystack = "hello", needle = "ll"
输出: 2
```
**示例 2:**
```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```
**说明:**

当 needle 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 needle 是空字符串时我们应当返回 0 。这与C语言的 strstr() 以及 Java的 indexOf() 定义相符。



## 思路：
**方法一：KMP算法**
*  

**方法二：Sunday算法**
*

## 代码
**KMP算法**
```python
class a28_Solution(object):
    ##   KMP
    def strStr(self, t, p):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if not p:
            return 0
        ## get next
        def getnext(p):
            next_ = [0]*len(p)
            next_[0] = -1
            i, j = 0, -1
            while i < len(p)-1:  # 因为i是先加1，后赋值
                if j == -1 or p[i] == p[j]:
                    #先加1再赋值
                    i += 1  # 因为next是向右移了一位
                    j += 1  # 因为 j 在KMP中对比时，要比下一位
                    next_[i] = j
                else:
                    j = next_[j]
            return next_
        next_ = getnext(p)
        ## KMP
        i, j = 0, 0
        while i < len(t) and j < len(p):
            if j == -1 or t[i] == p[j]:
                i += 1
                j += 1
            else:
                j = next_[j]
        if j ==len(p):
            return i-j
        else:
            return -1
```
**Sunday算法**
```python
class a28__Solution(object):
    # Sunday
    def strStr(self, s, p):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if len(p) > len(s):
            return -1
        if not p:
            return 0
        # 计算偏移表
        len_p = len(p)
        def shiftdic(p):
            dic = {}
            for i in range(len_p-1, -1, -1):
                if not dic.get(p[i]):
                    dic[p[i]] = len_p - i
            return dic
        dic = shiftdic(p)
        # sunday 算法
        idx = 0
        while idx <= len(s)-len_p:
            str_cut = s[idx:idx+len_p]
            if str_cut == p:
                return idx
            else:
                if idx+len_p >= len(s):
                    return -1
                cur_c = s[idx+len_p]
                idx += dic.get(cur_c, len_p+1)
        return -1
```
