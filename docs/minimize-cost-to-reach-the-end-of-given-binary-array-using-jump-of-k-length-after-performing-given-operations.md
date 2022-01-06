# 在执行给定操作后，使用 K 长度的跳转最小化到达给定二进制数组末尾的成本

> 原文:[https://www . geeksforgeeks . org/最小化在执行给定操作后使用长度为 k 的跳转到达给定二进制数组末尾的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reach-the-end-of-given-binary-array-using-jump-of-k-length-after-performing-given-operations/)

给定一个二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**的 **N** 整数和一个整数 **P** ，任务是利用长度 **K** 的跳跃从 **P <sup>th</sup>** 索引中找到到达数组末尾的最小代价。如果 **arr[i] = 1** ，跳转到索引 **i** 有效。可以使用以下操作修改数组:

*   将数值为 **0** 的指数替换为 **1** 。本次手术费用为 **X** 。
*   删除索引 **P** 处的整数。本次手术费用为 **Y** 。

**示例:**

> **输入:** arr[] = {0，0，0，1，1，0，0，1，1，1}，P = 6，K = 2，X = 1，Y = 2
> **输出:** 1
> **说明:**在第 1 次操作中，将索引 6 处的值替换为 1。因此，arr[] = {0，0，0，1，1，1，0，1，1，1}。最初，当前指数= P = 6。从 P 跳到 P + K = >从 6 = >跳到 8。再次跳转到下一个可能的索引，即 8 = > 10，这是数组的结尾。
> 
> **输入:** arr[] = {0，1，0，0，0，0，1，0}，P = 4，K = 1，X = 2，Y = 1
> **输出:** 4

**方法:**给定的问题可以基于以下观察来解决:

*   对于给定的 **P** ，检查指数 **P** 、 **P+K** 、**P+2K……**的值是否为 1。如果没有，则更换为 **1** 并保持其计数。于是，最终**成本** **=** **计* X** 。
*   第二次操作 **i** 次后，起始指数变为 **P+i** 。因此最终**成本= (i * Y) +(计数* X)** 。

因此，给定的问题可以通过在范围**【1，N-P】**内迭代 **i** 的所有可能值并计算每一步的成本来解决。这可以通过维护一个数组**零[]** ，其中**零[i]** 在索引 **i，i+K，i+2K…** 处存储 **0 的频率**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost to
// reach the end of the given array
int minimumCost(int arr[], int N,
                int P, int K, int X,
                int Y)
{
    // Convert P to 0-based indexing
    P = P - 1;

    // Vector to store the count of zeros
    // till the current index
    vector<int> zeros(N, 0);

    // Traverse the array and store the
    // count of zeros in vector
    for (int i = 0; i < N; i++) {

        // If element is 0
        if (arr[i] == 0) {
            zeros[i]++;
        }
    }
    // Iterate in the range [N-K-1, 0]
    // and increment zeros[i] by zeros[i+K]
    for (int i = N - K - 1; i >= 0; i--) {
        zeros[i] += zeros[i + K];
    }

    // Variable to store the min cost
    int cost = INT_MAX;

    // Loop to calculate the cost for all
    // values of i in range [P, N]
    for (int i = P; i < N; i++) {
        cost = min(cost,
                   ((i - P) * Y)
                       + (zeros[i] * X));
    }

    // Return Answer
    return cost;
}

// Driver Code
int main()
{
    int arr[] = { 0, 1, 0, 0, 0, 1, 0 };
    int P = 4;
    int K = 1;
    int X = 2;
    int Y = 1;
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << minimumCost(arr, N, P, K, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

public class GFG {

// Function to find the minimum cost to
// reach the end of the given array
static int minimumCost(int arr[], int N,
                int P, int K, int X,
                int Y)
{
    // Convert P to 0-based indexing
    P = P - 1;

    // Vector to store the count of zeros
    // till the current index
    int zeros[] = new int[N] ;

    // Traverse the array and store the
    // count of zeros in vector
    for (int i = 0; i < N; i++) {

        // If element is 0
        if (arr[i] == 0) {
            zeros[i]++;
        }
    }
    // Iterate in the range [N-K-1, 0]
    // and increment zeros[i] by zeros[i+K]
    for (int i = N - K - 1; i >= 0; i--) {
        zeros[i] += zeros[i + K];
    }

    // Variable to store the min cost
    int cost = Integer.MAX_VALUE;

    // Loop to calculate the cost for all
    // values of i in range [P, N]
    for (int i = P; i < N; i++) {
        cost = Math.min(cost,
                   ((i - P) * Y)
                       + (zeros[i] * X));
    }

    // Return Answer
    return cost;
}

    // Driver Code
    public static void main (String[] args) {

    int arr[] = { 0, 1, 0, 0, 0, 1, 0 };
    int P = 4;
    int K = 1;
    int X = 2;
    int Y = 1;
    int N = arr.length;

    System.out.println(minimumCost(arr, N, P, K, X, Y));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach
import sys

# Function to find the minimum cost to
# reach the end of the given array
def minimumCost(arr, N, P, K,  X, Y) :

    # Convert P to 0-based indexing
    P = P - 1;

    # Vector to store the count of zeros
    # till the current index
    zeros = [0] * N ;

    # Traverse the array and store the
    # count of zeros in vector
    for i in range(N) :

        # If element is 0
        if (arr[i] == 0) :
            zeros[i] += 1;

    # Iterate in the range [N-K-1, 0]
    # and increment zeros[i] by zeros[i+K]
    for i in range( N - K - 1, -1, -1) :
        zeros[i] += zeros[i + K];

    # Variable to store the min cost
    cost = sys.maxsize;

    # Loop to calculate the cost for all
    # values of i in range [P, N]
    for i in range(P, N) :
        cost = min(cost,((i - P) * Y) + (zeros[i] * X));

    # Return Answer
    return cost;

# Driver Code
if __name__ == "__main__" :

    arr = [ 0, 1, 0, 0, 0, 1, 0 ];
    P = 4;
    K = 1;
    X = 2;
    Y = 1;
    N = len(arr);

    print(minimumCost(arr, N, P, K, X, Y));

   # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

    // Function to find the minimum cost to
    // reach the end of the given array
    static int minimumCost(int[] arr, int N, int P, int K, int X, int Y)
    {

        // Convert P to 0-based indexing
        P = P - 1;

        // Vector to store the count of zeros
        // till the current index
        int[] zeros = new int[N];

        // Traverse the array and store the
        // count of zeros in vector
        for (int i = 0; i < N; i++)
        {

            // If element is 0
            if (arr[i] == 0)
            {
                zeros[i]++;
            }
        }
        // Iterate in the range [N-K-1, 0]
        // and increment zeros[i] by zeros[i+K]
        for (int i = N - K - 1; i >= 0; i--)
        {
            zeros[i] += zeros[i + K];
        }

        // Variable to store the min cost
        int cost = int.MaxValue;

        // Loop to calculate the cost for all
        // values of i in range [P, N]
        for (int i = P; i < N; i++)
        {
            cost = Math.Min(cost,
                       ((i - P) * Y)
                           + (zeros[i] * X));
        }

        // Return Answer
        return cost;
    }

    // Driver Code
    public static void Main()
    {

        int[] arr = { 0, 1, 0, 0, 0, 1, 0 };
        int P = 4;
        int K = 1;
        int X = 2;
        int Y = 1;
        int N = arr.Length;

        Console.WriteLine(minimumCost(arr, N, P, K, X, Y));
    }
}

// This code is contributed by _Saurabh_Jaiswal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the minimum cost to
// reach the end of the given array
function minimumCost(arr, N, P, K, X, Y)
{
    // Convert P to 0-based indexing
    P = P - 1;

    // Vector to store the count of zeros
    // till the current index
    var zeros = Array(N).fill(0);

    // Traverse the array and store the
    // count of zeros in vector
    for (var i = 0; i < N; i++) {

        // If element is 0
        if (arr[i] == 0) {
            zeros[i]++;
        }
    }
    // Iterate in the range [N-K-1, 0]
    // and increment zeros[i] by zeros[i+K]
    for (var i = N - K - 1; i >= 0; i--) {
        zeros[i] += zeros[i + K];
    }

    // Variable to store the min cost
    var cost = 1000000000;

    // Loop to calculate the cost for all
    // values of i in range [P, N]
    for (var i = P; i < N; i++) {
        cost = Math.min(cost,
                   ((i - P) * Y)
                       + (zeros[i] * X));
    }

    // Return Answer
    return cost;
}

// Driver Code
var arr = [ 0, 1, 0, 0, 0, 1, 0 ];
var P = 4;
var K = 1;
var X = 2;
var Y = 1;
var N = arr.length;
document.write(minimumCost(arr, N, P, K, X, Y));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)