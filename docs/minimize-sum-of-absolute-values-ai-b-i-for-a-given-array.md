# 最小化给定数组的 A[I]–( b+ I)的绝对值之和

> 原文:[https://www . geeksforgeeks . org/给定数组的最小化绝对值之和-ai-B- I/](https://www.geeksforgeeks.org/minimize-sum-of-absolute-values-ai-b-i-for-a-given-array/)

给定一个大小为 N 的 [**数组**](https://www.geeksforgeeks.org/array-data-structure/)**【arr】**，的任务是找到表达式**ABS(arr[1]–(b+1))+ABS(arr[2]–(b+2))的最小**可能值**。。。ABS(arr[N]–(b+ N))**，其中 **b** 为独立整数。

> **输入:** arr[ ] = { 2，2，3，5，5 }
> **输出:** 2
> **说明:**考虑 b = 0:表达式的值为 ABS(2 –( 0+1))+ABS(2–(0+2))+ABS(3–(0+3))+ABS(5–(0+4))+ABS(5–(0+5))= 1+0+1+0 = 2
> 因此，的最小可能值为
> 
> **输入:** arr[ ] = { 6，5，4，3，2，1 }
> T3】输出: 18

**方法:**考虑到**B[I]= A[I]I，**问题是减少到**最小化 ABS(B[I]B)的总和。**可以观察到，最好将 **b** 作为修改数组 **B[]的[中值](https://www.geeksforgeeks.org/median-of-two-sorted-arrays-of-different-sizes/)。**所以，排序数组 **B[]，**后，问题可以按照下面给出的步骤**解决。**

*   遍历数组**arr【】**并通过它们的**索引(i + 1)** 减少**每个元素**。
*   [按升序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   现在选择 **b** 作为**arr【】**的中位数，说 **b = arr[N/2]** 。
*   初始化一个变量，说 **ans** 为 **0，**存储表达式的最小可能值。
*   再次遍历数组并将**和**更新为**ABS(arr[I]–b)。**
*   返回**和**的值。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum
// possible sum of all (arr[i] - b + i)
int MinSum(int arr[], int N)
{

    // Modify the array
    for (int i = 0; i < N; i++) {
        arr[i] = arr[i] - (i + 1);
    }

    // Sort the array
    sort(arr, arr + N);

    // Calculate median
    int b = arr[N / 2];

    // Stores the required answer
    int ans = 0;
    for (int i = 0; i < N; i++) {

        // Update answer
        ans += abs(arr[i] - b);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { 2, 2, 3, 5, 5 };
    int N = sizeof(arr) / sizeof(int);

    // Function Call
    int ans = MinSum(arr, N);

    cout << ans << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
// Function to calculate minimum
// possible sum of all (arr[i] - b + i)
import java.util.*;
class GFG{

static int MinSum(int arr[], int N)
{

    // Modify the array
    for (int i = 0; i < N; i++) {
        arr[i] = arr[i] - (i + 1);
    }

    // Sort the array
    Arrays.sort(arr);

    // Calculate median
    int b = arr[N / 2];

    // Stores the required answer
    int ans = 0;
    for (int i = 0; i < N; i++) {

        // Update answer
        ans += Math.abs(arr[i] - b);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given Input
    int arr[] = { 2, 2, 3, 5, 5 };
    int N = arr.length;

    // Function Call
    int ans = MinSum(arr, N);

    System.out.print(ans);

}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Java program for above approach
# Function to calculate minimum
# possible sum of all (arr[i] - b + i)
def MinSum(arr, N):

  # Modify the array
    for i in range(N):
        arr[i] -= (i+1)

    # sort the array   
    arr.sort()

    # calculate median
    b = arr[N//2]

     # Stores the required answer
    ans = 0
    for i in range(N):

      # Update answer
        ans += abs(arr[i]-b)

        # Return the answer
    return ans

# Driver code
arr = [2, 2, 3, 5, 5]
N = len(arr)
print(MinSum(arr, N))

# This code is contributed by Parth Manchanda
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to calculate minimum
// possible sum of all (arr[i] - b + i)
static int MinSum(int []arr, int N)
{

    // Modify the array
    for(int i = 0; i < N; i++)
    {
        arr[i] = arr[i] - (i + 1);
    }

    // Sort the array
    Array.Sort(arr);

    // Calculate median
    int b = arr[N / 2];

    // Stores the required answer
    int ans = 0;
    for(int i = 0; i < N; i++)
    {

        // Update answer
        ans += Math.Abs(arr[i] - b);
    }

    // Return the answer
    return ans;
}

// Driver Code
static void Main()
{

    // Given Input
    int []arr = { 2, 2, 3, 5, 5 };
    int N = arr.Length;

    // Function Call
    int ans = MinSum(arr, N);

    Console.Write(ans);
}
}

// This code is contributed by SoumikMondal
```

## java 描述语言

```
<script>
        // JavaScript Program for the above approach

        // Function to calculate minimum
        // possible sum of all (arr[i] - b + i)
        function MinSum(arr, N) {

            // Modify the array
            for (let i = 0; i < N; i++) {
                arr[i] = arr[i] - (i + 1);
            }

            // Sort the array
            arr.sort(function (a, b) { return a - b });

            // Calculate median
            let b = arr[Math.floor(N / 2)];

            // Stores the required answer
            let ans = 0;
            for (let i = 0; i < N; i++) {

                // Update answer
                ans += Math.abs(arr[i] - b);
            }

            // Return the answer
            return ans;
        }

        // Driver Code

        // Given Input
        let arr = [2, 2, 3, 5, 5];
        let N = arr.length;

        // Function Call
        let ans = MinSum(arr, N);

        document.write(ans + "<br>");

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*logN)*
***辅助空间:** O(1)*