# 数组中任意元素前的最大倍数

> 原文:[https://www . geeksforgeeks . org/任意元素前的最大数组倍数/](https://www.geeksforgeeks.org/maximum-number-of-multiples-in-an-array-before-any-element/)

给定一个数组 **arr[]** ，任务是在所有数组元素中找到最大数量的索引 **j < i** ，使得 **(arr[j] % arr[i]) = 0** 。

**示例:**

> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:** 3
> 自身前各元素的倍数–
> N(8)= 0()
> N(1)= 1(8)
> N(28)= 0()
> N(4)= 2(28，8)
> N(2) = 3 (4，28，8)
> N(6) =
> 
> **输入:** arr[] = {8，12，56，32，10，3，2，4}
> **输出:** 5

**进场:**

1.  使用[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储每个数组元素的所有除数。
2.  使用[这篇](https://www.geeksforgeeks.org/find-all-divisors-of-a-natural-number-set-2/)文章中讨论的方法，在 **sqrt(n)** 时间内生成一个元素的所有除数。
3.  现在，取每个元素所有存储除数的最大值并更新它。

下面是上述方法的实现:

## C++14

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;

// Map to store the divisor count
int divisors[MAX];

// Function to generate the divisors
// of all the array elements
int generateDivisors(int n)
{
    for (int i = 1; i <= sqrt(n); i++) {
        if (n % i == 0) {
            if (n / i == i) {
                divisors[i]++;
            }
            else {
                divisors[i]++;
                divisors[n / i]++;
            }
        }
    }
}

// Function to find the maximum number
// of multiples in an array before it
int findMaxMultiples(int* arr, int n)
{
    // To store the maximum divisor count
    int ans = 0;

    for (int i = 0; i < n; i++) {

        // Update ans if more number
        // of divisors are found
        ans = max(divisors[arr[i]], ans);

        // Generating all the divisors of
        // the next element of the array
        generateDivisors(arr[i]);
    }
    return ans;
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = sizeof(arr) / sizeof(int);

    cout << findMaxMultiples(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 100000;

// Map to store the divisor count
static int []divisors = new int[MAX];

// Function to generate the divisors
// of all the array elements
static void generateDivisors(int n)
{
    for (int i = 1; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (n / i == i)
            {
                divisors[i]++;
            }
            else
            {
                divisors[i]++;
                divisors[n / i]++;
            }
        }
    }
}

// Function to find the maximum number
// of multiples in an array before it
static int findMaxMultiples(int []arr, int n)
{
    // To store the maximum divisor count
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // Update ans if more number
        // of divisors are found
        ans = Math.max(divisors[arr[i]], ans);

        // Generating all the divisors of
        // the next element of the array
        generateDivisors(arr[i]);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.length;

    System.out.print(findMaxMultiples(arr, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import ceil,sqrt
MAX = 100000

# Map to store the divisor count
divisors = [0] * MAX

# Function to generate the divisors
# of all the array elements
def generateDivisors(n):
    for i in range(1,ceil(sqrt(n)) + 1):
        if (n % i == 0):
            if (n // i == i):
                divisors[i]+=1
            else:
                divisors[i] += 1
                divisors[n // i] += 1

# Function to find the maximum number
# of multiples in an array before it
def findMaxMultiples(arr, n):

    # To store the maximum divisor count
    ans = 0
    for i in range(n):

        # Update ans if more number
        # of divisors are found
        ans = max(divisors[arr[i]], ans)

        # Generating all the divisors of
        # the next element of the array
        generateDivisors(arr[i])
    return ans

# Driver code
arr = [8, 1, 28, 4, 2, 6, 7]
n = len(arr)

print(findMaxMultiples(arr, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int MAX = 100000;

// Map to store the divisor count
static int []divisors = new int[MAX];

// Function to generate the divisors
// of all the array elements
static void generateDivisors(int n)
{
    for (int i = 1; i <= Math.Sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (n / i == i)
            {
                divisors[i]++;
            }
            else
            {
                divisors[i]++;
                divisors[n / i]++;
            }
        }
    }
}

// Function to find the maximum number
// of multiples in an array before it
static int findMaxMultiples(int []arr, int n)
{
    // To store the maximum divisor count
    int ans = 0;

    for (int i = 0; i < n; i++)
    {

        // Update ans if more number
        // of divisors are found
        ans = Math.Max(divisors[arr[i]], ans);

        // Generating all the divisors of
        // the next element of the array
        generateDivisors(arr[i]);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.Length;

    Console.Write(findMaxMultiples(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach
const MAX = 100000;

// Map to store the divisor count
var divisors = new Array(MAX).fill(0);

// Function to generate the divisors
// of all the array elements
function generateDivisors(n)
{
    for(var i = 1; i <= Math.sqrt(n); i++)
    {
        if (n % i == 0)
        {
            if (n / i == i)
            {
                divisors[i]++;
            }
            else
            {
                divisors[i]++;
                divisors[n / i]++;
            }
        }
    }
}

// Function to find the maximum number
// of multiples in an array before it
function findMaxMultiples(arr, n)
{

    // To store the maximum divisor count
    var ans = 0;

    for(var i = 0; i < n; i++)
    {

        // Update ans if more number
        // of divisors are found
        ans = Math.max(divisors[arr[i]], ans);

        // Generating all the divisors of
        // the next element of the array
        generateDivisors(arr[i]);
    }
    return ans;
}

// Driver code
var arr = [ 8, 1, 28, 4, 2, 6, 7 ];
var n = arr.length;

document.write(findMaxMultiples(arr, n));

// This code is contributed by rdtank

</script>
```

**Output:** 

```
3
```