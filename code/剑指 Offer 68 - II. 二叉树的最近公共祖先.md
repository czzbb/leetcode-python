# 剑指 Offer 68 - II. 二叉树的最近公共祖先
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]

**示例 1:**
```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```

## 代码
```python
class j68_2_Solution(object):
    # 同236
    # 一共三种情况
    # 1. p，q在 root 两侧，则返回root
    # 2. p，q在 root 同侧，则变为该侧的子问题
    # 3. p，q中有个值为root, 则返回 root
    #
    # 再看代码，也可以这样理解：
    # 从下至上，如果有目标值，则往上传递目标值，否则传null；
    # 如果上传到某个节点时，左右都有值，则上传该节点
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        if not root or root == p or root == q:
            return root # 如果root==null，或者 p，q中有一个值是root，则返回root
        l = self.lowestCommonAncestor(root.left, p, q)
        r = self.lowestCommonAncestor(root.right, p, q)
        if not l: return r # 不在左边，则返回右边
        if not r: return l # 不在右边，则返回左边
        return root # 否则p，q在root的两边，则返回root
```
