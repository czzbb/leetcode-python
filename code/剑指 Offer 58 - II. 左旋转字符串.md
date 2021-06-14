# 剑指 Offer 58 - II. 左旋转字符串
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

**示例 1：**
```
输入: s = "abcdefg", k = 2
输出: "cdefgab"
```
**示例 2：**
```
输入: s = "lrloseumgh", k = 6
输出: "umghlrlose"
```

## 代码
```python
class j58_2_Solution:
    def reverseLeftWords(self, s: str, n: int) -> str:
        return s[n:]+s[:n]
class j58_2__Solution:
    # 由于python的str是不能改动的，因此空间复杂度不能为O(1)
    # 但若为list或者是其他str能改动的语言，则可以实现空间复杂度O(1)，即用反转。
    # 因此，对于反转或左/右移动的题目，可以通过整体+局部的反转实现空间复杂度为O(1)的操作。
    def reverseLeftWords(self, s: str, n: int) -> str:
        def reverse(s, l, r):
            # inplace 反转
            while l<r:
                s[l], s[r] = s[r], s[l]
                l+=1
                r-=1
        s = list(s)
        # 整体反转
        reverse(s, 0, len(s)-1)
        # 两次局部反转
        reverse(s, 0, len(s)-1-n)
        reverse(s, len(s)-n, len(s)-1)
        return ''.join(s)
```
