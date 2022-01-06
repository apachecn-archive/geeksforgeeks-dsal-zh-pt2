# 统计到达第 n 站的方式

> 原文:[https://www . geesforgeks . org/count-way-to-th-station/](https://www.geeksforgeeks.org/count-ways-to-reach-the-nth-station/)

给定 **N 站**和三列 **A** 、 **B** 、 **C** 使得列车 **A** 每站停一次，列车 **B** 每隔一站停一次，列车 **C** 每隔三站停一次，任务是找到从**站到达 **N <sup>第</sup>站**的路数**

**示例:**

> **输入:** N = 4
> **输出:** 3
> **说明:**
> 以下是从 1 号站到达 4 号站的方式:
> 
> 1.  在 1 号站乘坐列车 A，然后仅使用列车 A 作为(A→A→A→A→A)继续前往 4 号站。
> 2.  在 1 号站乘坐列车 B，在 3 号站停车，从 3 号站乘坐列车 A 到 4 号站 as (B→)。→ A)。
> 3.  从 1 号站乘坐 C 列车，在 4 号站(C→)停车。)
> 
> 因此，从车站 1 到达车站 4 的总方式数为 3。
> 
> **输入:**N = 15
> T3】输出: 338

**方法:**给定的问题可以使用以下观察结果来解决:

*   只有当列车 **A** 到达**X–1**时，列车 **A** 才能到达车站 **X** 。
*   只有当列车 **B** 到达**X–2**时，列车 **B** 才能到达车站 **X** 。
*   只有当列车 **C** 到达**X–3**时，列车 **C** 才能到达车站 **X** 。

因此，从上面的观察来看，想法是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念。按照下面给出的步骤解决问题:

*   初始化一个 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)T2 阵这样:
    *   **DP[i][1]** 存储使用列车 **A** 到达 I 站的方式数。
    *   **DP[i][2]** 存储使用列车 **B** 到达 I 站的方式数。
    *   **DP[i][3]** 存储使用列车 **C** 到达 I 站的方式数。
    *   **DP[i][4]** 存储使用列车 **A** 、 **B** 或 **C** 到达 I 站的方式数。
*   只有一条路可以到达车站 1。因此，将 **DP[1][1]** 、 **DP[1][2]** 、 **DP[1][3]** 、 **DP[1][4]** 的值更新为 **1** 。
*   使用上面的观察，通过迭代循环更新每个状态的值，如下所示:
    *   **DP[i][1] = DP[i-1][4]**
    *   **DP[i][2] = DP[i-2][4]**
    *   **DP[i][3] = DP[i-3][4]**
    *   **DP[i][4] = DP[i][1] + DP[i][2] + DP[i][3]**
*   完成上述步骤后，打印 **DP[N][4]** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of ways
// to reach Nth station
int numberOfWays(int N)
{
    // Declares the DP[] array
    int DP[N + 1][5];

    // Initialize dp[][] array
    memset(DP, 0, sizeof(DP));

    // Only 1 way to reach station 1
    DP[1][1] = 1;
    DP[1][2] = 1;
    DP[1][3] = 1;
    DP[1][4] = 1;

    // Find the remaining states from
    // the 2nd station
    for (int i = 2; i <= N; i++) {

        // If the train A is present
        // at station i - 1
        if (i - 1 > 0 && DP[i - 1][1] > 0)
            DP[i][1] = DP[i - 1][4];

        // If the train B is present
        // at station i-2
        if (i - 2 > 0 && DP[i - 2][2] > 0)
            DP[i][2] = DP[i - 2][4];

        // If train C is present at
        // station i-3
        if (i - 3 > 0 && DP[i - 3][3] > 0)
            DP[i][3] = DP[i - 3][4];

        // The total number of ways to
        // reach station i
        DP[i][4] = (DP[i][1] + DP[i][2]
                    + DP[i][3]);
    }

    // Return the total count of ways
    return DP[N][4];
}

