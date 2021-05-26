# 剑指 Offer 36. 二叉搜索树与双向链表
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

为了让您更好地理解问题，以下面的二叉搜索树为例：

我们希望将这个二叉搜索树转化为双向循环链表。链表中的每个节点都有一个前驱和后继指针。对于双向循环链表，第一个节点的前驱是最后一个节点，最后一个节点的后继是第一个节点。

下图展示了上面的二叉搜索树转化成的链表。“head” 表示指向链表中有最小元素的节点。

特别地，我们希望可以就地完成转换操作。当转化完成以后，树中节点的左指针需要指向前驱，树中节点的右指针需要指向后继。还需要返回链表中的第一个节点的指针。


## 代码
```python
class j36_Solution:
    # 二叉搜索树中序遍历为升序
    # 在遍历的过程中，记录上一个节点pre，
    # 每次到一个节点，都将 pre 和 cur 互指，即 pre.right, cur.left = cur, pre
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        if not root:return
        cur = root
        st = []
        pre = None
        while cur or st:
            while cur:
                st.append(cur)
                cur = cur.left
            cur = st.pop()
            # 对节点进行操作
            if pre:
                pre.right, cur.left = cur, pre
            else:
                head = cur
            pre = cur
            #
            cur = cur.right
        head.left, pre.right = pre, head
        return head
```
```python
class j36__Solution:
    # 递归
    # 递归过程中记录下上一个节点
    def treeToDoublyList(self, root: 'Node') -> 'Node':
        def dfs(node):
            if not node:return
            # 左
            dfs(node.left)
            # 中
            if self.pre:
                self.pre.right, node.left = node, self.pre
            else:
                self.head = node
            self.pre = node
            # 右
            dfs(node.right)

        if not root:return
        self.pre = None
        dfs(root)
        self.head.left, self.pre.right = self.pre, self.head
        return self.head
```
