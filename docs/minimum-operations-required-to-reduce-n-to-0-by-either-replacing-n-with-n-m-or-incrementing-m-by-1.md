# 通过用 N/M 替换 N 或用 1 增加 M 将 N 减少到 0 所需的最小操作

> 原文:[https://www . geeksforgeeks . org/minimum-operations-required-to-reduct-n-to-0-or-n-replacement-n-m-by-1/](https://www.geeksforgeeks.org/minimum-operations-required-to-reduce-n-to-0-by-either-replacing-n-with-n-m-or-incrementing-m-by-1/)

给定两个整数 **N** 和 **M** ，任务是使用以下操作计算将 **N** 减少到 **0** 所需的最小操作数:

*   将 **N** 替换为 **(N/M)** 。
*   将 **M** 的值增加 **1** 。

**示例:**

> **输入:** N = 9，M = 2
> **输出:** 4
> **解释:**给定的例子可以按照下面的操作顺序求解:
> 
> *   在第一个操作中，将 N 替换为(N/M)，即 N = 9/2 = 4。
> *   在第二次操作中，再次用 N/M 替换 N，即 N = 4/2 = 2。
> *   在第三次操作中，将 M 增加 1，即 M = M+1 = 2+1 = 3。
> *   在第四个操作中，用 N/M 替换 N，即 N = 2/3 = 0。
> 
> 因此，所需操作的数量是 4，这是可能的最小值。
> 
> **输入:** N = 15，M = 1
> T3】输出: 5

**方法:**观察到最优的操作选择是将 **M** 的值递增假设 **x** 次，然后将 **N** 的值减少到 **N / (M+x)** 直到变成 **0** 即可解决给定的问题。为了找到最佳情况，[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，√N】**内 **x** 的所有值，并通过将其除以 **(M+i)计算将 **N** 减少到 **0** 所需的步数。**记录变量**和**中 **(M+i)** 所有可能值的最小运算次数，这是必需值。

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum count of
// operations to reduce N to 0 using M
int findMinimum(int N, int M)
{
    // If N is already 0
    if (N == 0) {
        return 0;
    }

    // Stores the minimum count of operations
    int ans = INT_MAX;

    // Loop to iterate in the range [0, √N]
    for (int i = 0; i * i <= N; i++) {

        // Edge case to prevent infinite looping
        if (M == 1 && i == 0) {
            continue;
        }

        // Stores the current count of moves
        int count = i;
        int tempN = N;

        // Number of operations required to
        // reduce N to 0 by dividing by M + i
        while (tempN != 0) {
            tempN /= (M + i);
            count++;
        }

        // Update the final count
        ans = min(count, ans);
    }

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int N = 9;
    int M = 2;

    cout << findMinimum(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */

import java.io.*;

class GFG {

    public static int findMinimum(int N, int M)
    {
        // If N is already 0
        if (N == 0) {
            return 0;
        }

        // Stores the minimum count of operations
        int ans = 1000000007;

        // Loop to iterate in the range [0, √N]
        for (int i = 0; i * i <= N; i++) {

            // Edge case to prevent infinite looping
            if (M == 1 && i == 0) {
                continue;
            }

            // Stores the current count of moves
            int count = i;
            int tempN = N;

            // Number of operations required to
            // reduce N to 0 by dividing by M + i
            while (tempN != 0) {
                tempN /= (M + i);
                count++;
            }

            // Update the final count
            if(count < ans){
              ans = count;
            }
        }

        // Return answer
        return ans;
    }

    // Driver code

    public static void main(String[] args)
    {
        int N = 9;
        int M = 2;

        System.out.println(findMinimum(N, M));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find the minimum count of
# operations to reduce N to 0 using M
def findMinimum(N, M):

    # If N is already 0
    if (N == 0):
        return 0

    # Stores the minimum count of operations
    ans = 10**9

    # Loop to iterate in the range[0, √N]
    i = 0
    while(i * i <= N):
        i += 1

        # Edge case to prevent infinite looping
        if (M == 1 and i == 0):
            continue

        # Stores the current count of moves
        count = i
        tempN = N

        # Number of operations required to
        # reduce N to 0 by dividing by M + i
        while (tempN != 0):
            tempN = tempN // (M + i)
            count += 1

        # Update the final count
        ans = min(count, ans)

    # Return answer
    return ans

# Driver code
N = 9
M = 2

print(findMinimum(N, M))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
/*package whatever //do not write package name here */

using System;

class GFG
{

    public static int findMinimum(int N, int M)
    {
        // If N is already 0
        if (N == 0)
        {
            return 0;
        }

        // Stores the minimum count of operations
        int ans = 1000000007;

        // Loop to iterate in the range [0, √N]
        for (int i = 0; i * i <= N; i++)
        {

            // Edge case to prevent infinite looping
            if (M == 1 && i == 0)
            {
                continue;
            }

            // Stores the current count of moves
            int count = i;
            int tempN = N;

            // Number of operations required to
            // reduce N to 0 by dividing by M + i
            while (tempN != 0)
            {
                tempN /= (M + i);
                count++;
            }

            // Update the final count
            if (count < ans)
            {
                ans = count;
            }
        }

        // Return answer
        return ans;
    }

    // Driver code

    public static void Main()
    {
        int N = 9;
        int M = 2;

        Console.WriteLine(findMinimum(N, M));
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the minimum count of
       // operations to reduce N to 0 using M
       function findMinimum(N, M)
       {

           // If N is already 0
           if (N == 0) {
               return 0;
           }

           // Stores the minimum count of operations
           let ans = Number.MAX_VALUE;

           // Loop to iterate in the range [0, √N]
           for (let i = 0; i * i <= N; i++) {

               // Edge case to prevent infinite looping
               if (M == 1 && i == 0) {
                   continue;
               }

               // Stores the current count of moves
               let count = i;
               let tempN = N;

               // Number of operations required to
               // reduce N to 0 by dividing by M + i
               while (tempN != 0) {
                   tempN = Math.floor(tempN / (M + i));
                   count++;
               }

               // Update the final count
               ans = Math.min(count, ans);
           }

           // Return answer
           return ans;
       }

       // Driver code
       let N = 9;
       let M = 2;

       document.write(findMinimum(N, M));

   // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
4
```

***时间复杂度:**O(***√***N * log N)*
***辅助空间:** O(1)*