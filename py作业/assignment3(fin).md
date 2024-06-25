# Assignment #3: March月考

Updated 1537 GMT+8 March 6, 2024

2024 spring, Complied by ==刘子暄 环境科学与工程学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:
- Learn about Time and Space complexities
- Learn the basics of individual Data Structures
- Learn the basics of Algorithms
- Practice Problems on DSA

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11

Python编程环境: PyCharm Community Edition 2023.3



## 1. 题目

**02945: 拦截导弹**

http://cs101.openjudge.cn/practice/02945/



思路：



##### 代码

```python
n = int(input())
lis = [int(x) for x in input().split()]
dp = [0]*n
for i in range(n-1,-1,-1):
    maxn = 1
    for j in range(n-1,i,-1):
        if lis[j] <= lis[i] and dp[j]+1 > maxn:
            maxn = dp[j] + 1
    dp[i] = maxn
print(max(dp))

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image.png)




**04147:汉诺塔问题(Tower of Hanoi)**

http://cs101.openjudge.cn/practice/04147



思路：递归思路，参考标答搞的简洁了一点



##### 代码

```python
def moveOne(numDisk: int, init: str, desti: str):
    print("{}:{}->{}".format(numDisk, init, desti))

def move(numDisks: int, init: str, temp: str, desti: str):
    if numDisks == 1:
        moveOne(1, init, desti)
    else:
        move(numDisks - 1, init, desti, temp)
        moveOne(numDisks, init, desti)
        move(numDisks - 1, temp, init, desti)


n, a, b, c = input().split()
move(int(n), a, b, c)
```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-2.png)




**03253: 约瑟夫问题No.2**

http://cs101.openjudge.cn/practice/03253



思路：大概懂什么思路，但是有些细节不太对，还是参考标答了



##### 代码

```python
while True:
    n, p, m = map(int, input().split())
    if {n,p,m} == {0}:
        break
    monkey = [i for i in range(1, n+1)]
    for _ in range(p-1):
        tmp = monkey.pop(0)
        monkey.append(tmp)
    # print(monkey)

    index = 0
    ans = []
    while len(monkey) != 1:
        temp = monkey.pop(0)
        index += 1
        if index == m:
            index = 0
            ans.append(temp)
            continue
        monkey.append(temp)

    ans.extend(monkey)

    print(','.join(map(str, ans)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![alt text](image-3.png)



**21554:排队做实验 (greedy)v0.2**

http://cs101.openjudge.cn/practice/21554



思路：



##### 代码

```python
while True:
    n, p, m = map(int, input().split())
    if {n,p,m} == {0}:
        break
    monkey = [i for i in range(1, n+1)]
    for _ in range(p-1):
        tmp = monkey.pop(0)
        monkey.append(tmp)
    # print(monkey)

    index = 0
    ans = []
    while len(monkey) != 1:
        temp = monkey.pop(0)
        index += 1
        if index == m:
            index = 0
            ans.append(temp)
            continue
        monkey.append(temp)

    ans.extend(monkey)

    print(','.join(map(str, ans)))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![alt text](image-5.png)



**19963:买学区房**

http://cs101.openjudge.cn/practice/19963



思路：



##### 代码

```python
import statistics
n = int(input())
distance = list(map(lambda x:sum(eval(x)),input().split()))
prize = list(map(int,input().split()))
average = list(distance[i]/prize[i] for i in range(n))
prize_median = statistics.median(prize)
average_median = statistics.median(average)
num = 0
for i in range(n):
    if average[i] > average_median and prize[i] < prize_median:
        num += 1
print(num)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-6.png)




**27300: 模型整理**

http://cs101.openjudge.cn/practice/27300



思路：



##### 代码

```python
from collections import defaultdict

n = int(input())
d = defaultdict(list)
for _ in range(n):
    #name, para = input().strip().split('-')
    name, para = input().split('-')
    if para[-1]=='M':
        d[name].append((para, float(para[:-1])/1000) )
    else:
        d[name].append((para, float(para[:-1])))


sd = sorted(d)
#print(d)
for k in sd:
    paras = sorted(d[k],key=lambda x: x[1])
    #print(paras)
    value = ', '.join([i[0] for i in paras])
    print(f'{k}: {value}')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-7.png)




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==
这些月考题目，前四道都是上学期计概上过的题目，但是还是没有很好地掌握（悲伤），真的应该好好复习一下，后两道题目的确对我太难了，要再好好看一下
每日选作最近没时间做，我反思自己太懈怠了（悲伤）




