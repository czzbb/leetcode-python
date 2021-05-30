# 剑指 Offer 38. 字符串的排列
**难度:Medium**
## 题目
原文链接：https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

**示例:**
```
输入：s = "abc"
输出：["abc","acb","bac","bca","cab","cba"]
```

## 代码
```python
class j38_Solution:
    # 与47题相同：即可能出现重复元素，因此全排列可能会出现重复答案
    # 会有重复选择的情况：同一“层”时，选择了相同元素
    # 同一层：回溯时，for循环中表示同一层
    # 因此只要每层遍历时，排除选择过的选项就行，用集合cut表示选择过的选项
    def permutation(self, s: str) -> List[str]:
        def backtrace(path, ind):
            if ind == size:
                ans.append(path)
                return
            cur_seen = set() # 该层选择过的元素
            for i in range(size):
                if seen[i] == 0 and s[i] not in cur_seen:
                    cur_seen.add(s[i])
                    seen[i] = 1
                    backtrace(path + s[i], ind + 1)
                    seen[i] = 0

        if not s: return []
        size = len(s)
        seen = [0] * size
        ans = []
        backtrace('', 0)
        return ans
```
