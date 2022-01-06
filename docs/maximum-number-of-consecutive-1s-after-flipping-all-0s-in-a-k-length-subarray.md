# 翻转 K 长度子阵列中所有 0 后连续 1 的最大数量

> 原文:[https://www . geeksforgeeks . org/最大翻转后连续 1 的数量-k 长度中的所有 0-subarray/](https://www.geeksforgeeks.org/maximum-number-of-consecutive-1s-after-flipping-all-0s-in-a-k-length-subarray/)

给定一个长度为 **N** 的二进制数组**arr【】**，以及一个**整数 K** ，任务是在长度为 K 的子数组中翻转所有的 0 后，找到连续 1 的最大数量

**示例:**

> **输入:** arr[]= {0，0，1，1，1，1，0，1，1，0}，K = 2
> **输出:** 7
> **解释:**
> 取子阵【6，7】翻转 0 到 1 我们得到 7 个连续的 1。
> 
> **输入:** arr[]= {0，0，1，1，0，0，0}，K = 3
> **输出:** 5
> **解释:**
> 取子阵【4，6】翻转 0 到 1，我们得到 5 个连续的 1。

**方法:**要解决问题，请按照下面给出的步骤操作:

*   初始化一个变量，比如说 *trav* ，它将在数组中从每个位置 I 到 **(0 到 i-1)** 沿**左**方向迭代，从**沿**右**方向迭代(i+k 到 n-1)** 。
*   检查并保持一个帐户，当在数组中迭代时，任何方向都不会出现零。
*   如果有 0，则从该方向的循环中断开。
*   所以最终对于 **i 到 i+k** 如果有任何 0，我们已经将它翻转为 1，所以不需要计算这个范围内的 1 的数量，因为它将只等于整数 K。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// consecutive 1's after flipping all
// zero in a K length subarray
int findmax(int arr[], int n, int k)
{
    // Initialize variable
    int trav, i;
    int c = 0, maximum = 0;

    // Iterate unil n-k+1 as we
    // have to go till i+k
    for (i = 0; i < n - k + 1; i++) {
        trav = i - 1;
        c = 0;

        /*Iterate in the array in left direction
        till you get 1 else break*/
        while (trav >= 0 && arr[trav] == 1) {
            trav--;
            c++;
        }
        trav = i + k;

        /*Iterate in the array in right direction
        till you get 1 else break*/
        while (trav < n && arr[trav] == 1) {
            trav++;
            c++;
        }
        c += k;

        // Compute the maximum length
        if (c > maximum)
            maximum = c;
    }

    // Return the length
    return maximum;
}

// Driver code
int main()
{
    int k = 3;
    // Array initialization
    int arr[] = { 0, 0, 1, 1, 0, 0, 0, 0 };

    // Size of array
    int n = sizeof arr / sizeof arr[0];
    int ans = findmax(arr, n, k);
    cout << ans << '\n';
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the maximum number of
// consecutive 1's after flipping all
// zero in a K length subarray
static int findmax(int arr[], int n, int k)
{

    // Initialize variable
    int trav, i;
    int c = 0, maximum = 0;

    // Iterate unil n-k+1 as we
    // have to go till i+k
    for(i = 0; i < n - k + 1; i++)
    {
        trav = i - 1;
        c = 0;

        // Iterate in the array in left direction
        // till you get 1 else break
        while (trav >= 0 && arr[trav] == 1)
        {
            trav--;
            c++;
        }
        trav = i + k;

        // Iterate in the array in right direction
        // till you get 1 else break
        while (trav < n && arr[trav] == 1)
        {
            trav++;
            c++;
        }
        c += k;

        // Compute the maximum length
        if (c > maximum)
            maximum = c;
    }

    // Return the length
    return maximum;
}

// Driver code
public static void main(String args[])
{
    int k = 3;

    // Array initialization
    int arr[] = { 0, 0, 1, 1, 0, 0, 0, 0 };

    // Size of array
    int n = arr.length;
    int ans = findmax(arr, n, k);

    System.out.println(ans);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum number of
# consecutive 1's after flipping all
# zero in a K length subarray
def findmax(arr, n, k):

    # Initialize variable
    trav, i = 0, 0
    c = 0
    maximum = 0

    # Iterate unil n-k+1 as we
    # have to go till i+k
    while i < n - k + 1:
        trav = i - 1
        c = 0

        # Iterate in the array in left direction
        # till you get 1 else break
        while trav >= 0 and arr[trav] == 1:
            trav -= 1
            c += 1
        trav = i + k

        # Iterate in the array in right direction
        # till you get 1 else break
        while (trav < n and arr[trav] == 1):
            trav += 1
            c += 1

        c += k

        # Compute the maximum length
        if (c > maximum):
            maximum = c
        i += 1

    # Return the length
    return maximum

# Driver code
if __name__ == '__main__':
    k = 3

    # Array initialization
    arr = [0, 0, 1, 1, 0, 0, 0, 0]

    # Size of array
    n = len(arr)
    ans = findmax(arr, n, k)
    print(ans)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the maximum number of
// consecutive 1's after flipping all
// zero in a K length subarray
static int findmax(int []arr, int n, int k)
{

    // Initialize variable
    int trav, i;
    int c = 0, maximum = 0;

    // Iterate unil n-k+1 as we
    // have to go till i+k
    for(i = 0; i < n - k + 1; i++)
    {
        trav = i - 1;
        c = 0;

        // Iterate in the array in left direction
        // till you get 1 else break
        while (trav >= 0 && arr[trav] == 1)
        {
            trav--;
            c++;
        }
        trav = i + k;

        // Iterate in the array in right direction
        // till you get 1 else break
        while (trav < n && arr[trav] == 1)
        {
            trav++;
            c++;
        }
        c += k;

        // Compute the maximum length
        if (c > maximum)
            maximum = c;
    }

    // Return the length
    return maximum;
}

// Driver code
public static void Main()
{
    int k = 3;

    // Array initialization
    int []arr = { 0, 0, 1, 1, 0, 0, 0, 0 };

    // Size of array
    int n = arr.Length;
    int ans = findmax(arr, n, k);

    Console.WriteLine(ans);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum number of
// consecutive 1's after flipping all
// zero in a K length subarray
function findmax(arr, n, k) {
    // Initialize variable
    let trav, i;
    let c = 0, maximum = 0;

    // Iterate unil n-k+1 as we
    // have to go till i+k
    for (i = 0; i < n - k + 1; i++) {
        trav = i - 1;
        c = 0;

        /*Iterate in the array in left direction
        till you get 1 else break*/
        while (trav >= 0 && arr[trav] == 1) {
            trav--;
            c++;
        }
        trav = i + k;

        /*Iterate in the array in right direction
        till you get 1 else break*/
        while (trav < n && arr[trav] == 1) {
            trav++;
            c++;
        }
        c += k;

        // Compute the maximum length
        if (c > maximum)
            maximum = c;
    }

    // Return the length
    return maximum;
}

// Driver code

let k = 3;
// Array initialization
let arr = [0, 0, 1, 1, 0, 0, 0, 0];

// Size of array
let n = arr.length;
let ans = findmax(arr, n, k);
document.write(ans)

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output**

```
5
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(1)