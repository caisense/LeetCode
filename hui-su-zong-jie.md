# 回溯总结

## 经典格式：

例如78题

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.res = []
        tmpList = []
        for i in range(len(nums)+1):  #len+1轮循环，每次输出长度为i的所有组合
            self.backtrack(nums, tmpList, i, 0)
        return self.res

    def backtrack(self, nums, tmpList, k, start):
        if len(tmpList) == k:
            self.res.append(list(tmpList))
        else:
            for i in range(start, len(nums)):
                #经典回溯格式
                tmpList.append(nums[i])
                self.backtrack(nums, tmpList, k, i + 1)
                tmpList.pop()
```

### 简化

上面的递归操作**实质**上是将本层tmpList修改后传入下一层递归，待递归完成后再将tmpList还原。这波操作可以简化为直接在下一层**递归函数的参数**中对tmpList修改，这样本层递归的tmpList其实是不变的。

```python
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        self.res = []
        tmpList = []
        for i in range(len(nums)+1):  #len+1轮循环，每次输出长度为i的所有组合
            self.backtrack(nums, tmpList, i, 0)
        return self.res

    def backtrack(self, nums, tmpList, k, start):
        if len(tmpList) == k:
            self.res.append(list(tmpList))
        else:
            for i in range(start, len(nums)):    
                #tmp的修改直接写在递归里
                self.backtrack(nums, tmpList+[nums[i]], k, i + 1)
```

## 题目列表：

**22.括号生成**

**36.有效的数独**

**37.解数独**

**39.组合总和**

**40.组合总和Ⅱ**

**46.全排列**

**47.全排列Ⅱ**

**77.组合**

**78.子集**

**90.子集Ⅱ**

