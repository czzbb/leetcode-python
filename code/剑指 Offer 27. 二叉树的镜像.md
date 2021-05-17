# 剑指 Offer 27. 二叉树的镜像
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/

请完成一个函数，输入一个二叉树，该函数输出它的镜像。
```
例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
**示例 1：**
```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

## 代码
```python
class j27_Solution:
    # 同26题
    # 递归
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root:return
        root.left, root.right = self.mirrorTree(root.right), self.mirrorTree(root.left)
        return root
```
```python
class j27__Solution:
    # 迭代
    # 用栈或队列都行, 这里用栈
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root:return
        st = [root]
        while st:
            node = st.pop()
            node.left, node.right = node.right, node.left
            if node.left:st.append(node.left)
            if node.right:st.append(node.right)
        return root
```
