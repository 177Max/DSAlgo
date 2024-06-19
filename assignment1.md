# Assignment #1

2024 spring, Complied by 胡豪俊 工学院

**编程环境**

操作系统：Windows11

Python编程环境：Visiual Studio Code

**注**：闫老师您好，我以前不太习惯用注释导致很多代码在写完一段时间后再看发现自己都看不明白了，为了强化使用注释的意识，我就索性将解题思路以代码中结尾注释的形式给出，希望您能注意到。

## 1. 题目

### 20742: 泰波拿契數

http://cs101.openjudge.cn/practice/20742/

##### 代码

```python
n=int(input())
L=[0,1,1]
i=2
while i<=31:
    endnum=L[i-2]+L[i-1]+L[i]
    L.append(endnum)
    i+=1
print(L[n])
##这题没什么难度，当作复健了，因为30是一个很小的数，可以直接把所有可能的情况打出来，找对应的就可以
##如果可以取到一个大的上限并且给的n较大，做法也是这样递归，但是递归到题目给的n为止就可以，最后的endnum即为答案
##若给大上限但n只为1，2，3这样的小数，在上述情况单独if讨论即可
```

![ad5eb9fd756c3ead96a5df79d9d8867](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\ad5eb9fd756c3ead96a5df79d9d8867.png)

### 58A. Chat room

greedy/strings, 1000, http://codeforces.com/problemset/problem/58/A

##### 代码

```python
L=list(input())
x=0##用这个记录hello每个字母是否出现
i=len(L)-1
j=0

while j<=i:
    if L[j]=="h":
        x+=1
        j+=1
        break
    j+=1
##这里不要动j的数值，在跳出循环前+1保证了接下来的j对应的字母不会受之前的影响
while j<=i:
    if L[j]=="e":
        x+=1
        j+=1
        break
    j+=1

while j<=i:
    if L[j]=="l":
        x+=1
        j+=1
        break
    j+=1

while j<=i:
    if L[j]=="l":
        x+=1
        j+=1
        break
    j+=1

while j<=i:
    if L[j]=="o":
        x+=1
        j+=1
        break
    j+=1

if x==5:
    print("YES")
else:
    print("NO")


##这题遍历一遍就好，最开始语法忘了pop和del函数怎么用卡了半天，后面瞎用又卡了半天，最后想着没必要删掉已经判断的字母，遂AC。总的来说还是得多练，不练就会忘干净，而且有时候debug有点折磨人，末了发现错在语法真的很亏，基础要牢牢筑实
##而且这题我之前好像做过
```

![267385951226137cd51cd91cf8155c8](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\267385951226137cd51cd91cf8155c8.png)

### 118A. String Task

implementation/strings, 1000, http://codeforces.com/problemset/problem/118/A

##### 代码

```python
L=['a','e','i','o','u','A','E','I','O','U','y','Y']##先把所有的元音拿出来
l=list(input())##转化为列表考虑
k=[]
for x in l:
    if x not in L:##涉及到in的语法，这个还好记得
        k.append(x.lower())
finalstring=''
for x in k:
    finalstring+="."+x
print(finalstring)
##没注意到y也是元音错了一次...这题比较简单，当作回忆语法了

```

![f66f5e605d3917f30e3e97adf32a016](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\f66f5e605d3917f30e3e97adf32a016.png)

### 22359: Goldbach Conjecture

http://cs101.openjudge.cn/practice/22359/

##### 代码

```python
def primejudge(num):
    if num <= 1:
        return False
    
    for i in range(2, int(num**0.5) + 1):
        if num % i == 0:
            return False
            
    return True

x=int(input())
i=3
if x%2!=0:##2+奇质数才能得到奇数
    print("2 "+str(x-2))
else:
    t=x//3+1
    while i <=t:
        if primejudge(i) is True and primejudge(x-i) is True:
            print(str(i)+" "+str(x-i))
            break
        else:
            i+=2##步长用2快一点
##写了一个质数判断函数，比较方便，当然能这么写其实是因为题目确定了给的数能写成两个质数的和，毕竟哥德巴赫猜想还没有被证明（）
##第一眼看到还是被吓了一跳的，毕竟质数这个东西比较神奇，质数判断函数也是比较笨的办法，遍历一遍根号以下的数就能判断，后面倒是有一点小技巧，比如题目给的数如果是奇数那必然是2+质数的形式，这样就直接砍掉一半情况（因为已经确定给的数能写成两个质数的和了），剩下一半情况就从3开始用奇数去遍历，其实也挺慢的，但好在ac了。依稀记得之前有个很恶心的T-Primes，我最终不断优化步长才解决，不过现在大概知道了筛法，应该能更快
```

![30215d822ad1152b0293a650b262c71](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\30215d822ad1152b0293a650b262c71.png)

### 23563: 多项式时间复杂度

http://cs101.openjudge.cn/practice/23563/

##### 代码

```python
L=input().split("+")##split函数很好用

max=0
for x in L:
    a=x.find("n")
    x1=x[:a]
    if x1=="":##这是例如n^10的情况，1没有直接出现，按上面取会得到空字符串
        x1=1
    else:
        x1=int(x1)
    x2=int(x[a+2:])
    if x1!=0 and x2>=max:
        max=x2

print("n^"+str(max))
##一开始把debug时用的测试输出也给print了，错了一次。本题找n即可，根据n定位前后关键信息，n前面是1的情况比较坑，判断一下即可
##这题之前好像也做过，但这回想得快多了，我主要在考虑会不会有0n^0或者0000n^0这种东西,好在测试数据应该没有单独给前者（这种没什么意义，时间复杂度要是0那不是起飞了)，后者python自己帮我解决了(int(“0000”)会得到0）
```

![6b5e2130861a82c1329b3dd0e3e603e](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\6b5e2130861a82c1329b3dd0e3e603e.png)

### 24684: 直播计票

http://cs101.openjudge.cn/practice/24684/

##### 代码

```python
L=[int(i) for i in input().split()]
l=set(L)##set集合可以比较直接地看出列表元素种类
k=[]

max=L.count(L[0])
for x in l:

    num=L.count(x)##count函数也很好用，但是列表数据多了的话可能会tle

    if num==max:
        k.append(x)
    elif num>max:
        max=num##更新max的值千万别忘了
        k=[x]
k.sort()
ans=""
for i in k:
    ans+=str(i)+" "
print(ans[:-1])
##最开始的尝试忘记更改max的值了，思路都比较直接，做完之后感觉python的语法回来一点了，没忘太干净
```

![c0f090d0b014dab713895358ae74a35](D:\Downloads\WeChat Files\wxid_nhylnrft428522\FileStorage\Temp\c0f090d0b014dab713895358ae74a35.png)

## 2. 学习总结和收获

很开心又选到了闫老师的课，2022 fall 修的计算概论B提高班，此后由于院系课程安排没能学数算，这学期看到闫老师开课了毫不犹豫就选了。但是python语法已经忘得差不多了，这个星期主要复习了一点语法，额外的题目后续会跟上，这学期的其他课还比较硬要抓紧时间了。





