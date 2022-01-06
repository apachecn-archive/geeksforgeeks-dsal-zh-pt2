# 计数方法，使一个数字串的 K 个连接形成的数可被 5 整除

> 原文:[https://www . geesforgeks . org/count-way-to-make-by-k-concations-of-numeric-string-除尽-5/](https://www.geeksforgeeks.org/count-ways-to-make-the-number-formed-by-k-concatenations-of-a-numeric-string-divisible-by-5/)

给定一个由 **N** 个数字和一个整数 **K** 组成的[串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是计算从由串 **S** 、 **K** 个次数串联而成的数字中去除数字的方法数，这样得到的[串](https://www.geeksforgeeks.org/string-data-structure/)可以被 **5** 整除。由于计数会很大，所以打印到[模 **10 <sup>9</sup> + 7**](https://www.geeksforgeeks.org/modulo-1097-1000000007/) 。

**示例:**

> **输入:** S = 1256，K = 1
> **输出:** 4
> **解释:**
> 以下是删除字符的方法，使字符串 S(=“1256”)可被 5 整除:
> 
> 1.  从字符串 S 中删除字符 6 会将字符串修改为 125，可被 5 整除。
> 2.  从字符串 S 中删除字符 1 和 6 会将字符串修改为 25，可被 5 整除。
> 3.  从字符串 S 中删除字符 2 和 6，将字符串修改为 15，可被 5 整除。
> 4.  从字符串 S 中删除字符 1、2 和 6 会将字符串修改为可被 5 整除的 5。
> 
> 因此，可被 5 整除的数的总数是 4。
> 
> **输入:** S = 13390，K = 2
> T3】输出: 528

**方法:**当且仅当最后一位数字为 **0** 或 **5** 时，[数可被 5](https://www.geeksforgeeks.org/java-program-to-check-whether-number-is-divisible-by-5/) 整除，即可解决给定问题。如果 **sol[i]** 是形成以 **i** 结束的可被 **5** 整除的数的方式数，那么数的计数由**给出(sol[1] + sol[2] + … + sol[N])** 。对于每个索引 **i** ，在 **i** 的**右**上，选择是删除所有数字，而在 **i** 的**左**上，则有两个选择，要么删除，要么取，即**2<sup>(I–1)</sup>**。

因此 **K** 个串联数的总数由下式给出:

> ans = ans *(2<sup>(k * n)</sup>-1)/(2<sup>n</sup>–1)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
typedef long long LL;
const int MOD = 1000000007;

// Function to find the value of a^b
// modulo 1000000007
int exp_mod(LL a, LL b)
{

    // Stores the resultant value a^b
    LL ret = 1;

    // Find the value of a^b
    for (; b; b >>= 1, a = a * a % MOD) {
        if (b & 1)
            ret = ret * a % MOD;
    }

    return ret;
}

// Function to count the number of ways
// such that the formed number is divisible
// by 5 by removing digits
int countOfWays(string s, int k)
{
    int N = s.size();

    // Stores the count of ways
    LL ans = 0;

    // Find the count for string S
    for (int i = 0; i < N; i++) {

        // If the digit is 5 or 0
        if (s[i] == '5' || s[i] == '0') {
            ans = (ans + exp_mod(2, i)) % MOD;
        }
    }

    // Find the count of string for K
    // concatenation of string S
    LL q = exp_mod(2, N);
    LL qk = exp_mod(q, k);
    LL inv = exp_mod(q - 1, MOD - 2);

    // Find the total count
    ans = ans * (qk - 1) % MOD;
    ans = ans * inv % MOD;

    return ans;
}

// Driver Code
int main()
{
    string S = "1256";
    int K = 1;
    cout << countOfWays(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG
{
  static long MOD = 1000000007;

  // Function to find the value of a^b
  // modulo 1000000007
  public static long exp_mod(long a, long b) {

    // Stores the resultant value a^b
    long ret = 1;

    // Find the value of a^b
    for (; b > 0; b >>= 1, a = a * a % MOD) {
      if ((b & 1) > 0)
        ret = ret * a % MOD;
    }

    return ret;
  }

  // Function to count the number of ways
  // such that the formed number is divisible
  // by 5 by removing digits
  public static long countOfWays(String s, int k) {
    int N = s.length();

    // Stores the count of ways
    long ans = 0;

    // Find the count for string S
    for (int i = 0; i < N; i++) {

      // If the digit is 5 or 0
      if (s.charAt(i) == '5' || s.charAt(0) == '0') {
        ans = (ans + exp_mod(2, i)) % MOD;
      }
    }

    // Find the count of string for K
    // concatenation of string S
    long q = exp_mod(2, N);
    long qk = exp_mod(q, k);
    long inv = exp_mod(q - 1, MOD - 2);

    // Find the total count
    ans = ans * (qk - 1) % MOD;
    ans = ans * inv % MOD;

    return ans;
  }

  // Driver Code
  public static void main(String args[]) {
    String S = "1256";
    int K = 1;
    System.out.println(countOfWays(S, K));

  }

}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python program for the above approach
MOD = 1000000007

# Function to find the value of a^b
# modulo 1000000007
def exp_mod(a, b):

    # Stores the resultant value a^b
    ret = 1

    # Find the value of a^b
    while(b):
        if (b & 1):
            ret = ret * a % MOD
        b >>= 1
        a = a * a % MOD

    return ret

# Function to count the number of ways
# such that the formed number is divisible
# by 5 by removing digits
def countOfWays(s, k):

    N = len(s)

    # Stores the count of ways
    ans = 0

    # Find the count for string S
    for i in range(N):

        # If the digit is 5 or 0
        if (s[i] == '5' or s[i] == '0'):
            ans = (ans + exp_mod(2, i)) % MOD

    # Find the count of string for K
    # concatenation of string S
    q = exp_mod(2, N)
    qk = exp_mod(q, k)
    inv = exp_mod(q - 1, MOD - 2)

    # Find the total count
    ans = ans * (qk - 1) % MOD
    ans = ans * inv % MOD

    return ans

# Driver Code
S = "1256"
K = 1
print(countOfWays(S, K))

# This code is contributed by shivani
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{
  static long MOD = 1000000007;

  // Function to find the value of a^b
  // modulo 1000000007
  public static long exp_mod(long a, long b) {

    // Stores the resultant value a^b
    long ret = 1;

    // Find the value of a^b
    for (; b > 0; b >>= 1, a = a * a % MOD) {
      if ((b & 1) > 0)
        ret = ret * a % MOD;
    }

    return ret;
  }

  // Function to count the number of ways
  // such that the formed number is divisible
  // by 5 by removing digits
  public static long countOfWays(String s, int k) {
    int N = s.Length;

    // Stores the count of ways
    long ans = 0;

    // Find the count for string S
    for (int i = 0; i < N; i++) {

      // If the digit is 5 or 0
      if (s[i] == '5' || s[0] == '0') {
        ans = (ans + exp_mod(2, i)) % MOD;
      }
    }

    // Find the count of string for K
    // concatenation of string S
    long q = exp_mod(2, N);
    long qk = exp_mod(q, k);
    long inv = exp_mod(q - 1, MOD - 2);

    // Find the total count
    ans = ans * (qk - 1) % MOD;
    ans = ans * inv % MOD;

    return ans;
  }

  // Driver Code
  public static void Main(String []args) {
    String S = "1256";
    int K = 1;
    Console.WriteLine(countOfWays(S, K));

  }

}

// This code is contributed by shikhasingrajput
```

**Output:** 

```
4
```

***时间复杂度:** O(N*log K)*
***辅助空间:** O(1)*