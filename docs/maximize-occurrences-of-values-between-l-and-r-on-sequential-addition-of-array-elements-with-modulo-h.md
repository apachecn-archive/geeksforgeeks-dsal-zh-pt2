# 通过以 H 为模的数组元素的顺序相加，最大化 L 和 R 之间值的出现

> 原文:[https://www . geeksforgeeks . org/以模 h 对数组元素进行顺序加法时最大化 l 和 r 之间的值出现次数/](https://www.geeksforgeeks.org/maximize-occurrences-of-values-between-l-and-r-on-sequential-addition-of-array-elements-with-modulo-h/)

给定一个具有 **N** 正整数和一个 **H** 正整数的数组 **arr[]** ，任务是在添加 **arr[i]** 或**arr[I]–1**到 **X** (初始为 0)时，计算范围内某个值的最大出现次数。整数 **X** 必须始终小于 **H** 。如果大于 **H** ，用 **X % H** 代替 **X**

**示例:**

> **输入:** arr = {16，17，14，20，20，11，22}，H = 24，L = 21，R = 23
> **输出:** 3
> **解释:**
> 最初 X = 0。
> 然后将 arr[0]–1 加到 X 上，现在 X 是 15。这个 X 不好。
> 然后把 arr[1]–1 加到 X 上，现在 X 是 15 + 16 = 31。31 % H = 7。这个 X 也不好。
> 然后把 arr[2]加到 X 上，现在 X 是 7 + 14 = 21。这个 X 不错。
> 然后把 arr[3]–1 加到 X 上，现在 X 是(21 + 19) % H = 16。这个 X 不好。
> 然后把 arr[4]加到 X 上，现在 X 是(16 + 20) % H = 12。这个 X 不好。
> 然后把 arr[5]加到 X 上，现在 X 是 12 + 11 = 23。这个 X 不错。
> 然后把 arr[6]加到 X 上，现在 X 是 23 + 22 = 21。这个 X 也不错。
> 那么，例子中的好 X 的最大个数是 3。
> 
> **输入:** arr = {1，2，3}，H = 5，L = 1，R = 2
> T3】输出: 2

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。维护一个表**DP【N+1】【H】**，该表代表一个元素在添加到 **i** 元素时在范围【L，R】内的最大出现次数。对于每个 **i <sup>th</sup>** 指数，通过将 arr[i]和 arr[I]–1 相加，计算可获得的最大可能频率。一旦计算出所有指数，从 **dp[][]** 矩阵的最后一行找到最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach
#include <bits/stdc++.h>
using namespace std;

// Function that prints the number
// of times X gets a value
// between L and R
void goodInteger(int arr[], int n,
                 int h, int l, int r)
{

    vector<vector<int> > dp(
        n + 1,
        vector<int>(h, -1));

    // Base condition
    dp[0][0] = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < h; j++) {

            // Condition if X can be made
            // equal to j after i additions
            if (dp[i][j] != -1) {

                // Compute value of X
                // after adding arr[i]
                int h1 = (j + arr[i]) % h;

                // Compute value of X after
                // adding arr[i] - 1
                int h2 = (j + arr[i] - 1) % h;

                // Update dp as the maximum value
                dp[i + 1][h1]
                    = max(dp[i + 1][h1],
                          dp[i][j]
                              + (h1 >= l
                                 && h1 <= r));
                dp[i + 1][h2]
                    = max(dp[i + 1][h2],
                          dp[i][j]
                              + (h2 >= l
                                 && h2 <= r));
            }
        }
    }

    int ans = 0;

    // Compute maximum answer from all
    // possible cases
    for (int i = 0; i < h; i++) {
        if (dp[n][i] != -1)
            ans = max(ans, dp[n][i]);
    }

    // Printing maximum good occurrence of X
    cout << ans << "\n";
}

