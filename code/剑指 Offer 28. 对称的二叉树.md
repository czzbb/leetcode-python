# 剑指 Offer 28. 对称的二叉树
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
```
**示例 1：**
```
输入：root = [1,2,2,3,4,4,3]
输出：true
```
**示例 2：**
```
输入：root = [1,2,2,null,3,null,3]
输出：false
```

## 代码
```python
class j28_Solution(object):
    # 同101
    # 递归
	def isSymmetric(self, root):
		"""
		:type root: TreeNode
		:rtype: bool
		"""
		if not root:
			return True
		def dfs(left,right):
			# 递归的终止条件是两个节点都为空
			# 或者两个节点中有一个为空
			# 或者两个节点的值不相等
			if not (left or right):
				return True
			if not (left and right):
				return False
			if left.val!=right.val:
				return False
			return dfs(left.left,right.right) and dfs(left.right,right.left)
		# 用递归函数，比较左节点，右节点
		return dfs(root.left,root.right)
```
```python
class j28__Solution(object):
    # 迭代
    # 用bfs的方法
    # 判断每个对称位置的值是否相同
    # 入队时，从头尾开始入队，这样每次出队两个时，都是对称的节点，判断是否相同
    # 对于比较过的两个节点，将其子节点对称入队
	def isSymmetric(self, root):
		"""
		:type root: TreeNode
		:rtype: bool
		"""
		if not root or not (root.left or root.right):
			return True
		# 用队列保存节点
		queue = [root.left,root.right]
		while queue:
			# 从队列中取出两个节点，再比较这两个节点
			left = queue.pop(0)
			right = queue.pop(0)
			# 如果两个节点都为空就继续循环，两者有一个为空就返回false
			if not (left or right):
				continue
			if not (left and right):
				return False
			if left.val!=right.val:
				return False

			# 将左节点的左孩子， 右节点的右孩子放入队列
			queue.append(left.left)
			queue.append(right.right)
			# 将左节点的右孩子，右节点的左孩子放入队列
			queue.append(left.right)
			queue.append(right.left)
            # 或者用extend
            # queue.extend([left.left,right.right,left.right, right.left])
		return True
```
