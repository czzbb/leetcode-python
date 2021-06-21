# 剑指 Offer 62. 圆圈中最后剩下的数字
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/

0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。  
例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

**示例 1：**
```
输入: n = 5, m = 3
输出: 3
```
**示例 2：**
```
输入: n = 10, m = 17
输出: 2
```

## 代码
```python
class j62_Solution:
    # 模拟算法
    def lastRemaining(self, n: int, m: int) -> int:
        nums = list(range(n))
        ind = 0
        for _ in range(n-1):
            ind = (ind+m-1)%n
            nums.pop(ind)
            n-=1
        return nums[0]
class j62__Solution(object):
    # 数学法解约瑟夫环
    def lastRemaining(self, n, m):
        ans = 0
        for i in range(2, n+1):
            ans = (ans+m)%i
        return ans
```
