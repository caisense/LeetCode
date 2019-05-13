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

{% page-ref page="1-200/22.-kuo-hao-sheng-cheng.md" %}

{% page-ref page="1-200/36.-you-xiao-de-shu-du.md" %}

{% page-ref page="1-200/37.-jie-shu-du.md" %}

{% page-ref page="1-200/39.-zu-he-zong-he.md" %}

{% page-ref page="1-200/40.-zu-he-zong-he-ii.md" %}

{% page-ref page="1-200/46.-quan-pai-lie.md" %}

{% page-ref page="1-200/47.-quan-pai-lie-ii.md" %}

{% page-ref page="1-200/77.-zu-he.md" %}

{% page-ref page="1-200/78.-zi-ji.md" %}

{% page-ref page="1-200/90.-zi-ji-ii.md" %}

