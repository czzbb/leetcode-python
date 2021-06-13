# 剑指 Offer 55 - I. 二叉树的深度
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

**例如：**
```
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```


## 代码
```python
class j55_1_Solution:
    # 同104
    # dfs
    def maxDepth(self, root: TreeNode) -> int:
        if not root:return 0
        return max(self.maxDepth(root.left), self.maxDepth(root.right))+1
class j55_1__Solution:
    # bfs
    def maxDepth(self, root: TreeNode) -> int:
        if not root:return 0
        level = 0
        cur_line = [root]
        while cur_line:
            level+=1
            next_line = []
            for node in cur_line:
                if node.left:next_line.append(node.left)
                if node.right:next_line.append(node.right)
            cur_line = next_line
        return level
```
