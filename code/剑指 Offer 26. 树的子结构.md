# 剑指 Offer 26. 树的子结构
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。
```
例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。
```
**示例 1：**
```
输入：A = [1,2,3], B = [3,1]
输出：false
```
**示例 2：**
```
输入：A = [3,4,5,1,2], B = [4,1]
输出：true
```

## 代码
```python
class j26_Solution:
    # 递归
    # 问题拆解：B是以A为根的子结构 + A的左子问题 + A的右子问题
    # 遍历每一个A的节点，对每一个节点，判断B是不是以该节点为根节点的子树。
    # 类似的题还有101，572，1367
    def helper(self, A, B):
        # 判断 B 是不是以 A为根节点的子树
        if not B:return True
        if not A or A.val != B.val:return False
        return self.helper(A.left, B.left) and self.helper(A.right, B.right)

    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:
        if not B or not A:return False
        flag = self.helper(A, B) # 判断A是不是根
        return flag or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)
```
