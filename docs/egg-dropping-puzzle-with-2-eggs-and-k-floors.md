# 2 蛋 K 层落蛋拼图

> 原文:[https://www . geeksforgeeks . org/蛋花拼图-两个鸡蛋和 k 层/](https://www.geeksforgeeks.org/egg-dropping-puzzle-with-2-eggs-and-k-floors/)

给定 2 个鸡蛋和 k 层，找出最坏情况下所需的最小试验次数。这个问题是 [n 个鸡蛋 k 个楼层的具体情况。](https://www.geeksforgeeks.org/dynamic-programming-set-11-egg-dropping-puzzle/)
**例:**

```
Input : k = 10
Output : 4
We first try from 4-th floor. Two cases arise,
(1) If egg breaks, we have one egg left so we
    need three more trials.
(2) If egg does not break, we try next from 7-th
    floor. Again two cases arise.
We can notice that if we choose 4th floor as first
floor, 7-th as next floor and 9 as next of next floor,
we never exceed more than 4 trials.

Input : k = 100
Output : 14
```

**如果我们只有一个卵子，最坏情况下的试验次数是多少？**
答案是 k。我们将从一楼开始尝试，然后是二楼，然后是三楼，在最坏的情况下，鸡蛋会从顶楼打破。
**如果我们有两个鸡蛋，我们尝试的第一层是什么？**
我们可以注意到，如果我们的答案是 x，那么我们尝试的第一层就必须是楼层号 x，因为最坏的情况下如果鸡蛋破了，我们就只剩下一个鸡蛋了，从 1 到 x-1 每一层都要尝试。所以总的试验变成 1+(x–1)。
**如果第一次尝试鸡蛋不碎，我们尝试的第二层会是什么？**
我们尝试的下一个楼层必须是 x+(x–1)，因为我们的最优答案是 x，如果鸡蛋从 x + (x-1)楼层打破，我们必须从 x+1 楼层线性尝试到 x-2 楼层。
**我们能概括一下吗？**
如果第一个鸡蛋到目前为止还没有破，那么第 I 次试验必须从楼层号 x+(x–1)+…+(x–I–1)开始。
**我们可以用 x 审判覆盖多少层？**
我们从上面可以观察到，我们可以覆盖 x+(x–1)+(x–2)…。+ 2 + 1 层，有 x 个审判。这个表达式的值是 x * (x + 1) / 2。
**给定 k 的最优 x 是多少？**
从上面我们知道，

```
x * (x + 1)/2 >= k
The optimal value of x can be written as,
⌈((-1 + √(1+8k))/2)⌉
```

## C++

```
// CPP program to find optimal number of trials
// for k floors and 2 eggs.
#include<bits/stdc++.h>
using namespace std;

int twoEggDrop(int k)
{
   return ceil((-1.0 + sqrt(1 + 8*k))/2.0);
}

int main()
{
   int k = 100;
   cout << twoEggDrop(k);
   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// optimal number of trials
// for k floors and 2 eggs.
import java.io.*;

class GFG
{
    static int twoEggDrop(int k)
    {
        return (int)Math.ceil((-1.0 +
                    Math.sqrt(1 + 8 * k)) / 2.0);
    }

    // Driver code
    public static void main (String[] args)
    {
        int k = 100;
        System.out.println(twoEggDrop(k));
    }
}

// This code is contributed
// by Mahadev.
```

## 蟒蛇 3

```
# Python3 program to find optimal number
# of trials for k floors and 2 eggs.
import math as mt

def twoEggDrop(k):
    return mt.ceil((-1.0 +
           mt.sqrt(1 + 8 * k)) / 2)

# Driver Code
k = 100
print(twoEggDrop(k))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find optimal number
// of trials for k floors and 2 eggs.
class GFG
{
static int twoEggDrop(int k)
{
    return (int)System.Math.Ceiling((-1.0 +
                System.Math.Sqrt(1 + 8 * k)) / 2.0);
}

// Driver code
public static void Main ()
{
    int k = 100;
    System.Console.WriteLine(twoEggDrop(k));
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find optimal number
// of trials for k floors and 2 eggs.

function twoEggDrop($k)
{
    return ceil((-1.0 +
           sqrt(1 + 8 * $k)) / 2.0);
}

// Driver Code
$k = 100;
echo twoEggDrop($k);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript program to find optimal number of trials
// for k floors and 2 eggs.

function twoEggDrop(k)
{
   return Math.ceil((-1.0 + Math.sqrt(1 + 8*k))/2.0);
}

var k = 100;
document.write( twoEggDrop(k));

</script>
```

**输出:**

```
14
```

**时间复杂度:** O(1)