# BFS总结
类似于102. 二叉树的层次遍历的复杂版，只是二叉树每个节点最多只有两个相邻，且单向图而已，BFS对图结构操作，每个节点可以有N个相邻结点，且是无向图。
思路：从起点出发，每轮迭代（一步）访问起点的所有邻结点，下一轮（第二步）访问邻结点的邻结点……一直到终点。还是用队列实现，而且要记录已访问结点（无向图，避免重复访问）。
### 通用范式

```python
    def BFS(start, target):
        q = queue.Queue()   #队列
        q.put(start)   #初始放入起点
        visited = set()  #记录访问过的结点
        step = 0  #搜索迭代次数
        visited.add(start)
        
        while not q.empty():
            #记录当前队列大小（BFS本轮迭代），以供后续遍历
            size = q.qsize()
            for i in range(size):                
                cur = q.get()  #从队列取出一个
                #visited.add(cur)    #【2】加入已访问结点集合
               
                if cur == target:
                    return step
                #遍历cur结点的所有相邻结点，若未访问则加入队列
                for node in cur.adj():
                    if node not in visited:
                        q.put(node)
                        visited.add(node)	 #【1】加入已访问结点集合
            #注意要在此处更新迭代次数
            step += 1
```
关于标记已访问结点visited的时机，注释中有体现，一是在入队列时就标记（标记【1】），二是实际访问时标记（标记【2】），这两者虽然是等效的，但是这里有个小技巧，在入队时标记能减少很多重复的结点入队。

