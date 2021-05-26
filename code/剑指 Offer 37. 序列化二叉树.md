# 剑指 Offer 37. 序列化二叉树
**难度:Hard**
## 题目
原文链接：https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/

请实现两个函数，分别用来序列化和反序列化二叉树。

**示例: **
```
你可以将以下二叉树：

    1
   / \
  2   3
     / \
    4   5

序列化为 "[1,2,3,null,null,4,5]"
```

## 代码
```python
class j37_Codec:
    # 同297
    # DFS，先序遍历
    # 因为先序遍历好判断根节点
    # 将空节点赋值为 #
    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root: return ['#']
        l = self.serialize(root.left)
        r = self.serialize(root.right)
        return [root.val] + l + r

    def deserialize(self, data):
        # 这里data是共享的同一个变量，因此data在遍历完左子树后，再次输入遍历右子树时和输入左子树时的不同
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        node = data.pop(0)
        if node == '#': return None
        root = TreeNode(node)
        # print(data)
        root.left = self.deserialize(data)
        # print(data)
        root.right = self.deserialize(data)
        return root
```
```python
class j37__Codec:
    # BFS
    def serialize(self, root):
        # 先讲根节点入队
        # 在出队时，填入ans，并将左右子树入队
        # 如果出队时为空，则填入 #
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        if not root: return []
        ans = []
        q = deque([root])
        while q:
            node = q.popleft()
            if node:
                ans.append(node.val)
                q.append(node.left)
                q.append(node.right)
            else:
                ans.append('#')
        return ans

    def deserialize(self, data):
        # 先将第一个值入队
        # 在出队时，寻找左右子树，若子树非空，则再将子树入队
        # 使用队列是因为：我们先构建的节点，是之后节点的父节点，因此需要记录下
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data: return
        q = deque([TreeNode(data[0])])
        root = q[0]
        # 从第二个开始
        data = deque(data[1:])
        while data:
            node = q.popleft()
            # 左
            l_val = data.popleft()
            if l_val != '#':
                node.left = TreeNode(l_val)
                q.append(node.left)
            # 右
            r_val = data.popleft()
            if r_val != '#':
                node.right = TreeNode(r_val)
                q.append(node.right)
        return root
```
