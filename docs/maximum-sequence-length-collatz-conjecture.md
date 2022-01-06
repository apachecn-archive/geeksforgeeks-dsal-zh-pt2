# 最大序列长度|柯拉茨猜想

> 原文:[https://www . geeksforgeeks . org/最大序列长度-collaz-猜想/](https://www.geeksforgeeks.org/maximum-sequence-length-collatz-conjecture/)

给定一个整数 **N** 。任务是找到从 **1** 到 **N-1** 范围内的数字，该数字在其[排序序列](https://en.wikipedia.org/wiki/Collatz_conjecture)中具有最大的术语数和该序列中的术语数。
数字 **N** 的排序顺序定义为:

*   如果 **N** 为**奇数**，则将 **N** 改为 **3*N + 1** 。
*   如果 **N** 为**偶数**，则更改 **N** 为 **N / 2** 。

比如我们来看看**N = 13**:
13->40->20->10->5>16->8->4->2->1
**例:**

> **输入:** 10
> **输出:** (9，20)
> 9 在其 Collatz 序列
> **中有 20 个术语输入:** 50
> **输出:** (27，112)
> 27 有 112 个术语

**方法:**
与上面讨论的 **N = 13** 的例子一样， **N = 13** 和 **N = 40** 的排序规则有相似的术语，除了一个之外，这确保了可能涉及动态编程来存储子问题的答案并重用它。
但是这里正常的记忆不起作用，因为在一个步骤中，我们要么使一个数变大(在上面的例子中，N = 13 取决于 N = 40 的解)，要么除以 **2** ( N = 40 的解取决于 N = 20 的解)。
因此，我们将使用 Map/ dictionary 数据结构来存储子问题的解决方案，而不是使用 dp 数组，并且将执行排序器序列中讨论的正常操作。
以下是上述方法的实施:

## 蟒蛇 3

```
def collatzLenUtil(n, collLenMap):

    # If value already
    # computed, return it
    if n in collLenMap:
        return collLenMap[n]

    # Base case
    if(n == 1):
        collLenMap[n] = 1

    # Even case
    elif(n % 2 == 0):
        collLenMap[n] \
        = 1 \
           + collatzLenUtil(n//2, collLenMap)

    # Odd case
    else:
        collLenMap[n] \
        = 1 \
          + collatzLenUtil(3 * n + 1, collLenMap)

    return collLenMap[n]

def collatzLen(n):

    # Declare empty Map / Dict
    # to store collatz lengths
    collLenMap = {}

    collatzLenUtil(n, collLenMap)

    # Initialise ans and
    # its collatz length
    num, l =-1, 0

    for i in range(1, n):

        # If value not already computed,
        # pass Dict to Helper function
        # and calculate and store value
        if i not in collLenMap:
            collatzLenUtil(i, collLenMap)

        cLen = collLenMap[i]
        if l < cLen:
            l = cLen
            num = i

    # Return ans and
    # its collatz length
    return (num, l)

print(collatzLen(10))
```

**Output:** 

```
(9, 20)
```