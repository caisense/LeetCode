# python初学问题总结

## 1.注意浮点除法`'/'`和整数除法`'//'` 的区别

## 2.注意整数除法与c语言的区别，c语言是向0取整，python是向下取整：
先用浮点除法python计算`5➗3`的精确值：
```
>>> 5/3
1.6666666666666667
>>> -5/3
-1.6666666666666667
```
c语言整数除法：
```
5 / 3    //1
-5 / 3    //-1
```
python整数除法：
```
>>> 5 // 3
1
>>> -5 // 3
-2

```
由此可得结论，对于**正数**的整数除法，python与c的结果一样；对于**负数**则不一样。

## 3.注意取模运算python与c语言的区别：
具体分析：
c语言：

```
5 % 3 = 2
-5 % 3 = -2
```
python：

```
5 % 3 = 2
-5 % 3 = 1
```
发现c语言和py中，-5对3取模，结果分别为-2和1。这两种结果都对，因为

```
-5 = 3 * (-1) + (-2)
-5 = 3 * (-2) + 1  #由于py向下取整，因此-5/3结果为-2
```
总结：对于**正数**，py与c语言取模结果一样；对于**负数**则不一样，一般c语言取模为负数，py为正


## 4.list和tuple的双冒号切片：
`s[i:j:k]`表示：切片第从`i`到`j`，间隔为1`k`

10以内的数，默认从开始到末尾，且间隔为`1`：
```
>>> range(10)[::]
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```
20以内的数，从第1到第18号，间隔为3
```
>>> range(20)[1:18:3]
[1, 4, 7, 10, 13, 16]
```

若`k`为负数，表示`反向`

```
>>> range(10)[::-1]
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

k为-2，表示从0号开始，反向每2个元素取一个（第一个是0，第二个是9，第三个是8，第四个是7，以此类推......)

```
>>> range(10)[::-2]
[9, 7, 5, 3, 1]
```

**注意**：使用负数间隔时，若要自己指定起始范围，则范围应该也是反向的。
如：20以内的数，从10号开始，到0号结束，每次间隔为2

```
>>> range(20)[10:0:-2]
[10, 8, 6, 4, 2]
```
若范围与间隔不匹配，取到的切片为空
```
>>> range(20)[0:10:-2]  #范围是正向，而间隔反向，取不到
[]
```

## 5.逻辑运算符与c语言不同
c语言中与、或、非分别为`&&`、`||`和`!`
而py中为`and`、`or`和`not`
其他的比如`==`, `>`，`>=` ,`!=`等**比较运算符**相同

## 6.python中的三目运算符
python中没有其他语言中的三元表达式，不过有类似的实现方法 
c++中三目运算符：

```
int a = 1;
int b = 2;
int c = a > b ? a : b;  //c等于a和b中的较大者
```

python中只有类似的替代办法，将if-else语句嵌套在赋值语句中：

```
a = 1
b = 2
c = a if a > b else b  #c等于a和b中的较大者
```

## 7.C++中的NULL，在Python中为None
`None`是一种特殊数据类型

```
>>>type(None)
<class 'NoneType'>
```

在判断表达式中，均为False：

```
f = None
if f:
	print("f is True")
else:
	print("f is False")
```
输出：f is False

## 8.if判断语句为真或者假的情况：
判断为`True`：只要x是**非零数值**（正数、负数）、非空字符串、非空list等（即为非`None`）
判断为`False`：数值`0`（包括负0：-0）和`None`、空字符串、空list等：

```
l = []  #空list
if l:
    print("True")
else:
    print("False")  #输出False
```

```
l = ""  #空串
if l:
    print("True")
else:
    print("False")  #输出False
