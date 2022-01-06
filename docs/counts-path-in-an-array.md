# 计算数组中的路径

> 原文:[https://www.geeksforgeeks.org/counts-path-in-an-array/](https://www.geeksforgeeks.org/counts-path-in-an-array/)

给定一个由正整数组成的数组**，数组大小为 **N** 。如果数组中索引 **i** 处的元素是 **K** ，那么您可以在索引范围 **(i + 1)** 到 **(i + K)** 之间跳转。
任务是找到数个可能的方法，用模块 **10 <sup>9</sup> + 7** 到达终点。
起始位置视为索引 **0** 。
**例:**** 

> ****输入:** A = {5，3，1，4，3}
> **输出:** 6
> **输入:** A = {2，3，1，1，2}
> **输出:** 4**

****天真方法:**我们可以形成递归结构来解决问题。
让 F[i]表示从索引 **i** 开始的路径数，在每个索引 **i** 如果元素 **A[i]** 是 **K** ，那么可以执行跳转的总路径数是:** 

```
F(i) = F(i+1) + F(i+2) +...+ F(i+k), where i + k <= n, 
where F(n) = 1
```

**通过使用这个递归公式，我们可以解决这个问题:** 

## **C++**

```
// C++ implementation of
// the above approach
#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// Find the number of ways
// to reach the end
int ways(int i, int arr[], int n)
{
    // Base case
    if (i == n - 1)
        return 1;

    int sum = 0;

    // Recursive structure
    for (int j = 1;
         j + i < n && j <= arr[i];
         j++) {
        sum += (ways(i + j,
                     arr, n))
               % mod;
        sum %= mod;
    }

    return sum % mod;
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 1, 4, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << ways(0, arr, n) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of
// the above approach
import java.io.*;

class GFG
{
static int mod = 1000000000;

// Find the number of ways
// to reach the end
static int ways(int i,
                int arr[], int n)
{
    // Base case
    if (i == n - 1)
        return 1;

    int sum = 0;

    // Recursive structure
    for (int j = 1; j + i < n &&
                    j <= arr[i]; j++)
    {
        sum += (ways(i + j,
                     arr, n)) % mod;
        sum %= mod;
    }
    return sum % mod;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 5, 3, 1, 4, 3 };

    int n = arr.length;

    System.out.println (ways(0, arr, n));
}
}

// This code is contributed by ajit
```

## **蟒蛇 3**

```
# Python3 implementation of
# the above approach

mod = 1e9 + 7;

# Find the number of ways
# to reach the end
def ways(i, arr, n):

    # Base case
    if (i == n - 1):
        return 1;

    sum = 0;

    # Recursive structure
    for j in range(1, arr[i] + 1):
        if(i + j < n):
            sum += (ways(i + j, arr, n)) % mod;
            sum %= mod;

    return int(sum % mod);

# Driver code
if __name__ == '__main__':
    arr = [5, 3, 1, 4, 3];

    n = len(arr);

    print(ways(0, arr, n));

# This code is contributed by PrinciRaj1992
```

## **C#**

```
// C# implementation of
// the above approach
using System;

class GFG
{
static int mod = 1000000000;

// Find the number of ways
// to reach the end
static int ways(int i,
                int []arr, int n)
{
    // Base case
    if (i == n - 1)
        return 1;

    int sum = 0;

    // Recursive structure
    for (int j = 1; j + i < n &&
                    j <= arr[i]; j++)
    {
        sum += (ways(i + j,
                     arr, n)) % mod;
        sum %= mod;
    }
    return sum % mod;
}

// Driver code
public static void Main (String[] args)
{
    int []arr = { 5, 3, 1, 4, 3 };

    int n = arr.Length;

    Console.WriteLine(ways(0, arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
    // Javascript implementation of the above approach

    let mod = 1000000000;

    // Find the number of ways
    // to reach the end
    function ways(i, arr, n)
    {
        // Base case
        if (i == n - 1)
            return 1;

        let sum = 0;

        // Recursive structure
        for (let j = 1; j + i < n && j <= arr[i]; j++)
        {
            sum += (ways(i + j, arr, n)) % mod;
            sum %= mod;
        }
        return sum % mod;
    }

    let arr = [ 5, 3, 1, 4, 3 ];

    let n = arr.length;

    document.write(ways(0, arr, n));

</script>
```

****Output:** 

```
6
```** 

****高效方法:**在前面的方法中，有些计算不止一次进行。最好将这些值存储在 dp 数组中，dp[i]将存储从索引 **i** 开始到数组末尾的路径数。
因此 dp[0]将是问题的解决方案。
以下是实施办法:** 

## **C++**

```
// C++ implementation
#include <bits/stdc++.h>
using namespace std;

const int mod = 1e9 + 7;

// find the number of ways to reach the end
int ways(int arr[], int n)
{
    // dp to store value
    int dp[n + 1];

    // base case
    dp[n - 1] = 1;

    // Bottom up dp structure
    for (int i = n - 2; i >= 0; i--) {
        dp[i] = 0;

        // F[i] is dependent of
        // F[i+1] to F[i+k]
        for (int j = 1; ((j + i) < n
                         && j <= arr[i]);
             j++) {
            dp[i] += dp[i + j];
            dp[i] %= mod;
        }
    }

    // Return value of dp[0]
    return dp[0] % mod;
}

// Driver code
int main()
{
    int arr[] = { 5, 3, 1, 4, 3 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << ways(arr, n) % mod << endl;
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of above approach
class GFG
{
    static final int mod = (int)(1e9 + 7);

    // find the number of ways to reach the end
    static int ways(int arr[], int n)
    {
        // dp to store value
        int dp[] = new int[n + 1];

        // base case
        dp[n - 1] = 1;

        // Bottom up dp structure
        for (int i = n - 2; i >= 0; i--)
        {
            dp[i] = 0;

            // F[i] is dependent of
            // F[i+1] to F[i+k]
            for (int j = 1; ((j + i) < n &&
                              j <= arr[i]); j++)
            {
                dp[i] += dp[i + j];
                dp[i] %= mod;
            }
        }

        // Return value of dp[0]
        return dp[0] % mod;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 5, 3, 1, 4, 3 };

        int n = arr.length;

        System.out.println(ways(arr, n) % mod);
    }
}

// This code is contributed by AnkitRai01
```

## **蟒蛇 3**

```
# Python3 implementation of above approach
mod = 10**9 + 7

# find the number of ways to reach the end
def ways(arr, n):

    # dp to store value
    dp = [0] * (n + 1)

    # base case
    dp[n - 1] = 1

    # Bottom up dp structure
    for i in range(n - 2, -1, -1):
        dp[i] = 0

        # F[i] is dependent of
        # F[i + 1] to F[i + k]
        j = 1
        while((j + i) < n and j <= arr[i]):
            dp[i] += dp[i + j]
            dp[i] %= mod
            j += 1

    # Return value of dp[0]
    return dp[0] % mod

# Driver code
arr = [5, 3, 1, 4, 3 ]
n = len(arr)
print(ways(arr, n) % mod)

# This code is contributed by SHUBHAMSINGH10
```

## **C#**

```
// C# implementation of above approach
using System;

class GFG
{
    static readonly int mod = (int)(1e9 + 7);

    // find the number of ways to reach the end
    static int ways(int []arr, int n)
    {
        // dp to store value
        int []dp = new int[n + 1];

        // base case
        dp[n - 1] = 1;

        // Bottom up dp structure
        for (int i = n - 2; i >= 0; i--)
        {
            dp[i] = 0;

            // F[i] is dependent of
            // F[i+1] to F[i+k]
            for (int j = 1; ((j + i) < n &&
                              j <= arr[i]); j++)
            {
                dp[i] += dp[i + j];
                dp[i] %= mod;
            }
        }

        // Return value of dp[0]
        return dp[0] % mod;
    }

    // Driver code
    public static void Main (String[] args)
    {
        int []arr = { 5, 3, 1, 4, 3 };

        int n = arr.Length;

        Console.WriteLine(ways(arr, n) % mod);
    }
}

// This code is contributed by Rajput-Ji
```

## **java 描述语言**

```
<script>

    // Javascript implementation
    // of above approach

    let mod = (1e9 + 7);

    // find the number of ways
    // to reach the end
    function ways(arr, n)
    {
        // dp to store value
        let dp = new Array(n + 1);
        dp.fill(0);

        // base case
        dp[n - 1] = 1;

        // Bottom up dp structure
        for (let i = n - 2; i >= 0; i--)
        {
            dp[i] = 0;

            // F[i] is dependent of
            // F[i+1] to F[i+k]
            for (let j = 1; ((j + i)
            < n && j <= arr[i]); j++)
            {
                dp[i] += dp[i + j];
                dp[i] %= mod;
            }
        }

        // Return value of dp[0]
        return dp[0] % mod;
    }

    let arr = [ 5, 3, 1, 4, 3 ];

    let n = arr.length;

    document.write(ways(arr, n) % mod);

</script>
```

****Output:** 

```
6
```** 

****时间复杂度:** O(K)**