# 对总和等于其“异或”的最多为 N 的对进行计数

> 原文:[https://www . geeksforgeeks . org/count-pairs-up-to-n-having-sum-等于-xor/](https://www.geeksforgeeks.org/count-pairs-up-to-n-having-sum-equal-to-their-xor/)

给定一个整数 **N** ，任务是计算对的数量 **(X，Y)** ，使得 **X + Y = X ^ Y** 和 **X + Y ≤ N** 。
***注:** ^表示* [*按位异或*](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) *。*

**示例:**

> **输入:** N = 3
> **输出:** 9
> **说明:**满足给定条件的对为{{0，0}、{0，1}、{1，0}、{0，2}、{2，0}、{3，0}、{0，3}、{2，1}、{1，2}
> 
> **输入:**N = 10
> T3】输出: 37

**天真方法:**最简单的方法是生成所有可能的对 **(X，Y)** 并检查条件 **X + Y = X ^ Y** 和 **X + Y ≤ N** 是否满足。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以基于观察到 **X+Y ≥ X ^ Y** 对于 **X** 和 **Y** 的任意值进行优化。考虑 **X** 和 **Y** 的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)。让**位(X，pos)** 和**位(Y，pos)** 为某一固定位置 **pos** 对应 **X** 和 **Y** 的位。条件 **X+Y = X^Y** 只有在{ **bit(X，pos)、bit(Y，pos)}∞{ { 1，0}、{0，1}、{0，0}}** 的情况下才会满足。换句话说， **X** 和 **Y** 不能在相同的位置设置位。

在有效的方法中，可以使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决问题。问题有重叠子问题和最优子结构。使用[记忆](https://www.geeksforgeeks.org/memoization-1d-2d-and-3d/)将子问题存储在 **dp[][]表**中，其中 **dp[i][bound]** 存储从**I ' th**位置到终点的答案， **bound** 是一个布尔变量，以确保数字之和不超过 **N.**

*   [将极限 **N** 转换为其二进制表示](https://www.geeksforgeeks.org/program-decimal-binary-conversion/)。将二进制表示存储在一个字符串中，比如说 **S** ，这样只迭代字符串的长度就足够了，而不是实际的限制。
*   通过执行以下步骤定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **IsSumEqualsXor(i，bound)** 。
    *   检查[基本情况](https://www.geeksforgeeks.org/recursion/)，如果 **i ==长度 S** ，那么**返回 1** ，因为已经形成有效对。
    *   如果状态 **dp[i][bound]** 的结果已经被计算，那么返回状态 **dp[i][bound]** 。
    *   在当前位置 **i** ， **{{0，0}，{0，1}，{1，0}}** 中的任意三对可以通过检查几个条件来分配。他们是
        *   如果**绑定的**为**真**且 **S** 即**S【I】**中的当前字符为**‘0’**，那么只有 **{0，0}** 才能作为有效对放置在当前位置。这样做是为了确保总和不超过 **N** 。
        *   否则， **{{0，0}、{0，1}、{1，0}}** 中的任意一对都可以放置，**绑定的**相应设置为真或假。
    *   在当前位置放置一个有效对后，递归调用索引 **(i + 1)处元素的 **IsSumEqualsXor** 函数。**
    *   返回所有可能的有效数字位置的总和作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// 2D array for memoization
int dp[1000][2];

// Recursive Function to count pairs
// (x, y) such that x+y = x^y
int IsSumEqualsXor(int i, int n,
                   bool bound, string& s)
{
    // If the string is traversed completely
    if (i == n)
        return 1;

    // If the current subproblem
    // is already calculated
    if (dp[i][bound] != -1)
        return dp[i][bound];

    int ans = 0;

    // If bound = 1 and  s[i] == '0',
    // only (0, 0) can be placed
    if (bound and s[i] == '0') {
        ans = IsSumEqualsXor(i + 1, n, 1, s);
    }

    // Otherwise
    else {
        // Placing (0, 1) and (1, 0) are
        // equivalent. Hence, multiply by 2.
        ans = 2
              * IsSumEqualsXor(i + 1, n,
                               bound & (s[i] == '1'), s);

        // Place (0, 0) at the current position.
        ans += IsSumEqualsXor(i + 1, n, 0, s);
    }

    // Return the answer
    return dp[i][bound] = ans;
}

// Utility Function to convert N
// to its binary representation
string convertToBinary(int n)
{
    string ans;
    while (n) {

        char rem = char(n % 2 + '0');
        ans.push_back(rem);
        n /= 2;
    }
    reverse(ans.begin(), ans.end());
    return ans;
}

// Function to count pairs (x, y)
// such that x + y = x^y
void IsSumEqualsXorUtil(int N)
{
    // Convert the number to
    // equivalent binary representation
    string s = convertToBinary(N);

    // Initialize dp array with -1.
    memset(dp, -1, sizeof dp);

    // Print answer returned by recursive function
    cout << IsSumEqualsXor(0, s.size(), 1, s) << endl;
}

// Driver code
int main()
{
    // Input
    int N = 10;

    // Function call
    IsSumEqualsXorUtil(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// 2D array for memoization
static int [][]dp = new int[1000][2];

// Recursive Function to count pairs
// (x, y) such that x+y = x^y
static int IsSumEqualsXor(int i, int n,
                   int bound, char[] s)
{
    // If the String is traversed completely
    if (i == n)
        return 1;

    // If the current subproblem
    // is already calculated
    if (dp[i][bound] != -1)
        return dp[i][bound];

    int ans = 0;

    // If bound = 1 and  s[i] == '0',
    // only (0, 0) can be placed
    if (bound!=0 && s[i] == '0') {
        ans = IsSumEqualsXor(i + 1, n, 1, s);
    }

    // Otherwise
    else {
        // Placing (0, 1) and (1, 0) are
        // equivalent. Hence, multiply by 2.
        ans = 2
              * IsSumEqualsXor(i + 1, n,
                               bound!=0 & (s[i] == '1')?1:0, s);

        // Place (0, 0) at the current position.
        ans += IsSumEqualsXor(i + 1, n, 0, s);
    }

    // Return the answer
    return dp[i][bound] = ans;
}
static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.valueOf(a);
}
// Utility Function to convert N
// to its binary representation
static String convertToBinary(int n)
{
    String ans="";
    while (n>0) {

        char rem = (char)(n % 2 + '0');
        ans+=(rem);
        n /= 2;
    }
    ans = reverse(ans);
    return ans;
}

// Function to count pairs (x, y)
// such that x + y = x^y
static void IsSumEqualsXorUtil(int N)
{
    // Convert the number to
    // equivalent binary representation
    String s = convertToBinary(N);

    // Initialize dp array with -1.
    for(int i = 0; i < dp.length; i++)
    {
        for (int j = 0; j < dp[0].length; j++) {
            dp[i][j] = -1;
        }
    }

    // Print answer returned by recursive function
    System.out.print(IsSumEqualsXor(0, s.length(), 1, s.toCharArray()) +"\n");
}

// Driver code
public static void main(String[] args)
{
    // Input
    int N = 10;

    // Function call
    IsSumEqualsXorUtil(N);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# 2D array for memoization
dp = [[-1 for i in range(2)]
          for j in range(1000)]

# Recursive Function to count pairs
# (x, y) such that x+y = x^y
def IsSumEqualsXor(i, n, bound, s):

    # If the string is traversed completely
    if (i == n):
        return 1

    # If the current subproblem
    # is already calculated
    if (dp[i][bound] != -1):
        return dp[i][bound]

    ans = 0

    # If bound = 1 and  s[i] == '0',
    # only (0, 0) can be placed
    if (bound and s[i] == '0'):
        ans = IsSumEqualsXor(i + 1, n, 1, s)

    # Otherwise
    else:

        # Placing (0, 1) and (1, 0) are
        # equivalent. Hence, multiply by 2.
        ans = 2 * IsSumEqualsXor(
            i + 1, n, bound & (s[i] == '1'), s)

        # Place (0, 0) at the current position.
        ans += IsSumEqualsXor(i + 1, n, 0, s)

    dp[i][bound] = ans

    # Return the answer
    return ans

# Utility Function to convert N
# to its binary representation
def convertToBinary(n):

    ans = []

    while (n):
        rem = chr(n % 2 + 48)
        ans.append(rem)
        n //= 2

    ans = ans[::-1]
    return ans

# Function to count pairs (x, y)
# such that x + y = x^y
def IsSumEqualsXorUtil(N):

    # Convert the number to
    # equivalent binary representation
    s = convertToBinary(N)

    # Print answer returned by recursive function
    print(IsSumEqualsXor(0, len(s), 1, s))

# Driver code
if __name__ == '__main__':

    # Input
    N = 10

    # Function call
    IsSumEqualsXorUtil(N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// 2D array for memoization
static int [,]dp = new int[1000, 2];

// Recursive Function to count pairs
// (x, y) such that x+y = x^y
static int IsSumEqualsXor(int i, int n,
                          int bound, char[] s)
{

    // If the String is traversed completely
    if (i == n)
        return 1;

    // If the current subproblem
    // is already calculated
    if (dp[i,bound] != -1)
        return dp[i,bound];

    int ans = 0;

    // If bound = 1 and  s[i] == '0',
    // only (0, 0) can be placed
    if (bound != 0 && s[i] == '0')
    {
        ans = IsSumEqualsXor(i + 1, n, 1, s);
    }

    // Otherwise
    else
    {

        // Placing (0, 1) and (1, 0) are
        // equivalent. Hence, multiply by 2.
        ans = 2 * IsSumEqualsXor(i + 1, n,
                                 bound != 0 &
                                 (s[i] == '1') ? 1 : 0, s);

        // Place (0, 0) at the current position.
        ans += IsSumEqualsXor(i + 1, n, 0, s);
    }

    // Return the answer
    return dp[i, bound] = ans;
}

static String reverse(String input)
{
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;

    for(l = 0; l < r; l++, r--)
    {
        char temp = a[l];
        a[l] = a[r];
        a[r] = temp;
    }
    return String.Join("", a);
}

// Utility Function to convert N
// to its binary representation
static String convertToBinary(int n)
{
    String ans = "";
    while (n > 0)
    {
        char rem = (char)(n % 2 + '0');
        ans += (rem);
        n /= 2;
    }
    ans = reverse(ans);
    return ans;
}

// Function to count pairs (x, y)
// such that x + y = x^y
static void IsSumEqualsXorUtil(int N)
{

    // Convert the number to
    // equivalent binary representation
    String s = convertToBinary(N);

    // Initialize dp array with -1.
    for(int i = 0; i < dp.GetLength(0); i++)
    {
        for(int j = 0; j < dp.GetLength(1); j++)
        {
            dp[i, j] = -1;
        }
    }

    // Print answer returned by recursive function
    Console.Write(IsSumEqualsXor(0, s.Length, 1,
                                 s.ToCharArray()) +"\n");
}

// Driver code
public static void Main(String[] args)
{

    // Input
    int N = 10;

    // Function call
    IsSumEqualsXorUtil(N);
}
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // 2D array for memoization
    let dp = new Array(1000);
    for(let i = 0; i < 1000; i++)
    {
        dp[i] = new Array(2);
    }

    // Recursive Function to count pairs
    // (x, y) such that x+y = x^y
    function IsSumEqualsXor(i, n, bound, s)
    {

        // If the String is traversed completely
        if (i == n)
            return 1;

        // If the current subproblem
        // is already calculated
        if (dp[i][bound] != -1)
            return dp[i][bound];

        let ans = 0;

        // If bound = 1 and  s[i] == '0',
        // only (0, 0) can be placed
        if (bound!=0 && s[i] == '0') {
            ans = IsSumEqualsXor(i + 1, n, 1, s);
        }

        // Otherwise
        else {
            // Placing (0, 1) and (1, 0) are
            // equivalent. Hence, multiply by 2.
            ans = 2
                  * IsSumEqualsXor(i + 1, n,
                                   bound!=0 & (s[i] == '1')?1:0, s);

            // Place (0, 0) at the current position.
            ans += IsSumEqualsXor(i + 1, n, 0, s);
        }

        // Return the answer
        dp[i][bound] = ans
        return dp[i][bound];
    }
    function reverse(input) {
        let a = input.split('');
        let l, r = a.length - 1;
        for (l = 0; l < r; l++, r--) {
            let temp = a[l];
            a[l] = a[r];
            a[r] = temp;
        }
        return a.join("");
    }

    // Utility Function to convert N
    // to its binary representation
    function convertToBinary(n)
    {
        let ans="";
        while (n>0) {

            let rem = String.fromCharCode(n % 2 + 48);
            ans+=(rem);
            n = parseInt(n / 2, 10);
        }
        ans = reverse(ans);
        return ans;
    }

    // Function to count pairs (x, y)
    // such that x + y = x^y
    function IsSumEqualsXorUtil(N)
    {
        // Convert the number to
        // equivalent binary representation
        let s = convertToBinary(N);

        // Initialize dp array with -1.
        for(let i = 0; i < dp.length; i++)
        {
            for (let j = 0; j < dp[0].length; j++) {
                dp[i][j] = -1;
            }
        }

        // Print answer returned by recursive function
        document.write(IsSumEqualsXor(0, s.length, 1, s.split('')) +"</br>");
    }

    // Input
    let N = 10;

    // Function call
    IsSumEqualsXorUtil(N);

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
37
```

***时间复杂度:**O(Log<sub>2</sub>N)*
*T8】辅助空间: O(Log <sub>2</sub> N)*