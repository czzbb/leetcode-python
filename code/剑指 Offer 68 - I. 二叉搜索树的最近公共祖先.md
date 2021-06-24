# 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

**示例 1:**
```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6 
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

## 代码
```python
class j68_1_Solution:
    # 同235
    # 因为是二叉搜索树，所以容易判断是在哪一侧
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if p.val>q.val: p, q = q, p # 保证p是小的那个
        small, big = p.val, q.val
        while root:
            if root.val < small: # p，q都在右子树中
                root = root.right
            elif root.val > big: # p，q都在左子树中
                root = root.left
            else: # p，q分别在root的左、右子树或其中一个值就为root
                return root
```
