# 最小递减，使一个数组最多为 0，这样所有数组元素在一个数减少到 0 后循环递减

> 原文:[https://www . geeksforgeeks . org/最小递减到最多 0 个数组，使得所有数组元素在一个数字被减少到 0 后循环递减/](https://www.geeksforgeeks.org/minimum-decrements-to-make-an-array-at-most-0-such-that-all-array-elements-are-cyclically-decremented-after-a-number-is-reduced-to-0/)

给定一个由 **N 个**整数组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/)**arr【】**和一个[数组](https://www.geeksforgeeks.org/array-data-structure/)**cost【】**，任务是计算使数组所有元素等于 **0** 所需的最小操作数，其中在每次操作时将索引 **i** 的值减 **1** 。如果某个指标的值变为 0，则将**arr【I+1】**的值减**cost【I】**，将**arr【I+2】**的值减**cost【I+1】**以此类推。

**注意:**如果一个元素变得小于 0，则认为是 0。

**示例:**

> **输入:** arr[] = {7，2，5}，成本[] = {8，9，3}
> **输出:** 6
> **说明:**递减可以通过以下方式进行:
> 
> *   将 arr[1]的值递减两次。因此，arr[2]的值将减去成本[1]，arr[0]的值将减去成本[2]。因此，最终的数组将是 arr[] = {4，0，0}。
> *   现在，将 arr[0]，**的值减 4 次**使其为 0。因此，数组变成 arr[] = {0，0，0}。
> 
> 因此，使数组的所有元素等于零所需的操作数是 6，这是最小的可能。
> 
> **输入:** arr[] = {6，7，7，10，8，2}，成本[] = {5，10，1，4，7，7}
> **输出:** 16

**方法:**给定的问题可以使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)通过以下观察来解决:

*   [数组最后剩余的非零元素](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，假设 **x** 将需要 **x** 的减量操作。
*   假设减量操作后 **arr[i]** 的值变为 **0** ，那么对于 **arr[i]** ，所需的减量次数为 **arr[i]** ，对于 **arr[i+1]** ，所需的减量次数将为**arr[I+1]–max(0，arr[I+1]–cost[I])**等等。

以下是要遵循的步骤:

*   使用变量 **i** 在范围**【0，N】**内遍历给定数组 **arr[]** 。
*   使数组的第 i <sup>个</sup>索引等于零所需的操作数是**arr[I]–min(arr[I]，cost[i-1])** 。因此，在变量**和**中保持所有指数的这个值的总和。
*   在**【0，N】**范围内的所有指标上，将**和**的值增加 arr[i]或成本[i]的最小值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum decrements
// required to make all array elements 0
int minDecrements(int arr[], int powr[], int N)
{
    // Variable to store the answer
    int ans = 0;
    int mn = INT_MAX;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        int idx = (i + 1) % N;
        int val = min(arr[idx], powr[i]);

        ans += arr[idx] - val;

        // Store the minimum one
        mn = min(mn, val);
    }
    ans += mn;

    // Return the ans
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 6, 7, 7, 10, 8, 2 };
    int powr[] = { 5, 10, 1, 4, 7, 7 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minDecrements(arr, powr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

public class GFG
{
// Function to find minimum decrements
// required to make all array elements 0
static int minDecrements(int []arr, int []powr, int N)
{
    // Variable to store the answer
    int ans = 0;
    int mn = Integer.MAX_VALUE;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        int idx = (i + 1) % N;
        int val = Math.min(arr[idx], powr[i]);

        ans += arr[idx] - val;

        // Store the minimum one
        mn = Math.min(mn, val);
    }
    ans += mn;

    // Return the ans
    return ans;
}

// Driver Code
public static void main(String args[])
{
    int []arr = { 6, 7, 7, 10, 8, 2 };
    int []powr = { 5, 10, 1, 4, 7, 7 };
    int N = arr.length;

    System.out.println(minDecrements(arr, powr, N));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find minimum decrements
# required to make all array elements 0
def minDecrements(arr, powr, N):

    # Variable to store the answer
    ans = 0
    mn = 99999999

    # Traverse the array
    for i in range(N):
        idx = (i + 1) % N
        val = min(arr[idx], powr[i])

        ans += arr[idx] - val

       # Store the minimum one
        mn = min(mn, val)
    ans += mn

    # Return the ans
    return ans

# Driver Code
if __name__ == "__main__":
    arr = [6, 7, 7, 10, 8, 2]
    powr = [5, 10, 1, 4, 7, 7]
    N = len(arr)
    print(minDecrements(arr, powr, N))

# This code is contributed by Potta Lokesh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG
{
// Function to find minimum decrements
// required to make all array elements 0
static int minDecrements(int []arr, int []powr, int N)
{
    // Variable to store the answer
    int ans = 0;
    int mn = Int32.MaxValue;

    // Traverse the array
    for (int i = 0; i < N; i++) {
        int idx = (i + 1) % N;
        int val = Math.Min(arr[idx], powr[i]);

        ans += arr[idx] - val;

        // Store the minimum one
        mn = Math.Min(mn, val);
    }
    ans += mn;

    // Return the ans
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 6, 7, 7, 10, 8, 2 };
    int []powr = { 5, 10, 1, 4, 7, 7 };
    int N = arr.Length;

    Console.Write(minDecrements(arr, powr, N));
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find minimum decrements
// required to make all array elements 0
function minDecrements(arr, powr, N)
{
    // Variable to store the answer
    let ans = 0;
    let mn = Number.MAX_SAFE_INTEGER

    // Traverse the array
    for (let i = 0; i < N; i++) {
        let idx = (i + 1) % N;
        let val = Math.min(arr[idx], powr[i]);

        ans += arr[idx] - val;

        // Store the minimum one
        mn = Math.min(mn, val);
    }
    ans += mn;

    // Return the ans
    return ans;
}

// Driver Code

let arr = [ 6, 7, 7, 10, 8, 2 ];
let powr = [ 5, 10, 1, 4, 7, 7 ];
let N = arr.length;

document.write(minDecrements(arr, powr, N));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
16
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)