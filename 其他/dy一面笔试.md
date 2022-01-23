# dy一面笔试

m*n宫格里，.表示路，#表示障碍，s表示起点，e表示终点，无法完成任务输出-1，求最短步数

用例：
```
* 测试1：Ans=7
s.....
......
.....e
* 测试2: Ans=9
s##...
....#.
.####e
* 测试3: Ans=-1
s.....
....##
....#e
```

## 解法：bfs

从起点开始bfs，每圈算一步，直到终点

```python
import queue
class Solution:
    def leastStep(self, grid):
        visited = []
        q = queue.Queue()   #队列
        q.put((0,0))
        visited.append((0,0))
        step = -1	#从起点开始算步数
        while not q.empty():
            size = q.qsize()
            step += 1
            for _ in range(size):
                i, j = q.get()
                visited.append((i, j))
                if grid[i][j] == 'e':	#到达终点直接返回
                    return step
               	#看上下左右位置是否有路（在格子内，非路障），并且未访问，则加入队列
                if i-1 >= 0 and grid[i-1][j] != '#' and (i-1, j) not in visited:
                    q.put((i-1, j))
                if i+1 < 3 and grid[i+1][j] != '#' and (i+1, j) not in visited:
                    q.put((i+1, j))
                if j-1 >= 0 and grid[i][j-1] != '#' and (i, j-1) not in visited:
                    q.put((i, j-1))
                if j+1 < 6 and grid[i][j+1] != '#' and (i, j+1) not in visited:
                    q.put((i, j+1))
        return -1	#无法到达终点

#测试
grid0 = ["s.....", "......", ".....e"]
grid1 = ["s##...", "....#.", ".####e"]
grid2 = ["s.....", "....##", "....#e"]
s = Solution()
print(s.leastStep(grid0))
print(s.leastStep(grid1))
print(s.leastStep(grid2))
```