# 计算从一点到原点的路径:内存优化

> 原文:[https://www . geesforgeks . org/counts-path-从点到原点-内存优化/](https://www.geeksforgeeks.org/counts-paths-from-a-point-to-reach-origin-memory-optimized/)

给定两个整数 **N** 和 **M** ，表示在坐标系中的位置，任务是通过向左或向下走几步来计算从该点到原点的路径。
**例:**

> **输入:** 3 6
> **输出:**路径数 84
> **输入:**3
> **输出:**路径数 20

我们在本文中已经讨论过这个问题–
[计算从一点到达原点](https://www.geeksforgeeks.org/counts-paths-point-reach-origin/)
**的路径方法:**想法是使用[动态编程范式](https://www.geeksforgeeks.org/dynamic-programming/)来解决这个问题。在这个问题中，有一个限制，在一条路径中只能向左或向下移动，由于这一限制，对于任何一点，路径数等于左边点的路径数和右边点的路径数之和，这样，我们以自下而上的方式从(0，0)到(N，M)计算每个点的路径。在这个问题中，缩小空间的关键是计算一个点的解，比如(I，j)，我们只需要(i-1，j)和(I，j-1)的值，也就是说，一旦使用了(i-1，j-1)计算值，我们就不需要它们的部分。
以下是上述方法的实施:

## C++

```
// C++ implementation to count the
// paths from a points to origin

#include <iostream>
#include<cstring>

using namespace std;

// Function to count the paths from
// a point to the origin
long Count_Paths(int x,int y)
{
    // Base Case when the point
    // is already at origin
    if(x == 0 && y == 0)
        return 0;

    // Base Case when the point
    // is on the x or y-axis
    if(x == 0 || y == 0)
        return 1;

    long dp[max(x,y)+1],
     p=max(x,y),q=min(x,y);

    // Loop to fill all the
    // position as 1 in the array
    for(int i=0;i<=p;i++)
        dp[i]=1;

    // Loop to count the number of
    // paths from a point to origin
    // in bottom-up manner
    for(int i=1;i<=q;i++)
        for(int j=1;j<=p;j++)
            dp[j]+=dp[j-1];

    return dp[p];
}

// Driver Code
int main()
{
    int x = 3,y = 3;

    // Function Call
    cout<< "Number of Paths "
        << Count_Paths(x,y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count the
// paths from a points to origin

class GFG {

    // Function to count the paths from
    // a point to the origin
    static long Count_Paths(int x, int y) {
        // Base Case when the point
        // is already at origin
        if (x == 0 && y == 0)
            return 0;

        // Base Case when the point
        // is on the x or y-axis
        if (x == 0 || y == 0)
            return 1;

        int[] dp = new int[Math.max(x, y) + 1];
        int p = Math.max(x, y), q = Math.min(x, y);

        // Loop to fill all the
        // position as 1 in the array
        for (int i = 0; i <= p; i++)
            dp[i] = 1;

        // Loop to count the number of
        // paths from a point to origin
        // in bottom-up manner
        for (int i = 1; i <= q; i++)
            for (int j = 1; j <= p; j++)
                dp[j] += dp[j - 1];

        return dp[p];
    }

    // Driver Code
    public static void main(String[] args) {
        int x = 3, y = 3;

        // Function Call
        System.out.print("Number of Paths " + Count_Paths(x, y));
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation to count the
# paths from a points to origin

# Function to count the paths from
# a point to the origin
def Count_Paths(x, y):

    # Base Case when the point
    # is already at origin
    if (x == 0 and y == 0):
        return 0

    # Base Case when the point
    # is on the x or y-axis
    if (x == 0 and y == 0):
        return 1

    dp = [0] * (max(x, y) + 1)

    p = max(x, y)
    q = min(x, y)

    # Loop to fill all the
    # position as 1 in the array
    for i in range(p + 1):
        dp[i] = 1

    # Loop to count the number of
    # paths from a point to origin
    # in bottom-up manner
    for i in range(1, q + 1):
        for j in range(1, p + 1):
            dp[j] += dp[j - 1]

    return dp[p]

# Driver Code
x = 3
y = 3

# Function call
print("Number of Paths ", Count_Paths(x, y))

# This code is contributed by sanjoy_62
```

## C#

```
// C# implementation to count the
// paths from a points to origin
using System;

class GFG {

    // Function to count the paths from
    // a point to the origin
    static long Count_Paths(int x, int y) {
        // Base Case when the point
        // is already at origin
        if (x == 0 && y == 0)
            return 0;

        // Base Case when the point
        // is on the x or y-axis
        if (x == 0 || y == 0)
            return 1;

        int[] dp = new int[Math.Max(x, y) + 1];
        int p = Math.Max(x, y), q = Math.Min(x, y);

        // Loop to fill all the
        // position as 1 in the array
        for (int i = 0; i <= p; i++)
            dp[i] = 1;

        // Loop to count the number of
        // paths from a point to origin
        // in bottom-up manner
        for (int i = 1; i <= q; i++)
            for (int j = 1; j <= p; j++)
                dp[j] += dp[j - 1];

        return dp[p];
    }

    // Driver Code
    public static void Main(String[] args) {
        int x = 3, y = 3;

        // Function Call
        Console.Write("Number of Paths " + Count_Paths(x, y));
    }
}

// This code is contributed by sapnasingh4991
```

**输出:**

```
Number of Paths  20
```

**性能分析:**

*   **时间复杂度:**在上面给出的方法中，在最坏的情况下，有两个循环需要 O(N*M)时间。因此，这种方法的时间复杂度将是 **O(N*M)** 。
*   **空间复杂度:**在上面给出的方法中，有一个大小最大值为 N 和 M 的单个数组，因此上面方法的空间复杂度为 **O(max(N，M))**