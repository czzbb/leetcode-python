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

---
### 位运算
[136. 只出现一次的数字](https://github.com/czzbb/leetcode-python/blob/master/code/0136-%E5%8F%AA%E5%87%BA%E7%8E%B0%E4%B8%80%E6%AC%A1%E7%9A%84%E6%95%B0%E5%AD%97.md)，
[137. 只出现一次的数字 II](https://github.com/czzbb/leetcode-python/blob/master/code/0137-%E5%8F%AA%E5%87%BA%E7%8E%B0%E4%B8%80%E6%AC%A1%E7%9A%84%E6%95%B0%E5%AD%97%20II.md)，
[260. 只出现一次的数字 III](https://github.com/czzbb/leetcode-python/blob/master/code/0260-%E5%8F%AA%E5%87%BA%E7%8E%B0%E4%B8%80%E6%AC%A1%E7%9A%84%E6%95%B0%E5%AD%97%20III.md)

---
### 股票问题
一种简单的**动态规划**解决[股票6问](https://github.com/czzbb/leetcode-python/blob/master/code/0000-%E8%82%A1%E7%A5%A86%E9%97%AE%E6%B1%87%E6%80%BB.md)

---
### 二叉树的非递归遍历
* [中序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0094-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [前序遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0144-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86.md)
* [后续遍历](https://github.com/czzbb/leetcode-python/blob/master/code/0145-%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%90%8E%E7%BB%AD%E9%81%8D%E5%8E%86.md)

*前序遍历和后续遍历可以看成是一种（后续遍历中有介绍）*

---
### 回溯问题
例：[46-全排列](https://github.com/czzbb/leetcode-python/blob/master/code/0046-%E5%85%A8%E6%8E%92%E5%88%97.md)，
[22-括号生成](https://github.com/czzbb/leetcode-python/blob/master/code/0022-%E6%8B%AC%E5%8F%B7%E7%94%9F%E6%88%90.md)  
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
如果我们使用的**路径、选择**是相互独立的，就不用**撤销选择**，可见[22-括号生成](https://github.com/czzbb/leetcode-python/blob/master/code/0022-%E6%8B%AC%E5%8F%B7%E7%94%9F%E6%88%90.md)  

#### 子集/组合/排列问题
* 该类问题都可以抽象为**树的遍历**问题。
* **子集&组合**问题是没有顺序的；**排列**问题是有顺序的。
* **无重复元素**问题
  * 因此**子集&组合**的遍历是不完全树，可以通过start（索引）来对树进行减枝，即我们通过保证元素之间的**相对顺序不变**来防止出现重复的子集&组合。如[78. 子集](https://leetcode.cn/problems/subsets/)，[77. 组合](https://leetcode.cn/problems/combinations/)。
  * **排列**问题通常通过一个集合(set)记录下访问过的元素，避免重复访问。如[46. 全排列](https://leetcode.cn/problems/permutations/)。**子集&组合**通过上述方法已经避免了重复访问。
* **有重复元素**问题：
  * 避免出现重复解：**避免同一层中，选择相同的值**
  * **子集&组合**: 通过**对原始数组进行排序**；若**当前值与上一个值相同，则跳过（因为上一个值是必选的）**。从而避免了同一层选择相同的值。[90. 子集 II](https://leetcode.cn/problems/subsets-ii/)，[40. 组合总和 II](https://leetcode.cn/problems/combination-sum-ii/)。
  * **排列**: 通过使用当前层一个集合(cur_set)来判断是否选择了重复值。[47. 全排列 II](https://leetcode.cn/problems/permutations-ii/)。
---
### 二分查找
二分查找思路虽然简单。。。但是细节真是要命。  
这里用**统一的思维解决所有二分查找问题。**
* 二分查找流程（三步骤）：
  1. 先筛选特例：
    例如：数组为空，或待查元素大于最大元素，导致下标溢出
  2. 框架：
      * 使用`while l<r, l=0, r=size-1`, 这样while出来后一定是l=r。 **是左闭右闭区间**。
      * `mid = (l+r)//2` 向下取整 或  `mid = (l+r+1)//2` 向上取整；具体根据情况，下面会介绍
      * 利用**排除法**：***排除肯定不是解的部分，那么剩下就是解了。把肯定不是解的放在if中。*** 
  3. 根据题目看是否需要对最终选出的元素进行判断。
* 如果 else 下是l=mid，则要向上取整；否则可能会跳不出while  
* 可以看看[34-在排序数组中查找元素的第一个和最后一个位置](https://github.com/czzbb/leetcode-python/blob/master/code/0034-%E5%9C%A8%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E6%9F%A5%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%E5%92%8C%E6%9C%80%E5%90%8E%E4%B8%80%E4%B8%AA%E4%BD%8D%E7%BD%AE.md)和
[35-搜索插入的位置](https://github.com/czzbb/leetcode-python/blob/master/code/0035-%E6%90%9C%E7%B4%A2%E6%8F%92%E5%85%A5%E4%BD%8D%E7%BD%AE.md)加深理解
* 此外，**旋转排序数组**的题目也可以练练，进一步熟悉下：
[33-搜索旋转排序数组](https://github.com/czzbb/leetcode-python/blob/master/code/0033-%E6%90%9C%E7%B4%A2%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84.md), 
[81-搜索旋转排序数组 II](https://github.com/czzbb/leetcode-python/blob/master/code/0081-%E6%90%9C%E7%B4%A2%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%20II.md), 
[153-寻找旋转排序数组中的最小值](https://github.com/czzbb/leetcode-python/blob/master/code/0153-%E5%AF%BB%E6%89%BE%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9C%80%E5%B0%8F%E5%80%BC.md), 
[154-寻找旋转排序数组中的最小值 II](https://github.com/czzbb/leetcode-python/blob/master/code/0154-%E5%AF%BB%E6%89%BE%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9C%80%E5%B0%8F%E5%80%BC%20II.md)

---
### 并查集
并查集经常用于：变量之间的**关系具有传递性**时  
[并查集基本模板](https://github.com/czzbb/leetcode-python/blob/master/code/0000-%E5%B9%B6%E6%9F%A5%E9%9B%86%E5%9F%BA%E6%9C%AC%E6%A8%A1%E6%9D%BF.md)  

**无权重并查集**
[547. 省份数量](https://github.com/czzbb/leetcode-python/blob/master/code/0547-%E7%9C%81%E4%BB%BD%E6%95%B0%E9%87%8F.md), 
[990. 等式方程的可满足性](https://github.com/czzbb/leetcode-python/blob/master/code/0990-%E7%AD%89%E5%BC%8F%E6%96%B9%E7%A8%8B%E7%9A%84%E5%8F%AF%E6%BB%A1%E8%B6%B3%E6%80%A7.md), 
[785. 判断二分图](https://github.com/czzbb/leetcode-python/blob/master/code/0785-%E5%88%A4%E6%96%AD%E4%BA%8C%E5%88%86%E5%9B%BE.md), 
[130. 被围绕的区域](https://github.com/czzbb/leetcode-python/blob/master/code/0130-%E8%A2%AB%E5%9B%B4%E7%BB%95%E7%9A%84%E5%8C%BA%E5%9F%9F.md)  
**带权重并查集**
[399. 除法求值](https://github.com/czzbb/leetcode-python/blob/master/code/0399-%E9%99%A4%E6%B3%95%E6%B1%82%E5%80%BC.md)
