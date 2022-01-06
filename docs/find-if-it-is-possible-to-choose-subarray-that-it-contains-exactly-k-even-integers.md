# 查找是否有可能选择恰好包含 K 个偶数的子阵

> 原文:[https://www . geeksforgeeks . org/find-如果有可能的话-选择-它-包含-精确-k-偶数整数的子数组/](https://www.geeksforgeeks.org/find-if-it-is-possible-to-choose-subarray-that-it-contains-exactly-k-even-integers/)

给定 2 个正整数 **N** 和 **K** 以及一个数组**arr【】**，任务是找出是否有可能选择数组的一个非空子数组，使得该子数组恰好包含 **K** 个偶数。
**举例:**

> **输入:** N = 4，K = 2，arr[] = {1，2，4，5}
> **输出:**是
> **说明:**
> 我们可以选择恰好包含 K = 2 个偶数的子阵列{2，4}。
> **输入:** N = 3，K = 3，arr[] = {2，4，5}
> **输出:**否
> **说明:**
> 只有两个偶数。因此，我们不能选择 K = 3 偶数的子阵。

**方法:**思路是统计数组中偶数的个数。现在可以有 3 种情况:

*   如果数组中偶数的计数为 **0** (即数组中只有奇数)，那么我们就不能选择任何子数组
*   如果数组中偶数的个数是 **≥ K** ，那么我们就可以很容易地选择出一个正好是 K 个偶数的子数组
*   否则就不可能选择一个正好是 K 个偶数的子阵列

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to check if it is possible to
// choose a subarray that contains exactly
// K even integers
#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// choose a subarray that contains exactly
// K even integers
void isPossible(int A[], int n, int k)
{
    // Variable to store the count of
    // even numbers
    int countOfTwo = 0;
    for (int i = 0; i < n; i++) {
        if (A[i] % 2 == 0) {
            countOfTwo++;
        }
    }

    // If we have to select 0 even numbers
    // but there is all odd numbers in the array
    if (k == 0 && countOfTwo == n)
        cout << "NO\n";

    // If the count of even numbers is greater than
    // or equal to K then we can select a
    // subarray with exactly K even integers
    else if (countOfTwo >= k) {
        cout << "Yes\n";
    }

    // If the count of even numbers is less than K
    // then we cannot select any subarray with
    // exactly K even integers
    else
        cout << "No\n";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 4, 5 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    isPossible(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if it is possible to
// choose a subarray that contains exactly
// K even integers
import java.util.*;

class GFG{
// Function to check if it is possible to
// choose a subarray that contains exactly
// K even integers
static void isPossible(int []A, int n, int k)
{
    // Variable to store the count of
    // even numbers
    int countOfTwo = 0;
    for (int i = 0; i < n; i++) {
        if (A[i] % 2 == 0) {
            countOfTwo++;
        }
    }

    // If we have to select 0 even numbers
    // but there is all odd numbers in the array
    if (k == 0 && countOfTwo == n)
        System.out.print("NO");

    // If the count of even numbers is greater than
    // or equal to K then we can select a
    // subarray with exactly K even integers
    else if (countOfTwo >= k) {
        System.out.print("YES");
    }

    // If the count of even numbers is less than K
    // then we cannot select any subarray with
    // exactly K even integers
    else
        System.out.print("No");
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 1, 2, 4, 5 };
    int K = 2;
    int n = arr.length;

    isPossible(arr, n, K);
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program to check if it is possible to
# choose a subarray that contains exactly
# K even integers

# Function to check if it is possible to
# choose a subarray that contains exactly
# K even integers
def isPossible(A, n, k):

    # Variable to store the count of
    # even numbers
    countOfTwo = 0
    for i in range(n):
        if (A[i] % 2 == 0):
            countOfTwo += 1

    # If we have to select 0 even numbers
    # but there is all odd numbers in the array
    if (k == 0 and countOfTwo == n):
        print("NO\n")

    # If the count of even numbers is greater than
    # or equal to K then we can select a
    # subarray with exactly K even integers
    elif (countOfTwo >= k):
        print("Yes\n")

    # If the count of even numbers is less than K
    # then we cannot select any subarray with
    # exactly K even integers
    else:
        print("No\n")

# Driver code
if __name__ == '__main__':
    arr=[1, 2, 4, 5]
    K = 2
    N = len(arr)

    isPossible(arr, N, K)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to check if it is possible to
// choose a subarray that contains exactly
// K even integers
using System;

class GFG{

// Function to check if it is possible to
// choose a subarray that contains exactly
// K even integers
static void isPossible(int []A, int n, int k)
{
    // Variable to store the count of
    // even numbers
    int countOfTwo = 0;
    for (int i = 0; i < n; i++) {
        if (A[i] % 2 == 0) {
            countOfTwo++;
        }
    }

    // If we have to select 0 even numbers
    // but there is all odd numbers in the array
    if (k == 0 && countOfTwo == n)
        Console.Write("NO");

    // If the count of even numbers is greater than
    // or equal to K then we can select a
    // subarray with exactly K even integers
    else if (countOfTwo >= k) {
        Console.Write("Yes");
    }

    // If the count of even numbers is less than K
    // then we cannot select any subarray with
    // exactly K even integers
    else
        Console.Write("No");
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 4, 5 };
    int K = 2;
    int n = arr.Length;

    isPossible(arr, n, K);
}
}

// This code is contributed by AbhiThakur
```

## java 描述语言

```
<script>

// JavaScript program to check if it is possible to
// choose a subarray that contains exactly
// K even integers

// Function to check if it is possible to
// choose a subarray that contains exactly
// K even integers
function isPossible(A, n, k)
{
    // Variable to store the count of
    // even numbers
    var countOfTwo = 0;
    for (var i = 0; i < n; i++) {
        if (A[i] % 2 == 0) {
            countOfTwo++;
        }
    }

    // If we have to select 0 even numbers
    // but there is all odd numbers in the array
    if (k == 0 && countOfTwo == n)
        document.write("NO");

    // If the count of even numbers is greater than
    // or equal to K then we can select a
    // subarray with exactly K even integers
    else if (countOfTwo >= k) {
        document.write("Yes");
    }

    // If the count of even numbers is less than K
    // then we cannot select any subarray with
    // exactly K even integers
    else
        document.write("NO");
}

// Driver code
var arr = [ 1, 2, 4, 5 ];
var K = 2;
var N = arr.length;
isPossible(arr, N, K);

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(1)