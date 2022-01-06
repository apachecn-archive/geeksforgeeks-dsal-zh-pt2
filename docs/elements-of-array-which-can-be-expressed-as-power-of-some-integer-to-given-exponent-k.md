# 可以表示为给定指数 K 的某个整数的幂的数组元素

> 原文:[https://www . geeksforgeeks . org/数组元素可以表示为给定指数 k 的整数次方/](https://www.geeksforgeeks.org/elements-of-array-which-can-be-expressed-as-power-of-some-integer-to-given-exponent-k/)

给定一个大小为 **N** 的数组**arr【】**和一个整数 **K** ，任务是打印数组的所有元素，这些元素可以表示为某个整数(X)与指数 K 的幂，即 **X <sup>K</sup>** 。
**举例:**

> **输入:** arr[] = {46656，64，256，729，16，1000}，K = 6
> **输出:** 46656 64 729
> **解释:**
> 只有数字 46656，64，729 可以表示为 6 的幂。
> 46656 = 6 <sup>6</sup> ，
> 64 = 2 <sup>6</sup> ，
> 729 = 3 <sup>6</sup>
> **输入:** arr[] = {23，81，256，125，16，1000}，K = 4
> **输出:** 81 256 16
> **解释**

**方法:**解决上述问题的主要思想是，对于数组中的每个数字，找到一个数字的[第 N 个根](https://www.geeksforgeeks.org/n-th-root-number/)。然后检查这个数字是否是整数。如果是，那么打印出来，否则跳到下一个数字。
以下是上述方法的实施:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to print elements of
// the Array which can be expressed as
// power of some integer to given exponent K

#include <bits/stdc++.h>
using namespace std;
#define ll long long

// Method returns Nth power of A
double nthRoot(ll A, ll N)
{

    double xPre = 7;

    // Smaller eps, denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by INT_MAX
    double delX = INT_MAX;

    // x^K denotes current value of x
    double xK;

    // loop untill we reach desired accuracy
    while (delX > eps) {

        // calculating current value from previous
        // value by newton's method
        xK = ((N - 1.0) * xPre
              + (double)A / pow(xPre, N - 1))
             / (double)N;

        delX = abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

// Function to check
// whether its k root
// is an integer or not
bool check(ll no, int k)
{
    double kth_root = nthRoot(no, k);
    ll num = kth_root;

    if (abs(num - kth_root) < 1e-4)
        return true;

    return false;
}

// Function to find the numbers
void printExpo(ll arr[], int n, int k)
{
    for (int i = 0; i < n; i++) {
        if (check(arr[i], k))
            cout << arr[i] << " ";
    }
}

// Driver code
int main()
{

    int K = 6;

    ll arr[] = { 46656, 64, 256,
                 729, 16, 1000 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printExpo(arr, n, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to print elements of
// the Array which can be expressed as
// power of some integer to given exponent K

class GFG{

// Method returns Nth power of A
static double nthRoot(long A, long N)
{

    double xPre = 7;

    // Smaller eps, denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by Integer.MAX_VALUE
    double delX = Integer.MAX_VALUE;

    // x^K denotes current value of x
    double xK = 0;

    // loop untill we reach desired accuracy
    while (delX > eps) {

        // calculating current value from previous
        // value by newton's method
        xK = ((N - 1.0) * xPre
              + (double)A / Math.pow(xPre, N - 1))
             / (double)N;

        delX = Math.abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

// Function to check
// whether its k root
// is an integer or not
static boolean check(long no, int k)
{
    double kth_root = nthRoot(no, k);
    long num = (long) kth_root;

    if (Math.abs(num - kth_root) < 1e-4)
        return true;

    return false;
}

// Function to find the numbers
static void printExpo(long arr[], int n, int k)
{
    for (int i = 0; i < n; i++) {
        if (check(arr[i], k))
            System.out.print(arr[i]+ " ");
    }
}

// Driver code
public static void main(String[] args)
{

    int K = 6;

    long arr[] = { 46656, 64, 256,
                 729, 16, 1000 };
    int n = arr.length;

    printExpo(arr, n, K);

}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to prelements of
# the Array which can be expressed as
# power of some integer to given exponent K

# Method returns Nth power of A
def nthRoot(A, N):

    xPre = 7

    # Smaller eps, denotes more accuracy
    eps = 1e-3

    # Initializing difference between two
    # roots by INT_MAX
    delX = 10**9

    # x^K denotes current value of x
    xK = 0

    # loop untiwe reach desired accuracy
    while (delX > eps):

        # calculating current value from previous
        # value by newton's method
        xK = ((N - 1.0) * xPre+ A /pow(xPre, N - 1))/ N

        delX = abs(xK - xPre)
        xPre = xK

    return xK

# Function to check
# whether its k root
# is an integer or not
def check(no, k):
    kth_root = nthRoot(no, k)
    num = int(kth_root)

    if (abs(num - kth_root) < 1e-4):
        return True

    return False

# Function to find the numbers
def printExpo(arr, n, k):
    for i in range(n):
        if (check(arr[i], k)):
            print(arr[i],end=" ")

# Driver code
if __name__ == '__main__':

    K = 6

    arr = [46656, 64, 256,729, 16, 1000]
    n = len(arr)

    printExpo(arr, n, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to print elements of
// the Array which can be expressed as
// power of some integer to given exponent K
using System;

class GFG{

// Method returns Nth power of A
static double nthRoot(long A, long N)
{

    double xPre = 7;

    // Smaller eps, denotes more accuracy
    double eps = 1e-3;

    // Initializing difference between two
    // roots by int.MaxValue
    double delX = int.MaxValue;

    // x^K denotes current value of x
    double xK = 0;

    // loop untill we reach desired accuracy
    while (delX > eps) {

        // calculating current value from previous
        // value by newton's method
        xK = ((N - 1.0) * xPre
              + (double)A / Math.Pow(xPre, N - 1))
             / (double)N;

        delX = Math.Abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

// Function to check
// whether its k root
// is an integer or not
static bool check(long no, int k)
{
    double kth_root = nthRoot(no, k);
    long num = (long) kth_root;

    if (Math.Abs(num - kth_root) < 1e-4)
        return true;

    return false;
}

// Function to find the numbers
static void printExpo(long []arr, int n, int k)
{
    for (int i = 0; i < n; i++) {
        if (check(arr[i], k))
            Console.Write(arr[i]+ " ");
    }
}

// Driver code
public static void Main(String[] args)
{

    int K = 6;

    long []arr = { 46656, 64, 256,
                 729, 16, 1000 };
    int n = arr.Length;

    printExpo(arr, n, K);

}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript implementation to print elements of
// the Array which can be expressed as
// power of some integer to given exponent K

// Method returns Nth power of A
function nthRoot(A,N)
{
    let xPre = 7;

    // Smaller eps, denotes more accuracy
    let eps = 1e-3;

    // Initializing difference between two
    // roots by Integer.MAX_VALUE
    let delX = Number.MAX_VALUE;

    // x^K denotes current value of x
    let xK = 0;

    // loop untill we reach desired accuracy
    while (delX > eps) {

        // calculating current value from previous
        // value by newton's method
        xK = ((N - 1.0) * xPre
              + A / Math.pow(xPre, N - 1))
             / N;

        delX = Math.abs(xK - xPre);
        xPre = xK;
    }

    return xK;
}

// Function to check
// whether its k root
// is an integer or not
function check(no,k)
{
    let kth_root = nthRoot(no, k);
    let num =  Math.floor(kth_root);

    if (Math.abs(num - kth_root) < 1e-4)
        return true;

    return false;
}

// Function to find the numbers
function printExpo(arr,n,k)
{
    for (let i = 0; i < n; i++) {
        if (check(arr[i], k))
            document.write(arr[i]+ " ");
    }
}

// Driver code
let K = 6;
let arr=[46656, 64, 256,
                 729, 16, 1000];
let n = arr.length;
 printExpo(arr, n, K);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
46656 64 729
```