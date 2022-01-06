# 在

之间的任意位置添加 K 个点后，最小化相邻点之间的最大距离

> 原文:[https://www . geeksforgeeks . org/最小化添加 k 点后相邻点之间的最大距离-中间任意位置/](https://www.geeksforgeeks.org/minimize-the-maximum-distance-between-adjacent-points-after-adding-k-points-anywhere-in-between/)

给定一个代表沿直线的 **N** 点位置的[N 整数和一个整数 **K** 的](https://www.geeksforgeeks.org/introduction-to-arrays/)[数组**arr【】】**，任务是在两个整数之间的任意位置添加 **K** 点后，找到相邻点之间最大距离的最小值，而不一定是在一个整数位置上。](https://www.geeksforgeeks.org/introduction-to-arrays/)

**示例:**

> **输入:** arr[] = {2，4，8，10}，K = 1
> **输出:** 2
> **说明:**可以增加位置 6 的一个点。因此，新的点数组变成{2，4，6，8，10}，两个相邻点之间的最大距离是 2，这是最小可能的。
> 
> **输入:** arr[] = {1，2，3，4，5，6，7，8，9，10}，K = 9
> **输出:** 0.5

**方法:**给定的问题可以用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)解决。其思想是对范围**【0，10<sup>8</sup>**中的值 **D** 执行二分搜索法运算，其中 D 表示添加 **K** 点后相邻点之间的最大距离值。按照以下步骤解决给定的问题:

*   初始化变量，**低** = **1** 和**高** = **10 <sup>8</sup>** ，其中**低**代表下界，**高**代表二分搜索法上界。
*   创建一个函数 **isPossible()** ，返回数组中是否可以添加 **K** 点的布尔值，使得相邻点之间的最大距离为 **D** 。根据观察，对于两个相邻的点 **(i，j)** ，需要放置在它们中间的点的数量使得它们之间的最大距离为 **D = (j -i)/D** 。
*   因此，使用这里讨论的二分搜索法算法[、](https://www.geeksforgeeks.org/binary-search/)遍历范围，如果对于范围**【X，Y】**中的中间值 **D** ，如果**为假，则迭代范围的上半部分，即**【D，Y】**。否则，迭代下半部分，即**【X，D】**。**
*   重复一个循环，直到**(高–低)> 10 <sup>-6</sup>** 。
*   存储在 **low** 中的值是要求的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to check if it is possible
// to add K points such that the maximum
// distance between adjacent points is D
bool isPossible(double D, int arr[],
                int N, int K)
{
    // Stores the count of point used
    int used = 0;

    // Iterate over all given points
    for (int i = 0; i < N - 1; ++i) {

        // Add number of points required
        // to be placed between ith
        // and (i+1)th point
        used += (int)((arr[i + 1]
                       - arr[i])
                      / D);
    }

    // Return answer
    return used <= K;
}

// Function to find the minimum value of
// maximum distance between adjacent points
// after adding K points any where between
double minMaxDist(int stations[], int N, int K)
{
    // Stores the lower bound and upper
    // bound of the given range
    double low = 0, high = 1e8;

    // Perform binary search
    while (high - low > 1e-6) {

        // Find the middle value
        double mid = (low + high) / 2.0;

        if (isPossible(mid, stations, N, K)) {

            // Update the current range
            // to lower half
            high = mid;
        }

        // Update the current range
        // to upper half
        else {
            low = mid;
        }
    }

    return low;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    int K = 9;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minMaxDist(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.math.BigDecimal;

class GFG {

    // Function to check if it is possible
    // to add K points such that the maximum
    // distance between adjacent points is D
    public static boolean isPossible(double D, int arr[],
                                     int N, int K)
    {
        // Stores the count of point used
        int used = 0;

        // Iterate over all given points
        for (int i = 0; i < N - 1; ++i) {

            // Add number of points required
            // to be placed between ith
            // and (i+1)th point
            used += (int) ((arr[i + 1] - arr[i]) / D);
        }

        // Return answer
        return used <= K;
    }

    // Function to find the minimum value of
    // maximum distance between adjacent points
    // after adding K points any where between
    public static double minMaxDist(int stations[], int N, int K)
    {

        // Stores the lower bound and upper
        // bound of the given range
        double low = 0, high = 1e8;

        // Perform binary search
        while (high - low > 1e-6) {

            // Find the middle value
            double mid = (low + high) / 2.0;

            if (isPossible(mid, stations, N, K)) {

                // Update the current range
                // to lower half
                high = mid;
            }

            // Update the current range
            // to upper half
            else {
                low = mid;
            }
        }

        // System.out.printf("Value: %.2f", low);
        return low;
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
        int K = 9;
        int N = arr.length;

        System.out.printf("%.1f", minMaxDist(arr, N, K));
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to check if it is possible
# to add K points such that the maximum
# distance between adjacent points is D
def isPossible(D, arr, N, K) :

    # Stores the count of point used
    used = 0;

    # Iterate over all given points
    for i in range(N - 1) :

        # Add number of points required
        # to be placed between ith
        # and (i+1)th point
        used += int((arr[i + 1] - arr[i]) / D);

    # Return answer
    return used <= K;

# Function to find the minimum value of
# maximum distance between adjacent points
# after adding K points any where between
def minMaxDist(stations, N, K) :

    # Stores the lower bound and upper
    # bound of the given range
    low = 0; high = 1e8;

    # Perform binary search
    while (high - low > 1e-6) :

        # Find the middle value
        mid = (low + high) / 2.0;

        if (isPossible(mid, stations, N, K)) :

            # Update the current range
            # to lower half
            high = mid;

        # Update the current range
        # to upper half
        else :

            low = mid;

    return round(low, 2);

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ];
    K = 9;
    N = len(arr);

    print(minMaxDist(arr, N, K));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

    // Function to check if it is possible
    // to add K points such that the maximum
    // distance between adjacent points is D
    public static bool isPossible(double D, int []arr,
                                     int N, int K)
    {

        // Stores the count of point used
        int used = 0;

        // Iterate over all given points
        for (int i = 0; i < N - 1; ++i) {

            // Add number of points required
            // to be placed between ith
            // and (i+1)th point
            used += (int) ((arr[i + 1] - arr[i]) / D);
        }

        // Return answer
        return used <= K;
    }

    // Function to find the minimum value of
    // maximum distance between adjacent points
    // after adding K points any where between
    public static double minMaxDist(int []stations, int N, int K)
    {

        // Stores the lower bound and upper
        // bound of the given range
        double low = 0, high = 1e8;

        // Perform binary search
        while (high - low > 1e-6) {

            // Find the middle value
            double mid = (low + high) / 2.0;

            if (isPossible(mid, stations, N, K)) {

                // Update the current range
                // to lower half
                high = mid;
            }

            // Update the current range
            // to upper half
            else {
                low = mid;
            }
        }

        // Console.Write("Value: %.2f", low);
        return low;
    }

    // Driver Code
    public static void Main(String []args)
    {
        int []arr = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
        int K = 9;
        int N = arr.Length;

        Console.Write("{0:F1}", minMaxDist(arr, N, K));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to check if it is possible
       // to add K points such that the maximum
       // distance between adjacent points is D
       function isPossible(D, arr,
           N, K)
       {

           // Stores the count of point used
           let used = 0;

           // Iterate over all given points
           for (let i = 0; i < N - 1; ++i) {

               // Add number of points required
               // to be placed between ith
               // and (i+1)th point
               used += Math.floor((arr[i + 1]
                   - arr[i])
                   / D);
           }

           // Return answer
           return used <= K;
       }

       // Function to find the minimum value of
       // maximum distance between adjacent points
       // after adding K points any where between
       function minMaxDist(stations, N, K)
       {

           // Stores the lower bound and upper
           // bound of the given range
           let low = 0, high = 1e8;

           // Perform binary search
           while (high - low > 1e-6) {

               // Find the middle value
               let mid = (low + high) / 2;

               if (isPossible(mid, stations, N, K)) {

                   // Update the current range
                   // to lower half
                   high = mid;
               }

               // Update the current range
               // to upper half
               else {
                   low = mid;
               }
           }

           return low.toFixed(1);
       }

       // Driver Code
       let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
       let K = 9;
       let N = arr.length;

       document.write(minMaxDist(arr, N, K));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
0.5
```

***时间复杂度:** O(N*log M)，其中 M 的值为 10 <sup>14</sup> 。*
***辅助空间:** O(1)*