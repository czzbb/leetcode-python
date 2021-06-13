# 剑指 Offer 54. 二叉搜索树的第k大节点
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/

给定一棵二叉搜索树，请找出其中第k大的节点。

**示例 1:**
```
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 4
```
**示例 2:**
```
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 4
```

## 代码
```python
class j54_Solution:
    # 逆中序遍历
    def kthLargest(self, root: TreeNode, k: int) -> int:
        st = []
        p = root
        while st or p:
            while p:
                st.append(p)
                p = p.right
            p = st.pop()
            #
            k -= 1
            if k == 0:
                return p.val
            #
            p = p.left
class j54__Solution:
    # 递归
    def kthLargest(self, root: TreeNode, k: int) -> int:
        def dfs(root):
            if not root: return
            if self.k == 0: return #已经找到了，不用麻烦了
            #
            dfs(root.right)
            #
            self.k -= 1
            if self.k == 0:
                self.ans = root.val
                return
            #
            dfs(root.left)

        self.k = k
        dfs(root)
        return self.ans
```
