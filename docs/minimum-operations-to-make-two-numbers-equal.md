# 使两个数相等的最小运算

> 原文:[https://www . geesforgeks . org/最小运算使两个数相等/](https://www.geeksforgeeks.org/minimum-operations-to-make-two-numbers-equal/)

给定两个数字 **n** 和 **m** ，任务是找到使它们相等所需的最小操作数，如果可以对它们执行以下操作的话。

*   在第一次操作中，这两个数字中的任何一个都可以加 1。
*   在第二次操作中，这两个数字中的任何一个都可以加二。
*   在第三次操作中，这两个数字中的任何一个都可以增加三，以此类推。

**例:**

```
Input : n = 1, m = 3
Output : 3
Explanation: 
Add 1 to n; n = 2
Add 2 to m; m = 5
Add 3 to n; n = 5
Both n and m are equal now
N of operations = 3

Input : n = 30, m = 20
Output : 4
```

**方法:**
用于解决问题的方法是一个 AP 中 N 个项的和。
由公式
给出

```
S(n) = (n*(n+1))/2
```

因此，任务是找出这两个数字之间的差异，看看是否可以通过添加前 n 个元素来实现差异。因此，

```
S(n) = max(m,n) - min(m,n)
```

在第一个方程中代入这个和的值；
我们得到
给出的元素个数 n

```
n=(-1+sqrt(1+8*S(n)))/2
```

如果这个 n 是一个完美的整数，那么它就是我们的最终答案。
否则，我们将*目标值增加 1 以达到*并继续。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum no of operations
int minOperations(int n, int m)
{
    int a = 0, k = 1;

    // find the maximum of two and store it in p
    int p = max(n, m);

    // increase it until it is achievable from
    // given n and m
    while (n != m) {

        // Here value added to n and m will be
        // S(n)=p-n+p-m;
        // check whether integer value of n exist
        // by the formula
        // n=(-1+sqrt(1+8*S(n)))/2
        float s = (float)(p - n + p - m);
        float q = (-1 + sqrt(8 * s + 1)) / 2;
        if (q - floor(q) == 0) {
            a = q;
            n = m;
        }

        p = p + 1;
    }
    return a;
}

// Driver code
int main()
{
    int n = 1, m = 3;

    // Function calling
    cout << minOperations(n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to find the minimum no of operations
static int minOperations(int n, int m)
{
    int a = 0, k = 1;

    // find the maximum of two and store it in p
    int p = Math.max(n, m);

    // increase it until it is achievable from
    // given n and m
    while (n != m)
    {

        // Here value added to n and m will be
        // S(n)=p-n+p-m;
        // check whether integer value of n exist
        // by the formula
        // n=(-1+Math.sqrt(1+8*S(n)))/2
        float s = (float)(p - n + p - m);
        float q = (float) ((-1 + Math.sqrt(8 * s + 1)) / 2);
        if (q - Math.floor(q) == 0)
        {
            a = (int) q;
            n = m;
        }

        p = p + 1;
    }
    return a;
}

// Driver code
public static void main(String[] args)
{
    int n = 1, m = 3;

    // Function calling
    System.out.print(minOperations(n, m));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach
from math import sqrt, floor

# Function to find the minimum
# no. of operations
def minOperations( n, m) :

    a = 0; k = 1;

    # find the maximum of two and
    # store it in p
    p = max(n, m);

    # increase it until it is achievable
    # from given n and m
    while (n != m) :

        # Here value added to n and m will be
        # S(n)=p-n+p-m;
        # check whether integer value of n 
        # exist by the formula
        # n=(-1+sqrt(1+8*S(n)))/2
        s = float(p - n + p - m);
        q = (-1 + sqrt(8 * s + 1)) / 2;
        if (q - floor(q) == 0) :
            a = q;
            n = m;

        p = p + 1;

    return a;

# Driver code
if __name__ == "__main__" :

    n = 1; m = 3;

    # Function calling
    print(minOperations(n, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to find the minimum no of operations
    static int minOperations(int n, int m)
    {
        int a = 0, k = 1;

        // find the maximum of two and store it in p
        int p = Math.Max(n, m);

        // increase it until it is achievable from
        // given n and m
        while (n != m)
        {

            // Here value added to n and m will be
            // S(n)=p-n+p-m;
            // check whether integer value of n exist
            // by the formula
            // n=(-1+Math.sqrt(1+8*S(n)))/2
            float s = (float)(p - n + p - m);
            float q = (float) ((-1 + Math.Sqrt(8 * s + 1)) / 2);
            if (q - Math.Floor(q) == 0)
            {
                a = (int) q;
                n = m;
            }

            p = p + 1;
        }
        return a;
    }

    // Driver code
    public static void Main()
    {
        int n = 1, m = 3;

        // Function calling
        Console.Write(minOperations(n, m));
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    // Function to find the minimum no of operations
    function minOperations(n , m) {
        var a = 0, k = 1;

        // find the maximum of two and store it in p
        var p = Math.max(n, m);

        // increase it until it is achievable from
        // given n and m
        while (n != m)
        {

            // Here value added to n and m will be
            // S(n)=p-n+p-m;
            // check whether integer value of n exist
            // by the formula
            // n=(-1+Math.sqrt(1+8*S(n)))/2
            var s =  (p - n + p - m);
            var q =  ((-1 + Math.sqrt(8 * s + 1)) / 2);
            if (q - Math.floor(q) == 0)
            {
                a = parseInt( q);
                n = m;
            }

            p = p + 1;
        }
        return a;
    }

    // Driver code
        var n = 1, m = 3;

        // Function calling
        document.write(minOperations(n, m));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
3
```