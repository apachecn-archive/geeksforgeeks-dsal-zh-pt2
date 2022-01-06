# 在排序数组中插入最小元素，形成算术级数

> 原文:[https://www . geesforgeks . org/最小元素插入排序数组形成算术级数/](https://www.geeksforgeeks.org/minimum-elements-inserted-in-a-sorted-array-to-form-an-arithmetic-progression/)

给定一个[排序的](https://www.geeksforgeeks.org/sorting-algorithms/)数组 **arr[]** ，任务是找到需要插入到数组中的最小元素，使得数组形成一个[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)。
**举例:**

> **输入:** arr[] = {1，6，8，10，14，16}
> **输出:** 10
> **解释:**
> 形成 A.P .所需的最小元素为 10。
> 插入元素后的变换数组。
> arr[] = {1， **2** ， **3** ， **4** ， **5** ，6， **7** ，8，
> **9** ，10， **11** ， **12** ， **13** ，14， **15** ，
> 元素插入后的变换数组。
> arr[] = {1，3，5，7， **9** ，11}

**方法:**思路是找出排序后数组连续元素的差，然后找出所有差的[最大公约数](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/)。差异的 GCD 将是可以形成的[等差数列](https://www.geeksforgeeks.org/arithmetic-progression/)的公差。以下是步骤说明:

*   找出数组中连续元素之间的差异并存储在其中 **diff[]** 。
*   现在 **diff[]** 数组的 GCD 将给出给定排序数组的元素之间的公共差。
    **例如:**

```
Given array be {1, 5, 7}
Difference of Consecutive elements will be -
Difference(1, 5) = |5 - 1| = 4
Difference(5, 7) = |7 - 5| = 2

Then, GCD of the Differences will be 
gcd(4, 2) = 2

This means there can be A.P. formed
with common-difference as 2\. That is - 
{1, 3, 5, 7}
```

*   如果排序数组 **arr[]** 的连续元素之间的差值大于上面计算的 GCD，则需要在给定数组中插入的元素的最小数量，以使数组的元素在算术级数中由下式给出:

```
Number of possible elements = 
    (Difference / Common Difference) - 1
```

*   为给定排序数组中的所有连续元素集合添加需要插入的元素计数。

以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum elements required to
// be inserted into an array to
// form an arithmetic progression

#include <bits/stdc++.h>
using namespace std;

// Function to find the greatest
// common divisor of two numbers
int gcdFunc(int a, int b)
{
    if (b == 0)
        return a;
    return gcdFunc(b, a % b);
}

// Function to find the minimum
// the minimum number of elements
// required to be inserted into array
int findMinimumElements(int* a, int n)
{
    int b[n - 1];

    // Difference array of consecutive
    // elements of the array
    for (int i = 1; i < n; i++) {
        b[i - 1] = a[i] - a[i - 1];
    }
    int gcd = b[0];

    // GCD of the difference array
    for (int i = 0; i < n - 1; i++) {
        gcd = gcdFunc(gcd, b[i]);
    }
    int ans = 0;

    // Loop to calculate the minimum
    // number of elements required
    for (int i = 0; i < n - 1; i++) {
        ans += (b[i] / gcd) - 1;
    }
    return ans;
}

// Driver Code
int main()
{
    int arr1[] = { 1, 6, 8, 10, 14, 16 };
    int n1 = sizeof(arr1)/sizeof(arr1[0]);
    // Function calling
    cout << findMinimumElements(arr1, n1)
         << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum elements required to
// be inserted into an array to
// form an arithmetic progression

class GFG{

    // Function to find the greatest
    // common divisor of two numbers
    static int gcdFunc(int a, int b)
    {
        if (b == 0)
            return a;
        return gcdFunc(b, a % b);
    }

    // Function to find the minimum
    // the minimum number of elements
    // required to be inserted into array
    static int findMinimumElements(int[] a, int n)
    {
        int[] b = new int[n - 1];

        // Difference array of consecutive
        // elements of the array
        for (int i = 1; i < n; i++) {
            b[i - 1] = a[i] - a[i - 1];
        }
        int gcd = b[0];

        // GCD of the difference array
        for (int i = 0; i < n - 1; i++) {
            gcd = gcdFunc(gcd, b[i]);
        }
        int ans = 0;

        // Loop to calculate the minimum
        // number of elements required
        for (int i = 0; i < n - 1; i++) {
            ans += (b[i] / gcd) - 1;
        }
        return ans;
    }

 // Driver Code
public static void main(String[] args)
{
    int arr1[] = { 1, 6, 8, 10, 14, 16 };
    int n1 = arr1.length;
    // Function calling
    System.out.print(findMinimumElements(arr1, n1)
         +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum elements required to
# be inserted into an array to
# form an arithmetic progression

# Function to find the greatest
# common divisor of two numbers
def gcdFunc(a, b):
    if (b == 0):
        return a

    return gcdFunc(b, a % b)

# Function to find the minimum
# the minimum number of elements
# required to be inserted into array
def findMinimumElements(a, n):
    b = [0]*(n - 1)

    # Difference array of consecutive
    # elements of the array
    for i in range(1,n):
        b[i - 1] = a[i] - a[i - 1]

    gcd = b[0]

    # GCD of the difference array
    for i in range(n-1):
        gcd = gcdFunc(gcd, b[i])

    ans = 0

    # Loop to calculate the minimum
    # number of elements required
    for i in range(n-1):
        ans += (b[i] // gcd) - 1

    return ans

# Driver Code
arr1 = [1, 6, 8, 10, 14, 16]
n1 = len(arr1)
# Function calling
print(findMinimumElements(arr1, n1))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# implementation to find the
// minimum elements required to
// be inserted into an array to
// form an arithmetic progression
using System;

class GFG{

    // Function to find the greatest
    // common divisor of two numbers
    static int gcdFunc(int a, int b)
    {
        if (b == 0)
            return a;
        return gcdFunc(b, a % b);
    }

    // Function to find the minimum
    // the minimum number of elements
    // required to be inserted into array
    static int findMinimumElements(int[] a, int n)
    {
        int[] b = new int[n - 1];

        // Difference array of consecutive
        // elements of the array
        for (int i = 1; i < n; i++) {
            b[i - 1] = a[i] - a[i - 1];
        }
        int gcd = b[0];

        // GCD of the difference array
        for (int i = 0; i < n - 1; i++) {
            gcd = gcdFunc(gcd, b[i]);
        }
        int ans = 0;

        // Loop to calculate the minimum
        // number of elements required
        for (int i = 0; i < n - 1; i++) {
            ans += (b[i] / gcd) - 1;
        }
        return ans;
    }

    // Driver Code
    static public void Main ()
    {
        int[] arr1 = new int[] { 1, 6, 8, 10, 14, 16 };
        int n1 = arr1.Length;
        // Function calling
        Console.WriteLine(findMinimumElements(arr1, n1));
    }
}

// This code is contributed by shivanisingh
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum elements required to
// be inserted into an array to
// form an arithmetic progression

// Function to find the greatest
// common divisor of two numbers
function gcdFunc(a, b)
{
    if (b == 0)
        return a;
    return gcdFunc(b, a % b);
}

// Function to find the minimum
// the minimum number of elements
// required to be inserted into array
function findMinimumElements(a, n)
{
    let b = new Array(n - 1);

    // Difference array of consecutive
    // elements of the array
    for (let i = 1; i < n; i++) {
        b[i - 1] = a[i] - a[i - 1];
    }
    let gcd = b[0];

    // GCD of the difference array
    for (let i = 0; i < n - 1; i++) {
        gcd = gcdFunc(gcd, b[i]);
    }
    let ans = 0;

    // Loop to calculate the minimum
    // number of elements required
    for (let i = 0; i < n - 1; i++) {
        ans += (b[i] / gcd) - 1;
    }
    return ans;
}

// Driver Code

    let arr1 = [ 1, 6, 8, 10, 14, 16 ];
    let n1 = arr1.length;
    // Function calling
    document.write(findMinimumElements(arr1, n1)
        + "<br>");

// This code is contributed by Mayank Tyagi

</script>
```

**Output:** 

```
10
```

**时间复杂度:** O(N * log(MAX))，其中 N 为数组中的元素个数，MAX 为数组中的最大元素个数。
**辅助空间** : O(N + log(MAX))