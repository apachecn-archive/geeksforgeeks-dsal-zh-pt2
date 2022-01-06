# 使用给定数字达到目标的求和和模运算的最小次数

> 原文:[https://www . geesforgeks . org/最小和模运算数-使用给定的数字到达目标/](https://www.geeksforgeeks.org/minimum-number-of-sum-and-modulo-operations-using-given-numbers-to-reach-target/)

给定一个数字 **N** 、一个数组**arr【】**和一个目标数 **K** ，任务是通过选择任意**数组元素**并将 **N** 改为 **(N + arr[i]) mod 100000** 来找到达到 **K** 的最小**步数。**

**示例:**

> **输入:** N = 99880，K = 89，arr = {100，3}
> **输出:** 5
> **说明:**数字“100”用了 2 次，数字“3”推了 3 次，由 N 得 K
> 
> **输入:** N = 10000，K = 10004，arr = { 1 }
> T3】输出: 4

**逼近:**上述问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决，因为它有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构。](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)初始化 **dp** 表，其中**DP【I】**存储达到状态 **i** on N 所需的**最小**移动，而 **dp【目标】**将是所需的答案。从每个 **arr[i]，**找到所有可达状态并最小化 **dp** 值。按照以下步骤进行操作:

*   [初始化一个数组](https://www.geeksforgeeks.org/g-fact-92/)，比如说 **dp[ ]** 来存储达到状态 **i.** 所需的**最小**步数
*   迭代[数组 arr](https://www.geeksforgeeks.org/arrays-in-c-cpp/) 并检查当前数字 N 的每个位置为 **x** :
    *   如果 **dp[x]** 等于 **-1，**则继续。
    *   否则，在循环的同时循环一次[，直到 **dp【下一个】**等于 **-1** 或 **dp【下一个】**大于**DP【x】+1**，并将**下一个更新为**(x+按钮[i])%100000** 和 **dp【下一个】**为**DP【x】+1**。**](https://www.geeksforgeeks.org/python-while-loop/)
*   最后，返回 **dp【目标】的值。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum moves
// to reach K from N
int minPushes(int N, int K, vector<int> arr)
{

    // Initialization of dp vector
    vector<int> dp(100000, -1);

    // dp[i] = minimum pushes
    // required to reach i
    dp[N] = 0;

    // Traversing through the buttons
    for (int i = 0; i < arr.size(); i++) {

        // Iterating through all the positions
        for (int xx = 0; xx < 100000; xx++) {
            int x = xx;

            // If not visited
            if (dp[x] == -1)
                continue;

            // Next status of lock
            int next = (x + arr[i]) % 100000;
            while (dp[next] == -1
                   || dp[next] > dp[x] + 1) {
                dp[next] = dp[x] + 1;

                // Advance to next state
                x = next;
                next = (next + arr[i]) % 100000;
            }
        }
    }

    // Return the final dp[target]
    return dp[K];
}

// Driver function
int main()
{
    // Given Input
    int N = 99880, K = 89;
    vector<int> arr{ 100, 3 };

    // Function Call
    cout << minPushes(N, K, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG{

// Function to find the minimum moves
// to reach K from N
static int minPushes(int N, int K, int[] arr)
{

    // Initialization of dp vector
    int[] dp = new int[100000];
    for (int i = 0; i < dp.length; i++)
        dp[i] = -1;

    // dp[i] = minimum pushes
    // required to reach i
    dp[N] = 0;

    // Traversing through the buttons
    for (int i = 0; i < arr.length; i++) {

        // Iterating through all the positions
        for (int xx = 0; xx < 100000; xx++) {
            int x = xx;

            // If not visited
            if (dp[x] == -1)
                continue;

            // Next status of lock
            int next = (x + arr[i]) % 100000;
            while (dp[next] == -1
                   || dp[next] > dp[x] + 1) {
                dp[next] = dp[x] + 1;

                // Advance to next state
                x = next;
                next = (next + arr[i]) % 100000;
            }
        }
    }

    // Return the final dp[target]
    return dp[K];
}

// Driver function
public static void main(String[] args)
{
    // Given Input
    int N = 99880, K = 89;
    int[] arr = { 100, 3 };

    // Function Call
    System.out.print(minPushes(N, K, arr));

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the minimum moves
# to reach K from N
def minPushes(N, K, arr):

    # Initialization of dp vector
    dp = [-1] * 100000

    # dp[i] = minimum pushes
    # required to reach i
    dp[N] = 0

    # Traversing through the buttons
    for i in range(len(arr)):

        # Iterating through all the positions
        for xx in range(100000):
            x = xx

            # If not visited
            if (dp[x] == -1) :
                continue

            # Next status of lock
            next = (x + arr[i]) % 100000
            while (dp[next] == -1
                   or dp[next] > dp[x] + 1) :
                dp[next] = dp[x] + 1

                # Advance to next state
                x = next
                next = (next + arr[i]) % 100000

    # Return the final dp[target]
    return dp[K]

# Driver function

# Given Input
N = 99880
K = 89
arr = [ 100, 3 ]

# Function Call
print(minPushes(N, K, arr))

# This code is contributed by sanjoy_62.
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG{

// Function to find the minimum moves
// to reach K from N
static int minPushes(int N, int K, int[] arr)
{

    // Initialization of dp vector
    int[] dp = new int[100000];
    for (int i = 0; i < dp.Length; i++)
        dp[i] = -1;

    // dp[i] = minimum pushes
    // required to reach i
    dp[N] = 0;

    // Traversing through the buttons
    for (int i = 0; i < arr.Length; i++) {

        // Iterating through all the positions
        for (int xx = 0; xx < 100000; xx++) {
            int x = xx;

            // If not visited
            if (dp[x] == -1)
                continue;

            // Next status of lock
            int next = (x + arr[i]) % 100000;
            while (dp[next] == -1
                   || dp[next] > dp[x] + 1) {
                dp[next] = dp[x] + 1;

                // Advance to next state
                x = next;
                next = (next + arr[i]) % 100000;
            }
        }
    }

    // Return the readonly dp[target]
    return dp[K];
}

// Driver function
public static void Main(String[] args)
{
    // Given Input
    int N = 99880, K = 89;
    int[] arr = { 100, 3 };

    // Function Call
    Console.Write(minPushes(N, K, arr));

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach;

        // Function to find the minimum moves
        // to reach K from N
        function minPushes(N, K, arr) {

            // Initialization of dp vector
            let dp = new Array(100000).fill(-1);

            // dp[i] = minimum pushes
            // required to reach i
            dp[N] = 0;

            // Traversing through the buttons
            for (let i = 0; i < arr.length; i++) {

                // Iterating through all the positions
                for (let xx = 0; xx < 100000; xx++) {
                    let x = xx;

                    // If not visited
                    if (dp[x] == -1)
                        continue;

                    // Next status of lock
                    let next = (x + arr[i]) % 100000;
                    while (dp[next] == -1
                        || dp[next] > dp[x] + 1) {
                        dp[next] = dp[x] + 1;

                        // Advance to next state
                        x = next;
                        next = (next + arr[i]) % 100000;
                    }
                }
            }

            // Return the final dp[target]
            return dp[K];
        }

        // Driver function

        // Given Input
        let N = 99880, K = 89;
        let arr = [100, 3];

        // Function Call
        document.write(minPushes(N, K, arr));

   // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
5
```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N)*