```

## 9.二维数组的创建和初始化

首先介绍下`*`运算，对于一个整数，`*`表示乘法运算：

```
>>> m = 1
>>> m * 5
5
```
对于字符串和列表，`*`进行了重载，表示重复：

```
>>> m = "hello "
>>> m * 3  #字符串重复三遍，注意包括末尾空格
'hello hello hello '
```

```
>>> m = [0,1]
>>> m * 3  #列表重复三遍
[0, 1, 0, 1, 0, 1]
```
需要注意，若要构造**嵌套列表**，需要加上`[]`：

```
>>> m = [0,1]
>>> [m] * 3  #注意加上列表符号
[[0, 1], [0, 1], [0, 1]]
```
**由此引出二维数组的第一种创建方式：**
创建5*6的矩阵，初始为0
```
>>> n = [0] * 6  #创建列表[0, 0, 0, 0, 0, 0]
>>> matrix = [n] * 5  #创建5*6矩阵
```
终极简化版：

```
matrix = [[0]*6]*5
```

**第二种方式：**
用[列表推导式](https://jizhi.im/course/dl_python/2)先在`[]`中用for循环创建一个list，在外层`[]`继续用for循环创建list
```
>>> matrix = [[0 for i in range(6)] for i in range(5)]  #注意内外层区别。
```
或者写作：
```
>>> matrix = [[0 for _ in range(6)] for _ in range(5)]  #因为i不用，可以用缺省符号‘_’代替
```
什么是列表推导式：

```
l1 = [ x for x in range(10) ]
# [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
# 创建0-9的列表

l2 = [ x + 1 for x in range(10) ]
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
# 创建1-10的列表


l3 = [ x for x in range(10) if x % 2 == 0 ]
# [0, 2, 4, 6, 8]
# 10以内偶数列表
```
**然而实际使用时发现**，第一种方式创建的二维数组，列方向上的元素会集体改变：

```
>>> dp = [[False] * 3] * 4
>>> dp  #3行4列bool数组，初始为FALSE
[[False, False, False], [False, False, False], [False, False, False], [False, False, False]]
>>> dp[1][2]=True
>>> dp  #发现第2列的全部变TRUE
[[False, False, True], [False, False, True], [False, False, True], [False, False, True]]
>>> dp[2][0]=True
>>> dp  #发现第0列的全部变TRUE
[[True, False, True], [True, False, True], [True, False, True], [True, False, True]]
>>> 

```
因此若二维数组之后还需使用的话，外层不能用`*`的方法构建，可以改为：

**第三种方法：**

```
matrix = [[0] * 6 for _ in range(5)]
```

## 10.`in`运算符还有对应的`not in`运算符
`in`运算符可以用于判断字符串是否包含另一个字符串，返回的是布尔值
同理`not in`可以用来判断字符串是否`不包含`另一个字符串，返回也是布尔值
因此没必要先用in然后在表达式前面加not了，直接not in。

## 11.py中的for循环内改变循环变量（i），并不会改变循环次数，而c++会改变次数。此外循环范围也不能改变（start，end）
看下面C++代码：

```
for (int i = 0; i < 10; i++) {
		cout << i << endl;
        if (i == 2) {
            i += 1;
        }        
    }
```
输出：

```
0
1
2
4
5
6
7
8
9
```
可以看到在i==2时，i增加了1，下一次for循环i加1，因此直接从4开始，跳过了i==3。`循环只执行了9次！`
而类似的py代码中：

```
for i in range(10): 
	print(i)
    if i == 2:      
        i += 1              
