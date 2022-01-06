# 将一个数表示为连续数的和

> 原文:[https://www . geesforgeks . org/express-number-sum-continuous-numbers/](https://www.geeksforgeeks.org/express-number-sum-consecutive-numbers/)

给定一个数字 N，编写一个函数，将 N 表示为两个或多个连续正数的和。如果没有解决方案，输出-1。如果有多个解决方案，则打印其中一个。
示例:

```
Input : N = 10
Output : 4 + 3 + 2 + 1

Input  : N = 8
Output : -1

Input  : N = 24
Output : 9 + 8 + 7
```

```
Sum of first n natural numbers = n * (n + 1)/2

Sum of first (n + k) numbers = (n + k) * (n + k + 1)/2

If N is sum of k consecutive numbers, then
following must be true.

N = [(n+k)(n+k+1) - n(n+1)] / 2

OR 

2 * N = [(n+k)(n+k+1) - n(n+1)]
```

以下是基于上述思想的实现。

## C++

```
// C++ program to print a consecutive sequence
// to express N if possible.
#include <bits/stdc++.h>
using namespace std;

// Print consecutive numbers from
// last to first
void printConsecutive(int last, int first)
{
    cout << first++;
    for (int x = first; x<= last; x++)
        cout << " + " << x;
}

void findConsecutive(int N)
{
    for (int last=1; last<N; last++)
    {
        for (int first=0; first<last; first++)
        {
            if (2*N == (last-first)*(last+first+1))
            {
                cout << N << " = ";
                printConsecutive(last, first+1);
                return;
            }
        }
    }
    cout << "-1";
}

// Driver code
int main()
{
    int n = 12;
    findConsecutive(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print a consecutive sequence
// to express N if possible.
import java.util.*;
class GFG
{

// Print consecutive numbers from
// last to first
static void printConsecutive(int last, int first)
{
    System.out.print(first++);
    for (int x = first; x<= last; x++)
        System.out.print(" + " +  x);
}

static void findConsecutive(int N)
{
    for (int last = 1; last < N; last++)
    {
        for (int first = 0; first < last; first++)
        {
            if (2*N == (last-first)*(last+first+1))
            {
                System.out.print(N+ " = ");
                printConsecutive(last, first+1);
                return;
            }
        }
    }
    System.out.print("-1");
}

// Driver code
public static void main(String[] args)
{
    int n = 12;
    findConsecutive(n);
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python3 program to print a consecutive
# sequence to express N if possible.

# Print consecutive numbers
# from last to first
def printConsecutive(last, first):
    print (first, end = "")
    first += 1
    for x in range(first, last + 1):
        print (" +", x, end = "")

def findConsecutive(N):
    for last in range(1, N):

        for first in range(0, last):

            if 2 * N == (last - first) * (last + first + 1):
                print (N, "= ", end = "")
                printConsecutive(last, first + 1)
                return
    print ("-1")

# Driver code
n = 12
findConsecutive(n)

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# program to print a consecutive sequence
// to express N if possible.
using System;

class GfG
{
    // Print consecutive numbers from
    // last to first
    static void printConsecutive(int last, int first)
    {
        Console.Write(first++);
        for (int x = first; x <= last; x++)
            Console.Write(" + "+x);
    }

    static void findConsecutive(int N)
    {
        for (int last = 1; last < N; last++)
        {
            for (int first = 0; first < last; first++)
            {
                if (2 * N == (last - first)
                    * (last + first + 1))
                {
                    Console.Write(N + " = ");
                    printConsecutive(last, first + 1);
                    return;
                }
            }
        }
        Console.Write("-1");
    }

    // Driver code
    public static void Main ()
    {
        int n = 12;
        findConsecutive(n);
    }
}

// This code is contributed by vt_m
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print a consecutive
// sequence to express N if possible.

// Print consecutive numbers from
// last to first
function printConsecutive($last, $first)
{
    echo $first++;
    for ($x = $first; $x<= $last; $x++)
        echo " + " , $x;
}

function findConsecutive($N)
{
    for ($last = 1; $last < $N; $last++)
    {
        for ($first = 0; $first < $last; $first++)
        {
            if (2 * $N == ($last - $first) *
                      ($last + $first + 1))
            {
                 echo $N , " = ";
                printConsecutive($last, $first + 1);
                return;
            }
        }
    }
    echo "-1";
}

    // Driver Code
    $n = 12;
    findConsecutive($n);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>
    // Javascript program to print a consecutive
// sequence to express N if possible.

// Print consecutive numbers from
// last to first
function printConsecutive(last, first)
{
    document.write(first++);
    for (let x = first; x<= last; x++)
        document.write( " + " + x);
}

function findConsecutive(N)
{
    for (let last = 1; last < N; last++)
    {
        for (let first = 0; first < last; first++)
        {
            if (2 * N == (last - first) *
                      (last + first + 1))
            {
                 document.write(N + " = ");
                printConsecutive(last, first + 1);
                return;
            }
        }
    }
    document.write("-1");
}

    // Driver Code
    let n = 12;
    findConsecutive(n);

// This code is contributed by _saurabh_jaiswal
</script>
```

输出:

```
12 = 3 + 4 + 5
```

**参考:**
[https://math . stackexchange . com/questions/139842/in-how-how-a-number-can-expression-as-sum-of-continuous-numbers](https://math.stackexchange.com/questions/139842/in-how-many-ways-can-a-number-be-expressed-as-a-sum-of-consecutive-numbers)
本文由 **Roshni Agarwal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。