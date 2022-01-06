# 数 N 位数字，后缀可被 K 整除的数字

> 原文:[https://www . geeksforgeeks . org/用 n 位数计算数字，其后缀可被 k 整除/](https://www.geeksforgeeks.org/count-the-numbers-with-n-digits-and-whose-suffix-is-divisible-by-k/)

给定两个正整数 **N** 和 **K** ，任务是计算正整数 **D** 的数量，使得 D 有 N 个数字，并且其十进制表示的任何后缀都可以被 K 整除

**示例:**

> **输入:** N = 1，K = 2
> **输出:** 4
> **解释:**
> 有 4 个这样的整数，其中任何一个后缀都可以被 K 整除:
> {2，4，6，8}
> 
> **输入:** N = 2，K = 2
> **输出:** 45
> **解释:**
> 有 45 个两位数的整数，其中任何一个后缀都可以被 2 整除:
> 下面给出了其中一些整数–
> { 10，12，13，14，15，16，18，19，20，21，22，23…}
> 注意，21 和 23 是数字但是它们的后缀 2 可以被 2 整除。

**天真方法:**迭代 N 位的所有整数，对于每个整数，检查该数的任何后缀是否可被 K 整除，如果是，则将该数的计数增加 1。
**方法:**思路是使用[动态编程](http://www.geeksforgeeks.org/dynamic-programming/)的概念，增加后缀长度，将数字从 0 到 9 递归放置。下面是步骤的图示:

*   **函数定义:**这个问题可以递归解决，在每一步中，我们可以为 N 位数选择后缀的位数。因此，递归解的函数定义将是:

```
// Recursive Function to count of values
// whose suffixes of length pos 
// have remainder rem with K
recur(pos, rem)
```

*   **基本情况:**这个问题的基本情况是，对于任何一个索引，带 K 的后缀的余数变成 0，那么所有其他的数字都可以用从 0 到 9 的所有可能的整数来放置。

```
f(pos, 0) = 9 * (10^(n-i-1))
```

*   **递归情况:**在递归的每一步，我们通过放置 0-9 之间的所有整数将后缀长度增加 1，相应地用 K 改变余数，并进入下一步。

```
for num in range [0-9]:
     f(pos, rem) += f(pos+1, (rem*10 + num)%k)
```

下面是上述方法的实现:

## C++

```
// C++ implementation to Count the
// numbers with N digits and whose
// suffix is divisible by K

#include <bits/stdc++.h>

using namespace std;

int mod = 1000000007;
int dp[1005][105][2];
int powers[1005];
int powersModk[1005];

// Suffix of length pos with
// remainder rem and Z representing
// whether the suffix has a
// non zero digit until now
int calculate(int pos, int rem,
           int z, int k, int n)
{
    // Base case
    if (rem == 0 && z) {

        // If count of digits
        // is less than n
        if (pos != n)

            // Placing all possible
            // digits in remaining
            // positions
            return (powers[n - pos -
                        1] * 9) % mod;
        else
            return 1;
    }

    // If remainder non zero
    // and suffix has n digits
    if (pos == n)
        return 0;

    // If the subproblem
    // is already solved
    if (dp[pos][rem][z] != -1)
        return dp[pos][rem][z];

    int count = 0;

    // Placing all digits at MSB
    // of suffix and increasing
    // it's length by 1
    for (int i = 0; i < 10; i++) {
        if (i == 0)
            count = (count + (calculate(
             pos + 1, (rem + (i *
                 powersModk[pos]) % k) %
                    k, z, k, n))) % mod;

        // Non zero digit is placed
        else
            count = (count + (calculate(
                pos + 1, (rem + (i *
                powersModk[pos]) % k) %
                k, 1, k, n))) % mod;
    }

    // Store and return the
    // solution to this subproblem
    return dp[pos][rem][z] = count;
}

// Function to Count the numbers
// with N digits and whose suffix
// is divisible by K
int countNumbers(int n, int k)
{

    // Since we need powers of 10
    // for counting, it's better to
    // pre store them along with their
    // modulo with 1e9 + 7 for counting
    int st = 1;
    for (int i = 0; i <= n; i++) {
        powers[i] = st;
        st *= 10;
        st %= mod;
    }

    // Since at each recursive step
    // we increase the suffix length by 1
    // by placing digits at its leftmost
    // position, we need powers of 10
    // modded with k, in order to fpos
    // the new remainder efficiently
    st = 1;
    for (int i = 0; i <= n; i++) {
        powersModk[i] = st;
        st *= 10;
        st %= mod;
    }

    // Initialising dp table values -1
    // represents subproblem hasn't
    // been solved yet
    memset(dp, -1, sizeof(dp));

    return calculate(0, 0, 0, k, n);
}

// Driver Code
int main()
{
    int N = 2;
    int K = 2;

    cout << countNumbers(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Count the
// numbers with N digits and whose
// suffix is divisible by K
import java.util.*;
import java.util.Arrays;

class GFG
{

    static int mod = 1000000007;
    static int dp[][][] = new int[1005][105][2];
    static int powers[] = new int[1005];
    static int powersModk[] = new int[1005];

    // Suffix of length pos with
    // remainder rem and Z representing
    // whether the suffix has a
    // non zero digit until now
    static int calculate(int pos, int rem,
            int z, int k, int n)
    {
        // Base case
        if (rem == 0 && z!=0) {

            // If count of digits
            // is less than n
            if (pos != n)

                // Placing all possible
                // digits in remaining
                // positions
                return (powers[n - pos -
                            1] * 9) % mod;
            else
                return 1;
        }

        // If remainder non zero
        // and suffix has n digits
        if (pos == n)
            return 0;

        // If the subproblem
        // is already solved
        if (dp[pos][rem][z] != -1)
            return dp[pos][rem][z];

        int count = 0;

        // Placing all digits at MSB
        // of suffix and increasing
        // it's length by 1
        for (int i = 0; i < 10; i++) {
            if (i == 0)
                count = (count + (calculate(
                pos + 1, (rem + (i *
                    powersModk[pos]) % k) %
                        k, z, k, n))) % mod;

            // Non zero digit is placed
            else
                count = (count + (calculate(
                    pos + 1, (rem + (i *
                    powersModk[pos]) % k) %
                    k, 1, k, n))) % mod;
        }

        // Store and return the
        // solution to this subproblem
        return dp[pos][rem][z] = count;
    }

    // Function to Count the numbers
    // with N digits and whose suffix
    // is divisible by K
    static int countNumbers(int n, int k)
    {

        // Since we need powers of 10
        // for counting, it's better to
        // pre store them along with their
        // modulo with 1e9 + 7 for counting
        int st = 1;
        int i;
        for (i = 0; i <= n; i++) {
            powers[i] = st;
            st *= 10;
            st %= mod;
        }

        // Since at each recursive step
        // we increase the suffix length by 1
        // by placing digits at its leftmost
        // position, we need powers of 10
        // modded with k, in order to fpos
        // the new remainder efficiently
        st = 1;
        for (i = 0; i <= n; i++) {
            powersModk[i] = st;
            st *= 10;
            st %= mod;
        }

        // Initialising dp table values -1
        // represents subproblem hasn't
        // been solved yet
        for (int[][] row: dp)
        {
            for (int[] innerRow: row)
            {
                Arrays.fill(innerRow, -1);
            }
        };

        return calculate(0, 0, 0, k, n);
    }

    // Driver Code
    public static void main(String []args)
    {
        int N = 2;
        int K = 2;

        System.out.print(countNumbers(N, K));
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to Count the
# numbers with N digits and whose
# suffix is divisible by K

mod = 1000000007
dp = [[[-1 for i in range(2)] for i in range(105)] for i in range(1005)]
powers = [0]*1005
powersModk = [0]*1005

# Suffix of length pos with
# remainder rem and Z representing
# whether the suffix has a
# non zero digit until now
def calculate(pos, rem, z, k, n):
    # Base case
    if (rem == 0 and z):

        # If count of digits
        # is less than n
        if (pos != n):

            # Placing all possible
            # digits in remaining
            # positions
            return (powers[n - pos -1] * 9) % mod
        else:
            return 1

    # If remainder non zero
    # and suffix has n digits
    if (pos == n):
        return 0

    # If the subproblem
    # is already solved
    if (dp[pos][rem][z] != -1):
        return dp[pos][rem][z]

    count = 0

    # Placing all digits at MSB
    # of suffix and increasing
    # it's length by 1
    for i in range(10):
        if (i == 0):
            count = (count + (calculate(
            pos + 1, (rem + (i *
                powersModk[pos]) % k) %
                    k, z, k, n))) % mod

        # Non zero digit is placed
        else:
            count = (count + (calculate(
                pos + 1, (rem + (i *
                powersModk[pos]) % k) %
                k, 1, k, n))) % mod

    # Store and return the
    # solution to this subproblem
    dp[pos][rem][z] = count
    return count

# Function to Count the numbers
# with N digits and whose suffix
# is divisible by K
def countNumbers(n, k):

    # Since we need powers of 10
    # for counting, it's better to
    # pre store them along with their
    # modulo with 1e9 + 7 for counting
    st = 1
    for i in range(n + 1):
        powers[i] = st
        st *= 10
        st %= mod

    # Since at each recursive step
    # we increase the suffix length by 1
    # by placing digits at its leftmost
    # position, we need powers of 10
    # modded with k, in order to fpos
    # the new remainder efficiently
    st = 1
    for i in range(n + 1):
        powersModk[i] = st
        st *= 10
        st %= mod

    # Initialising dp table values -1
    # represents subproblem hasn't
    # been solved yet
    # memset(dp, -1, sizeof(dp))

    return calculate(0, 0, 0, k, n)

# Driver Code
if __name__ == '__main__':
    N = 2
    K = 2

    print(countNumbers(N, K))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to Count the
// numbers with N digits and whose
// suffix is divisible by K
using System;

class GFG
{

    static int mod = 1000000007;
    static int [,,]dp = new int[1005, 105, 2];
    static int []powers = new int[1005];
    static int []powersModk = new int[1005];

    // Suffix of length pos with
    // remainder rem and Z representing
    // whether the suffix has a
    // non zero digit until now
    static int calculate(int pos, int rem,
            int z, int k, int n)
    {
        // Base case
        if (rem == 0 && z != 0) {

            // If count of digits
            // is less than n
            if (pos != n)

                // Placing all possible
                // digits in remaining
                // positions
                return (powers[n - pos -
                            1] * 9) % mod;
            else
                return 1;
        }

        // If remainder non zero
        // and suffix has n digits
        if (pos == n)
            return 0;

        // If the subproblem
        // is already solved
        if (dp[pos, rem, z] != -1)
            return dp[pos,rem,z];

        int count = 0;

        // Placing all digits at MSB
        // of suffix and increasing
        // it's length by 1
        for (int i = 0; i < 10; i++) {
            if (i == 0)
                count = (count + (calculate(
                pos + 1, (rem + (i *
                    powersModk[pos]) % k) %
                        k, z, k, n))) % mod;

            // Non zero digit is placed
            else
                count = (count + (calculate(
                    pos + 1, (rem + (i *
                    powersModk[pos]) % k) %
                    k, 1, k, n))) % mod;
        }

        // Store and return the
        // solution to this subproblem
        return dp[pos,rem,z] = count;
    }

    // Function to Count the numbers
    // with N digits and whose suffix
    // is divisible by K
    static int countNumbers(int n, int k)
    {

        // Since we need powers of 10
        // for counting, it's better to
        // pre store them along with their
        // modulo with 1e9 + 7 for counting
        int st = 1;
        int i;
        for (i = 0; i <= n; i++) {
            powers[i] = st;
            st *= 10;
            st %= mod;
        }

        // Since at each recursive step
        // we increase the suffix length by 1
        // by placing digits at its leftmost
        // position, we need powers of 10
        // modded with k, in order to fpos
        // the new remainder efficiently
        st = 1;
        for (i = 0; i <= n; i++) {
            powersModk[i] = st;
            st *= 10;
            st %= mod;
        }

        // Initialising dp table values -1
        // represents subproblem hasn't
        // been solved yet
        for(i = 0; i < 1005; i++){
            for(int j = 0; j < 105; j++){
                for(int l = 0; l < 2; l++)
                    dp[i, j, l] = -1;
            }
        }

        return calculate(0, 0, 0, k, n);
    }

    // Driver Code
    public static void Main(String []args)
    {
        int N = 2;
        int K = 2;

        Console.Write(countNumbers(N, K));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation to Count the
// numbers with N digits and whose
// suffix is divisible by K

var mod = 1000000007;
var dp = Array.from(Array(1005), ()=>Array(105));

for(var i = 0; i< 1005; i++)
{
    for(var j =0; j<105; j++)
    {
        dp[i][j] = Array(2).fill(-1);
    }
}
var powers = Array(1005);
var powersModk= Array(1005);

// Suffix of length pos with
// remainder rem and Z representing
// whether the suffix has a
// non zero digit until now
function calculate(pos, rem, z, k, n)
{
    // Base case
    if (rem == 0 && z) {

        // If count of digits
        // is less than n
        if (pos != n)

            // Placing all possible
            // digits in remaining
            // positions
            return (powers[n - pos -
                        1] * 9) % mod;
        else
            return 1;
    }

    // If remainder non zero
    // and suffix has n digits
    if (pos == n)
        return 0;

    // If the subproblem
    // is already solved
    if (dp[pos][rem][z] != -1)
        return dp[pos][rem][z];

    var count = 0;

    // Placing all digits at MSB
    // of suffix and increasing
    // it's length by 1
    for (var i = 0; i < 10; i++) {
        if (i == 0)
            count = (count + (calculate(
             pos + 1, (rem + (i *
                 powersModk[pos]) % k) %
                    k, z, k, n))) % mod;

        // Non zero digit is placed
        else
            count = (count + (calculate(
                pos + 1, (rem + (i *
                powersModk[pos]) % k) %
                k, 1, k, n))) % mod;
    }

    // Store and return the
    // solution to this subproblem
    return dp[pos][rem][z] = count;
}

// Function to Count the numbers
// with N digits and whose suffix
// is divisible by K
function countNumbers(n, k)
{

    // Since we need powers of 10
    // for counting, it's better to
    // pre store them along with their
    // modulo with 1e9 + 7 for counting
    var st = 1;
    for (var i = 0; i <= n; i++) {
        powers[i] = st;
        st *= 10;
        st %= mod;
    }

    // Since at each recursive step
    // we increase the suffix length by 1
    // by placing digits at its leftmost
    // position, we need powers of 10
    // modded with k, in order to fpos
    // the new remainder efficiently
    st = 1;
    for (var i = 0; i <= n; i++) {
        powersModk[i] = st;
        st *= 10;
        st %= mod;
    }

    return calculate(0, 0, 0, k, n);
}

// Driver Code
var N = 2;
var K = 2;
document.write( countNumbers(N, K));

</script>
```

**Output:** 

```
45
```

**时间复杂度:** O(N * K)

**辅助空间:** O(1005 * 105 * 2)