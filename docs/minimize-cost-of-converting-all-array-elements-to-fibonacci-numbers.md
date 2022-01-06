# 最小化将所有数组元素转换为斐波那契数的成本

> 原文:[https://www . geeksforgeeks . org/将所有数组元素转换为斐波那契数的最小成本/](https://www.geeksforgeeks.org/minimize-cost-of-converting-all-array-elements-to-fibonacci-numbers/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是最小化将所有数组元素转换为[个斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)的成本，其中将一个数 **A** 转换为 **B** 的成本是 **A** 和 **B** 之间的绝对差值。

**示例:**

> **输入:** arr[] = {56，34，23，98，7}
> **输出:** 13
> **解释:**
> 以下是将所有数组元素转换为斐波那契数所需的元素转换:
> 
> 1.  将 arr[0](= 56)转换为 55。成本= | 56–55 | = 1。
> 2.  将 arr[1](= 34)转换为 34。成本= | 34–34 | = 0。
> 3.  将 arr[2](= 23)转换为 21。成本= | 23–21 | = 2。
> 4.  将 arr[3](= 98)转换为 89。成本= | 98–89 | = 9。
> 5.  将 arr[4](= 7)转换为 8。成本= | 7–8 | = 1。
> 
> 因此，将所有数组元素更改为斐波那契数的总成本= 1 + 0 + 2 + 9 + 1 = 13。
> 
> **输入:** {543，32，7，23，641}
> **输出:** 103

**方法:**给定的问题可以通过将每个数组元素替换为[其最近的斐波那契数](https://www.geeksforgeeks.org/nearest-fibonacci-number-to-n/)来解决，以获得将所有数组元素更改为[斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)的最小成本。按照以下步骤解决给定的问题:

*   初始化一个变量，比如**成本**，它存储了将所有数组元素更改为斐波那契数的最小成本。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   要找到最接近 **arr[i]** 的斐波那契数，首先，使用公式![N = \frac {\log(\sqrt 5*arr[i])}{\log \frac{1 + \sqrt 5}{2}}](img/80b83a2fdf31a027a9d3438f96103628.png "Rendered by QuickLaTeX.com")找到 **N** 的值，使得[T5】N<sup>第</sup>斐波那契数 T9】为 **arr[i]**](https://www.geeksforgeeks.org/find-nth-fibonacci-number-using-golden-ratio/)
    *   现在，找到 [**N <sup>th</sup> 和(N + 1) <sup>th</sup> 斐波那契数**](https://www.geeksforgeeks.org/find-nth-fibonacci-number-using-golden-ratio/) ，分别说出 **X** 和 **Y** ，将**(X–arr[I])**和**(Y–arr[I])**的绝对值的最小值加到**成本**上。
*   完成上述步骤后，打印**成本**的值作为最终最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// N-th Fibonacci Number
int nthFibo(int n)
{

    // Find the value of a, b, and r
    double a = (pow(5, 0.5) + 1) / 2;
    double b = (-1*(pow(5, 0.5) ) + 1) / 2;
    double r = pow(5, 0.5);

    // Find the N-th Fibonacci
    double ans = (pow(a, n) - pow(b, n)) / r;

    // Return the result
    return int(ans);
}

// Function to find the Fibonacci
// number which is nearest to X
int nearFibo(int X)
{
    double a = (pow(5, 0.5) + 1) / 2;

    // Calculate the value of n for X
    int n = int(log((pow(5, 0.5)) * X) / log(a));

    int nth = nthFibo(n);
    int nplus = nthFibo(n + 1);

    // Return the nearest
    // Fibonacci Number
    if (abs(X - nth) < abs(X - nplus))
        return nth;
    else
        return nplus;
}

// Function to find the minimum
// cost to convert all array
// elements to Fibonacci Numbers
int getCost(int arr[], int n)
{

    // Stores the total minimum cost
    int cost = 0;

    // Traverse the given array arr[]
    for(int i = 0; i < n; i++)
    {

        // Find the nearest
        // Fibonacci Number
        int fibo = nearFibo(arr[i]);

        // Add the cost
        cost += abs(arr[i] - fibo);
    }

    // Return the final cost
    return cost;
}

// Driver Code
int main()
{
    int arr[] = { 56, 34, 23, 98, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << (getCost(arr, n));
}

// This code is contributed by ukasp
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG
{

// Function to find the
// N-th Fibonacci Number
static int nthFibo(int n)
{

    // Find the value of a, b, and r
    double a = (Math.pow(5, 0.5) + 1) / 2;
    double b = (-1*(Math.pow(5, 0.5) ) + 1) / 2;
    double r = Math.pow(5, 0.5);

    // Find the N-th Fibonacci
    double ans = (Math.pow(a, n) - Math.pow(b, n)) / r;

    // Return the result
    return (int)ans;
}

// Function to find the Fibonacci
// number which is nearest to X
static int nearFibo(int X)
{
    double a = (Math.pow(5, 0.5) + 1) / 2;

    // Calculate the value of n for X
    int n = (int)(Math.log((Math.pow(5, 0.5)) * X) / Math.log(a));

    int nth = nthFibo(n);
    int nplus = nthFibo(n + 1);

    // Return the nearest
    // Fibonacci Number
    if (Math.abs(X - nth) < Math.abs(X - nplus))
        return nth;
    else
        return nplus;
}

// Function to find the minimum
// cost to convert all array
// elements to Fibonacci Numbers
static int getCost(int arr[], int n)
{

    // Stores the total minimum cost
    int cost = 0;

    // Traverse the given array arr[]
    for(int i = 0; i < n; i++)
    {

        // Find the nearest
        // Fibonacci Number
        int fibo = nearFibo(arr[i]);

        // Add the cost
        cost += Math.abs(arr[i] - fibo);
    }

    // Return the final cost
    return cost;
}

// Driver code
public static void main (String[] args)
{
 int arr[] = { 56, 34, 23, 98, 7 };
    int n = arr.length;
 System.out.print(getCost(arr, n));
    }
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program for the above approach

import math

# Function to find the
# N-th Fibonacci Number
def nthFibo(n):

    # Find the value of a, b, and r
    a = (5**(1 / 2) +1)/2
    b = (-5**(1 / 2) +1)/2
    r = 5**(1 / 2)

    # Find the N-th Fibonacci
    ans = (a**n - b**n)/r

    # Return the result
    return int(ans)

# Function to find the Fibonacci
# number which is nearest to X
def nearFibo(X):

    a = (5**(1 / 2)+1)/2

    # Calculate the value of n for X
    n = int(math.log((5**(1 / 2))*X) / math.log(a))

    nth = nthFibo(n)
    nplus = nthFibo(n + 1)

    # Return the nearest
    # Fibonacci Number
    if abs(X - nth) < abs(X - nplus):
        return nth
    else:
        return nplus

# Function to find the minimum
# cost to convert all array
# elements to Fibonacci Numbers
def getCost(arr):

    # Stores the total minimum cost
    cost = 0

    # Traverse the given array arr[]
    for i in arr:

        # Find the nearest
        # Fibonacci Number
        fibo = nearFibo(i)

        # Add the cost
        cost += abs(i-fibo)

    # Return the final cost
    return cost

# Driver Code

arr = [56, 34, 23, 98, 7]

print(getCost(arr))
```

## C#

```
// C# program to count frequencies of array items
using System;

class GFG{

// Function to find the
// N-th Fibonacci Number
static int nthFibo(int n)
{

    // Find the value of a, b, and r
    double a = (Math.Pow(5, 0.5) + 1) / 2;
    double b = (-1*(Math.Pow(5, 0.5) ) + 1) / 2;
    double r = Math.Pow(5, 0.5);

    // Find the N-th Fibonacci
    double ans = (Math.Pow(a, n) -
                  Math.Pow(b, n)) / r;

    // Return the result
    return (int)ans;
}

// Function to find the Fibonacci
// number which is nearest to X
static int nearFibo(int X)
{
    double a = (Math.Pow(5, 0.5) + 1) / 2;

    // Calculate the value of n for X
    int n = (int)(Math.Log((Math.Pow(5, 0.5)) * X) /
                            Math.Log(a));

    int nth = nthFibo(n);
    int nplus = nthFibo(n + 1);

    // Return the nearest
    // Fibonacci Number
    if (Math.Abs(X - nth) < Math.Abs(X - nplus))
        return nth;
    else
        return nplus;
}

// Function to find the minimum
// cost to convert all array
// elements to Fibonacci Numbers
static int getCost(int []arr, int n)
{

    // Stores the total minimum cost
    int cost = 0;

    // Traverse the given array arr[]
    for(int i = 0; i < n; i++)
    {

        // Find the nearest
        // Fibonacci Number
        int fibo = nearFibo(arr[i]);

        // Add the cost
        cost += Math.Abs(arr[i] - fibo);
    }

    // Return the final cost
    return cost;
}   

// Driver code
public static void Main(String []args)
{
    int []arr = { 56, 34, 23, 98, 7 };
    int n = arr.Length;

    Console.WriteLine(getCost(arr, n));
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the
// N-th Fibonacci Number
function nthFibo(n)
{

    // Find the value of a, b, and r
    let a = (Math.pow(5, 0.5) + 1) / 2;
    let b = (-1*(Math.pow(5, 0.5) ) + 1) / 2;
    let r = Math.pow(5, 0.5);

    // Find the N-th Fibonacci
    let ans = (Math.pow(a, n) - Math.pow(b, n)) / r;

    // Return the result
    return Math.floor(ans);
}

// Function to find the Fibonacci
// number which is nearest to X
function nearFibo(X)
{
    let a = (Math.pow(5, 0.5) + 1) / 2;

    // Calculate the value of n for X
    let n = Math.floor(Math.log((Math.pow(5, 0.5)) * X) / Math.log(a));

    let nth = nthFibo(n);
    let nplus = nthFibo(n + 1);

    // Return the nearest
    // Fibonacci Number
    if (Math.abs(X - nth) < Math.abs(X - nplus))
        return nth;
    else
        return nplus;
}

// Function to find the minimum
// cost to convert all array
// elements to Fibonacci Numbers
function getCost(arr, n)
{

    // Stores the total minimum cost
    let cost = 0;

    // Traverse the given array arr[]
    for(let i = 0; i < n; i++)
    {

        // Find the nearest
        // Fibonacci Number
        let fibo = nearFibo(arr[i]);

        // Add the cost
        cost += Math.abs(arr[i] - fibo);
    }

    // Return the final cost
    return cost;
}

// Driver Code

    let arr = [ 56, 34, 23, 98, 7 ];
    let n = arr.length;
    document.write(getCost(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)