# 剑指 Offer 33. 二叉搜索树的后序遍历序列
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：
```
     5
    / \
   2   6
  / \
 1   3
```
**示例 1：**
```
输入: [1,6,3,2,5]
输出: false
```
**示例 2：**
```
输入: [1,3,2,6,5]
输出: true
```

## 代码
```python
class j33_Solution:
    # 因为后序遍历最后一个是根
    # 那么根的值可以将列表分为两组，左边的都比根小，右边的都比根大；否则，返回False
    # 再递归遍历下面的层是否也满足条件
    def verifyPostorder(self, postorder: List[int]) -> bool:
        def dfs(l, r):
            if r - l < 2: return True # 两个及以下的都可以
            # 找到第一个比根大的索引 mid
            mid = l
            while postorder[mid]<postorder[r]:
                mid += 1
            # mid 及右边的都要比根大
            for i in range(mid, r):
                if postorder[i] < postorder[r]: # 如果右边的不都比根大，返回False
                    return False
            # 递归遍历
            return dfs(l, mid-1) and dfs(mid, r-1)
        return dfs(0, len(postorder)-1)
```
```python
class j33__Solution:
    # 后续遍历逆之后，可以看成是先序遍历，不过会先遍历右子树，再遍历左子树
    # 而先序遍历，在二叉搜索树中，往右会一直增大，直到碰到一个小值，
    # 再出栈找到小值的父节点（且是父节点的左子树）
    # 则对于这个节点，其右子树的节点（比该值大的节点）都会小于父节点，否则返回False
    def verifyPostorder(self, postorder: List[int]) -> bool:
        st = [] # 单调栈
        root = float('inf') # 初始化root的值，将树看成是该值的左子树
        # 逆序遍历
        for i in range(len(postorder)-1, -1, -1):
            if postorder[i] > root:return False # 左子树的值比根的值大
            while st and st[-1]>postorder[i]: # 找到 postorder[i] 父亲节点。并且 postorder[i] 为左子树。
                root = st.pop()
            st.append(postorder[i])
        return True
```
