# 长度为 N 的二进制串的计数等于 0 和 1

> 原文:[https://www . geesforgeks . org/长度为 n 的二进制字符串计数等于 0 和 1/](https://www.geeksforgeeks.org/count-of-binary-strings-of-length-n-having-equal-count-of-0s-and-1s/)

给定一个整数 **N** ，任务是找出长度为 **N** 的二进制字符串的可能数量，该二进制字符串具有相同频率的 **0** s 和 **1** s。如果该字符串的长度为 **N** ，则打印 **-1** 。
**注意:**由于计数可能很大，所以以 **10 <sup>9</sup> +7** 为模返回答案。
**例:**

> **输入:** N = 2
> **输出:** 2
> **解释:**
> 长度为 2 的所有可能的二进制字符串为“00”、“01”、“10”和“11”。
> 其中，“10”和“01”的 0 和 1 出现频率相同。
> 因此，答案是 2。
> **输入:** 4
> **输出:** 6
> **解释:**
> 字符串“0011”、“0101”、“0110”、“1100”、“1010”和“1001”的 0 和 1 的频率相同。
> 于是，答案是 6。

**天真方法:**
最简单的方法是生成[长度为 **N** 的字符串](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)的所有可能的排列，其数量为**“0”**和**“1”**。对于生成的每个排列，增加**计数**。打印生成排列的总数**计数**。
***时间复杂度:** O(N*N！)*
***辅助空间** : O(N)*
**高效途径:**
上述途径可以通过使用[排列组合](https://www.geeksforgeeks.org/permutation-and-combination/)的概念进行优化。按照以下步骤解决问题:

*   由于 **N** 位置需要填充相同数量的 **0** 和 **1** 的位置，因此从 [**C(N，N/2) % mod**](https://www.geeksforgeeks.org/compute-ncr-p-set-1-introduction-and-dynamic-programming-solution/) 中的 N 个位置中选择 **N/2** 位置(其中 mod = 10 <sup>9</sup> + 7)的方式仅填充 1 个位置。
*   仅用 0 填充 **C(N/2，N/2) % mod** (即 1)方式中的剩余位置

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

// Function to calculate C(n, r) % MOD
// DP based approach
int nCrModp(int n, int r)
{
    // Corner case
    if (n % 2 == 1) {
        return -1;
    }

    // Stores the last row
    // of Pascal's Triangle
    int C[r + 1];

    memset(C, 0, sizeof(C));

    // Initialize top row
    // of pascal triangle
    C[0] = 1;

    // Construct Pascal's Triangle
    // from top to bottom
    for (int i = 1; i <= n; i++) {

        // Fill current row with the
        // help of previous row
        for (int j = min(i, r); j > 0;
            j--)

            // C(n, j) = C(n-1, j)
            // + C(n-1, j-1)
            C[j] = (C[j] + C[j - 1])
                % MOD;
    }

    return C[r];
}

// Driver Code
int main()
{
    int N = 6;
    cout << nCrModp(N, N / 2);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

final static int MOD = 1000000007;

// Function to calculate C(n, r) % MOD
// DP based approach
static int nCrModp(int n, int r)
{

    // Corner case
    if (n % 2 == 1)
    {
        return -1;
    }

    // Stores the last row
    // of Pascal's Triangle
    int C[] = new int[r + 1];

    Arrays.fill(C, 0);

    // Initialize top row
    // of pascal triangle
    C[0] = 1;

    // Construct Pascal's Triangle
    // from top to bottom
    for(int i = 1; i <= n; i++)
    {

        // Fill current row with the
        // help of previous row
        for(int j = Math.min(i, r);
                j > 0; j--)

            // C(n, j) = C(n-1, j)
            // + C(n-1, j-1)
            C[j] = (C[j] + C[j - 1]) % MOD;
    }
    return C[r];
}

// Driver Code
public static void main(String s[])
{
    int N = 6;
    System.out.println(nCrModp(N, N / 2));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
MOD = 1000000007

# Function to calculate C(n, r) % MOD
# DP based approach
def nCrModp (n, r):

    # Corner case
    if (n % 2 == 1):
        return -1

    # Stores the last row
    # of Pascal's Triangle
    C = [0] * (r + 1)

    # Initialize top row
    # of pascal triangle
    C[0] = 1

    # Construct Pascal's Triangle
    # from top to bottom
    for i in range(1, n + 1):

        # Fill current row with the
        # help of previous row
        for j in range(min(i, r), 0, -1):

            # C(n, j) = C(n-1, j)
            # + C(n-1, j-1)
            C[j] = (C[j] + C[j - 1]) % MOD

    return C[r]

# Driver Code
N = 6

print(nCrModp(N, N // 2))

# This code is contributed by himanshu77
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int MOD = 1000000007;

// Function to calculate C(n, r) % MOD
// DP based approach
static int nCrModp(int n, int r)
{

    // Corner case
    if (n % 2 == 1)
    {
        return -1;
    }

    // Stores the last row
    // of Pascal's Triangle
    int[] C = new int[r + 1];

    // Initialize top row
    // of pascal triangle
    C[0] = 1;

    // Construct Pascal's Triangle
    // from top to bottom
    for(int i = 1; i <= n; i++)
    {

        // Fill current row with the
        // help of previous row
        for(int j = Math.Min(i, r);
                j > 0; j--)

            // C(n, j) = C(n-1, j)
            // + C(n-1, j-1)
            C[j] = (C[j] + C[j - 1]) % MOD;
    }
    return C[r];
}

// Driver code
static void Main()
{
    int N = 6;
    Console.WriteLine(nCrModp(N, N / 2));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    var MOD = 1000000007;

    // Function to calculate C(n, r) % MOD
    // DP based approach
    function nCrModp(n , r) {

        // Corner case
        if (n % 2 == 1) {
            return -1;
        }

        // Stores the last row
        // of Pascal's Triangle
        var C = Array(r + 1).fill(0);

        // Initialize top row
        // of pascal triangle
        C[0] = 1;

        // Construct Pascal's Triangle
        // from top to bottom
        for (i = 1; i <= n; i++) {

            // Fill current row with the
            // help of previous row
            for (j = Math.min(i, r); j > 0; j--)

                // C(n, j) = C(n-1, j)
                // + C(n-1, j-1)
                C[j] = (C[j] + C[j - 1]) % MOD;
        }
        return C[r];
    }

    // Driver Code
        var N = 6;
        document.write(nCrModp(N, N / 2));

// This code contributed by gauravrajput1

</script>
```

**Output:** 

```
20
```

***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(N)*