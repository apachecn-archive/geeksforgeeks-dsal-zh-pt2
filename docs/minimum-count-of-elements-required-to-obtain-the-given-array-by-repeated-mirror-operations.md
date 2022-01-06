# 通过重复镜像操作获得给定阵列所需的最小元素数

> 原文:[https://www . geesforgeks . org/通过重复镜像操作获取给定数组所需的最小元素数/](https://www.geeksforgeeks.org/minimum-count-of-elements-required-to-obtain-the-given-array-by-repeated-mirror-operations/)

给定由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到最小可能长度的数组 **K[]** ，以便在对 **K[]** 执行多次镜像操作后，可以获得给定的数组 **arr[]** 。

> **镜像操作:**将所有数组元素以相反的顺序追加到原始数组中。
> **图解:**
> arr[] = {1，2，3}
> 在 1 <sup>st</sup> 镜像操作后，arr[]修改为{1，2，3，3，2，1}
> 在 2 <sup>nd</sup> 镜像操作后，arr[]修改为{1，2，3，3，2，1，1，2，3，3，2，1}

**例:**

> **输入:** N = 6，arr[] = { 1，2，3，3，2，1 }
> **输出:** 3
> **解释:**
> 子阵{ 1，2，3}和{3，2，1 }是彼此的镜像。
> 对{1，2，3}的单镜像操作获得给定的数组。
> 因此，所需元素的最小数量为 3。
> **输入:** N = 8，arr[] = {1，2，2，1，1，2，2，1}
> **输出:** 2
> **说明:**
> 子阵{ 1，2，2，1 }和{ 1，2，2，1 }是彼此的镜像。
> 斯巴莱{1，2}和{2，1}是彼此的镜像。
> {1，2} - > {1，2，2，1} - > {1，2，2，1，1，2，2，1}
> 因此，所需元素的最小数量为 2。

**天真方法:**
解决问题最简单的方法是[从给定的小于或等于 **N/2** 的阵列中生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，并且对于每个子阵列，检查执行镜像操作是否给出阵列**arr【】**。打印满足条件的最小长度子阵列。如果没有找到满意的子阵列，打印**否**。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*
**高效途径:**
以上途径可以利用[分治](https://www.geeksforgeeks.org/divide-and-conquer-algorithm-introduction/)手法进一步优化。按照以下步骤解决问题:

*   初始化一个变量 **K** **=** **N** ，然后检查长度 **K** 的 **A[]** 的前缀是否为回文。
*   如果长度为 **K** 的前缀是回文，则用 **2** 除 **K** ，进行上述检查。
*   如果前缀不是回文，那么答案就是 **K** 的当前值。
*   在 **K > 0** 时继续检查，直到 **K** 为奇数。
*   如果 **K** 为**奇数**，则打印 **K** 的当前值。

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number
// of elements required to form A[]
// by performing mirroring operation
int minimumrequired(int A[], int N)
{
    // Initialize K
    int K = N;

    int ans;

    while (K > 0) {

        // Odd length array
        // cannot be formed by
        // mirror operation
        if (K % 2 == 1) {
            ans = K;
            break;
        }

        bool ispalindrome = 1;

        // Check if prefix of
        // length K is palindrome
        for (int i = 0; i < K / 2; i++) {

            // Check if not a palindrome
            if (A[i] != A[K - 1 - i])

                ispalindrome = 0;
        }

        // If found to be palindrome
        if (ispalindrome) {
            ans = K / 2;
            K /= 2;
        }

        // Otherwise
        else {
            ans = K;
            break;
        }
    }

    // Return the final answer
    return ans;
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 2, 1, 1, 2, 2, 1 };
    int N = sizeof a / sizeof a[0];

    cout << minimumrequired(a, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG{

// Function to find minimum number
// of elements required to form A[]
// by performing mirroring operation
static int minimumrequired(int A[], int N)
{
    // Initialize K
    int K = N;

    int ans=0;

    while (K > 0)
    {

        // Odd length array
        // cannot be formed by
        // mirror operation
        if (K % 2 == 1)
        {
            ans = K;
            break;
        }

        int ispalindrome = 1;

        // Check if prefix of
        // length K is palindrome
        for (int i = 0; i < K / 2; i++)
        {

            // Check if not a palindrome
            if (A[i] != A[K - 1 - i])

                ispalindrome = 0;
        }

        // If found to be palindrome
        if (ispalindrome == 1)
        {
            ans = K / 2;
            K /= 2;
        }

        // Otherwise
        else
        {
            ans = K;
            break;
        }
    }

    // Return the final answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 2, 2, 1, 1, 2, 2, 1 };
    int N = a.length;

    System.out.println(minimumrequired(a, N));
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find minimum number
# of elements required to form A[]
# by performing mirroring operation
def minimumrequired(A, N):

    # Initialize K
    K = N

    while (K > 0):

        # Odd length array
        # cannot be formed by
        # mirror operation
        if (K % 2) == 1:
            ans = K
            break

        ispalindrome = 1

        # Check if prefix of
        # length K is palindrome
        for i in range(0, K // 2):

            # Check if not a palindrome
            if (A[i] != A[K - 1 - i]):
                ispalindrome = 0

        # If found to be palindrome
        if (ispalindrome == 1):
            ans = K // 2
            K = K // 2

        # Otherwise
        else:
            ans = K
            break

    # Return the final answer
    return ans

# Driver code
A = [ 1, 2, 2, 1, 1, 2, 2, 1 ]
N = len(A)

print(minimumrequired(A, N))

# This code is contributed by VirusBuddah_
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find minimum number
// of elements required to form []A
// by performing mirroring operation
static int minimumrequired(int[] A, int N)
{

    // Initialize K
    int K = N;

    int ans = 0;

    while (K > 0)
    {

        // Odd length array
        // cannot be formed by
        // mirror operation
        if (K % 2 == 1)
        {
            ans = K;
            break;
        }

        int ispalindrome = 1;

        // Check if prefix of
        // length K is palindrome
        for(int i = 0; i < K / 2; i++)
        {

            // Check if not a palindrome
            if (A[i] != A[K - 1 - i])
                ispalindrome = 0;
        }

        // If found to be palindrome
        if (ispalindrome == 1)
        {
            ans = K / 2;
            K /= 2;
        }

        // Otherwise
        else
        {
            ans = K;
            break;
        }
    }

    // Return the readonly answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int[] a = { 1, 2, 2, 1, 1, 2, 2, 1 };
    int N = a.Length;

    Console.WriteLine(minimumrequired(a, N));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
    // Javascript Program to implement
    // the above approach

    // Function to find minimum number
    // of elements required to form A[]
    // by performing mirroring operation
    function minimumrequired(A, N)
    {
        // Initialize K
        let K = N;

        let ans;

        while (K > 0) {

            // Odd length array
            // cannot be formed by
            // mirror operation
            if (K % 2 == 1) {
                ans = K;
                break;
            }

            let ispalindrome = true;

            // Check if prefix of
            // length K is palindrome
            for (let i = 0; i < parseInt(K / 2, 10); i++) {

                // Check if not a palindrome
                if (A[i] != A[K - 1 - i])

                    ispalindrome = false;
            }

            // If found to be palindrome
            if (ispalindrome) {
                ans = parseInt(K / 2, 10);
                K = parseInt(K / 2, 10);
            }

            // Otherwise
            else {
                ans = K;
                break;
            }
        }

        // Return the final answer
        return ans;
    }

    let a = [ 1, 2, 2, 1, 1, 2, 2, 1 ];
    let N = a.length;

    document.write(minimumrequired(a, N));

    // This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*