// Driver Code
int main()
{

    int A[] = { 16, 17, 14, 20, 20, 11, 22 };
    int H = 24;
    int L = 21;
    int R = 23;

    int size = sizeof(A) / sizeof(A[0]);

    goodInteger(A, size, H, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

// Function that prints the number
// of times X gets a value
// between L and R
static void goodInteger(int arr[], int n,
                        int h, int l, int r)
{
    int [][]dp = new int[n + 1][h];
    for(int i = 0; i < n; i++)
        for(int j = 0; j < h; j++)
            dp[i][j] = -1;

    // Base condition
    dp[0][0] = 0;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < h; j++)
        {

            // Condition if X can be made
            // equal to j after i additions
            if (dp[i][j] != -1)
            {

                // Compute value of X
                // after adding arr[i]
                int h1 = (j + arr[i]) % h;

                // Compute value of X after
                // adding arr[i] - 1
                int h2 = (j + arr[i] - 1) % h;

                // Update dp as the maximum value
                dp[i + 1][h1] = Math.max(dp[i + 1][h1],
                                         dp[i][j] +
                                        ((h1 >= l &&
                                          h1 <= r) ?
                                           1 : 0));
                dp[i + 1][h2] = Math.max(dp[i + 1][h2],
                                         dp[i][j] +
                                        ((h2 >= l &&
                                          h2 <= r) ?
                                           1 : 0));
            }
        }
    }
    int ans = 0;

    // Compute maximum answer from all
    // possible cases
    for(int i = 0; i < h; i++)
    {
        if (dp[n][i] != -1)
            ans = Math.max(ans, dp[n][i]);
    }

    // Printing maximum good occurrence of X
    System.out.print(ans + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 16, 17, 14, 20, 20, 11, 22 };
    int H = 24;
    int L = 21;
    int R = 23;

    int size = A.length;

    goodInteger(A, size, H, L, R);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function that prints the number
# of times X gets a value
# between L and R
def goodInteger(arr, n, h, l, r):

    dp = [[-1 for i in range(h)]
              for j in range(n + 1)]

    # Base condition
    dp[0][0] = 0

    for i in range(n):
        for j in range(h):

            # Condition if X can be made
            # equal to j after i additions
            if(dp[i][j] != -1):

                # Compute value of X
                # after adding arr[i]
                h1 = (j + arr[i]) % h

                # Compute value of X after
                # adding arr[i] - 1
                h2 = (j + arr[i] - 1) % h

                # Update dp as the maximum value
                dp[i + 1][h1] = max(dp[i + 1][h1],
                                    dp[i][j] +
                                    (h1 >= l and h1 <= r))

                dp[i + 1][h2] = max(dp[i + 1][h2],
                                    dp[i][j] +
                                    (h2 >= l and h2 <= r))
    ans = 0

    # Compute maximum answer from all
    # possible cases
    for i in range(h):
        if(dp[n][i] != -1):
            ans = max(ans, dp[n][i])

    # Printing maximum good occurrence of X
    print(ans)

# Driver Code
if __name__ == '__main__':

    A = [ 16, 17, 14, 20, 20, 11, 22 ]
    H = 24
    L = 21
    R = 23

    size = len(A)
    goodInteger(A, size, H, L, R)

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function that prints the number
// of times X gets a value
// between L and R
static void goodint(int []arr, int n,
                    int h, int l, int r)
{
    int [,]dp = new int[n + 1, h];

    for(int i = 0; i < n; i++)
        for(int j = 0; j < h; j++)
            dp[i, j] = -1;

    // Base condition
    dp[0, 0] = 0;

    for(int i = 0; i < n; i++)
    {
        for(int j = 0; j < h; j++)
        {

            // Condition if X can be made
            // equal to j after i additions
            if (dp[i, j] != -1)
            {

                // Compute value of X
                // after adding arr[i]
                int h1 = (j + arr[i]) % h;

                // Compute value of X after
                // adding arr[i] - 1
                int h2 = (j + arr[i] - 1) % h;

                // Update dp as the maximum value
                dp[i + 1, h1] = Math.Max(dp[i + 1, h1],
                                         dp[i, j] +
                                        ((h1 >= l &&
                                          h1 <= r) ?
                                           1 : 0));
                dp[i + 1, h2] = Math.Max(dp[i + 1, h2],
                                         dp[i, j] +
                                        ((h2 >= l &&
                                          h2 <= r) ?
                                           1 : 0));
            }
        }
    }
    int ans = 0;

    // Compute maximum answer from all
    // possible cases
    for(int i = 0; i < h; i++)
    {
        if (dp[n, i] != -1)
            ans = Math.Max(ans, dp[n, i]);
    }

    // Printing maximum good occurrence of X
    Console.Write(ans + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 16, 17, 14, 20, 20, 11, 22 };
    int H = 24;
    int L = 21;
    int R = 23;

    int size = A.Length;

    goodint(A, size, H, L, R);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function that prlets the number
// of times X gets a value
// between L and R
function goodLeteger(arr, n, h, l, r)
{
    let dp = new Array(n + 1);
    for(var i = 0; i < dp.length; i++)
    {
        dp[i] = new Array(2);
    }

    for(let i = 0; i < n+1; i++)
        for(let j = 0; j < h; j++)
            dp[i][j] = -1;

    // Base condition
    dp[0][0] = 0;

    for(let i = 0; i < n; i++)
    {
        for(let j = 0; j < h; j++)
        {

            // Condition if X can be made
            // equal to j after i additions
            if (dp[i][j] != -1)
            {

                // Compute value of X
                // after adding arr[i]
                let h1 = (j + arr[i]) % h;

                // Compute value of X after
                // adding arr[i] - 1
                let h2 = (j + arr[i] - 1) % h;

                // Update dp as the maximum value
                dp[i + 1][h1] = Math.max(dp[i + 1][h1],
                                         dp[i][j] +
                                        ((h1 >= l &&
                                          h1 <= r) ?
                                           1 : 0));
                dp[i + 1][h2] = Math.max(dp[i + 1][h2],
                                         dp[i][j] +
                                        ((h2 >= l &&
                                          h2 <= r) ?
                                           1 : 0));
            }
        }
    }
    let ans = 0;

    // Compute maximum answer from all
    // possible cases
    for(let i = 0; i < h; i++)
    {
        if (dp[n][i] != -1)
            ans = Math.max(ans, dp[n][i]);
    }

    // Printing maximum good occurrence of X
    document.write(ans + "\n");
}

// Driver Code
let A = [ 16, 17, 14, 20, 20, 11, 22 ];
let H = 24;
let L = 21;
let R = 23;

let size = A.length;

goodLeteger(A, size, H, L, R);

// This code is contributed by sanjoy_62

</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N * H)*