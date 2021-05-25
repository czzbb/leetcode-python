# 剑指 Offer 35. 复杂链表的复制
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

**示例 1：**
```
输入：head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
输出：[[7,null],[13,0],[11,4],[10,2],[1,0]]
```
**示例 2：**
```
输入：head = [[1,1],[2,1]]
输出：[[1,1],[2,1]]
```

## 代码
```python
class j35_Solution:
    # 同138
    # 一般而言，如果没有random，直接遍历就行。
    # 但是用random，遍历时并不知道random的具体位置。
    # 本题的关键在于：如何确定random的位置。
    # 因此，对每个节点，我们用哈希表记录其对应的新节点；再次遍历后即可
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:return
        # 负值各个节点，并且用哈希表记录：原节点对应的新节点
        cur = head
        dic = {}
        while cur:
            dic[cur] = Node(cur.val)
            cur = cur.next
        #
        cur = head
        while cur:
            node = dic[cur]
            node.next = dic.get(cur.next) # 这里要用get，不能直接 dic[cur.next]，因为有可能cur.next是空节点
            node.random = dic.get(cur.random)
            cur = cur.next
        #
        return dic[head]
```
```python
class j35__Solution:
    # 本题也可以看作对图的复制。图的遍历有bfs和dfs，这里用dfs
    # 关键在于如何确定 random 的位置。
    # 对每一个新节点，找到其next和random节点（若没有，则新建），使用哈希表记录已经创建过的节点。
    # 哈希表：key为原节点，value为新节点
    def copyRandomList(self, head: 'Node') -> 'Node':
        def dfs(head):
            # 返回对应的新建节点
            if not head: return
            if head not in dic:  # 如果该节点已经建立了，则直接返回建立的新节点
                node = Node(head.val)
                dic[head] = node # 一建立就需要放到哈希表中
                node.next = dfs(head.next)
                node.random = dfs(head.random)
            return dic[head]

        dic = {} #
        return dfs(head)
```
```python
class j35___Solution:
    # 使用bfs
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:return
        q = collections.deque()
        #
        q.append(head) # q 中记录着代处理的节点：即该节点的新节点已经创建，但是指针还没赋值
        head_c = Node(head.val)
        dic = {head:head_c} # key为原节点，value为新节点
        while q:
            node = q.popleft()
            node_c = dic[node]
            ## 对节点指针进行赋值
            # next
            if node.next and node.next not in dic: # 下一个指针没有出现过，创建节点，并记得要入队
                node_n = Node(node.next.val)
                dic[node.next] = node_n
                q.append(node.next)
            node_c.next = dic.get(node.next)
            # random
            if node.random and node.random not in dic:
                node_r = Node(node.random.val)
                dic[node.random] = node_r
                q.append(node.random)
            node_c.random = dic.get(node.random)
        return dic[head]
```
```python
class j35____Solution:
    # 之间空间复杂度都是O(n)，因为用到了哈希表
    # 哈希表的用途主要是找到random节点的位置
    # 如果对每个节点之后都复制一个节点，即
    # 原本：o1->o2->... 变成 :o1->n1->o2->n2....
    # 这样就可以找到random节点的位置，不需要额外的空间
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:return
        # 插入新的节点
        cur = head
        while cur:
            new = Node(cur.val)
            new.next = cur.next
            cur.next = new
            cur = cur.next.next
        # 处理新节点的 random。因为问题的关键就是找random节点，因此先处理random，再处理next
        cur = head
        while cur:
            new = cur.next
            new.random = cur.random.next if cur.random else None
            cur = cur.next.next
        # 处理next，并拆分
        cur = head
        top = head.next
        while cur:
            new = cur.next
            cur.next = cur.next.next
            new.next = new.next.next if new.next else new.next
            cur = cur.next
        return top
```