```
输出：

```
0
1
2
3
4
5
6
7
8
9
```
可以看到`循环依然执行了10次`，即i==2时虽然i增加1，但是下一次for循环依然从i=3执行。

**结论：py中对for循环变量的修改不会影响到for的循环次数，也就是说，对循环变量的修改只在当前轮次内有效，不影响下一个循环**

**若要对循环变量进行修改，且下一轮仍有效，应该使用while循环。**

**对循环范围修改也是无效的，应改用while：**
https://blog.csdn.net/u012033124/article/details/79080631

## 12. py中的多变量for循环（使用zip打包）
c++中有如下形式：

```
for (int i = 0, j = 1, k = 2; i < 9, j < 9, k < 11; i++, j++, k++) {
    cout << i << " " << j << " " << k << " " << endl;
}
```
输出：

```
0 1 2 
1 2 3 
2 3 4 
3 4 5 
4 5 6 
5 6 7 
6 7 8 
7 8 9 //j先到达终点，然而并未停下
8 9 10
```

py中：
```
>>> for i,j,k in zip(range(9), range(1,9), range(2,11)):  #每次对三个变量分别循环，用zip打包，实际上是用for遍历zip
...    print(i,j,k)
... 
0 1 2
1 2 3
2 3 4
3 4 5
4 5 6
5 6 7
6 7 8
7 8 9  #j先到达终点，所有变量一起结束
```
可以看到c++与py的区别，当某一个变量到达终点时，py全部停止，而c++是继续，直到所有变量到达终点。

在这一题中有用到：
https://blog.csdn.net/u012033124/article/details/80695353

## 13.列表表达式

```
[表达式 for 变量 in 列表]    或者  [表达式 for 变量 in 列表 if 条件]
```

顾名思义，列表（list）表达式包含一个list
详见：https://www.cnblogs.com/yupeng/p/3428556.html


## 14.解包**（符号：`*`）
https://blog.csdn.net/pfm685757/article/details/50464426

以上两点再这道题目第二种解法中展现得淋漓尽致：
https://blog.csdn.net/u012033124/article/details/80515131

## 15.and or表达式的进一步理解
实际上是起到一个`“短路”`的作用
`and`：从左到右扫描，返回第一个为`假`的表达式值，无假值则返回最后一个表达式值。

```
>>> 1 and 0
0
>>> 0 and -1
0
>>> 2 and 4
4
```

`or`：从左到右扫描，返回第一个为`真`的表达式值，无真值则返回最后一个表达式值（因为真值是非0值，所以无真值一般只有全0的情况，返回假）。

```
>>> 2 or 3
2
>>> 3 or 0
3
>>> 0 or 0
0
```
https://blog.csdn.net/niuniuyuh/article/details/71213887

## 16.list（或tuple）之间的比较是字典序的：
先比较第一个元素，谁的大相应的list就大；相等则比较第二个元素，以此类推。。。
```
>>> (1, 9) < (2, 7)
True
>>> (2, 7) == (2, 7)
True
>>> (2, 7) < (2, 8)
True
>>> (-1, 7) < (0, 8)  #负数也适用
True
>>> (-2, 7) < (-1.5, 8)  #小数也是
True
```
因此按字典排序（第一位比第二位重要，第二位比第三位重要。。。），可以在sorted函数中的key参数使用lambda表达式：

```
>>> people
[[9, 0], [7, 0], [1, 9], [3, 0], [2, 7], [5, 3], [6, 0], [3, 4], [6, 2], [5, 2]]
#排序，按第一位降序，若第一位相等则第二位升序
>>> sorted(people, key=lambda x:(-x[0], x[1]))
[[9, 0], [7, 0], [6, 0], [6, 2], [5, 2], [5, 3], [3, 0], [3, 4], [2, 7], [1, 9]]
```
在这一题中有使用：
https://blog.csdn.net/u012033124/article/details/79099404

## 17.多个lambda式的写法

```
        cal = {"+" : lambda x,y :x+y, "-" : lambda x,y : x-y, "*" : lambda x,y : x*y, "/" : lambda x,y : int(x/y)}
        #处理每个字符
        for t in tokens:
            if t in ops:  
                num1 = stack.pop()
                num2 = stack.pop()
                #注意运算顺序
                stack.append(cal[t](num2, num1))
