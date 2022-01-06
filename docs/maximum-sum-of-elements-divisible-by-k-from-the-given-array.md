# 给定数组中可被 K 整除的元素的最大和

> 原文:[https://www . geeksforgeeks . org/给定数组中元素的最大和可被 k 整除/](https://www.geeksforgeeks.org/maximum-sum-of-elements-divisible-by-k-from-the-given-array/)

给定一个整数数组和一个数字 K，任务是从给定的数组中找到可被 K 整除的最大和。
**例:**

> **输入:** arr[] = {3，6，5，1，8}，k = 3
> **输出:** 18
> **说明:** 18 由元素 3，6，1，8 构成。
> **输入:** arr = { 43，1，17，26，15 }，k = 16
> **输出:** 32
> **解释:** 32 由元素 17，15 构成。

**天真方法:**递归检查所有可能的组合，找到解决方案。该解决方案的时间复杂度为指数级，因此效率低下。
**高效方法:**通过维护*二维数组* **dp** 的动态编程方法，该数组存储变量和的状态和 **i** (其中**和**是当前和，I 是整数数组的第 I 个索引)。通过在所有元素上循环，计算包括索引 **i** 处的元素的和以及排除它，并检查是否可被 k 整除，如果是，则将它们的最大值存储在**DP【I】【和】**中并返回。
以下代码是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int dp[1001][1001];

// Function to return the maximum sum
// divisible by k from elements of v
int find_max(int i, int sum, vector<int>& v,int k)
{

    if (i == v.size())
        return 0;

    if (dp[i][sum] != -1)
        return dp[i][sum];

    int ans = 0;
    // check if sum of elements excluding the
    // current one is divisible by k
    if ((sum + find_max(i + 1, sum, v, k)) % k == 0)
        ans = find_max(i + 1, sum, v, k);

    // check if sum of elements including the
    // current one is divisible by k
    if((sum + v[i] + find_max(i + 1,(sum + v[i]) % k,
                                   v, k)) % k == 0)
        // Store the maximum
        ans = max(ans, v[i] + find_max(i + 1,
                            (sum + v[i]) % k,v, k));

    return dp[i][sum] = ans;
}

// Driver code
int main()
{
    vector<int> arr = { 43, 1, 17, 26, 15 };
    int k = 16;
    memset(dp, -1, sizeof(dp));
    cout << find_max(0, 0, arr, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG{

static int [][]dp = new int[1001][1001];

// Function to return the maximum sum
// divisible by k from elements of v
static int find_max(int i, int sum, int []v, int k)
{

    if (i == v.length)
        return 0;

    if (dp[i][sum] != -1)
        return dp[i][sum];

    int ans = 0;

    // check if sum of elements excluding the
    // current one is divisible by k
    if ((sum + find_max(i + 1, sum, v, k)) % k == 0)
        ans = find_max(i + 1, sum, v, k);

    // check if sum of elements including the
    // current one is divisible by k
    if((sum + v[i] + find_max(i + 1,(sum + v[i]) % k,
                                   v, k)) % k == 0)
        // Store the maximum
        ans = Math.max(ans, v[i] + find_max(i + 1,
                            (sum + v[i]) % k, v, k));

    return dp[i][sum] = ans;
}

// Driver code
public static void main(String[] args)
{
    int []arr = { 43, 1, 17, 26, 15 };
    int k = 16;
    for (int i = 0; i < 1001; i++)
        for (int j = 0; j < 1001; j++)
            dp[i][j] = -1;
    System.out.print(find_max(0, 0, arr, k));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation
dp = [[-1 for i in range(1001)] for j in range(1001)]

# Function to return the maximum sum
# divisible by k from elements of v
def find_max(i, sum, v, k):
    if (i == len(v)):
        return 0

    if (dp[i][sum] != -1):
        return dp[i][sum]

    ans = 0

    # check if sum of elements excluding the
    # current one is divisible by k
    if ((sum + find_max(i + 1, sum, v, k)) % k == 0):
        ans = find_max(i + 1, sum, v, k)

    # check if sum of elements including the
    # current one is divisible by k
    if((sum + v[i] + find_max(i + 1,(sum + v[i]) % k, v, k)) % k == 0):

        # Store the maximum
        ans = max(ans, v[i] + find_max(i + 1,(sum + v[i]) % k, v, k))

    dp[i][sum] = ans

    return dp[i][sum]

# Driver code
if __name__ == '__main__':
    arr = [43, 1, 17, 26, 15]
    k = 16
    print(find_max(0, 0, arr, k))

# This code is contributed by Surendra_Gangwar
```

## C#

```
using System;

class GFG{

static int [,]dp = new int[1001,1001];

// Function to return the maximum sum
// divisible by k from elements of v
static int find_max(int i, int sum, int []v, int k)
{

    if (i == v.Length)
        return 0;

    if (dp[i,sum] != -1)
        return dp[i,sum];

    int ans = 0;

    // check if sum of elements excluding the
    // current one is divisible by k
    if ((sum + find_max(i + 1, sum, v, k)) % k == 0)
        ans = find_max(i + 1, sum, v, k);

    // check if sum of elements including the
    // current one is divisible by k
    if((sum + v[i] + find_max(i + 1,(sum + v[i]) % k,
                                   v, k)) % k == 0)
        // Store the maximum
        ans = Math.Max(ans, v[i] + find_max(i + 1,
                            (sum + v[i]) % k, v, k));

    return dp[i, sum] = ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 43, 1, 17, 26, 15 };
    int k = 16;
    for (int i = 0; i < 1001; i++)
        for (int j = 0; j < 1001; j++)
            dp[i,j] = -1;
    Console.Write(find_max(0, 0, arr, k));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach
let dp = new Array(1000 + 1);

// Function to return the maximum sum
// divisible by k from elements of v
function find_max(i, sum, v, k)
{

    if (i == v.length)
        return 0;

    if (dp[i][sum] != -1)
        return dp[i][sum];

    let ans = 0;
    // check if sum of elements excluding the
    // current one is divisible by k
    if ((sum + find_max(i + 1, sum, v, k)) % k == 0)
        ans = find_max(i + 1, sum, v, k);

    // check if sum of elements including the
    // current one is divisible by k
    if((sum + v[i] + find_max(i + 1,(sum + v[i]) % k,
                                   v, k)) % k == 0)
        // Store the maximum
        ans = Math.max(ans, v[i] + find_max(i + 1,
                            (sum + v[i]) % k,v, k));

    return dp[i][sum] = ans;
}

// Driver Code
    let arr = [ 43, 1, 17, 26, 15 ];
    let k = 16;

    // Loop to create 2D array using 1D array
    for (var i = 0; i < dp.length; i++) {
        dp[i] = new Array(2);
    }

    for (var i = 0; i < dp.length; i++) {
        for (var j = 0; j < dp.length; j++) {

            dp[i][j] = -1;
        }
    }

    document.write(find_max(0, 0, arr, k));

    // This code is contributed by Dharanendra L V.
</script>
```

**Output**

```
32
```

**使用自上而下 dp 的迭代实现:**

我们将使用指数和模量值作为 dp 的状态。dp[i][j]将存储数组的最大和，直到模数为 j 的第 I 个索引。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int k=16;
    vector<int>arr={ 43, 1, 17, 26, 15 } ;
    int n=arr.size();
    vector<vector<int>> dp(n+2, vector<int>(k, 0));
    for (int i = 1; i <= n; i++) {

        for (int j = 0; j < k ; j++) {
            dp[i][j] = dp[i - 1][j];
        }

        dp[i][arr[i - 1] % k] = max(dp[i][arr[i - 1] % k], arr[i - 1]);

        for (int j = 0; j < k; j++) {
            int m = (j + arr[i - 1]) % k;
            if (dp[i - 1][j] != 0)
                dp[i][m] = max(dp[i][m],arr[i - 1] + dp[i - 1][j]);
        }

    }
    cout <<dp[n][0];
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG {

    public static void main(String[] args)
    {
        int k = 16;
        int[] arr = { 43, 1, 17, 26, 15 };
        int n = arr.length;
        int[][] dp = new int[n + 2][k];
        for (int i = 1; i <= n; i++) {

            for (int j = 0; j < k; j++) {
                dp[i][j] = dp[i - 1][j];
            }

            dp[i][arr[i - 1] % k] = Math.max(
                dp[i][arr[i - 1] % k], arr[i - 1]);

            for (int j = 0; j < k; j++) {
                int m = (j + arr[i - 1]) % k;
                if (dp[i - 1][j] != 0)
                    dp[i][m] = Math.max(dp[i][m],
                                        arr[i - 1]
                                            + dp[i - 1][j]);
            }
        }
        System.out.print(dp[n][0]);
    }
}

// This code is contributed by ukasp.
```

## 蟒蛇 3

```
k = 16
arr = [ 43, 1, 17, 26, 15 ]
n = len(arr)
dp = [[0 for i in range(k)] for j in range(n+2)]
for i in range(1, n+1):
    for j in range(k):
        dp[i][j] = dp[i - 1][j]

    dp[i][arr[i - 1] % k] = max(dp[i][arr[i - 1] % k], arr[i - 1])

    for j in range(k):
        m = (j + arr[i - 1]) % k
        if dp[i - 1][j] != 0:
            dp[i][m] = max(dp[i][m],arr[i - 1] + dp[i - 1][j])

print(dp[n][0])

# This code is contributed by suresh07.
```

## C#

```
using System;
class GFG {
  static void Main() {
    int k = 16;
    int[] arr = { 43, 1, 17, 26, 15 };
    int n = arr.Length;
    int[,] dp = new int[n + 2, k];
    for (int i = 1; i <= n; i++) {

        for (int j = 0; j < k ; j++) {
            dp[i,j] = dp[i - 1,j];
        }

        dp[i,arr[i - 1] % k] = Math.Max(dp[i,arr[i - 1] % k], arr[i - 1]);

        for (int j = 0; j < k; j++) {
            int m = (j + arr[i - 1]) % k;
            if (dp[i - 1,j] != 0)
                dp[i,m] = Math.Max(dp[i,m],arr[i - 1] + dp[i - 1,j]);
        }
    }
    Console.Write(dp[n,0]);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    let k = 16;
    let arr = [ 43, 1, 17, 26, 15 ] ;
    let n = arr.length;
    let dp = new Array(n+2);
    for(let i = 0; i < n+2; i++)
    {
        dp[i] = new Array(k);
        for(let j = 0; j < k; j++)
        {
            dp[i][j] = 0;
        }
    }
    for (let i = 1; i <= n; i++) {

        for (let j = 0; j < k ; j++) {
            dp[i][j] = dp[i - 1][j];
        }

        dp[i][arr[i - 1] % k] = Math.max(dp[i][arr[i - 1] % k], arr[i - 1]);

        for (let j = 0; j < k; j++) {
            let m = (j + arr[i - 1]) % k;
            if (dp[i - 1][j] != 0)
                dp[i][m] = Math.max(dp[i][m],arr[i - 1] + dp[i - 1][j]);
        }

    }
    document.write(dp[n][0]);

    // This code is contributed by mukesh07.
</script>
```

**Output**

```
32
```