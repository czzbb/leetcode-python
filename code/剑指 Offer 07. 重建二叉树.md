# 剑指 Offer 07. 重建二叉树
**难度:medium**
## 题目
原文链接：https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

例如，给出
```
前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```

## 思路
* 与[105. 从前序与中序遍历序列构造二叉树](https://github.com/czzbb/leetcode-python/blob/master/code/0105-%E4%BB%8E%E5%89%8D%E5%BA%8F%E4%B8%8E%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97%E6%9E%84%E9%80%A0%E4%BA%8C%E5%8F%89%E6%A0%91.MD)相同
* 先序遍历可以确定根节点，而根节点在中序遍历中可以确定左右子树。
* 再通过递归子问题来求解

## 代码
```python
class j7_Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not preorder:return
        root = TreeNode(preorder[0])
        cnt = inorder.index(preorder[0])
        root.left = self.buildTree(preorder[1:1+cnt], inorder[:cnt]) # 左子树子问题
        root.right = self.buildTree(preorder[1+cnt:], inorder[cnt+1:]) # 右子树子问题
        return root
```
