# 不包含相邻元素的子集计数

> 原文:[https://www . geesforgeks . org/不包含相邻元素的子集计数/](https://www.geeksforgeeks.org/count-of-subsets-not-containing-adjacent-elements/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出给定数组中不包含相邻元素的所有子集的计数。

**示例:**

> **输入:** arr[] = {2，7}
> **输出:** 3
> 所有可能的子集都是{}、{2}和{7}。
> 
> **输入:** arr[] = {3，5，7 }
> T3】输出: 5

**方法 1:** 想法是使用位掩码模式来生成所有组合，如[这篇](https://www.geeksforgeeks.org/power-set/)文章中所讨论的。在考虑子集时，我们需要检查它是否包含相邻元素。如果在其位掩码中设置了两个或多个连续位，子集将包含相邻元素。为了检查位掩码是否设置了连续位，我们可以将掩码右移一位，并将其与掩码“与”。如果“与”运算的结果为 0，则掩码没有连续的集合，因此，相应的子集将没有来自数组的相邻元素。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
#include <math.h>
using namespace std;

// Function to return the count
// of possible subsets
int cntSubsets(int* arr, int n)
{

    // Total possible subsets of n
    // sized array is (2^n - 1)
    unsigned int max = pow(2, n);

    // To store the required
    // count of subsets
    int result = 0;

    // Run from i 000..0 to 111..1
    for (int i = 0; i < max; i++) {
        int counter = i;

        // If current subset has consecutive
        // elements from the array
        if (counter & (counter >> 1))
            continue;
        result++;
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << cntSubsets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count
// of possible subsets
static int cntSubsets(int[] arr, int n)
{

    // Total possible subsets of n
    // sized array is (2^n - 1)
    int max = (int) Math.pow(2, n);

    // To store the required
    // count of subsets
    int result = 0;

    // Run from i 000..0 to 111..1
    for (int i = 0; i < max; i++)
    {
        int counter = i;

        // If current subset has consecutive
        if ((counter & (counter >> 1)) > 0)
            continue;
        result++;
    }
    return result;
}

// Driver code
static public void main (String []arg)
{
    int arr[] = { 3, 5, 7 };
    int n = arr.length;

    System.out.println(cntSubsets(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of possible subsets
def cntSubsets(arr, n):

    # Total possible subsets of n
    # sized array is (2^n - 1)
    max = pow(2, n)

    # To store the required
    # count of subsets
    result = 0

    # Run from i 000..0 to 111..1
    for i in range(max):
        counter = i

        # If current subset has consecutive
        # elements from the array
        if (counter & (counter >> 1)):
            continue
        result += 1

    return result

# Driver code
arr = [3, 5, 7]
n = len(arr)

print(cntSubsets(arr, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of possible subsets
static int cntSubsets(int[] arr, int n)
{

    // Total possible subsets of n
    // sized array is (2^n - 1)
    int max = (int) Math.Pow(2, n);

    // To store the required
    // count of subsets
    int result = 0;

    // Run from i 000..0 to 111..1
    for (int i = 0; i < max; i++)
    {
        int counter = i;

        // If current subset has consecutive
        if ((counter & (counter >> 1)) > 0)
            continue;
        result++;
    }
    return result;
}

// Driver code
static public void Main (String []arg)
{
    int []arr = { 3, 5, 7 };
    int n = arr.Length;

    Console.WriteLine(cntSubsets(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of possible subsets
function cntSubsets(arr, n)
{

    // Total possible subsets of n
    // sized array is (2^n - 1)
    var max = Math.pow(2, n);

    // To store the required
    // count of subsets
    var result = 0;

    // Run from i 000..0 to 111..1
    for (var i = 0; i < max; i++) {
        var counter = i;

        // If current subset has consecutive
        // elements from the array
        if (counter & (counter >> 1))
            continue;
        result++;
    }
    return result;
}

// Driver code
var arr = [3, 5, 7];
var n = arr.length;
document.write( cntSubsets(arr, n));

</script>
```

**Output:** 

```
5
```

**方法 2:** 上述方法需要指数时间。在上面的代码中，需要没有连续 1 的位掩码的数量。这个计数可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)在线性时间内获得，如在[这篇](https://www.geeksforgeeks.org/count-number-binary-strings-without-consecutive-1s/)文章中所讨论的。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function to return the count
// of possible subsets
int cntSubsets(int* arr, int n)
{
    int a[n], b[n];

    a[0] = b[0] = 1;

    for (int i = 1; i < n; i++) {

        // If previous element was 0 then 0
        // as well as 1 can be appended
        a[i] = a[i - 1] + b[i - 1];

        // If previous element was 1 then
        // only 0 can be appended
        b[i] = a[i - 1];
    }

    // Store the count of all possible subsets
    int result = a[n - 1] + b[n - 1];

    return result;
}

// Driver code
int main()
{
    int arr[] = { 3, 5, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << cntSubsets(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the count
// of possible subsets
static int cntSubsets(int []arr, int n)
{
    int []a = new int[n];
    int []b = new int[n];

    a[0] = b[0] = 1;

    for (int i = 1; i < n; i++)
    {

        // If previous element was 0 then 0
        // as well as 1 can be appended
        a[i] = a[i - 1] + b[i - 1];

        // If previous element was 1 then
        // only 0 can be appended
        b[i] = a[i - 1];
    }

    // Store the count of all possible subsets
    int result = a[n - 1] + b[n - 1];

    return result;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 3, 5, 7 };
    int n = arr.length;

    System.out.println(cntSubsets(arr, n));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of possible subsets
def cntSubsets(arr, n) :

    a = [0] * n
    b = [0] * n;

    a[0] = b[0] = 1;

    for i in range(1, n) :

        # If previous element was 0 then 0
        # as well as 1 can be appended
        a[i] = a[i - 1] + b[i - 1];

        # If previous element was 1 then
        # only 0 can be appended
        b[i] = a[i - 1];

    # Store the count of all possible subsets
    result = a[n - 1] + b[n - 1];

    return result;

# Driver code
if __name__ == "__main__" :

    arr = [ 3, 5, 7 ];
    n = len(arr);

    print(cntSubsets(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of possible subsets
static int cntSubsets(int []arr, int n)
{
    int []a = new int[n];
    int []b = new int[n];

    a[0] = b[0] = 1;

    for (int i = 1; i < n; i++)
    {

        // If previous element was 0 then 0
        // as well as 1 can be appended
        a[i] = a[i - 1] + b[i - 1];

        // If previous element was 1 then
        // only 0 can be appended
        b[i] = a[i - 1];
    }

    // Store the count of all possible subsets
    int result = a[n - 1] + b[n - 1];

    return result;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 5, 7 };
    int n = arr.Length;

    Console.WriteLine(cntSubsets(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of possible subsets
function cntSubsets(arr, n)
{
    var a = Array(n);
    var b = Array(n);

    a[0] = b[0] = 1;

    for (var i = 1; i < n; i++) {

        // If previous element was 0 then 0
        // as well as 1 can be appended
        a[i] = a[i - 1] + b[i - 1];

        // If previous element was 1 then
        // only 0 can be appended
        b[i] = a[i - 1];
    }

    // Store the count of all possible subsets
    var result = a[n - 1] + b[n - 1];

    return result;
}

// Driver code
var arr = [3, 5, 7 ];
var n = arr.length;
document.write( cntSubsets(arr, n));

</script>
```

**Output:** 

```
5
```

**方法 3；**如果仔细看图案，可以观察到计数实际上是 **(N + 2) <sup>th</sup>** [斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)为 **N ≥ 1** 。

> n = 1，计数= 2 = fib(3)
> n = 2，计数= 3 = fib(4)
> n = 3，计数= 5 = fib(5)
> n = 4，计数= 8 = fib(6)
> n = 5，计数= 13 = fib(7)
> ………。

因此，可以使用[这篇](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)文章的方法 5 在 **O(log n)** 时间内对子集进行计数。