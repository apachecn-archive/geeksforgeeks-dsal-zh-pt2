# X 的最大值，使得任何数组元素与 X 之间的差值不超过 K

> 原文:[https://www . geeksforgeeks . org/x 的最大值，这样任何数组元素和 x 之间的差值都不会超过-k/](https://www.geeksforgeeks.org/maximum-value-of-x-such-that-difference-between-any-array-element-and-x-does-not-exceed-k/)

给定一个由 **N** 个正整数和一个正整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】】**，任务是找出最大可能整数 **X** ，使得任意数组元素与 **X** 的绝对差最多为**K**。如果 **X** 没有这样的值，则打印**-1”**。

**示例:**

> **输入:** arr[] = {6，4，8，5}，K = 2
> **输出:** 6
> **说明:**考虑 **X** 为 **6** ，每个数组元素与 X(= 6)的绝对差最多为**K**(=**2**，如下图:
> 
> *   arr[0](= 6)和 X(= 6)= | 6–6 | = 0 之间的绝对差值。
> *   arr[1](= 4)和 X(= 6)= | 4–6 | = 2 之间的绝对差值。
> *   arr[2](= 8)和 X(= 6)= | 8–6 | = 2 之间的绝对差值。
> *   arr[3](= 5)和 X(= 6)= | 5–6 | = 1 之间的绝对差值。
> 
> **输入:** arr[] = {1，2，5}，K = 2
> T3】输出: 3

**方法:**给定的问题可以基于以下观察来解决:

*   考虑到数组元素为 **arr[i]** ，**| arr[I]–X |**的值最多为**。**
*   **如果 **arr[i] > X** ，那么**X≤(arr[I]–K)**。否则， **X ≤ (arr[i] + K)** 。**
*   **从以上两个方程可知， **X** 的最大值必须是**arr【I】**和 **K** 的最小值之和。**

**按照以下步骤解决问题:**

*   **在一个变量中找到给定数组 **arr[]** 的最小元素，比如 **S** 。**
*   **将 **X** 的最大值视为 **(S + K)** 。**
*   **[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，如果**arr[I]****X**的绝对值差为 **K** ，则更新 **X** 为**-1**[跳出循环](https://www.geeksforgeeks.org/break-statement-cc/)。否则，[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。**
*   **完成以上步骤后，打印 **X** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum value
// of X such that |A[i] - X| ≤ K
int maximumNumber(int arr[], int N,
                  int K)
{
    // Stores the smallest array element
    int minimum = *min_element(arr,
                               arr + N);

    // Store the possible value of X
    int ans = minimum + K;

    // Traverse the array A[]
    for (int i = 0; i < N; i++) {

        // If required criteria is not satisfied
        if (abs(arr[i] - ans) > K) {

            // Update ans
            ans = -1;
            break;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 5 };
    int K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);
    maximumNumber(arr, N, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find maximum value
// of X such that |A[i] - X| ≤ K
static void maximumNumber(int arr[], int N,
                          int K)
{

    // Stores the smallest array element
    int minimum =  Arrays.stream(arr).min().getAsInt();

    // Store the possible value of X
    int ans = minimum + K;

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {

        // If required criteria is not satisfied
        if (Math.abs(arr[i] - ans) > K)
        {

            // Update ans
            ans = -1;
            break;
        }
    }

    // Print the result
    System.out.print(ans);
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 1, 2, 5 };
    int K = 2;
    int N = arr.length;

    maximumNumber(arr, N, K);
}
}

// This code is contributed by sanjoy_62
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find maximum value
# of X such that |A[i] - X| ≤ K
def maximumNumber(arr, N, K):

    # Stores the smallest array element
    minimum = min(arr)

    # Store the possible value of X
    ans = minimum + K

    # Traverse the array A[]
    for i in range(N):

        # If required criteria is not satisfied
        if (abs(arr[i] - ans) > K):

            # Update ans
            ans = -1
            break

    # Print the result
    print(ans)

# Driver Code
if __name__ == '__main__':

    arr =  [1, 2, 5]
    K = 2
    N = len(arr)

    maximumNumber(arr, N, K)

# This code is contributed by SURENDRA_GANGWAR
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find maximum value
// of X such that |A[i] - X| ≤ K
static void maximumNumber(int []arr, int N,
                          int K)
{

    // Stores the smallest array element
    int mn = 100000000;
    for(int i = 0; i < N; i++)
    {
        if (arr[i] < mn)
          mn = arr[i];
    }

    // Store the possible value of X
    int ans = mn + K;

    // Traverse the array A[]
    for(int i = 0; i < N; i++)
    {

        // If required criteria is not satisfied
        if (Math.Abs(arr[i] - ans) > K)
        {

            // Update ans
            ans = -1;
            break;
        }
    }

    // Print the result
    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 2, 5 };
    int K = 2;
    int N = arr.Length;

    maximumNumber(arr, N, K);
}
}

// This code is contributed by ipg2016107
```

## **java 描述语言**

```
<script>

        // Javascript program for
        // the above approach

        // Function to find maximum value
        // of X such that |A[i] - X| ≤ K
        function maximumNumber(arr, N, K)
        {
            // Stores the smallest
            // array element
            let minimum = Math.min(...arr)

            // Store the possible value of X
            let ans = minimum + K;

            // Traverse the array A[]
            for (let i = 0; i < N; i++) {

                // If required criteria is
                // not satisfied
                if (Math.abs(arr[i] - ans) > K)
                {

                    // Update ans
                    ans = -1;
                    break;
                }
            }

            // Print the result
            document.write(ans)
        }

        // Driver Code
        let arr = [1, 2, 5]
        let K = 2
        let N = arr.length
        maximumNumber(arr, N, K);

        // This code is contributed by Hritik

    </script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**