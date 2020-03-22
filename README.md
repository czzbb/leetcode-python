# leetcode-python
记录一下自己做过的leetcode题，代码在code中。（持续更新）

每题都包含：
  1. 题目的难易度
  2. 原题链接，题目内容
  3. 解题思路
  4. python代码
## 做题总结
### 排序算法
[十大经典排序算法](https://github.com/czzbb/leetcode-python/blob/master/code/0000-%E5%8D%81%E5%A4%A7%E7%BB%8F%E5%85%B8%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95.md)
### 股票问题
一种简单的动态规划解决[股票6问](https://github.com/czzbb/leetcode-python/blob/master/code/0000-%E8%82%A1%E7%A5%A86%E9%97%AE%E6%B1%87%E6%80%BB.md)

---
### 二叉树的非递归遍历
* [中序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0094-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [前序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0144-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [后续遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0145-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%90%8E%E7%BB%AD%E9%81%8D%E5%8E%86.md)

*前序遍历和后续遍历可以看成是一种（后续遍历中有介绍）*

---
### 回溯问题
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

---
### 二分查找
二分查找思路虽然简单。。。但是细节真是要命。  
这里用**统一的思维解决所有二分查找问题。**
* 二分查找流程（三步骤）：
  1. 先筛选特例：
    例如：数组为空，或待查元素大于最大元素，导致下标溢出
  2. 框架：
      * 使用`while l<r`，这样while出来后一定是l=r
      * `mid = (l+r)//2` 向下取整 或  `mid = (l+r+1)//2` 向上取整；具体根据情况，下面会介绍
      * 利用**排除法**：排除肯定不是解的部分，那么剩下就是解了
  3. 根据题目看是否需要对最终选出的元素进行判断。
* 如果 else 下是l=mid，则要向上取整；否则可能会跳不出while  
可以看看[34-在排序数组中查找元素的第一个和最后一个位置](https://github.com/czzbb/leetcode-python/blob/master/code/0034-%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE.md)和
[35-搜索插入的位置](https://github.com/czzbb/leetcode-python/blob/master/code/0035-%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.md)加深理解
