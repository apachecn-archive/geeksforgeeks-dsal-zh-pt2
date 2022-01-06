# 将数组分成 K 段，使最小值之和最大

> 原文:[https://www . geeksforgeeks . org/分割 k 段数组-这样最小值之和最大化/](https://www.geeksforgeeks.org/divide-the-array-in-k-segments-such-that-the-sum-of-minimums-is-maximized/)

给定一个大小为 **N** 的数组**和一个整数 **K** ，任务是将数组分成 **K** 段，使得 **K** 段的**最小值**的**和**最大化。
**举例:**** 

> ****输入:** a[] = {5，7，4，2，8，1，6}，K = 3
> **输出:** 7
> 在索引 0 和 1 处划分数组。然后是{5}、{7}、{4、2、8、1、6}段。最小值之和为 5 + 7 + 1 = 13
> **输入:** a[] = {6，5，3，8，9，10，4，7，10}，K = 4
> **输出:** 27**

****逼近**:使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)可以解决问题。使用[递归](https://www.geeksforgeeks.org/recursion/)尝试所有可能的分区。设 **dp[i][k]** 为具有 k 个分区的索引 I 之前的最小值的最大和。因此，可能的状态将在从索引 I 到 n 的每个索引处被划分。所有这些状态的最小值的最大和将是我们的答案。写完这个循环，我们可以用背下来。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to find the sum of
// the minimum of all the segments
#include <bits/stdc++.h>
using namespace std;
const int MAX = 10;

// Function to maximize the sum of the minimums
int maximizeSum(int a[], int n, int ind,
                int k, int dp[MAX][MAX])
{

    // If k segments have been divided
    if (k == 0) {
        // If we are at the end
        if (ind == n)
            return 0;

        // If we donot reach the end
        // then return a negative number
        // that cannot be the sum
        else
            return -1e9;
    }

    // If at the end but
    // k segments are not formed
    else if (ind == n)
        return -1e9;

    // If the state has not been visited yet
    else if (dp[ind][k] != -1)
        return dp[ind][k];

    // If the state has not been visited
    else {
        int ans = 0;

        // Get the minimum element in the segment
        int mini = a[ind];

        // Iterate and try to break at every index
        // and create a segment
        for (int i = ind; i < n; i++) {

            // Find the minimum element in the segment
            mini = min(mini, a[i]);

            // Find the sum of all the segments trying all
            // the possible combinations
            ans = max(ans, maximizeSum(
              a, n, i + 1, k - 1, dp) + mini);
        }

        // Return the answer by
        // memoizing it
        return dp[ind][k] = ans;
    }
}

// Driver Code
int main()
{
    int a[] = { 5, 7, 4, 2, 8, 1, 6 };
    int k = 3;
    int n = sizeof(a) / sizeof(a[0]);

    // Initialize dp array with -1
    int dp[MAX][MAX];
    memset(dp, -1, sizeof dp);

    cout << maximizeSum(a, n, 0, k, dp);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the sum of
// the minimum of all the segments

class GFG
{

    static int MAX = 10;

    // Function to maximize the
    // sum of the minimums
    public static int maximizeSum(
              int[] a, int n, int ind,
                 int k, int[][] dp)
    {
        // If k segments have been divided
        if (k == 0)
        {
            // If we are at the end
            if (ind == n)
                return 0;

            // If we donot reach the end
            // then return a negative number
            // that cannot be the sum
            else
                return -1000000000;
        }

        // If at the end but
        // k segments are not formed
        else if (ind == n)
            return -1000000000;

        // If the state has not
        // been visited yet
        else if (dp[ind][k] != -1)
            return dp[ind][k];

        // If the state has
        // not been visited
        else
        {
            int ans = 0;

            // Get the minimum
            // element in the segment
            int mini = a[ind];

            // Iterate and try to break
            // at every index
            // and create a segment
            for (int i = ind; i < n; i++)
            {

                // Find the minimum element
                // in the segment
                mini = Math.min(mini, a[i]);

                // Find the sum of all the
                // segments trying all
                // the possible combinations
                ans = Math.max(ans,
                     maximizeSum(a, n, i + 1,
                           k - 1, dp) + mini);
            }

            // Return the answer by
            // memoizing it
            return dp[ind][k] = ans;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 5, 7, 4, 2, 8, 1, 6 };
        int k = 3;
        int n = a.length;

        // Initialize dp array with -1
        int[][] dp = new int[MAX][MAX];
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
                dp[i][j] = -1;
        }

        System.out.println(
          maximizeSum(a, n, 0, k, dp));
    }
}

// This code is contributed by
// sanjeev2552
```

## **蟒蛇 3**

```
# Python 3 program to find the sum of
# the minimum of all the segments
MAX = 10

# Function to maximize the
# sum of the minimums
def maximizeSum(a,n, ind, k, dp):
    # If k segments have been divided
    if (k == 0):
        # If we are at the end
        if (ind == n):
            return 0

        # If we donot reach the end
        # then return a negative number
        # that cannot be the sum
        else:
            return -1e9

    # If at the end but
    # k segments are not formed
    elif (ind == n):
        return -1e9

    # If the state has been visited already
    elif (dp[ind][k] != -1):
        return dp[ind][k]

    # If the state has not been visited
    else:
        ans = 0

        # Get the minimum element
        # in the segment
        mini = a[ind]

        # Iterate and try to break
        # at every index
        # and create a segment
        for i in range(ind,n,1):
            # Find the minimum element
            # in the segment
            mini = min(mini, a[i])

            # Find the sum of all the
            # segments trying all
            # the possible combinations
            ans = max(ans, maximizeSum(\
             a, n, i + 1, k - 1, dp) + mini)

        # Return the answer by
        # memoizing it
        dp[ind][k] = ans
        return ans

# Driver Code
if __name__ == '__main__':
    a = [5, 7, 4, 2, 1, 6]
    k = 3
    n = len(a)

    # Initialize dp array with -1
    dp = [[-1 for i in range(MAX)]\
          for j in range(MAX)]

    print(maximizeSum(a, n, 0, k, dp))

# This code is contributed by
# Surendra_Gangwar
```

## **C#**

```
// C# program to find the sum of
// the minimum of all the segments
using System;

class GFG
{
    static int MAX = 10;

    // Function to maximize the sum of the minimums
    public static int maximizeSum(
             int[] a, int n, int ind,
                  int k, int[] dp)
    {
        // If k segments have been divided
        if (k == 0)
        {
            // If we are at the end
            if (ind == n)
                return 0;

            // If we donot reach the end
            // then return a negative number
            // that cannot be the sum
            else
                return -1000000000;
        }

        // If at the end but
        // k segments are not formed
        else if (ind == n)
            return -1000000000;

        // If the state has not
        // been visited yet
        else if (dp[ind, k] != -1)
            return dp[ind, k];

        // If the state has not been visited
        else
        {
            int ans = 0;

            // Get the minimum element
            // in the segment
            int mini = a[ind];

            // Iterate and try to break
            // at every index
            // and create a segment
            for (int i = ind; i < n; i++)
            {

                // Find the minimum element
                // in the segment
                mini = Math.Min(mini, a[i]);

                // Find the sum of all the
                // segments trying all
                // the possible combinations
                ans = Math.Max(ans,
                      maximizeSum(a, n, i + 1,
                           k - 1, dp) + mini);
            }

            // Return the answer by
            // memoizing it
            return dp[ind,k] = ans;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 5, 7, 4, 2, 8, 1, 6 };
        int k = 3;
        int n = a.Length;

        // Initialize dp array with -1
        int[,] dp = new int[MAX, MAX];
        for (int i = 0; i < MAX; i++)
        {
            for (int j = 0; j < MAX; j++)
                dp[i, j] = -1;
        }

        Console.WriteLine(
          maximizeSum(a, n, 0, k, dp));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// JavaScript program to find the sum of
// the minimum of all the segments
    var MAX = 10;

    // Function to maximize the
    // sum of the minimums
    function maximizeSum(a , n , ind , k,  dp)
    {
        // If k segments have been divided
        if (k == 0) {
            // If we are at the end
            if (ind == n)
                return 0;

            // If we donot reach the end
            // then return a negative number
            // that cannot be the sum
            else
                return -1000000000;
        }

        // If at the end but
        // k segments are not formed
        else if (ind == n)
            return -1000000000;

        // If the state has not
        // been visited yet
        else if (dp[ind][k] != -1)
            return dp[ind][k];

        // If the state has
        // not been visited
        else {
            var ans = 0;

            // Get the minimum
            // element in the segment
            var mini = a[ind];

            // Iterate and try to break
            // at every index
            // and create a segment
            for (i = ind; i < n; i++) {

                // Find the minimum element
                // in the segment
                mini = Math.min(mini, a[i]);

                // Find the sum of all the
                // segments trying all
                // the possible combinations
                ans = Math.max(ans,
                maximizeSum(a, n, i + 1, k - 1, dp) + mini);
            }

            // Return the answer by
            // memoizing it
            return dp[ind][k] = ans;
        }
    }

    // Driver Code

        var a = [ 5, 7, 4, 2, 8, 1, 6 ];
        var k = 3;
        var n = a.length;

        // Initialize dp array with -1
        var dp =
        Array(MAX).fill().map(()=>Array(MAX).fill(0));
        for (var i = 0; i < MAX; i++) {
            for (j = 0; j < MAX; j++)
                dp[i][j] = -1;
        }

        document.write(maximizeSum(a, n, 0, k, dp));

// This code contributed by Rajput-Ji

</script>
```

****Output**

```
13
```** 

****时间复杂度**:O(N * N * K)
T3】辅助空间 : O(N * K)**