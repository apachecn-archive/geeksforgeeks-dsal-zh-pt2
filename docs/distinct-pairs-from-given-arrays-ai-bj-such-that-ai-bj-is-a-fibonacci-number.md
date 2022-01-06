# 给定数组(a[i]，b[j])的不同对，使得(a[i] + b[j])是斐波那契数

> 原文:[https://www . geesforgeks . org/distinct-pairs-from-给定数组-ai-bj-so-ai-bj-is-a-Fibonacci-number/](https://www.geeksforgeeks.org/distinct-pairs-from-given-arrays-ai-bj-such-that-ai-bj-is-a-fibonacci-number/)

给定两个数组 **a[]** 和 **b[]** ，任务是对配对 **(a[i]，b[j])** 进行计数，使得 **(a[i] + b[j])** 为斐波那契数。**注**说明 **(a，b)** 等于 **(b，a)** ，将计数一次。
前几个斐波那契数是:

> 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 141, … ..

**例:**

> **输入:** a[] = {99，1，33，2}，b[] = {1，11，2}
> **输出:** 4
> 总共不同的对是(1，1)，(1，2)，(33，1)和(2，11)
> **输入:** a[] = {5，0，8}，b[] = {0，9}
> **输出:** 3

**进场:**

*   取空[套](https://www.geeksforgeeks.org/set-in-cpp-stl/)。
*   运行两个嵌套循环，从两个数组中生成所有可能的对，从第一个数组中获取一个元素(称之为 a)，从第二个数组中获取一个元素(称之为 b)。
*   在 **(a + b)** 上应用斐波那契检验，即为了使数字 **x** 成为斐波那契数， **5 * x <sup>2</sup> + 4** 或**5 * x<sup>2</sup>–4**中的任何一个必须是一个完美的正方形。
*   如果是斐波那契数，则在集合中推 **(a，b)** ，如果是 **a < b** 或 **(b，a)** ，如果是 **b < a** 。这样做是为了避免重复。
*   集合的大小最终是有效对的总数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// x is a perfect square
bool isPerfectSquare(long double x)
{
    // Find floating point value of
    // square root of x
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function that returns true if
// n is a Fibonacci Number
bool isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of distinct pairs
// from the given array such that the sum of the
// pair elements is a Fibonacci number
int totalPairs(int a[], int b[], int n, int m)
{
    // Set is used to avoid duplicate pairs
    set<pair<int, int> > s;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If sum is a Fibonacci number
            if (isFibonacci(a[i] + b[j]) == true) {
                if (a[i] < b[j])
                    s.insert(make_pair(a[i], b[j]));
                else
                    s.insert(make_pair(b[j], a[i]));
            }
        }
    }

    // Return the size of the set
    return s.size();
}

// Driver code
int main()
{
    int a[] = { 99, 1, 33, 2 };
    int b[] = { 1, 11, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    int m = sizeof(b) / sizeof(b[0]);

    cout << totalPairs(a, b, n, m);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function that returns true if
// x is a perfect square
static boolean isPerfectSquare(double x)
{
    // Find floating point value of
    // square root of x
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function that returns true if
// n is a Fibonacci Number
static boolean isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of distinct pairs
// from the given array such that the sum of the
// pair elements is a Fibonacci number
static int totalPairs(int a[], int b[],
                      int n, int m)
{
    // Set is used to avoid duplicate pairs
    List<pair> s = new LinkedList<>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // If sum is a Fibonacci number
            if (isFibonacci(a[i] + b[j]) == true)
            {

                if (a[i] < b[j])
                {
                    if(checkDuplicate(s, new pair(a[i], b[j])))
                        s.add(new pair(a[i], b[j]));
                }
                else
                {
                    if(checkDuplicate(s, new pair(b[j], a[i])))
                        s.add(new pair(b[j], a[i]));
                }
            }
        }
    }

    // Return the size of the set
    return s.size();
}

static boolean checkDuplicate(List<pair> pairList,
                                    pair newPair)
{
    for(pair p: pairList)
    {
        if(p.first == newPair.first &&
           p.second == newPair.second)
            return false;
    }
    return true;
}

// Driver code
public static void main(String[] args)
{
    int a[] = { 99, 1, 33, 2 };
    int b[] = { 1, 11, 2 };
    int n = a.length;
    int m = b.length;

    System.out.println(totalPairs(a, b, n, m));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt,floor

# Function that returns true if
# x is a perfect square
def isPerfectSquare(x) :

    # Find floating point value of
    # square root of x
    sr = sqrt(x)

    # If square root is an integer
    return ((sr - floor(sr)) == 0)

# Function that returns true if
# n is a Fibonacci Number
def isFibonacci(n ) :

    return (isPerfectSquare(5 * n * n + 4) or
            isPerfectSquare(5 * n * n - 4))

# Function to return the count of distinct pairs
# from the given array such that the sum of the
# pair elements is a Fibonacci number
def totalPairs(a, b, n, m) :

    # Set is used to avoid duplicate pairs
    s = set();

    for i in range(n) :
        for j in range(m) :

            # If sum is a Fibonacci number
            if (isFibonacci(a[i] + b[j]) == True) :
                if (a[i] < b[j]) :
                    s.add((a[i], b[j]));
                else :
                    s.add((b[j], a[i]));

    # Return the size of the set
    return len(s);

# Driver code
if __name__ == "__main__" :

    a = [ 99, 1, 33, 2 ];
    b = [ 1, 11, 2 ];
    n = len(a);
    m = len(b);

    print(totalPairs(a, b, n, m));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;            

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function that returns true if
// x is a perfect square
static bool isPerfectSquare(double x)
{
    // Find floating point value of
    // square root of x
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function that returns true if
// n is a Fibonacci Number
static bool isFibonacci(int n)
{
    return isPerfectSquare(5 * n * n + 4) ||
           isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of distinct pairs
// from the given array such that the sum of the
// pair elements is a Fibonacci number
static int totalPairs(int []a, int []b,
                      int n, int m)
{
    // Set is used to avoid duplicate pairs
    List<pair> s = new List<pair>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < m; j++)
        {

            // If sum is a Fibonacci number
            if (isFibonacci(a[i] + b[j]) == true)
            {

                if (a[i] < b[j])
                {
                    if(checkDuplicate(s, new pair(a[i], b[j])))
                                   s.Add(new pair(a[i], b[j]));
                }
                else
                {
                    if(checkDuplicate(s, new pair(b[j], a[i])))
                                   s.Add(new pair(b[j], a[i]));
                }
            }
        }
    }

    // Return the size of the set
    return s.Count;
}

static bool checkDuplicate(List<pair> pairList,
                                      pair newPair)
{
    foreach(pair p in pairList)
    {
        if(p.first == newPair.first &&
           p.second == newPair.second)
            return false;
    }
    return true;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 99, 1, 33, 2 };
    int []b = { 1, 11, 2 };
    int n = a.Length;
    int m = b.Length;

    Console.WriteLine(totalPairs(a, b, n, m));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// x is a perfect square
function isPerfectSquare(x)
{
    // Find floating point value of
    // square root of x
    var sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function that returns true if
// n is a Fibonacci Number
function isFibonacci(n)
{
    return isPerfectSquare(5 * n * n + 4)
           || isPerfectSquare(5 * n * n - 4);
}

// Function to return the count of distinct pairs
// from the given array such that the sum of the
// pair elements is a Fibonacci number
function totalPairs(a, b, n, m)
{
    // Set is used to avoid duplicate pairs
    var s = new Set();

    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {

            // If sum is a Fibonacci number
            if (isFibonacci(a[i] + b[j])) {
                if (a[i] < b[j])
                {
                    var tmp = a[i]+" "+b[j];
                    s.add(tmp);
                }
                else
                {
                    var tmp = b[j]+" "+a[i];
                    s.add(tmp);
                }
            }
        }
    }

    // Return the size of the set
    return s.size;
}

// Driver code
var a = [99, 1, 33, 2 ];
var b = [1, 11, 2 ];
var n = a.length;
var m = b.length;
document.write( totalPairs(a, b, n, m));

</script>
```

**Output:** 

```
4
```