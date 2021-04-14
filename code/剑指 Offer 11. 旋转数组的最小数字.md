# 剑指 Offer 11. 旋转数组的最小数字
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

**示例 1：**
```
输入：[3,4,5,1,2]
输出：1
```
**示例 2：**
```
输入：[2,2,2,0,1]
输出：0
```

## 思路
* 同[154. 寻找旋转排序数组中的最小值 II](https://github.com/czzbb/leetcode-python/blob/master/code/0154-%E5%AF%BB%E6%89%BE%E6%97%8B%E8%BD%AC%E6%8E%92%E5%BA%8F%E6%95%B0%E7%BB%84%E4%B8%AD%E7%9A%84%E6%9C%80%E5%B0%8F%E5%80%BC%20II.md)
* 有序： `nums[mid] < nums[r]`，则在`[l, mid]`中
* 无序： `nums[mid] > nums[r]`, 则在`[mid+1, r]`中
* 若`nums[mid] == nums[r]`，是无法判断在左还是右区间，则将整个区间减一。例如`[1,1,1,0,1],[1,0,1,1,1]`
* 因为这样，若删除的元素`nums[r]`是最小的，`nums[mid]`也是最小的，还在数组中。
* **找最小值**，只能比较`mid`和`right`，不能比较`mid`和`left`！！例如`nums[left]<nums[mid]`时，会出现两种情况： `[0,1,2,3,4], [2,3,4,0,1]`。
* 因为当一个区间有序时，不能排除最左边的元素

## 代码
```python
class j11_Solution:
    def minArray(self, numbers: List[int]) -> int:
        l, r = 0, len(numbers)-1
        while l<r:
            mid = (l+r)>>1
            if numbers[mid] > numbers[r]:
                l = mid+1
            elif numbers[mid] < numbers[r]:
                r = mid
            else:
                r -= 1
        return numbers[l]
```
