# 剑指 Offer 31. 栈的压入、弹出序列
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

**示例 1：**
```
输入：pushed = [1,2,3,4,5], popped = [4,5,3,2,1]
输出：true
解释：我们可以按以下顺序执行：
push(1), push(2), push(3), push(4), pop() -> 4,
push(5), pop() -> 5, pop() -> 3, pop() -> 2, pop() -> 1
```
**示例 2：**
```
输入：pushed = [1,2,3,4,5], popped = [4,3,5,1,2]
输出：false
解释：1 不能在 2 之前弹出。
```

## 代码
```python
class j31_Solution:
    # 是用一个栈st来模拟
    # 按顺序入栈
    # 出栈判断：栈非空，且栈顶元素 == 出栈元素。一直出栈到不满足条件
    def validateStackSequences(self, pushed: List[int], popped: List[int]) -> bool:
        ind_pop = 0
        st = []
        for i in range(len(pushed)):
            st.append(pushed[i])
            while st and st[-1] == popped[ind_pop]:
                st.pop()
                ind_pop+=1
        return not st
```
