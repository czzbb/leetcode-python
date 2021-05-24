# 剑指 Offer 34. 二叉树中和为某一值的路径
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/

输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

**示例:**
```
给定如下二叉树，以及目标和 target = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

[
   [5,4,11,2],
   [5,8,4,5]
]
```

## 代码
```python
class j34_Solution(object):
    # 同113
    # 遍历二叉树，在遍历过程中，记录下经过的路径，在叶子节点时做判断
    # 使用BFS
    # stack中每个元素为([路径], 节点)
    def pathSum(self, root, sum_):
        ans = []
        if not root:
            return ans
        stack = [([root.val],root)]
        while stack:
            tmp_list, node = stack.pop()
            if not node.left and not node.right and sum(tmp_list)==sum_:
                ans.append(tmp_list)
            if node.right:
                stack.append((tmp_list + [node.right.val],node.right))
            if node.left:
                stack.append((tmp_list + [node.left.val],node.left))
        return ans
```
```python
class j34__Solution(object):
    # 回溯算法
    # 这里的路径（tmp）是相互独立的，因此不用撤销选择，但是浪费空间
    # 递归函数输入：下一个节点，当前经过的路径
    def pathSum(self, root, sum_):
        def helper(node, tmp):
            # 为空或者到叶子节点了
            if not node:
                return
            if not node.left and not node.right and node.val + sum(tmp)==sum_:
                ans.append(tmp+[node.val])
            # 做选择
            if node.left:
                helper(node.left, tmp+[node.val])
            if node.right:
                helper(node.right, tmp+[node.val])
        ans = []
        helper(root, [])
        return ans
```
```python
class j34___Solution:
    # 同上的回溯，不过这里使用的路径不是独立的，因此需要撤销选择
    # 函数输入：下一个节点，当前的路径和
    def pathSum(self, root: TreeNode, sum_: int) -> List[List[int]]:
        ans = []
        self.path = [] # 经过的路径
        def helper(root, s):
            #
            if not root:return
            s += root.val # 到当前节点的路径和
            if not root.left and not root.right and s == sum_: # 是叶子节点
                ans.append(self.path+[root.val])
            #
            if root.left:
                self.path += [root.val] # 做选择
                helper(root.left, s)    # 递归
                self.path.pop()         # 撤销选择
            #
            if root.right:
                self.path += [root.val] # 做选择
                helper(root.right, s)   # 递归
                self.path.pop()         # 撤销选择
        helper(root, 0)
        return ans
```
