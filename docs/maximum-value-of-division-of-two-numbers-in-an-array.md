# 数组中两个数相除的最大值

> 原文:[https://www . geesforgeks . org/数组中两个数的最大除法值/](https://www.geeksforgeeks.org/maximum-value-of-division-of-two-numbers-in-an-array/)

给定一个大小为 **N ( > 2)** 的数组 **A** 。任务是求 **A[i] / A[j]**
**的最大值注:** A[i] ≠ 0。

**示例:**

> **输入:** A[] = {1，2，3，4}
> **输出:** 4
> 4 / 1 = 4 是最大可能值。
> 
> **输入:** A[] = {3，7，9，3，11}
> **输出:** 3

**天真的方法:**天真的方法是运行嵌套循环并找到最大可能的答案。
T3】时间复杂度 : O(N <sup>2</sup> )。

**高效方法**:高效方法是在数组中找到**最大**和**最小**元素，打印**最大/最小**

**证明:**

> 让我们取一个数组 A[] = {a，b，c，d}，其中 a < b < c < d . 
> 现在:
> **(b/A)<(c/A)<(d/A)**(因为 b < c < d，分母是常数)
> 并且因为 A 是最小值，所以
> d / a 是最大值

下面是上述方法的实现:

## C++

```
// CPP program to maximum value of
// division of two numbers in an array
#include <bits/stdc++.h>
using namespace std;

// Function to maximum value of
// division of two numbers in an array
int Division(int a[], int n)
{
    int maxi = INT_MIN, mini = INT_MAX;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        maxi = max(a[i], maxi);
        mini = min(a[i], mini);
    }

    // Return the required answer
    return maxi / mini;
}

// Driver code
int main()
{
    int a[] = {3, 7, 9, 3, 11};

    int n = sizeof(a) / sizeof(a[0]);

    cout << Division(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to maximum value of
// division of two numbers in an array
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{

// Function to maximum value of
// division of two numbers in an array
static int Division(int a[], int n)
{
    int maxi = Integer.MIN_VALUE,
        mini = Integer.MAX_VALUE;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        maxi = Math.max(a[i], maxi);
        mini = Math.min(a[i], mini);
    }

    // Return the required answer
    return maxi / mini;
}

// Driver code
public static void main (String[] args)
              throws java.lang.Exception
{
    int a[] = {3, 7, 9, 3, 11};

    int n = a.length;

    System.out.print(Division(a, n));
}
}

// This code is contributed by Nidhiva
```

## 蟒蛇 3

```
#  Python3 program to maximum value of
# division of two numbers in an array

# Function to maximum value of
# division of two numbers in an array
def Division(a, n):

    maxi = -10**9
    mini = 10**9

    # Traverse through the array
    for i in a:
        maxi = max(i, maxi)
        mini = min(i, mini)

    # Return the required answer
    return maxi // mini

# Driver code
a = [3, 7, 9, 3, 11]

n = len(a)

print(Division(a, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program to maximum value of
// division of two numbers in an array
using System;

class GFG
{

// Function to maximum value of
// division of two numbers in an array
static int Division(int []a, int n)
{
    int maxi = int.MinValue,
        mini = int.MaxValue;

    // Traverse through the array
    for (int i = 0; i < n; i++)
    {
        maxi = Math.Max(a[i], maxi);
        mini = Math.Min(a[i], mini);
    }

    // Return the required answer
    return maxi / mini;
}

// Driver code
public static void Main (String[] args)
{
    int []a = {3, 7, 9, 3, 11};

    int n = a.Length;

    Console.WriteLine(Division(a, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to maximum value of
// division of two numbers in an array

// Function to maximum value of
// division of two numbers in an array
function Division(a, n)
{
    let maxi = Number.MIN_VALUE, mini = Number.MAX_VALUE;

    // Traverse through the array
    for (let i = 0; i < n; i++)
    {
        maxi = Math.max(a[i], maxi);
        mini = Math.min(a[i], mini);
    }

    // Return the required answer
    return parseInt(maxi / mini);
}

// Driver code
    let a = [3, 7, 9, 3, 11];

    let n = a.length;

    document.write(Division(a, n));

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间 : O(1)

**注:**上述解决方案仅适用于正整数