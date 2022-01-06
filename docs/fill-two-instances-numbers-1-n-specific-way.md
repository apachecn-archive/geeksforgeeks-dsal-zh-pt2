# 以特定方式填充从 1 到 n 的所有数字的两个实例

> 原文:[https://www . geesforgeks . org/fill-two-instance-numbers-1-n-specific-way/](https://www.geeksforgeeks.org/fill-two-instances-numbers-1-n-specific-way/)

给定一个数字 n，创建一个大小为 2n 的数组，使得数组包含从 1 到 n 的每个数字的 2 个实例，并且数字 I 的两个实例之间的元素数量等于 I。如果这样的配置是不可能的，那么打印相同的。
**例:**

```
Input: n = 3
Output: res[] = {3, 1, 2, 1, 3, 2}

Input: n = 2
Output: Not Possible

Input: n = 4
Output: res[] = {4, 1, 3, 1, 2, 4, 3, 2}
```

**强烈建议尽量减少浏览器，先自己试试这个。**
一个解决办法是回溯。这个想法很简单，我们在一个地方放置两个 n 的实例，然后对 n-1 重复。如果循环成功，我们返回 true，否则我们回溯并尝试在不同的位置放置 n。下面是这个想法的实现。

## C++

```
// A backtracking based C++ Program to fill
// two instances of all numbers from 1 to n
// in a specific way
#include <bits/stdc++.h>
using namespace std;

// A recursive utility function to fill
// two instances of numbers from 1 to n
// in res[0..2n-1]. 'curr' is current value of n.
bool fillUtil(int res[], int curr, int n)
{
    // If current number becomes 0,
    // then all numbers are filled
    if (curr == 0)
    return true;

    // Try placing two instances of 'curr' at
    // all possible locations till solution is found
    int i;
    for (i = 0; i < 2 * n - curr - 1; i++)
    {
        // Two 'curr' should be placed at
        // 'curr+1' distance
        if (res[i] == 0 && res[i + curr + 1] == 0)
        {

            // Plave two instances of 'curr'
            res[i] = res[i + curr + 1] = curr;

            // Recur to check if the above placement
            // leads to a solution
            if (fillUtil(res, curr - 1, n))
                return true;

            // If solution is not possible,
            // then backtrack
            res[i] = res[i + curr + 1] = 0;
        }
    }
    return false;
}

// This function prints the result for
// input number 'n' using fillUtil()
void fill(int n)
{
    // Create an array of size 2n and
    // initialize all elements in it as 0
    int res[2 * n], i;
    for (i = 0; i < 2 * n; i++)
    res[i] = 0;

    // If solution is possible,
    // then print it.
    if (fillUtil(res, n, n))
    {
        for (i = 0; i < 2 * n; i++)
        cout << res[i] << " ";
    }
    else
        cout << "Not Possible";
}

// Driver Code
int main()
{
    fill(7);
    return 0;
}

// This code is contributed
// by SHUBHAMSINGH8410
```

## C

```
// A backtracking based C Program to fill two instances of all numbers
// from 1 to n in a specific way
#include <stdio.h>
#include <stdbool.h>

// A recursive utility function to fill two instances of numbers from
// 1 to n in res[0..2n-1].  'curr' is current value of n.
bool fillUtil(int res[], int curr, int n)
{
     // If current number becomes 0, then all numbers are filled
     if (curr == 0) return true;

     // Try placing two instances of 'curr' at all possible locations
     // till solution is found
     int i;
     for (i=0; i<2*n-curr-1; i++)
     {
        // Two 'curr' should be placed at 'curr+1' distance
        if (res[i] == 0 && res[i + curr + 1] == 0)
        {
           // Plave two instances of 'curr'
           res[i] = res[i + curr + 1] = curr;

           // Recur to check if the above placement leads to a solution
           if (fillUtil(res, curr-1, n))
               return true;

           // If solution is not possible, then backtrack
           res[i] = res[i + curr + 1] = 0;
        }
     }
     return false;
}

// This function prints the result for input number 'n' using fillUtil()
void fill(int n)
{
    // Create an array of size 2n and initialize all elements in it as 0
    int res[2*n], i;
    for (i=0; i<2*n; i++)
       res[i] = 0;

    // If solution is possible, then print it.
    if (fillUtil(res, n, n))
    {
        for (i=0; i<2*n; i++)
           printf("%d ", res[i]);
    }
    else
        puts("Not Possible");
}

// Driver program
int main()
{
  fill(7);
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A backtracking based C++ Program to fill
// two instances of all numbers from 1 to n
// in a specific way
import java.io.*;

class GFG
{

// A recursive utility function to fill
// two instances of numbers from 1 to n
// in res[0..2n-1]. 'curr' is current value of n.
static boolean fillUtil(int res[], int curr, int n)
{
    // If current number becomes 0,
    // then all numbers are filled
    if (curr == 0)
    return true;

    // Try placing two instances of 'curr' at
    // all possible locations till solution is found
    int i;
    for (i = 0; i < 2 * n - curr - 1; i++)
    {
        // Two 'curr' should be placed at
        // 'curr+1' distance
        if (res[i] == 0 && res[i + curr + 1] == 0)
        {

            // Plave two instances of 'curr'
            res[i] = res[i + curr + 1] = curr;

            // Recur to check if the above placement
            // leads to a solution
            if (fillUtil(res, curr - 1, n))
                return true;

            // If solution is not possible,
            // then backtrack
            res[i] = res[i + curr + 1] = 0;
        }
    }
    return false;
}

// This function prints the result for
// input number 'n' using fillUtil()
static void fill(int n)
{
    // Create an array of size 2n and
    // initialize all elements in it as 0
    int res[] = new int[2 * n];
    int i;
    for (i = 0; i < 2 * n; i++)
    res[i] = 0;

    // If solution is possible,
    // then print it.
    if (fillUtil(res, n, n))
    {
        for (i = 0; i < 2 * n; i++)
            System.out.print(res[i] + " ");
    }
    else
        System.out.print("Not Possible");
}

// Driver Code
public static void main (String[] args)
{
    fill(7);
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# A backtracking based Python3 Program
# to fill two instances of all numbers
# from 1 to n in a specific way
def fillUtil(res, curr, n):

    # A recursive utility function to fill
    # two instances of numbers from 1 to n
    # in res[0..2n-1]. 'curr' is current value of n.

    # If current number becomes 0,
    # then all numbers are filled
    if curr == 0:
        return True

    # Try placing two instances of 'curr' at all
    # possible locations till solution is found
    for i in range(2 * n - curr - 1):

        # Two 'curr' should be placed
        # at 'curr+1' distance
        if res[i] == 0 and res[i + curr + 1] == 0:

            # Place two instances of 'curr'
            res[i] = res[i + curr + 1] = curr

            # Recur to check if the above
            # placement leads to a solution
            if fillUtil(res, curr - 1, n):
                return True

            # If solution is not possible,
            # then backtrack
            res[i] = 0
            res[i + curr + 1] = 0

    return False

def fill(n):

    # This function prints the result
    # for input number 'n' using fillUtil()

    # Create an array of size 2n and
    # initialize all elements in it as 0
    res = [0] * (2 * n)

    # If solution is possible, then print it.
    if fillUtil(res, n, n):
        for i in range(2 * n):
            print(res[i], end = ' ')
        print()
    else:
        print("Not Possible")

# Driver Code
if __name__ == '__main__':
    fill(7)

# This code is contributed by vibhu4agarwal
```

## C#

```
// A backtracking based C# Program to fill
// two instances of all numbers from 1 to n
// in a specific way
using System;

class GFG
{

// A recursive utility function to fill
// two instances of numbers from 1 to n
// in res[0..2n-1]. 'curr' is current value of n.
static bool fillUtil(int []res, int curr, int n)
{
    // If current number becomes 0,
    // then all numbers are filled
    if (curr == 0)
    return true;

    // Try placing two instances of 'curr' at
    // all possible locations till solution is found
    int i;
    for (i = 0; i < 2 * n - curr - 1; i++)
    {
        // Two 'curr' should be placed at
        // 'curr+1' distance
        if (res[i] == 0 && res[i + curr + 1] == 0)
        {

            // Plave two instances of 'curr'
            res[i] = res[i + curr + 1] = curr;

            // Recur to check if the above placement
            // leads to a solution
            if (fillUtil(res, curr - 1, n))
                return true;

            // If solution is not possible,
            // then backtrack
            res[i] = res[i + curr + 1] = 0;
        }
    }
    return false;
}

// This function prints the result for
// input number 'n' using fillUtil()
static void fill(int n)
{
    // Create an array of size 2n and
    // initialize all elements in it as 0
    int []res=new int[2 * n];
    int i;
    for (i = 0; i < (2 * n); i++)
    res[i] = 0;

    // If solution is possible,
    // then print it.
    if (fillUtil(res, n, n))
    {
        for (i = 0; i < 2 * n; i++)
        Console.Write (res[i] + " ");
    }
    else
        Console.Write ("Not Possible");
}

// Driver Code
static public void Main ()
{
    fill(7);
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>
    // A backtracking based Javascript Program to fill
    // two instances of all numbers from 1 to n
    // in a specific way

    // A recursive utility function to fill
    // two instances of numbers from 1 to n
    // in res[0..2n-1]. 'curr' is current value of n.
    function fillUtil(res, curr, n)
    {

        // If current number becomes 0,
        // then all numbers are filled
        if (curr == 0)
            return true;

        // Try placing two instances of 'curr' at
        // all possible locations till solution is found
        let i;
        for (i = 0; i < 2 * n - curr - 1; i++)
        {
            // Two 'curr' should be placed at
            // 'curr+1' distance
            if (res[i] == 0 && res[i + curr + 1] == 0)
            {

                // Plave two instances of 'curr'
                res[i] = res[i + curr + 1] = curr;

                // Recur to check if the above placement
                // leads to a solution
                if (fillUtil(res, curr - 1, n))
                    return true;

                // If solution is not possible,
                // then backtrack
                res[i] = res[i + curr + 1] = 0;
            }
        }
        return false;
    }

    // This function prints the result for
    // input number 'n' using fillUtil()
    function fill(n)
    {

        // Create an array of size 2n and
        // initialize all elements in it as 0
        let res=new Array(2 * n);
        let i;
        for (i = 0; i < (2 * n); i++)
            res[i] = 0;

        // If solution is possible,
        // then print it.
        if (fillUtil(res, n, n))
        {
            for (i = 0; i < 2 * n; i++)
            document.write(res[i] + " ");
        }
        else
            document.write("Not Possible");
    }

    fill(7);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
7 3 6 2 5 3 2 4 7 6 5 1 4 1
```

上述解决方案可能不是最好的解决方案。输出中似乎有一个模式。我正在从其他极客那里寻找更好的解决方案。
本文由 **Asif** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息