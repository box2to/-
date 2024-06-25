# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by ==刘子暄 环境科学与工程学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11

Python编程环境: PyCharm Community Edition 2023.3


## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：



代码

```python
class Deque:
    def __init__(self):
        self.items = []
    def isEmpty(self):
        return self.items == []
    def addFront(self,item):
        self.items.append(item)
    def addRear(self,item):
        self.items.insert(0,item)
    def removeFront(self):
        return self.items.pop()
    def removeRear(self):
        return self.items.pop(0)
    def size(self):
        return len(self.items)
    def list(self):
        return self.items


t = int(input())
for _ in range(t):
    deque = Deque()
    n = int(input())
    for _ in range(n):
        item = [int(x) for x in input().split()]
        if item[0] == 1:
            deque.addFront(item[1])
        if item[0] == 2:
            if item[1] == 0:
                deque.removeRear()
            elif item[1] == 1:
                deque.removeFront()

    if deque.list():
        print(' '.join(map(str,deque.list())))
    else:
        print('NULL')

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-17.png)




### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：按照波兰表达式的含义做了



代码

```python
lis = []
n = input().split()

for i in n[::-1]:
    if i not in ['+','-','*','/']:
        lis.append(i)

    if i in ['+','-','*','/']:
        a = float(lis.pop())
        b = float(lis.pop())
        if i == '+':
            lis.append(a + b)
        elif i == '-':
            lis.append(a - b)
        elif i == '*':
            lis.append(a * b)
        elif i == '/':
            lis.append(a / b)

for i1 in lis:
    print(f"{i1:.6f}")

```



代码运行截图 ==（至少包含有"Accepted"）==
![alt text](image-20.png)




### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：（.isnumeric()应用于字符串，判断是否是数字）



代码

```python
def infix_to_postfix(expression):
    precedence = {'+':1,'-':1,'*':2,'/':2}
    stack = []
    postfix = []
    number = ''

    for char in expression:
        if char.isnumeric() or char == '.':
            number += char#（重组数字）
        else:
            if number:  # 判断有没有number
                num = float(number)
                postfix.append(int(num) if num.is_integer() else num)
                number = ''
            if char in '+-*/':
                while stack and stack[-1] in '+-*/' and precedence[char] <= precedence[stack[-1]]:
                    postfix.append(stack.pop())
                stack.append(char)
            elif char == '(':
                stack.append(char)
            elif char == ')':
                while stack and stack[-1] != '(':
                    postfix.append(stack.pop())
                stack.pop()  # 一轮括号使用完毕

    if number:
        num = float(number)
        postfix.append(int(num) if num.is_integer() else num)#有可能还有number没有处理

    while stack:
        postfix.append(stack.pop())

    return ' '.join(str(x) for x in postfix)

n = int(input())
for _ in range(n):
    expression = input()
    print(infix_to_postfix(expression))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-22.png)




### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：用stack来模拟入栈出栈的过程，如果不能完全



代码

```python
def is_valid_pop_sequence(origin, output):
    if len(origin) != len(output):
        return False

    stack = []
    bank = list(origin)

    for char in output:
        while (not stack or stack[-1] != char) and bank:
            stack.append(bank.pop(0))

        if not stack or stack[-1] != char:
            return False

        stack.pop()

    return True

origin = input().strip()

while True:
    try:
        output = input().strip()
        if is_valid_pop_sequence(origin, output):
            print('YES')
        else:
            print('NO')
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-23.png)




### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：按照参考答案做的，这里两个def应该也可以直接并入class，按照数据类型的方法来定义



代码

```python
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None

def build_tree(node_list):
    nodes = {i: TreeNode(i) for i in range(1, len(node_list) + 1)}
    for i, (left, right) in enumerate(node_list, 1):
        if left != -1:
            nodes[i].left = nodes[left]
        if right != -1:
            nodes[i].right = nodes[right]
    return nodes[1]

def max_depth(root):
    if root is None:
        return 0
    else:
        left_depth = max_depth(root.left)
        right_depth = max_depth(root.right)
        return max(left_depth, right_depth) + 1

n = int(input())
node_list = []
for _ in range(n):
    left, right = map(int, input().split())
    node_list.append((left, right))

root = build_tree(node_list)
depth = max_depth(root)

print(depth)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==





### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：
有点没看懂题目，还有对快排不太熟悉，按照标答做的


代码

```python
def merge_sort(lst):
    
    if len(lst) <= 1:
        return lst, 0

    
    middle = len(lst) // 2
    left, inv_left = merge_sort(lst[:middle])
    right, inv_right = merge_sort(lst[middle:])

    merged, inv_merge = merge(left, right)

    
    return merged, inv_left + inv_right + inv_merge

def merge(left, right):
    merged = []
    inv_count = 0
    i = j = 0

    
    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
            inv_count += len(left) - i 

    merged += left[i:]
    merged += right[j:]

    return merged, inv_count

while True:
    n = int(input())
    if n == 0:
        break

    lst = []
    for _ in range(n):
        lst.append(int(input()))

    _, inversions = merge_sort(lst)
    print(inversions)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==
![alt text](image-24.png)




## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

#### 合法出栈序列
看的时候没有搞懂模拟出入栈操作是什么，所以决定拿例子来说明
ori = [1,2,3,4,5]
pop = [4,3,5,1,2]
stack = []
从pop中遍历，第一个抽出的元素是4
判断4不在stack的栈顶，说明4还没有到该出栈的时候，所以将ori中的元素依次压入栈，直到栈顶元素等于4,这时匹配成功，意味着该将4弹出stack
（这里我以为stack.pop()是错误的，因为没有进行判断，会导致每一个元素没有达成操作时就弹出。但是其实将while操作完成之后，元素一定满足条件，所以可以弹出，这是一个最终操作）
此时
ori = [5]
pop = [3,5,1,2]
stack = [1,2,3] pop = 4
(list(ori)是为了简化入栈操作)
接下来继续同样的操作
pop = 3 stack = [1,2] pop = [5,1,2]
5不匹配 压栈到5
pop = 5 stack = [1,2] pop = [1,2]
1不匹配 且ori为空 结束

还没学完树 代码就好长一个 要学盲打 估计还得多打几遍树的范式代码
