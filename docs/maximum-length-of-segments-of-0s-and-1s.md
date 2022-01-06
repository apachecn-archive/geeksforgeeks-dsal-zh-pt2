# 0 和 1 的线段最大长度

> 原文:[https://www . geeksforgeeks . org/最大段长度-0 和-1/](https://www.geeksforgeeks.org/maximum-length-of-segments-of-0s-and-1s/)

给定由 1 和 0 组成的字符串。任务是找到字符串段的最大长度，使得每个段中的数字 1 大于 0。
**注:**拍摄的每一段都要鲜明。索引从 0 开始。
**示例:**

> **输入:**str = " 100110001010001 "
> **输出:** 9
> 第一段从索引 0 到 4 (10011)，总长度= 5
> 第二段从索引 8 到 10 (101)，总长度= 3
> 第三段从索引 14 到 14 (1)，总长度= 1，
> 因此答案为 5 + 3 + 1 = 9
> **输入:**

**进场:**

1.  如果 start == n，限制条件出现，返回 0。
2.  从开始到 n 运行一个循环，计算每个子阵列直到 n。
3.  如果字符为 1，则增加 1 的计数，否则增加 0 的计数。
4.  如果计数 1 大于 0，递归调用索引(k+1)的函数，即下一个索引，并添加剩余长度，即 k-start+1。
5.  否则只递归调用下一个索引 k+1 的函数。
6.  返回 DP[开始]。

**以下是上述方法的实施:**

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Recursive Function to find total length of the array
// Where 1 is greater than zero
int find(int start, string adj, int n, int dp[])
{
    // If reaches till end
    if (start == n)
        return 0;

    // If dp is saved
    if (dp[start] != -1)
        return dp[start];

    dp[start] = 0;
    int one = 0, zero = 0, k;

    // Finding for each length
    for (k = start; k < n; k++) {

        // If the character scanned is 1
        if (adj[k] == '1')
            one++;
        else
            zero++;

        // If one is greater than zero, add total
        // length scanned till now
        if (one > zero)
            dp[start] = max(dp[start], find(k + 1, adj, n, dp)
                                           + k - start + 1);

        // Continue with next length
        else
            dp[start] = max(dp[start], find(k + 1, adj, n, dp));
    }

    // Return the value for start index
    return dp[start];
}

// Driver Code
int main()
{
    string adj = "100110001010001";

    // Size of string
    int n = adj.size();
    int dp[n + 1];
    memset(dp, -1, sizeof(dp));
    // Calling the function to find the value of function

    cout << find(0, adj, n, dp) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// above approach
import java.util.*;
import java.lang.Math;

class GFG
{
// Recursive Function to find
// total length of the array
// Where 1 is greater than zero
public static int find(int start, String adj,
                       int n, int dp[])
{

    // If reaches till end
    if (start == n)
        return 0;

    // If dp is saved
    if (dp[start] != -1)
        return dp[start];

    dp[start] = 0;
    int one = 0, zero = 0, k;

    // Finding for each length
    for (k = start; k < n; k++)
    {

        // If the character scanned is 1
        if (adj.charAt(k) == '1')
            one++;
        else
            zero++;

        // If one is greater than
        // zero, add total length
        // scanned till now
        if (one > zero)
            dp[start] = Math.max(dp[start],
                            find(k + 1, adj, n, dp) +
                                 k - start + 1);

        // Continue with next length
        else
            dp[start] = Math.max(dp[start],
                            find(k + 1, adj, n, dp));
    }

    return dp[start];
}

// Driver code
public static void main (String[] args)
{
    String adj = "100110001010001";

    // Size of string
    int n = adj.length();
    int dp[] = new int[n + 1];
    Arrays.fill(dp, -1);

        // Calling the function to find
        // the value of function
        System.out.println(find(0, adj, n, dp));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Recursive Function to find total length
# of the array where 1 is greater than zero
def find(start, adj, n, dp):

    # If reaches till end
    if (start == n):
        return 0

    # If dp is saved
    if (dp[start] != -1):
        return dp[start]

    dp[start] = 0
    one = 0
    zero = 0

    # Finding for each length
    for k in range(start, n, 1):

        # If the character scanned is 1
        if (adj[k] == '1'):
            one += 1
        else:
            zero += 1

        # If one is greater than zero, add
        # total length scanned till now
        if (one > zero):
            dp[start] = max(dp[start],
                            find(k + 1, adj, n, dp) +
                                 k - start + 1)

        # Continue with next length
        else:
            dp[start] = max(dp[start],
                            find(k + 1, adj, n, dp))

    # Return the value for start index
    return dp[start]

# Driver Code
if __name__ == '__main__':
    adj = "100110001010001"

    # Size of string
    n = len(adj)
    dp = [-1 for i in range(n + 1)]

    # Calling the function to find the
    # value of function
    print(find(0, adj, n, dp))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{
    // Recursive Function to find total length of the array
    // Where 1 is greater than zero
    public static int find(int start, string adj, int n, int[] dp)
    {
        // If reaches till end
        if (start == n)
            return 0;

        // If dp is saved
        if (dp[start] != -1)
            return dp[start];

        dp[start] = 0;
        int one = 0, zero = 0, k;

        // Finding for each length
        for (k = start; k < n; k++) {

            // If the character scanned is 1
            if (adj[k] == '1')
                one++;
            else
                zero++;

            // If one is greater than zero, add total
            // length scanned till now
            if (one > zero)
                dp[start] = Math.Max(dp[start], find(k + 1, adj, n, dp)
                                               + k - start + 1);

            // Continue with next length
            else
                dp[start] = Math.Max(dp[start], find(k + 1, adj, n, dp));
        }

        // Return the value for start index
        return dp[start];
    }

    // Driver Code
    static void Main()
    {
        string adj = "100110001010001";

        // Size of string
        int n = adj.Length;
        int[] dp = new int[n + 1];
        for(int i = 0; i <= n; i++)
            dp[i] = -1;
        // Calling the function to find the value of function

        Console.Write(find(0, adj, n, dp) + "\n");
    }
    //This code is contributed by DrRoot_
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of above approach

// Recursive Function to find total length
// of the array where 1 is greater than zero
function find($start, $adj, $n, $dp)
{

    // If reaches till end
    if ($start == $n)
        return 0;

    // If $dp is saved
    if ($dp[$start] != -1)
        return $dp[$start];

    $dp[$start] = 0;
    $one = 0;
    $zero = 0;

    // Finding for each length
    for ($k = $start; $k < $n; $k++)
    {

        // If the character scanned is 1
        if ($adj[$k] == '1')
            $one++;
        else
            $zero++;

        // If one is greater than zero, add total
        // length scanned till now
        if ($one > $zero)
            $dp[$start] = max($dp[$start],
                         find($k + 1, $adj, $n, $dp) +
                              $k - $start + 1);

        // Continue with next length
        else
            $dp[$start] = max($dp[$start],
                         find($k + 1, $adj, $n, $dp));
    }

    // Return the value for $start index
    return $dp[$start];
}

// Driver Code
$adj = "100110001010001";

// Size of string
$n = strlen($adj);
$dp = array_fill(0, $n + 1, -1);

// Calling the function
// to find the value of function
echo find(0, $adj, $n, $dp);

// This code is contributed by ihritik
?>
```

## java 描述语言

```
<script>
// javascript implementation of
// above approach

    // Recursive Function to find
    // total length of the array
    // Where 1 is greater than zero
    function find(start,  adj , n , dp) {

        // If reaches till end
        if (start == n)
            return 0;

        // If dp is saved
        if (dp[start] != -1)
            return dp[start];

        dp[start] = 0;
        var one = 0, zero = 0, k;

        // Finding for each length
        for (k = start; k < n; k++) {

            // If the character scanned is 1
            if (adj[k] == '1')
                one++;
            else
                zero++;

            // If one is greater than
            // zero, add total length
            // scanned till now
            if (one > zero)
                dp[start] = Math.max(dp[start], find(k + 1, adj, n, dp) + k - start + 1);

            // Continue with next length
            else
                dp[start] = Math.max(dp[start], find(k + 1, adj, n, dp));
        }

        return dp[start];
    }

    // Driver code
        var adj = "100110001010001";

        // Size of string
        var n = adj.length;
        var dp = Array(n + 1).fill(-1);

        // Calling the function to find
        // the value of function
        document.write(find(0, adj, n, dp));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
9
```