```
https://cai-sen-se.gitbook.io/leetcode/150.-ni-bo-lan-biao-da-shi-qiu-zhi
实质上是用了**字典**，将四个lambda表达式作为值，四种运算符号作为键。

## 18.list转dict
list转map需要每个元素都为长度2的子list，转dict后第0个元素为key，第1个元素为value

```
>>> l = [[0,29],[1,34]]
>> dict(l)
{0: 29, 1: 34}
```
若有元素长度不符合：
```
>>> l = [[0,29,3],[1,34]]
>>> dict(l)
#报错
```
见
https://cai-sen-se.gitbook.io/leetcode/601-800/732.-wo-de-ri-cheng-an-pai-biao-iii

## 19.dict初始化
dict的key没有默认对应value（不像c++），因此遇到第一次出现的key时往往需要特殊处理
详见：
https://cai-sen-se.gitbook.io/leetcode/~/edit/drafts/-Lav6nf8yvGNZMaYIw4t/601-800/609.-zai-xi-tong-zhong-cha-zhao-zhong-fu-wen-jian

## 20.二进制表示
c语言中是用补码，而py中使用原码加正负号表示：


     >>> bin(6)
    '0b110'
     >>> bin(-6)
     '-0b110'		#-6的补码应该是1010
     >>> bin(~6)
    '-0b111'		#6按位取反应该是1001

## 21.可哈希和不可哈希的类型
总结： 
（1）list、set、dict：是不可哈希的 
（2）int、float、str、tuple：是可以哈希的 
（3）list 不使用 hash 值进行索引，故其对所存储元素没有可哈希的要求；set / dict 使用 hash 值进行索引，也即其要求欲存储的元素有可哈希的要求。 
（4）dict 仅对键（key）有可哈希的要求，对值（value）无此要求。 

49题解法一用到
https://app.gitbook.com/@cai-sen-se/s/leetcode/1-200/49.-zi-mu-yi-wei-ci-fen-zu

## 22.map函数
map() 会根据提供的函数对指定序列做映射。

```
map(function, iterable, ...)
```
https://www.runoob.com/python/python-func-map.html
若function为基本数据类型（如int）：
则将iterable中所有元素转为int
例如键盘输入5 19，读取并转换为两个整数：

```
a,b=map(int, input().split())
print(a,b)  #5,19
```

```
a=list(map(int, input().split()))
print(a)  #[5,19]
```

## 23.集合（set）
集合（set）是一个无序的不重复元素序列。

可以使用大括号 { } 或者 set() 函数创建集合，**注意**：创建一个空集合必须用 set() 而不是 { }，因为 { } 是用来创建一个空字典。
使用for表达式创建集合：
```
b = {x for x in range(5)}
print(b)  #{0, 1, 2, 3, 4}
c = set(x for x in range(5))
print(c)  #{0, 1, 2, 3, 4}
```
或不用for，直接range：

```
b = {range(5)}
print(b)
```

## 24.python set运算操作
对两个集合（set）的运算操作有差集（`-`）、交集（`&`）和并集（`|`）：**（注意没有加）**
差集：

```
a = set(range(1, 10))    #{1,2, 3, 4, 5, 6, 7, 8, 9}
b = {0, 1}
a = a - b  #a集合有而b集合没有的
print(a)  #{2, 3, 4, 5, 6, 7, 8, 9}
```
交集并集：

```
>>> s1 = set([1, 2, 3])
>>> s2 = set([2, 3, 4])
>>> s1 & s2
{2, 3}
>>> s1 | s2
{1, 2, 3, 4}
```

## 25.统计词频
方法一（直观）：

```
 map = dict()    #词频
    for c in t: 
        if c in map:   #先判断是否存在
            map[c] += 1
        else:
            map[c] = 1
```
https://app.gitbook.com/@cai-sen-se/s/leetcode/1-200/76.-zui-xiao-fu-gai-zi-chuan#jie-fa-yi
方法二（简洁）：用get（）

```
dict.get(key, default=None)
key -- 字典中要查找的键。
default -- 如果指定键的值不存在时，返回该默认值。
```

```
nums = [1,1,2,2,3,4]
d = {}  #字典
for i in nums:
    d[i] = d.get(i, 0) + 1  #若字典中不存在i，则i词频为1
print(d)  #{1: 2, 2: 2, 3: 1, 4: 1}
```



## 26.全局变量关键字global和nonlocal

函数调用外部变量，要在**外部变量声明时**和**函数内部使用时**，都声明global

```python
def closedIsland(self, grid: List[List[int]]) -> int:
        #定义dfs辅助函数
        def dfs(grid, i, j):
            ...
            if grid[i][j] == 0 and (i == 0 or i == m-1 or j == 0 or j == n-1):
                global flag         #使用时也声明全局变量
                flag = False
                return
            ...
            dfs(grid, i, j+1)
        #调用dfs    
        m, n = len(grid), len(grid[0])  
        res = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 0:
                    global flag      #定义时声明全局变量      
                    flag = True
                    dfs(grid, i, j)
                    if flag:
                        res += 1
        return res
```

或者只在内部使用时，声明nonlocal

```python
def closedIsland(self, grid: List[List[int]]) -> int:
        #定义dfs辅助函数
        def dfs(grid, i, j):
            ...
            if grid[i][j] == 0 and (i == 0 or i == m-1 or j == 0 or j == n-1):
                nonlocal flag         #使用外部变量时声明
                flag = False
                return
            ...
            dfs(grid, i, j+1)
        #调用dfs  
        m, n = len(grid), len(grid[0])  
        res = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 0:  
                    flag = True		  #定义时不用声明nonlocal
                    dfs(grid, i, j)
                    if flag:
                        res += 1
        return res
```

