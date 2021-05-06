# 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

**示例：**
```
输入：nums = [1,2,3,4]
输出：[1,3,2,4] 
注：[3,1,2,4] 也是正确的答案之一。
```

## 代码
```python
class j21_Solution:
    # 双指针：快慢指针法
    # nums[:slow] 中为奇数
    # 判断条件：x&1 等价于 x%2
    def exchange(self, nums: List[int]) -> List[int]:
        slow, fast = 0, 0
        for _ in range(len(nums)):
            if nums[fast]&1:
                nums[fast], nums[slow] = nums[slow], nums[fast]
                slow+=1
            fast+=1
        return nums
```
```python
class j21__Solution:
    # 双指针：首尾指针
    # nums[:l]为奇数，nums[r:]为偶数
    def exchange(self, nums: List[int]) -> List[int]:
        l, r = 0, len(nums)-1
        while l<r:
            while l<r and nums[l]&1:l+=1 # l走到偶数，表示要交换
            while l<r and not nums[r]&1: r-=1 # r走到奇数，表示要交换
            nums[l], nums[r] = nums[r], nums[l] # 交换
        return nums
```
