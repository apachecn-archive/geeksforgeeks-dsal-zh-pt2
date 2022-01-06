# 求 N 的最大因子，使 N/F 小于 K

> 原文:[https://www . geesforgeks . org/find-最大因子 n-so-n-f-小于-k/](https://www.geeksforgeeks.org/find-largest-factor-of-n-such-that-n-f-is-less-than-k/)

给定两个数字 **N** 和 **K** ，任务是找到最小值 **X** ，使得 **N < X*K** 。

**示例:**

> **输入:** N = 8，K = 7
> **输出:** 2
> **说明:**
> 小于 K 被 N 整除的数是 1、2、4。
> 所以 X 的最小值是 2，这样 8 < 2*7 = 14。
> **输入:**N = 9999999733，K = 999999732
> **输出:**99999999733
> **说明:**
> 由于 9999999733 是素数，所以 99999733 可以被 1 和数字本身整除。因为 K 小于 999999733。
> 所以 X 的最小值是 9999999733 这样 99999733<9999999733 * 99999732。

**天真方法:**给定的问题陈述可以可视化为方程 **K * X = N** 。在这个等式中，目标是最小化 x。所以我们必须找到除以 N 的**最大值 K。以下是步骤:**

*   迭代**【1，K】**。
*   检查每个数字 **i** ，使得 **(N % i) = 0** 。继续更新**最大值**变量，该变量存储了 **N 遍历到 i** 的最大除数。
*   要求的答案是 **N/max** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the value of X
void findMaxValue(int N, int K)
{
    int packages;
    int maxi = 1;

    // Loop to check all the numbers
    // divisible by N that yield
    // minimum N/i value
    for (int i = 1; i <= K; i++) {
        if (N % i == 0)
            maxi = max(maxi, i);
    }

    packages = N / maxi;

    // Print the value of packages
    cout << packages << endl;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 8, K = 7;

    // Function Call
    findMaxValue(N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG{

// Function to find the value of X
static void findMaxValue(int N, int K)
{
    int packages;
    int maxi = 1;

    // Loop to check all the numbers
    // divisible by N that yield
    // minimum N/i value
    for(int i = 1; i <= K; i++)
    {
        if (N % i == 0)
            maxi = Math.max(maxi, i);
    }
    packages = N / maxi;

    // Print the value of packages
    System.out.println(packages);
}

// Driver code
public static void main (String[] args)
{

    // Given N and K
    int N = 8, K = 7;

    // Function call
    findMaxValue(N, K);
}
}

// This code is contributed by Shubham Prakash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the value of X
def findMaxValue(N, K):
    packages = 0;
    maxi = 1;

    # Loop to check all the numbers
    # divisible by N that yield
    # minimum N/i value
    for i in range(1, K + 1):
        if (N % i == 0):
            maxi = max(maxi, i);

    packages = N // maxi;

    # Print value of packages
    print(packages);

# Driver code
if __name__ == '__main__':

    # Given N and K
    N = 8;
    K = 7;

    # Function call
    findMaxValue(N, K);

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the value of X
static void findMaxValue(int N, int K)
{
    int packages;
    int maxi = 1;

    // Loop to check all the numbers
    // divisible by N that yield
    // minimum N/i value
    for(int i = 1; i <= K; i++)
    {
        if (N % i == 0)
            maxi = Math.Max(maxi, i);
    }
    packages = N / maxi;

    // Print the value of packages
    Console.WriteLine(packages);
}

// Driver code
public static void Main(String[] args)
{

    // Given N and K
    int N = 8, K = 7;

    // Function call
    findMaxValue(N, K);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the value of X
function findMaxValue(N, K)
{
    let packages;
    let maxi = 1;

    // Loop to check all the numbers
    // divisible by N that yield
    // minimum N/i value
    for (let i = 1; i <= K; i++) {
        if (N % i == 0)
            maxi = Math.max(maxi, i);
    }

    packages = parseInt(N / maxi);

    // Print the value of packages
    document.write(packages);
}

// Driver Code
// Given N and K
let N = 8, K = 7;

// Function Call
findMaxValue(N, K);

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(K)*
***辅助空间:** O(1)*

**有效方法:**为了优化上述方法，我们将使用[这篇](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)文章中讨论的有效方法来找到该因素。以下是步骤:

1.  初始化**和**变量，存储 **N** 的最大因子。
2.  迭代**【1，sqrt(N)】**并执行以下操作:
    *   检查 **N** 是否可以被 **i** 整除。
    *   如果没有，那么检查下一个号码。
    *   否则，如果 **i ≤ K** 和 **N/i ≤ K** ，则更新 **ans** 至最大值 **(i，N/i)** 。
3.  **X** 的值将为 **N/ans。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to find the largest
// factor of N which is less than
// or equal to K
int solve(int n, int k)
{
    // Initialise the variable to
    // store the largest factor of
    // N <= K
    int ans = 0;

    // Loop to find all factors of N
    for (int j = 1;
        j * j <= n; j++) {

        // Check if j is a
        // factor of N or not
        if (n % j == 0) {

            // Check if j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (j <= k) {
                ans = max(ans, j);
            }

            // Check if N/j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (n / j <= k) {
                ans = max(ans, n / j);
            }
        }
    }

    // Since max value is always
    // stored in ans, the maximum
    // value divisible by N less than
    // or equal to K will be returned.
    return ans;
}

// Driver Code
int main()
{
    // Given N and K
    int N = 8, K = 7;

    // Function Call
    cout << (N / solve(N, K));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the largest
// factor of N which is less than
// or equal to K
static int solve(int n, int k)
{

    // Initialise the variable to
    // store the largest factor of
    // N <= K
    int ans = 0;

    // Loop to find all factors of N
    for(int j = 1; j * j <= n; j++)
    {

        // Check if j is a
        // factor of N or not
        if (n % j == 0)
        {

            // Check if j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (j <= k)
            {
                ans = Math.max(ans, j);
            }

            // Check if N/j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (n / j <= k)
            {
                ans = Math.max(ans, n / j);
            }
        }
    }

    // Since max value is always
    // stored in ans, the maximum
    // value divisible by N less than
    // or equal to K will be returned.
    return ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given N and K
    int N = 8, K = 7;

    // Function call
    System.out.print((N / solve(N, K)));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the largest
# factor of N which is less than
# or equal to K
def solve(n, k):

    # Initialise the variable to
    # store the largest factor of
    # N <= K
    ans = 0;

    # Loop to find all factors of N
    for j in range(1, n + 1):
        if (j * j > n):
            break;

        # Check if j is a
        # factor of N or not
        if (n % j == 0):

            # Check if j <= K
            # If yes, then store
            # the larger value between
            # ans and j in ans
            if (j <= k):
                ans = max(ans, j);

            # Check if N/j <= K
            # If yes, then store
            # the larger value between
            # ans and j in ans
            if (n // j <= k):
                ans = max(ans, n // j);

    # Since max value is always
    # stored in ans, the maximum
    # value divisible by N less than
    # or equal to K will be returned.
    return ans;

# Driver Code
if __name__ == '__main__':

    # Given N and K
    N = 8; K = 7;

    # Function call
    print((N // solve(N, K)));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the largest
// factor of N which is less than
// or equal to K
static int solve(int n, int k)
{

    // Initialise the variable to
    // store the largest factor of
    // N <= K
    int ans = 0;

    // Loop to find all factors of N
    for(int j = 1; j * j <= n; j++)
    {

        // Check if j is a
        // factor of N or not
        if (n % j == 0)
        {

            // Check if j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (j <= k)
            {
                ans = Math.Max(ans, j);
            }

            // Check if N/j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (n / j <= k)
            {
                ans = Math.Max(ans, n / j);
            }
        }
    }

    // Since max value is always
    // stored in ans, the maximum
    // value divisible by N less than
    // or equal to K will be returned.
    return ans;
}

// Driver Code
public static void Main(String[] args)
{

    // Given N and K
    int N = 8, K = 7;

    // Function call
    Console.Write((N / solve(N, K)));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program implementation
// of the approach

// Function to find the largest
// factor of N which is less than
// or equal to K
function solve(n, k)
{

    // Initialise the variable to
    // store the largest factor of
    // N <= K
    let ans = 0;

    // Loop to find all factors of N
    for(let j = 1; j * j <= n; j++)
    {

        // Check if j is a
        // factor of N or not
        if (n % j == 0)
        {

            // Check if j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (j <= k)
            {
                ans = Math.max(ans, j);
            }

            // Check if N/j <= K
            // If yes, then store
            // the larger value between
            // ans and j in ans
            if (n / j <= k)
            {
                ans = Math.max(ans, n / j);
            }
        }
    }

    // Since max value is always
    // stored in ans, the maximum
    // value divisible by N less than
    // or equal to K will be returned.
    return ans;
}

// Driver Code

       // Given N and K
    let N = 8, K = 7;

    // Function call
    document.write((N / solve(N, K)));

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(sqrt(N))*
T5】辅助空间: *O(1)*