# 代价小于 K 的最长相等子串

> 原文:[https://www . geesforgeks . org/最长等成本小于 k 的子串/](https://www.geeksforgeeks.org/longest-equal-substring-with-cost-less-than-k/)

给定两个长度相同的字符串 **X** 和 **Y** ，它们由小写字母和整数 **K** 组成。任务是在给定的成本 **K** 内，找到 **X** 可以变为 **Y** 的最大长度。
改变一个字符的成本由字符的 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)之间的绝对差值给出。也就是说，要更改索引 **i** 处的字符，成本= | x[I]–Y[I]|

**示例:**

> **输入:** X = abcd，Y = bcde，K = 3
> **输出:** 3
> **说明:**最多可以更改 3 个字符，因为更改每篇文章的成本是 1。

**方法:**想法是维持一个长度为 N 的[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)来存储字符串的绝对和。也就是把弦 **X** 换成 **Y** 的费用。可以按照以下步骤计算结果:

*   保持两个指针，说 **i** 和 **j** 。
*   在一个 while 循环中，检查前缀数组的 i <sup>第</sup>个索引和 j <sup>第</sup>个索引之间的差异是否大于给定的成本。
*   如果差值大于给定的成本，则增加 j 指针来补偿成本，否则增加 I 指针。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// maximum length of equal substring
// within a given cost
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
int solve(string X, string Y, int N, int K)
{

    int count[N + 1] = { 0 };
    int sol = 0;
    count[0] = 0;

    // Fill the prefix array with
    // the difference of letters
    for (int i = 1; i <= N; i++) {

        count[i] = count[i - 1] + abs(X[i - 1] - Y[i - 1]);
    }

    int j = 0;

    for (int i = 1; i <= N; i++) {
        while ((count[i] - count[j]) > K) {

            j++;
        }

        // Update the maximum length
        sol = max(sol, i - j);
    }

    return sol;
}

// Driver code
int main()
{

    int N = 4;

    string X = "abcd", Y = "bcde";

    int K = 3;

    cout << solve(X, Y, N, K) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// maximum length of equal subString
// within a given cost
class GFG
{

// Function to find the maximum length
static int solve(String X, String Y,
                int N, int K)
{

    int []count = new int[N + 1];
    int sol = 0;
    count[0] = 0;

    // Fill the prefix array with
    // the difference of letters
    for (int i = 1; i <= N; i++)
    {

        count[i] = count[i - 1] +
                Math.abs(X.charAt(i - 1) -
                Y.charAt(i - 1));
    }

    int j = 0;

    for (int i = 1; i <= N; i++)
    {
        while ((count[i] - count[j]) > K)
        {
            j++;
        }

        // Update the maximum length
        sol = Math.max(sol, i - j);
    }

    return sol;
}

// Driver code
public static void main(String[] args)
{

    int N = 4;
    String X = "abcd", Y = "bcde";
    int K = 3;

    System.out.print(solve(X, Y, N, K) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find the
# maximum length of equal subString
# within a given cost

# Function to find the maximum length
def solve(X, Y, N, K):
    count = [0] * (N + 1);
    sol = 0;
    count[0] = 0;

    # Fill the prefix array with
    # the difference of letters
    for i in range(1, N + 1):
        count[i] = (count[i - 1] +
                    abs(ord(X[i - 1]) -
                    ord(Y[i - 1])));

    j = 0;

    for i in range(1, N + 1):
        while ((count[i] - count[j]) > K):
            j += 1;

        # Update the maximum length
        sol = max(sol, i - j);

    return sol;

# Driver code
if __name__ == '__main__':
    N = 4;
    X = "abcd";
    Y = "bcde";
    K = 3;

    print(solve(X, Y, N, K));

# This code is contributed by PrinciRaj1992
```

## C#

```
// C# program to find the
// maximum length of equal subString
// within a given cost
using System;

class GFG
{

    // Function to find the maximum length
    static int solve(string X, string Y,
                    int N, int K)
    {

        int []count = new int[N + 1];
        int sol = 0;
        count[0] = 0;

        // Fill the prefix array with
        // the difference of letters
        for (int i = 1; i <= N; i++)
        {

            count[i] = count[i - 1] +
                    Math.Abs(X[i - 1] -
                    Y[i - 1]);
        }

        int j = 0;

        for (int i = 1; i <= N; i++)
        {
            while ((count[i] - count[j]) > K)
            {
                j++;
            }

            // Update the maximum length
            sol = Math.Max(sol, i - j);
        }

        return sol;
    }

    // Driver code
    public static void Main()
    {

        int N = 4;
        string X = "abcd", Y = "bcde";
        int K = 3;

        Console.WriteLine(solve(X, Y, N, K) + "\n");
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
    // Javascript program to find the
    // maximum length of equal subString
    // within a given cost

    // Function to find the maximum length
    function solve(X, Y, N, K)
    {

        let count = new Array(N + 1);
        count.fill(0);
        let sol = 0;
        count[0] = 0;

        // Fill the prefix array with
        // the difference of letters
        for (let i = 1; i <= N; i++)
        {

            count[i] = count[i - 1] +
                    Math.abs(X[i - 1].charCodeAt() -
                    Y[i - 1].charCodeAt());
        }

        let j = 0;

        for (let i = 1; i <= N; i++)
        {
            while ((count[i] - count[j]) > K)
            {
                j++;
            }

            // Update the maximum length
            sol = Math.max(sol, i - j);
        }

        return sol;
    }

    let N = 4;
    let X = "abcd", Y = "bcde";
    let K = 3;

    document.write(solve(X, Y, N, K));

</script>
```

**Output:** 

```
3
```