// Driver Code
int main()
{
    int N = 15;
    cout << numberOfWays(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the number of ways
    // to reach Nth station
    static int numberOfWays(int N)
    {

        // Declares the DP[] array
        int[][] DP = new int[N + 1][5];

        // Initialize dp[][] array
        for (int i = 0; i < N + 1; i++) {
            for (int j = 0; j < 5; j++) {
                DP[i][j] = 0;
            }
        }

        // Only 1 way to reach station 1
        DP[1][1] = 1;
        DP[1][2] = 1;
        DP[1][3] = 1;
        DP[1][4] = 1;

        // Find the remaining states from
        // the 2nd station
        for (int i = 2; i <= N; i++) {

            // If the train A is present
            // at station i - 1
            if (i - 1 > 0 && DP[i - 1][1] > 0)
                DP[i][1] = DP[i - 1][4];

            // If the train B is present
            // at station i-2
            if (i - 2 > 0 && DP[i - 2][2] > 0)
                DP[i][2] = DP[i - 2][4];

            // If train C is present at
            // station i-3
            if (i - 3 > 0 && DP[i - 3][3] > 0)
                DP[i][3] = DP[i - 3][4];

            // The total number of ways to
            // reach station i
            DP[i][4] = (DP[i][1] + DP[i][2] + DP[i][3]);
        }

        // Return the total count of ways
        return DP[N][4];
    }

    // Driver Code
    static public void main(String[] args)
    {
        int N = 15;
        System.out.println(numberOfWays(N));
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of ways
# to reach Nth station
def numberOfWays(N):

    # Declares the DP[] array
    DP = [[0 for i in range(5)]
             for i in range(N + 1)]

    # Initialize dp[][] array
    # memset(DP, 0, sizeof(DP))

    # Only 1 way to reach station 1
    DP[1][1] = 1
    DP[1][2] = 1
    DP[1][3] = 1
    DP[1][4] = 1

    # Find the remaining states from
    # the 2nd station
    for i in range(2, N + 1):

        # If the train A is present
        # at station i - 1
        if (i - 1 > 0 and DP[i - 1][1] > 0):
            DP[i][1] = DP[i - 1][4]

        # If the train B is present
        # at station i-2
        if (i - 2 > 0 and DP[i - 2][2] > 0):
            DP[i][2] = DP[i - 2][4]

        # If train C is present at
        # station i-3
        if (i - 3 > 0 and DP[i - 3][3] > 0):
            DP[i][3] = DP[i - 3][4]

        # The total number of ways to
        # reach station i
        DP[i][4] = (DP[i][1] + DP[i][2] + DP[i][3])

    # Return the total count of ways
    return DP[N][4]

# Driver Code
if __name__ == '__main__':

    N = 15

    print(numberOfWays(N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of ways
// to reach Nth station
static int numberOfWays(int N)
{

    // Declares the DP[] array
    int[,] DP = new int[N + 1, 5];

    // Initialize dp[][] array
    for(int i = 0; i < N + 1; i++)
    {
        for(int j = 0; j < 5; j++)
        {
            DP[i, j] = 0;
        }
    }

    // Only 1 way to reach station 1
    DP[1, 1] = 1;
    DP[1, 2] = 1;
    DP[1, 3] = 1;
    DP[1, 4] = 1;

    // Find the remaining states from
    // the 2nd station
    for(int i = 2; i <= N; i++)
    {

        // If the train A is present
        // at station i - 1
        if (i - 1 > 0 && DP[i - 1, 1] > 0)
            DP[i, 1] = DP[i - 1, 4];

        // If the train B is present
        // at station i-2
        if (i - 2 > 0 && DP[i - 2, 2] > 0)
            DP[i, 2] = DP[i - 2, 4];

        // If train C is present at
        // station i-3
        if (i - 3 > 0 && DP[i - 3, 3] > 0)
            DP[i, 3] = DP[i - 3, 4];

        // The total number of ways to
        // reach station i
        DP[i, 4] = (DP[i, 1] + DP[i, 2] + DP[i, 3]);
    }

    // Return the total count of ways
    return DP[N, 4];
}

// Driver Code
static public void Main()
{
    int N = 15;
    Console.WriteLine(numberOfWays(N));
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
// Javascript program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the number of ways
// to reach Nth station
static int numberOfWays(int N)
{
    // Declares the DP[] array
    int DP[][] = new int[N + 1][5];

    // Initialize dp[][] array
    for (int i = 0; i < N +1; i++) {
        for (int j = 0; j < 5; j++) {
            DP[i][j] = 0;
        }
    }

    // Only 1 way to reach station 1
    DP[1][1] = 1;
    DP[1][2] = 1;
    DP[1][3] = 1;
    DP[1][4] = 1;

    // Find the remaining states from
    // the 2nd station
    for (int i = 2; i <= N; i++) {

        // If the train A is present
        // at station i - 1
        if (i - 1 > 0 && DP[i - 1][1] > 0)
            DP[i][1] = DP[i - 1][4];

        // If the train B is present
        // at station i-2
        if (i - 2 > 0 && DP[i - 2][2] > 0)
            DP[i][2] = DP[i - 2][4];

        // If train C is present at
        // station i-3
        if (i - 3 > 0 && DP[i - 3][3] > 0)
            DP[i][3] = DP[i - 3][4];

        // The total number of ways to
        // reach station i
        DP[i][4] = (DP[i][1] + DP[i][2]
                    + DP[i][3]);
    }

    // Return the total count of ways
    return DP[N][4];
}

// Driver Code
public static void main(String[] args)
{

    int N = 15;
    System.out.print(numberOfWays(N));
}
}

// This code is contributed by code_hunt.
```

**Output:** 

```
338
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)