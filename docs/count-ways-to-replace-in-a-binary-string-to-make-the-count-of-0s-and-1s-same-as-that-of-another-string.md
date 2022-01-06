# 计算替换“？”的方法在二进制字符串中使 0 和 1 的计数与另一个字符串相同

> 原文:[https://www . geesforgeks . org/count-way-in-replace-in-a-in-binary-string-to-make-count-of-0-and-1s-同另一个字符串/](https://www.geeksforgeeks.org/count-ways-to-replace-in-a-binary-string-to-make-the-count-of-0s-and-1s-same-as-that-of-another-string/)

给定两个大小分别为 **N** 和 **M** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/)**【S1】**和 **S2** ，使得字符串 **S2** 也包含字符**“？”**，任务是找到多少种方法来代替**'？'**在弦**中 S2** 使得弦 **中 **0s** 和 **1s** 的[计数与弦 **S1** 中的相同。](https://www.geeksforgeeks.org/count-of-sub-strings-with-equal-consecutive-0s-and-1s/)**

**示例:**

> **输入:**S1 =“1010”，S2 =“10？?"
> **输出:** 2
> **说明:**
> 以下是替换的方式？在弦乐 S2:
> 
> 1.  替换"？?"在字符串“01”中，S2 修改了字符串 S2 =“1001”。现在，字符串 S1 和 S2 中 0 和 1 的计数是相同的。
> 2.  替换"？?"在字符串“10”中，S2 修改了字符串 S2 =“1010”。现在，字符串 S1 和 S2 中 0 和 1 的计数是相同的。
> 
> 因此，路的总数是 2。
> 
> **输入:**S1 =“0000”，S2 =“？？10?"
> T3】输出: 0

**方法:**给定的问题可以用[组合](https://www.geeksforgeeks.org/category/algorithm/combinatorial/)的概念来解决。按照以下步骤解决问题:

*   初始化变量，比如说 **sum1** 为 **0** ， **sum2** 为 **0** ，存储给定字符串 **S1** 和 **S2** 中 **0s** 和 **1s** 的个数。
*   初始化一个变量，比如说为 **0** ，它存储替换**“？”满足给定标准的字符串 **S2** 中的**。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)**【S1】**，如果当前字符为 **1** ，则将 **sum1** 的值增加1。否则，将 **sum1** 的值递减 **1** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S2** ，如果当前字符为 **1** ，则将 **sum2** 的值增加 **1** 或者如果当前字符为 **0** ，则将 **sum2** 的值减少 **1** 。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **t** ，如果当前字符为**“+”**，则将 **sum2** 的值增加 **1** 。否则，将 **K** 的值增加 **1** 。
*   初始化一个变量，比如存储 **sum1** 和 **sum2** 的绝对差值的 **P** 。
*   如果 **P** 的值至少是**K**或者**(K–P)**的值是奇数，那么没有可能的方法来替换**'？'**因此打印 **0** 。否则，打印**<sup>K</sup>C<sub>(P+K)/2</sub>**的值作为路的合成计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the factorial of
// the given number N
int fact(int n)
{
    // Stores the factorial
    int res = 1;

    // Iterate over the range [2, N]
    for (int i = 2; i <= n; i++) {
        res = res * i;
    }

    // Return the resultant result
    return res;
}

// Function to find the number of ways
// of choosing r objects from n
// distinct objects
int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to replace '?' in string t to get
// the same count of 0s and 1s in the
// string S and T
void countWays(string s, string t)
{
    int n = s.length();
    int sum1 = 0, sum2 = 0, K = 0;

    // Traverse the string s
    for (int i = 0; i < n; i++) {

        // If the current character
        // is 1
        if (s[i] == '1') {

            // Update the value of
            // the sum1
            sum1++;
        }

        // Otherwise
        else
            sum1--;
    }

    int m = t.length();

    // Traverse the string t
    for (int i = 0; i < m; i++) {

        // If the current character
        // is 1, then update the
        // value of sum2
        if (t[i] == '1') {
            sum2++;
        }

        // If the current character
        // is 0
        else if (t[i] == '0') {
            sum2--;
        }

        // Otherwise, update the
        // value of K
        else
            K++;
    }

    int P = abs(sum1 - sum2);

    // Check if P is greater than K
    // or if K-P is odd
    if (P > K or (K - P) % 2) {
        cout << 0;
        return;
    }

    // Print the count of ways
    cout << nCr(K, (P + K) / 2);
}

// Driver Code
int main()
{
    string S1 = "1010";
    string S2 = "10??";
    countWays(S1, S2);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

class GFG{

    // Function to find the factorial of
    // the given number N
    static int fact(int n)
    {
        // Stores the factorial
        int res = 1;

        // Iterate over the range [2, N]
        for (int i = 2; i <= n; i++) {
            res = res * i;
        }

        // Return the resultant result
        return res;
    }

    // Function to find the number of ways
    // of choosing r objects from n
    // distinct objects
    static int nCr(int n, int r)
    {
        return fact(n) / (fact(r) * fact(n - r));
    }

    // Function to find the number of ways
    // to replace '?' in string t to get
    // the same count of 0s and 1s in the
    // string S and T
    static void countWays(String s, String t)
    {
        int n = s.length();
        int sum1 = 0, sum2 = 0, K = 0;

        // Traverse the string s
        for (int i = 0; i < n; i++) {

            // If the current character
            // is 1
            if (s.charAt(i) == '1') {

                // Update the value of
                // the sum1
                sum1++;
            }

            // Otherwise
            else
                sum1--;
        }

        int m = t.length();

        // Traverse the string t
        for (int i = 0; i < m; i++) {

            // If the current character
            // is 1, then update the
            // value of sum2
            if (t.charAt(i) == '1') {
                sum2++;
            }

            // If the current character
            // is 0
            else if (t.charAt(i) == '0') {
                sum2--;
            }

            // Otherwise, update the
            // value of K
            else
                K++;
        }

        int P = Math.abs(sum1 - sum2);

        // Check if P is greater than K
        // or if K-P is odd
        if ((P > K) || (K - P) % 2==1) {
            System.out.println(0);
        return;
    }

        // Print the count of ways
        System.out.println(nCr(K, (P + K) / 2));
    }

    // Driver Code
    public static void main(String[] args)
    {
        String S1 = "1010";
        String S2 = "10??";
        countWays(S1, S2);
    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to find the factorial of
# the given number N
def fact(n):
    # Stores the factorial
    res = 1

    # Iterate over the range [2, N]
    for i in range(2,n+1,1):
        res = res * i

    # Return the resultant result
    return res

# Function to find the number of ways
# of choosing r objects from n
# distinct objects
def nCr(n, r):
    return fact(n) // (fact(r) * fact(n - r))

# Function to find the number of ways
# to replace '?' in string t to get
# the same count of 0s and 1s in the
# string S and T
def countWays(s, t):
    n = len(s);
    sum1 = 0
    sum2 = 0
    K = 0

    # Traverse the string s
    for i in range(n):
        # If the current character
        # is 1
        if (s[i] == '1'):

            # Update the value of
            # the sum1
            sum1 += 1

        # Otherwise
        else:
            sum1 -= 1

    m = len(t)

    # Traverse the string t
    for i in range(m):
        # If the current character
        # is 1, then update the
        # value of sum2
        if (t[i] == '1'):
            sum2 += 1

        # If the current character
        # is 0
        elif (t[i] == '0'):
            sum2 -= 1

        # Otherwise, update the
        # value of K
        else:
            K += 1

    P = abs(sum1 - sum2)

    # Check if P is greater than K
    # or if K-P is odd
    if (P > K or (K - P) % 2):
        print(0)
        return

    # Print the count of ways
    print(nCr(K, (P + K) // 2))

# Driver Code
if __name__ == '__main__':
    S1 = "1010"
    S2 = "10??"
    countWays(S1, S2)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the factorial of
// the given number N
static int fact(int n)
{
    // Stores the factorial
    int res = 1;

    // Iterate over the range [2, N]
    for (int i = 2; i <= n; i++) {
        res = res * i;
    }

    // Return the resultant result
    return res;
}

// Function to find the number of ways
// of choosing r objects from n
// distinct objects
static int nCr(int n, int r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to replace '?' in string t to get
// the same count of 0s and 1s in the
// string S and T
static void countWays(string s, string t)
{
    int n = s.Length;
    int sum1 = 0, sum2 = 0, K = 0;

    // Traverse the string s
    for (int i = 0; i < n; i++) {

        // If the current character
        // is 1
        if (s[i] == '1') {

            // Update the value of
            // the sum1
            sum1++;
        }

        // Otherwise
        else
            sum1--;
    }

    int m = t.Length;

    // Traverse the string t
    for (int i = 0; i < m; i++) {

        // If the current character
        // is 1, then update the
        // value of sum2
        if (t[i] == '1') {
            sum2++;
        }

        // If the current character
        // is 0
        else if (t[i] == '0') {
            sum2--;
        }

        // Otherwise, update the
        // value of K
        else
            K++;
    }

    int P = Math.Abs(sum1 - sum2);

    // Check if P is greater than K
    // or if K-P is odd
    if ((P > K) || ((K - P) % 2) != 0) {
        Console.WriteLine(0);
        return;
    }

    // Print the count of ways
    Console.WriteLine( nCr(K, (P + K) / 2));
}

// Driver code
static public void Main()
{
    string S1 = "1010";
    string S2 = "10??";
    countWays(S1, S2);
}
}

// This code is contributed by target_2.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the factorial of
// the given number N
function fact(n)
{

    // Stores the factorial
    let res = 1;

    // Iterate over the range [2, N]
    for(let i = 2; i <= n; i++)
    {
        res = res * i;
    }

    // Return the resultant result
    return res;
}

// Function to find the number of ways
// of choosing r objects from n
// distinct objects
function nCr(n, r)
{
    return fact(n) / (fact(r) * fact(n - r));
}

// Function to find the number of ways
// to replace '?' in string t to get
// the same count of 0s and 1s in the
// string S and T
function countWays(s, t)
{
    let n = s.length;
    let sum1 = 0, sum2 = 0, K = 0;

    // Traverse the string s
    for(let i = 0; i < n; i++)
    {

        // If the current character
        // is 1
        if (s[i] == '1')
        {

            // Update the value of
            // the sum1
            sum1++;
        }

        // Otherwise
        else
            sum1--;
    }

    let m = t.length;

    // Traverse the string t
    for(let i = 0; i < m; i++)
    {

        // If the current character
        // is 1, then update the
        // value of sum2
        if (t[i] == '1')
        {
            sum2++;
        }

        // If the current character
        // is 0
        else if (t[i] == '0')
        {
            sum2--;
        }

        // Otherwise, update the
        // value of K
        else
            K++;
    }

    let P = Math.abs(sum1 - sum2);

    // Check if P is greater than K
    // or if K-P is odd
    if (P > K || (K - P) % 2)
    {
        document.write(0);
        return;
    }

    // Print the count of ways
    document.write(nCr(K, (P + K) / 2));
}

// Driver Code
let S1 = "1010";
let S2 = "10??";

countWays(S1, S2);

// This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(max(N，M))*
***辅助空间:** O(1)*