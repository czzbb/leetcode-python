# 从上到下打印二叉树
## 题目
原文链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/  
原文链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/  
原文链接：https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/submissions/

## 代码
打印为一行
```python
class j32_1_Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        if not root:return []
        q = deque()
        q.append(root)
        ans = []
        while q:
            node = q.popleft()
            #
            ans.append(node.val)
            #
            if node.left:q.append(node.left)
            if node.right:q.append(node.right)
        return ans
```
按层次打印
```python
class j32_2_Solution:
    # 同102
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:return []
        cur_layer = [root]
        ans = []
        while cur_layer:
            ans_line = []
            next_layer = []
            for node in cur_layer:
                ans_line.append(node.val)
                if node.left:next_layer.append(node.left)
                if node.right:next_layer.append(node.right)
            ans.append(ans_line)
            cur_layer = next_layer
        return ans
```
奇数层顺序，偶数层逆序打印
```python
class j32_3_Solution:
    # 同103
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root:return []
        cur_layer = [root]
        ans = []
        layer = 1
        while cur_layer:
            ans_line = []
            next_layer = []
            for node in cur_layer:
                ans_line.append(node.val)
                if node.left:next_layer.append(node.left)
                if node.right:next_layer.append(node.right)
            if layer&1 == 0:
                ans_line.reverse()
            ans.append(ans_line)
            cur_layer = next_layer
            layer+=1
        return ans
```
