# 剑指 Offer 51. 数组中的逆序对
**难度:Hard**
## 题目
原文链接：https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

**示例 1:**
```
输入: [7,5,6,4]
输出: 5
```

## 代码
```python
class j51_Solution:
    # 在归并排序的时候计算逆序的个数
    # 归并排序需要一个临时数组 tmp
    # 在左或右区间归并时计算逆序数；注意不可以都计算，只能选一个计算
    # 进阶题：315
    def reversePairs(self, nums: List[int]) -> int:
        size = len(nums)
        self.ans = 0
        if size < 2: return 0
        tmp = [0] *size # 临时数组
        self.merge_sort(nums, 0, size-1, tmp)
        return self.ans

    def merge_sort(self, nums, l, r, tmp):
        if l == r:
            return
        mid = (l+r)>>1
        self.merge_sort(nums, l, mid, tmp)
        self.merge_sort(nums, mid+1, r, tmp)
        if nums[mid] < nums[mid+1]:
            return
        self.merge_count(nums, l, mid, r, tmp)

    def merge_count(self, nums, l, mid, r, tmp):
        # 在左区间归并时计算逆序数
        tmp[l:r+1] = nums[l:r+1]
        p1, p2 = l, mid+1 # 左区间和右区间的指针
        for i in range(l, r+1):
            if p1 > mid:
                break
            elif p2 > r:
                nums[i] = tmp[p1]
                self.ans += r - mid # 计算逆序数
                p1 += 1
            elif tmp[p1] <= tmp[p2]: # 注意这里要取等（如果只是排序的话无所谓）
                nums[i] = tmp[p1]
                self.ans += p2 - mid - 1
                p1 += 1
            else:
                nums[i] = tmp[p2]
                p2 += 1
```
