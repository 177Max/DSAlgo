# Assignment #F: All-Killed 满分

2024 spring, Complied by 胡豪俊 工学院



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

操作系统：Windows11

Python编程环境：Visual Studio Code



## 1. 题目

### 22485: 升空的焰火，从侧面看

http://cs101.openjudge.cn/practice/22485/

代码

```python
n=int(input())
l,r=[-1]*(n+1),[-1]*(n+1)
for i in range(1,n+1):l[i],r[i]=map(int,input().split())
q,ans=[1],''
while q:
    ans+=str(q[-1])+' '
    tmp=[]
    for i in q:
        if l[i]!=-1:tmp.append(l[i])
        if r[i]!=-1:tmp.append(r[i])
    q=tmp
print(ans)
##bfs按层次遍历即可
```

![482c4170e7a2d7b8be8f4de6ff9d342](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\482c4170e7a2d7b8be8f4de6ff9d342.png)

### 28203:【模板】单调栈

http://cs101.openjudge.cn/practice/28203/

代码

```python
n = int(input())
a = list(map(int, input().split()))
stack = []
for i in range(n):
    while stack and a[stack[-1]] < a[i]:
        a[stack.pop()] = i + 1
    stack.append(i)
while stack:
    a[stack[-1]] = 0
    stack.pop()
print(*a)
##单调栈模板
```

![fac3cae706a5aef0e57bc4b08b55cca](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\fac3cae706a5aef0e57bc4b08b55cca.png)

### 09202: 舰队、海域出击！

http://cs101.openjudge.cn/practice/09202/

代码

```python
from collections import defaultdict

def dfs(node, color):
    color[node] = 1
    for neighbour in graph[node]:
        if color[neighbour] == 1:
            return True
        if color[neighbour] == 0 and dfs(neighbour, color):
            return True
    color[node] = 2
    return False

T = int(input())
for _ in range(T):
    N, M = map(int, input().split())
    graph = defaultdict(list)
    for _ in range(M):
        x, y = map(int, input().split())
        graph[x].append(y)
    color = [0] * (N + 1)
    is_cyclic = False
    for node in range(1, N + 1):
        if color[node] == 0:
            if dfs(node, color):
                is_cyclic = True
                break
    print("Yes" if is_cyclic else "No")
##学习了题解的模板写法
```

![96f86399a287e559232de94112fd499](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\96f86399a287e559232de94112fd499.png)

### 04135: 月度开销

http://cs101.openjudge.cn/practice/04135/

代码

```python
n,m=list(map(int,input().split()))
out=[int(input())for _ in range(n)]
l,r,ans=max(out),sum(out),0
def check(x):
    global out,m,n
    res,i,tot=m,0,0
    while res>0 and i<n:
        if tot+out[i]<=x:tot+=out[i]
        else:
            res-=1
            if res==0:return 0
            tot=out[i]
        i+=1
    if i==n:return 1
    return 0
while l<=r:
    mid=(l+r)//2
    if check(mid):
        ans=mid
        r=mid-1
    else:l=mid+1
print(ans) 
##二分法
```

![212c16fab4d3c3cb025cf354f23de1c](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\212c16fab4d3c3cb025cf354f23de1c.png)

### 07735: 道路

http://cs101.openjudge.cn/practice/07735/

代码

```python
from heapq import heappush as hu,heappop as hp
k,n,r=[int(input())for _ in range(3)]
edge,vis=[[]for _ in range(n+1)],[100000]*(n+1)
for _ in range(r):
    x,y,z,w=map(int,input().split())
    edge[x].append((y,z,w))
q,ans=[],-1
hu(q,(0,0,1))
while q:
    l,c,x=hp(q)
    if x==n:
        ans=l
        break
    vis[x]=c
    for y,z,w in edge[x]:
        if c+w<vis[y] and c+w<=k:hu(q,(l+z,c+w,y))
print(ans)
##难，学习了同学的解法
```

![0678b715287529e5b56dd7eff7892f6](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\0678b715287529e5b56dd7eff7892f6.png)

### 01182: 食物链

http://cs101.openjudge.cn/practice/01182/

代码

```python
n,k=list(map(int,input().split()))
f,ans=[i for i in range(n*3+1)],0
def find_x(x):
    global f
    if f[x]==x:return x
    f[x]=find_x(f[x])
    return f[x]
def union(x,y):
    global f
    fx,fy=find_x(x),find_x(y)
    f[fx]=fy
for _ in range(k):
    d,x,y=list(map(int,input().split()))
    if (x>n or y>n)or(d==2 and x==y):
        ans+=1
        continue
    fx1,fx2,fx3,fy=find_x(x),find_x(n+x),find_x(n*2+x),find_x(y)
    if (d==1 and (fx2==fy or fx3==fy)) or (d==2 and (fx1==fy or fx3==fy)):
        ans+=1
        continue
    if d==1:
        union(x,y)
        union(x+n,y+n)
        union(x+2*n,y+2*n)
    else:
        union(x,2*n+y)
        union(y,n+x)
        union(x+2*n,y+n)
print(ans)
##仍然是学的..
```

![e98540028942a44d718d03050a1152a](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\e98540028942a44d718d03050a1152a.png)

## 2. 学习总结和收获

最近在复习课件，把一些细致的东西再看一遍，感觉题目出难的话还是会束手无策啊...





