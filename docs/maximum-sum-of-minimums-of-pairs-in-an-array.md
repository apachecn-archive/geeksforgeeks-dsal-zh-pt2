# 数组中对的最小值的最大和

> 原文:[https://www . geeksforgeeks . org/最大最小阵列对总和/](https://www.geeksforgeeks.org/maximum-sum-of-minimums-of-pairs-in-an-array/)

给定一个由 **N** 整数组成的数组**arr【】**，其中 **N** 为偶数，任务是将数组元素分组成对 **(X1，Y1)，(X2，Y2)，(X3，Y3)，…** ，使得和 **min(X1，Y1) + min(X2，Y2) + min(X3，Y3) + …** 最大。
**举例:**

> **输入:** arr[] = {1，5，3，2}
> **输出:** 4
> (1，5)和(3，2) - > 1 + 2 = 3
> (1，3)和(5，2) - > 1 + 2 = 3
> (1，2)和(5，3) - > 1 + 3 = 4
> **输入:** arr[] = {1，3，2，1，4

**方法:**无论成对是如何形成的，来自数组的最大元素将总是被忽略，因为它将是它被放入的每个对中的最大元素。第二个最大元素也是如此，除非它与最大元素成对出现。因此，为了最大化和，一个最佳的方法是对数组进行排序，并从最大元素开始按顺序配对。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// required sum of the pairs
int maxSum(int a[], int n)
{

    // Sort the array
    sort(a, a + n);

    // To store the sum
    int sum = 0;

    // Start making pairs of every two
    // consecutive elements as n is even
    for (int i = 0; i < n - 1; i += 2) {

        // Minimum element of the current pair
        sum += a[i];
    }

    // Return the maximum possible sum
    return sum;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 1, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxSum(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to return the maximum
// required sum of the pairs
static int maxSum(int a[], int n)
{

    // Sort the array
    Arrays.sort(a);

    // To store the sum
    int sum = 0;

    // Start making pairs of every two
    // consecutive elements as n is even
    for (int i = 0; i < n - 1; i += 2)
    {

        // Minimum element of the current pair
        sum += a[i];
    }

    // Return the maximum possible sum
    return sum;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 2, 1, 4, 5 };
    int n = arr.length;

    System.out.println(maxSum(arr, n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# required sum of the pairs
def maxSum(a, n) :

    # Sort the array
    a.sort();

    # To store the sum
    sum = 0;

    # Start making pairs of every two
    # consecutive elements as n is even
    for i in range(0, n - 1, 2) :

        # Minimum element of the current pair
        sum += a[i];

    # Return the maximum possible sum
    return sum;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 3, 2, 1, 4, 5 ];
    n = len(arr);

    print(maxSum(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum
// required sum of the pairs
static int maxSum(int []a, int n)
{

    // Sort the array
    Array.Sort(a);

    // To store the sum
    int sum = 0;

    // Start making pairs of every two
    // consecutive elements as n is even
    for (int i = 0; i < n - 1; i += 2)
    {

        // Minimum element of the current pair
        sum += a[i];
    }

    // Return the maximum possible sum
    return sum;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 3, 2, 1, 4, 5 };
    int n = arr.Length;

    Console.WriteLine(maxSum(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the maximum
// required sum of the pairs
function maxSum(a, n) {

    // Sort the array
    a.sort((a, b) => a - b);

    // To store the sum
    let sum = 0;

    // Start making pairs of every two
    // consecutive elements as n is even
    for (let i = 0; i < n - 1; i += 2) {

        // Minimum element of the current pair
        sum += a[i];
    }

    // Return the maximum possible sum
    return sum;
}

// Driver code
let arr = [1, 3, 2, 1, 4, 5];
let n = arr.length;

document.write(maxSum(arr, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
7
```