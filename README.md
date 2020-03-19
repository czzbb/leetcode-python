# leetcode-python
记录一下自己做过的leetcode题，代码在code中。（持续更新）

每题都包含：
  1. 题目的难易度
  2. 原题链接，题目内容
  3. 解题思路
  4. python代码
# 做题总结
## 股票问题
一种简单的动态规划解决[股票6问](https://github.com/czzbb/leetcode-python/blob/master/code/0000-%E8%82%A1%E7%A5%A86%E9%97%AE%E6%B1%87%E6%80%BB.md)

## 二叉树的非递归遍历
* [中序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0094-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [前序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0144-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [后续遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0145-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%90%8E%E7%BB%AD%E9%81%8D%E5%8E%86.md)

**前序遍历和后续遍历可以看成是一种**

## 回溯问题
例：[46-全排列](https://github.com/czzbb/leetcode-python/blob/master/code/0046-%E5%85%A8%E6%8E%92%E5%88%97.md)  
解决一个回溯问题，实际上就是一个决策树的遍历过程。考虑三个问题
1. **路径**：即已经做出的选择
2. **选择列表**：即当前还可以做的选择
3. **结束条件**：到达决策树底层时，已无法再选择了

代码框架：核心就是*for*循环中的,即**递归前做选择，递归后撤销选择**, 撤销选择是为了不让当前选择影响到其他**平行**的选择
```python
ans = []
def backtrack(路径，选择列表):
  if 满足条件(一般是没有选择了):
    ans.append(路径)
    return
  
  for 选择 in 选择列表:
    # 1. 做选择
    从选择列表中删除选择
    添加选择到路径
    # 2. 递归
    backtrack(路径，选择列表)
    # 3. 撤销选择
    从选择列表中添加选择
    删除路径中的选择
```
