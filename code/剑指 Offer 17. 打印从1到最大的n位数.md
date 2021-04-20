# 剑指 Offer 17. 打印从1到最大的n位数
**难度:easy**
## 题目
原文链接：https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

**示例 1:**
```
输入: n = 1
输出: [1,2,3,4,5,6,7,8,9]
```

## 代码
```python
class j17_Solution:
    # 需要考虑大数的情况，即超出int范围的数。
    # 因此只能用str来表示数。（剑指中返回的应该要是str,但是这里返回int）
    # 通过递归遍历的方法得到所有答案
    # 但最终答案要删除前面多余的0，以及输出是从1开始
    def printNumbers(self, n: int) -> List[int]:
        def dfs(ind):
            # ind 表示当前要处理第ind位数
            if ind == n:#得到一个值，
                # 删除前面多余的0
                start = 0 # 表示第一个不是0的数的ind
                while start<n-1 and path[start] == '0':
                    start+=1
                #
                ans_one = ''.join(path[start:])
                ans.append(int(ans_one))
            else:
                for i in range(10):
                    path[ind] = str(i)
                    dfs(ind+1)

        path = ['0']*n
        ans = []
        dfs(0)
        return ans[1:]#输出从1开始
```
```python
class j17__Solution:
    # 上述方法在得到答案后要进行后处理：删除多余的0，即更新start的值。
    # 在遍历时，只有在9, 99, 999等之后，start才会改变，即减1。
    # 因此维护一个全局变量nine，表示出现9的个数。
    # start 初始值为n-1,并且可知遍历的结果是顺序的,即,1,2,3,4...
    # 因此，当 nine = n - start(有效个数),即有效个数全是9时，start-=1
    # 这里需要好好理解遍历的过程
    def printNumbers(self, n: int) -> List[int]:
        def dfs(ind):
            if ind == n:
                ans_one = ''.join(path[self.start:])
                if ans_one != '0':ans.append(int(ans_one))
                if n -self.start == self.nine: self.start -= 1 # 表示到了全是9的时候，要进一位了
            else:
                for i in range(10):
                    if i == 9:self.nine+=1
                    path[ind] = str(i)
                    dfs(ind+1)
                self.nine -= 1 # 需要撤回

        ans = []
        self.start = n-1 # 非0开始的位置
        self.nine = 0 # 出现9的个数
        path = ['0']*n
        dfs(0)
        return ans
```
