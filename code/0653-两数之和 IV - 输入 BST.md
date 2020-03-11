# 653. 两数之和 IV - 输入 BST
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/two-sum-iv-input-is-a-bst/

给定一个二叉搜索树和一个目标结果，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 true。

**案例 1:**
```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7
```
Target = 9

输出: True
 
**案例 2:**
```
输入: 
    5
   / \
  3   6
 / \   \
2   4   7
```
Target = 28

输出: False

## 思路
* 二叉搜索树的中序遍历为升序
* 先用数组 *nums* 保存中序遍历结果
* 再从两头向中间遍历数组直到满足条件或遍历结束
## 代码
```python
class a653_Solution(object):
    def findTarget(self, root, k):
        """
        :type root: TreeNode
        :type k: int
        :rtype: bool
        """
        if not root:
            return False
        # 非递归中序遍历
        st = []
        p = root
        nums = []
        while p or st:
            while p:
                st.append(p)
                p = p.left
            p = st.pop()
            nums.append(p.val)
            p = p.right
        # 双指针，头尾向中间查找
        i = 0
        j = len(nums)-1
        while i<j:
            if nums[i] + nums[j] ==k:
                return True
            if nums[i] + nums[j] >k:
                j -= 1
            else:
                i += 1
        return False
```
