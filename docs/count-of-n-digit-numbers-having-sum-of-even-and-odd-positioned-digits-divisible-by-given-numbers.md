# 偶数和奇数位置的数字之和可被给定数字整除的 N 位数字的计数

> 原文:[https://www . geeksforgeeks . org/n 位数字计数-具有偶数和奇数位数字之和-可被给定数字除尽/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-having-sum-of-even-and-odd-positioned-digits-divisible-by-given-numbers/)

给定整数 **A、B** 和 **N** ，任务是找出 **N 位**数的总数，这些数在**偶数位置**和**奇数位置**的位数之和可分别被 **A** 和 **B** 整除。

**示例:**

> **输入:** N = 2，A = 2，B = 5
> **输出:** 5
> **说明:**
> 唯一的两位数{50，52，54，56，58}，奇数位数字之和等于 5，偶数位数字{0，2，4，6，8}可被 2 整除。
> 
> **输入:** N = 2，A = 5，B = 3
> **输出:** 6
> **说明:**
> 仅有的两位数{30，35，60，65，90，95}有奇数位{3，6 或 9}，可被 3 整除，偶数位{0 或 5}，可被 5 整除。

**天真法:**解决这个问题最简单的方法就是迭代所有可能的 **N 位数**，对于每个数，检查偶数位置的位数之和是否可以被 **A** 整除，奇数位置的位数之和是否可以被 **B** 整除。如果发现是真的，增加**计数**。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate and
// return the reverse of the number
long reverse(long num)
{
    long rev = 0;
    while (num > 0)
    {
        int r = (int)(num % 10);
        rev = rev * 10 + r;
        num /= 10;
    }
    return rev;
}

// Function to calculate the total
// count of N-digit numbers satisfying
// the necessary conditions
long count(int N, int A, int B)
{

    // Initialize two variables
    long l = (long)pow(10, N - 1),
         r = (long)pow(10, N) - 1;

    if (l == 1)
        l = 0;

    long ans = 0;

    for(long i = l; i <= r; i++)
    {
        int even_sum = 0, odd_sum = 0;
        long itr = 0, num = reverse(i);

        // Calculate the sum of odd
        // and even positions
        while (num > 0)
        {
            if (itr % 2 == 0)
                odd_sum += num % 10;
            else
                even_sum += num % 10;

            num /= 10;
            itr++;
        }

        // Check for divisibility
        if (even_sum % A == 0 &&
             odd_sum % B == 0)
            ans++;
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    int N = 2, A = 5, B = 3;
    cout << (count(N, A, B));

}

// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Function to calculate and
    // return the reverse of the number
    public static long reverse(long num)
    {
        long rev = 0;
        while (num > 0) {
            int r = (int)(num % 10);
            rev = rev * 10 + r;
            num /= 10;
        }
        return rev;
    }

    // Function to calculate the total
    // count of N-digit numbers satisfying
    // the necessary conditions
    public static long count(int N, int A, int B)
    {
        // Initialize two variables
        long l = (long)Math.pow(10, N - 1),
             r = (long)Math.pow(10, N) - 1;

        if (l == 1)
            l = 0;

        long ans = 0;

        for (long i = l; i <= r; i++) {
            int even_sum = 0, odd_sum = 0;
            long itr = 0, num = reverse(i);

            // Calculate the sum of odd
            // and even positions
            while (num > 0) {

                if (itr % 2 == 0)
                    odd_sum += num % 10;
                else
                    even_sum += num % 10;
                num /= 10;
                itr++;
            }
            // Check for divisibility
            if (even_sum % A == 0
                && odd_sum % B == 0)
                ans++;
        }

        // Return the answer
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2, A = 5, B = 3;
        System.out.println(count(N, A, B));
    }
}
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to calculate and
# return the reverse of the number
def reverse(num):

    rev = 0;
    while (num > 0):
        r = int(num % 10);
        rev = rev * 10 + r;
        num = num // 10;

    return rev;

# Function to calculate the total
# count of N-digit numbers satisfying
# the necessary conditions
def count(N, A, B):

    # Initialize two variables
    l = int(pow(10, N - 1));
    r = int(pow(10, N) - 1);
    if (l == 1):
        l = 0;

    ans = 0;

    for i in range(l, r + 1):
        even_sum = 0;
        odd_sum = 0;
        itr = 0;
        num = reverse(i);

        # Calculate the sum of odd
        # and even positions
        while (num > 0):

            if (itr % 2 == 0):
                odd_sum += num % 10;
            else:
                even_sum += num % 10;
            num = num // 10;
            itr += 1;

        # Check for divisibility
        if (even_sum % A == 0 and
            odd_sum % B == 0):
            ans += 1;

    # Return the answer
    return ans;

# Driver Code
if __name__ == '__main__':

    N = 2;
    A = 5;
    B = 3;
    print(count(N, A, B));

# This code is contributed by gauravrajput1
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate and
// return the reverse of the number
public static long reverse(long num)
{
    long rev = 0;
    while (num > 0)
    {
        int r = (int)(num % 10);
        rev = rev * 10 + r;
        num /= 10;
    }
    return rev;
}

// Function to calculate the total
// count of N-digit numbers satisfying
// the necessary conditions
public static long count(int N, int A, int B)
{

    // Initialize two variables
    long l = (long)Math.Pow(10, N - 1),
         r = (long)Math.Pow(10, N) - 1;

    if (l == 1)
        l = 0;

    long ans = 0;

    for(long i = l; i <= r; i++)
    {
        int even_sum = 0, odd_sum = 0;
        long itr = 0, num = reverse(i);

        // Calculate the sum of odd
        // and even positions
        while (num > 0)
        {
            if (itr % 2 == 0)
                odd_sum += (int)num % 10;
            else
                even_sum += (int)num % 10;

            num /= 10;
            itr++;
        }

        // Check for divisibility
        if (even_sum % A == 0 &&
             odd_sum % B == 0)
            ans++;
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, A = 5, B = 3;
    Console.WriteLine(count(N, A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript Program to implement
// the above approach   
// Function to calculate and
    // return the reverse of the number
    function reverse(num) {
        var rev = 0;
        while (num > 0) {
            var r = parseInt( (num % 10));
            rev = rev * 10 + r;
            num = parseInt(num/10);
        }
        return rev;
    }

    // Function to calculate the total
    // count of N-digit numbers satisfying
    // the necessary conditions
    function count(N , A , B) {
        // Initialize two variables
        var l = Math.pow(10, N - 1), r = Math.pow(10, N) - 1;

        if (l == 1)
            l = 0;

        var ans = 0;

        for (i = l; i <= r; i++) {
            var even_sum = 0, odd_sum = 0;
            var itr = 0, num = reverse(i);

            // Calculate the sum of odd
            // and even positions
            while (num > 0) {

                if (itr % 2 == 0)
                    odd_sum += num % 10;
                else
                    even_sum += num % 10;
                num = parseInt(num/10);
                itr++;
            }
            // Check for divisibility
            if (even_sum % A == 0 && odd_sum % B == 0)
                ans++;
        }

        // Return the answer
        return ans;
    }

    // Driver Code

        var N = 2, A = 5, B = 3;
        document.write(count(N, A, B));

// This code contributed by aashish1995
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O((10<sup>N</sup>–10<sup>N–1</sup>–1)* N)*
***辅助空间:** O(N)*

**高效方法:**为了优化上述方法，使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)的概念。

按照以下步骤解决问题:

*   由于**偶数位置的**数字和**奇数位置的**数字并不相互依赖，因此，给定的问题可以分解为两个子问题:
    *   **对于偶数位置的数字:**从 0 到 9 的 **N/2** 数字序列的总计数(允许重复)，使得数字的总和可被 **A** 整除，其中第一个数字可以为零。
    *   **对于奇数位数字:**从 0 到 9 的 **Ceil(N/2)** 数字序列的总计数(允许重复)，使得数字的总和可被 **B** 整除，其中第一个数字不能为零。
*   所需的结果是以上两者的乘积。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the total
// count of N-digit numbers such
// that the sum of digits at even
// positions and odd positions are
// divisible by A and B respectively
long count(int N, int A, int B)
{
    // For single digit numbers
    if (N == 1)
    {
        return 9 / B + 1;
    }

    // Largest possible number
    int max_sum = 9 * N;

    // Count of possible odd digits
    int odd_count = N / 2 + N % 2;

    // Count of possible even digits
    int even_count = N - odd_count;

    // Calculate total count of sequences of
    // length even_count with sum divisible
    // by A where first digit can be zero
    long dp[even_count][max_sum + 1] = {0};
    for (int i = 0; i <= 9; i++)
        dp[0][i % A]++;

    for (int i = 1; i < even_count; i++)
    {
        for (int j = 0; j <= 9; j++)
        {
            for (int k = 0; k <= max_sum; k++)
            {
                if (dp[i - 1][k] > 0)
                    dp[i][(j + k) % A] += dp[i - 1][k];
            }
        }
    }

    // Calculate total count of sequences of
    // length odd_count with sum divisible
    // by B where cannot be zero
    long dp1[odd_count][max_sum + 1] = {0};
    for (int i = 1; i <= 9; i++)
        dp1[0][i % B]++;

    for (int i = 1; i < odd_count; i++)
    {
        for (int j = 0; j <= 9; j++)
        {
            for (int k = 0; k <= max_sum; k++)
            {
                if (dp1[i - 1][k] > 0)
                    dp1[i][(j + k) % B] += dp1[i - 1][k];
            }
        }
    }

    // Return their product as answer
    return dp[even_count - 1][0] * dp1[odd_count - 1][0];
}

// Driver Code
int main()
{
    int N = 2, A = 2, B = 5;
    cout << count(N, A, B);
}

// This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement
// the above approach
class GFG {

    // Function to calculate the total
    // count of N-digit numbers such
    // that the sum of digits at even
    // positions and odd positions are
    // divisible by A and B respectively
    public static long count(int N, int A, int B)
    {
        // For single digit numbers
        if (N == 1) {
            return 9 / B + 1;
        }

        // Largest possible number
        int max_sum = 9 * N;

        // Count of possible odd digits
        int odd_count = N / 2 + N % 2;

        // Count of possible even digits
        int even_count = N - odd_count;

        // Calculate total count of sequences of
        // length even_count with sum divisible
        // by A where first digit can be zero
        long dp[][]
            = new long[even_count][max_sum + 1];
        for (int i = 0; i <= 9; i++)
            dp[0][i % A]++;

        for (int i = 1; i < even_count; i++) {
            for (int j = 0; j <= 9; j++) {
                for (int k = 0; k <= max_sum; k++) {
                    if (dp[i - 1][k] > 0)
                        dp[i][(j + k) % A]
                            += dp[i - 1][k];
                }
            }
        }

        // Calculate total count of sequences of
        // length odd_count with sum divisible
        // by B where cannot be zero
        long dp1[][]
            = new long[odd_count][max_sum + 1];
        for (int i = 1; i <= 9; i++)
            dp1[0][i % B]++;

        for (int i = 1; i < odd_count; i++) {
            for (int j = 0; j <= 9; j++) {
                for (int k = 0; k <= max_sum; k++) {
                    if (dp1[i - 1][k] > 0)
                        dp1[i][(j + k) % B]
                            += dp1[i - 1][k];
                }
            }
        }

        // Return their product as answer
        return dp[even_count - 1][0]
            * dp1[odd_count - 1][0];
    }
    // Driver Code
    public static void main(String[] args)
    {
        int N = 2, A = 2, B = 5;
        System.out.println(count(N, A, B));
    }
}
```

## 蟒蛇 3

```
# Python 3 Program to implement
# the above approach

# Function to calculate the total
# count of N-digit numbers such
# that the sum of digits at even
# positions and odd positions are
# divisible by A and B respectively
def count(N, A, B):

    # For single digit numbers
    if (N == 1):
        return 9 // B + 1

    # Largest possible number
    max_sum = 9 * N

    # Count of possible odd digits
    odd_count = N // 2 + N % 2

    # Count of possible even digits
    even_count = N - odd_count

    # Calculate total count of
    # sequences of length even_count
    # with sum divisible by A where
    # first digit can be zero
    dp = [[0 for x in range (max_sum + 1)]
             for y in range (even_count)]

    for i in range(10):
        dp[0][i % A] += 1

    for i in range (1, even_count):
        for j in range (10):
            for k in range (max_sum + 1):
                if (dp[i - 1][k] > 0):
                    dp[i][(j + k) % A] += dp[i - 1][k]

    # Calculate total count of sequences of
    # length odd_count with sum divisible
    # by B where cannot be zero
    dp1 = [[0 for x in range (max_sum)]
              for y in range (odd_count)]
    for i in range (1, 10):
        dp1[0][i % B] += 1

    for i in range (1, odd_count): 
        for j in range (10):      
            for k in range (max_sum + 1):
                if (dp1[i - 1][k] > 0):
                    dp1[i][(j + k) % B] += dp1[i - 1][k]

    # Return their product as answer
    return dp[even_count - 1][0] * dp1[odd_count - 1][0]

# Driver Code
if __name__ == "__main__":

    N = 2
    A = 2
    B = 5
    print (count(N, A, B))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate the total
// count of N-digit numbers such
// that the sum of digits at even
// positions and odd positions are
// divisible by A and B respectively
public static long count(int N, int A, int B)
{

    // For single digit numbers
    if (N == 1)
    {
        return 9 / B + 1;
    }

    // Largest possible number
    int max_sum = 9 * N;

    // Count of possible odd digits
    int odd_count = N / 2 + N % 2;

    // Count of possible even digits
    int even_count = N - odd_count;

    // Calculate total count of sequences of
    // length even_count with sum divisible
    // by A where first digit can be zero
    long [,]dp = new long[even_count, max_sum + 1];
    for(int i = 0; i <= 9; i++)
        dp[0, i % A]++;

    for(int i = 1; i < even_count; i++)
    {
        for(int j = 0; j <= 9; j++)
        {
            for(int k = 0; k <= max_sum; k++)
            {
                if (dp[i - 1, k] > 0)
                    dp[i, (j + k) % A] += dp[i - 1, k];
            }
        }
    }

    // Calculate total count of sequences of
    // length odd_count with sum divisible
    // by B where cannot be zero
    long [,]dp1 = new long[odd_count, max_sum + 1];
    for(int i = 1; i <= 9; i++)
        dp1[0, i % B]++;

    for(int i = 1; i < odd_count; i++)
    {
        for(int j = 0; j <= 9; j++)
        {
            for(int k = 0; k <= max_sum; k++)
            {
                if (dp1[i - 1, k] > 0)
                    dp1[i, (j + k) % B] += dp1[i - 1, k];
            }
        }
    }

    // Return their product as answer
    return dp[even_count - 1, 0] *
           dp1[odd_count - 1, 0];
}

// Driver Code
public static void Main(String[] args)
{
    int N = 2, A = 2, B = 5;

    Console.WriteLine(count(N, A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

    // Function to calculate the total
    // count of N-digit numbers such
    // that the sum of digits at even
    // positions and odd positions are
    // divisible by A and B respectively
    function count(N, A, B)
    {
        // For single digit numbers
        if (N == 1) {
            return 9 / B + 1;
        }

        // Largest possible number
        let max_sum = 9 * N;

        // Count of possible odd digits
        let odd_count = N / 2 + N % 2;

        // Count of possible even digits
        let even_count = N - odd_count;

        // Calculate total count of sequences of
        // length even_count with sum divisible
        // by A where first digit can be zero
        let dp
            = new Array(even_count);
            // Loop to create 2D array using 1D array
        for (var i = 0; i < dp.length; i++) {
            dp[i] = new Array(2);
        }

        for (var i = 0; i < even_count; i++) {
            for (var j = 0; j < max_sum + 1; j++) {
            dp[i][j] = 0;
        }
        }

        for (let i = 0; i <= 9; i++)
            dp[0][i % A]++;

        for (let i = 1; i < even_count; i++) {
            for (let j = 0; j <= 9; j++) {
                for (let k = 0; k <= max_sum; k++) {
                    if (dp[i - 1][k] > 0)
                        dp[i][(j + k) % A]
                            += dp[i - 1][k];
                }
            }
        }

        // Calculate total count of sequences of
        // length odd_count with sum divisible
        // by B where cannot be zero
        let dp1
            = new Array(odd_count);
        // Loop to create 2D array using 1D array
        for (var i = 0; i < dp1.length; i++) {
            dp1[i] = new Array(2);
        }

        for (var i = 0; i < odd_count; i++) {
            for (var j = 0; j < max_sum + 1; j++) {
            dp1[i][j] = 0;
        }
        }

        for (let i = 1; i <= 9; i++)
            dp1[0][i % B]++;

        for (let i = 1; i < odd_count; i++) {
            for (let j = 0; j <= 9; j++) {
                for (let k = 0; k <= max_sum; k++) {
                    if (dp1[i - 1][k] > 0)
                        dp1[i][(j + k) % B]
                            += dp1[i - 1][k];
                }
            }
        }

        // Return their product as answer
        return dp[even_count - 1][0]
            * dp1[odd_count - 1][0];
    }

// Driver Code

    let N = 2, A = 2, B = 5;
    document.write(count(N, A, B));

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*