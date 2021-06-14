# 剑指 Offer 57 - II. 和为s的连续正数序列
**难度:easy**
## 题目
原文链接：

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

**示例 1：**
```
输入：target = 9
输出：[[2,3,4],[4,5]]
```
**示例 2：**
```
输入：target = 15
输出：[[1,2,3,4,5],[4,5,6],[7,8]]
```

## 代码
```python
class j57_2_Solution(object):
    #滑动窗口
    def findContinuousSequence(self, target):
        """
        :type target: int
        :rtype: List[List[int]]
        """
        l = r = 1  # 区间一般都是左闭右开
        sum_ = 0
        ans = []
        while l<=target//2:
            if sum_ > target:
                sum_ -= l
                l += 1
            elif sum_ < target:
                sum_ += r
                r += 1
            else:
                list_ = list(range(l, r))
                ans.append(list_)
                sum_ -= l
                l += 1
        return ans
class j57_2__Solution:
    # 数学方法
    # 公差为1的等差数列求和，其中个数为n，首项为a1。寻找满足条件的整数a1, n。
    def findContinuousSequence(self, target: int) -> List[List[int]]:
        ans = []
        for n in range(2, target+1):
            tmp = target - n*(n-1)//2
            if tmp <= 0: break
            if tmp % n == 0:
                a1 = tmp // n
                ans.append(list(range(a1,a1+n)))
        return ans[::-1]
```
