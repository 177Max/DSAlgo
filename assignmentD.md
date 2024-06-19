# Assignment #D: May月考

Updated 1654 GMT+8 May 8, 2024

2024 spring, Complied by ==同学的姓名、院系==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：macOS Ventura 13.4.1 (c)

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 02808: 校门外的树

http://cs101.openjudge.cn/practice/02808/

代码

```python
n=[int(i) for i in input().split()]
i=0
l=[]
while i<=n[1]-1:
    k=[int(j) for j in input().split()]
    l.append(k)
    i+=1
w=[i for i in range(n[0]+1)]
a=[]
for t in l:
    a+=w[t[0]:t[1]+1]
o=set(a)
x=len(w)-len(o)
print(x)
##以前写过
```

![58f8b53d088a9014d4505553a49dd0a](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\58f8b53d088a9014d4505553a49dd0a.png)

### 20449: 是否被5整除

http://cs101.openjudge.cn/practice/20449/

代码

```python
def binary_divisible_by_five(binary_string):
    result = ''
    num = 0
    for bit in binary_string:
        num = (num * 2 + int(bit)) % 5
        if num == 0:
            result += '1'
        else:
            result += '0'
    return result

binary_string = input().strip()
print(binary_divisible_by_five(binary_string))
##遍历直接模拟即可
```

![30ceb6d9e36ee572afdc84b7f4a6602](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\30ceb6d9e36ee572afdc84b7f4a6602.png)

### 01258: Agri-Net

http://cs101.openjudge.cn/practice/01258/

代码

```python
from heapq import heappop, heappush, heapify

def prim(graph, start_node):
    mst = set()
    visited = set([start_node])
    edges = [
        (cost, start_node, to)
        for to, cost in graph[start_node].items()
    ]
    heapify(edges)

    while edges:
        cost, frm, to = heappop(edges)
        if to not in visited:
            visited.add(to)
            mst.add((frm, to, cost))
            for to_next, cost2 in graph[to].items():
                if to_next not in visited:
                    heappush(edges, (cost2, to, to_next))

    return mst


while True:
    try:
        N = int(input())
    except EOFError:
        break

    graph = {i: {} for i in range(N)}
    for i in range(N):
        for j, cost in enumerate(map(int, input().split())):
            graph[i][j] = cost

    mst = prim(graph, 0)
    total_cost = sum(cost for frm, to, cost in mst)
    print(total_cost)
##用Prim算法可以解决
```

![618413735cb886a7c1d25bb55b7c8b5](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\618413735cb886a7c1d25bb55b7c8b5.png)

### 27635: 判断无向图是否连通有无回路(同23163)

http://cs101.openjudge.cn/practice/27635/

代码

```python
def is_connected(graph, n):
    visited = [False] * n
    stack = [0]
    visited[0] = True

    while stack:
        node = stack.pop()
        for neighbor in graph[node]:
            if not visited[neighbor]:
                stack.append(neighbor)
                visited[neighbor] = True

    return all(visited)

def has_cycle(graph, n):
    def dfs(node, visited, parent):
        visited[node] = True
        for neighbor in graph[node]:
            if not visited[neighbor]:
                if dfs(neighbor, visited, node):
                    return True
            elif parent != neighbor:
                return True
        return False

    visited = [False] * n
    for node in range(n):
        if not visited[node]:
            if dfs(node, visited, -1):
                return True
    return False

n, m = map(int, input().split())
graph = [[] for _ in range(n)]
for _ in range(m):
    u, v = map(int, input().split())
    graph[u].append(v)
    graph[v].append(u)

connected = is_connected(graph, n)
has_loop = has_cycle(graph, n)
print("connected:yes" if connected else "connected:no")
print("loop:yes" if has_loop else "loop:no")
##dfs的运用
```

![9ce8397a549c3177af25c79c27b8301](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\9ce8397a549c3177af25c79c27b8301.png)

### 27947: 动态中位数

http://cs101.openjudge.cn/practice/27947/

代码

```python
import heapq

def dynamic_median(nums):

    min_heap = []
    max_heap = []

    median = []
    for i, num in enumerate(nums):
        if not max_heap or num <= -max_heap[0]:
            heapq.heappush(max_heap, -num)
        else:
            heapq.heappush(min_heap, num)

        if len(max_heap) - len(min_heap) > 1:
            heapq.heappush(min_heap, -heapq.heappop(max_heap))
        elif len(min_heap) > len(max_heap):
            heapq.heappush(max_heap, -heapq.heappop(min_heap))

        if i % 2 == 0:
            median.append(-max_heap[0])

    return median

T = int(input())
for _ in range(T):

    nums = list(map(int, input().split()))
    median = dynamic_median(nums)
    print(len(median))
    print(*median)
##考试的时间不够了，后面下来学习了题解
```

![2856200a28498fe5e3ed3571716720d](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\2856200a28498fe5e3ed3571716720d.png)

### 28190: 奶牛排队

http://cs101.openjudge.cn/practice/28190/

代码

```python
from bisect import bisect_right as bl
lis,q1,q2,ans=[int(input())for _ in range(int(input()))],[-1],[-1],0
for i in range(len(lis)):
    while len(q1)>1 and lis[q1[-1]]>=lis[i]:q1.pop()
    while len(q2)>1 and lis[q2[-1]]<lis[i]:q2.pop()
    id=bl(q1,q2[-1])
    if id<len(q1):ans=max(ans,i-q1[id]+1)
    q1.append(i)
    q2.append(i)
print(ans)
##学习了同学的解法，简洁优美
```

![0885b3ae82878a4797f4aadff3c094b](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\0885b3ae82878a4797f4aadff3c094b.png)

## 2. 学习总结和收获

这次正常考试时间内大概能ac4的样子，还是不够，继续加油





