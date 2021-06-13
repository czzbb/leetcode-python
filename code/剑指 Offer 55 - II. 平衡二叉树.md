# 剑指 Offer 55 - II. 平衡二叉树
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

**示例 1:**
```
给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。
```
**示例 2:**
```
给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。
```


## 代码
```python
class j55_2_Solution:
    # 同110
    # 自顶向下，先序遍历
    # 即先求当前节点是否满足要求，再判断左右子树
    # 这样会出现很多的重复计算
    def height(self, root):
        if not root:return 0
        return max(self.height(root.left), self.height(root.right))+1

    def isBalanced(self, root: TreeNode) -> bool:
        if not root:return True
        l, r = self.height(root.left), self.height(root.right)
        return abs(l-r)<2 and self.isBalanced(root.left) and self.isBalanced(root.right)
class j55_2__Solution:
    # 自底向上，后续遍历，避免了每次比较时都要重新计算高度
    # 即先判断左、右子树是否满足条件，再判断当前子树
    # 返回该节点是否平衡以及该节点的高度
    def isBalancedHelper(self, root: TreeNode) -> (bool, int):
        if not root:
            return True, 0
        # 判断左右子树是否平衡
        leftIsBalanced, leftHeight = self.isBalancedHelper(root.left)
        if not leftIsBalanced:
            return False, -1
        rightIsBalanced, rightHeight = self.isBalancedHelper(root.right)
        if not rightIsBalanced:
            return False, -1
        # 如果左右子树都平衡了，返回该节点是否平衡
        return (abs(leftHeight - rightHeight) < 2), 1 + max(leftHeight, rightHeight)

    def isBalanced(self, root: TreeNode) -> bool:
        return self.isBalancedHelper(root)[0]
```
