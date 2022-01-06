# 所需的最小一位数素数，其和等于 N

> 原文:[https://www . geesforgeks . org/最小一位数素数-必选-其和等于-n/](https://www.geeksforgeeks.org/minimum-number-of-single-digit-primes-required-whose-sum-is-equal-to-n/)

求所需的最小一位数素数，其和等于 N.
**例:**

```
Input: 11
Output: 3
Explanation: 5 + 3 + 3.
Another possibility is 3 + 3 + 3 + 2, but it is not
the minimal

Input: 12
Output: 2
Explanation: 7 + 5
```

**方法:**动态规划可以解决上述问题。观察结果是:

*   只有 4 个一位数的素数{2，3，5，7}。
*   如果可以通过对个位数的素数求和得到 N，那么 N-2、N-3、N-5 或 N-7 中的至少一个也是可达的。
*   所需的最小一位数素数将比构成 ***{N-2，N-3，N-5，N-7}之一所需的最小素数多一位。**T3】*

利用这些观察，建立了一个递归来解决这个问题。循环将是:

> dp[i] = 1 + min（dp[i-2]， dp[i-3]， dp[i-5]， dp[i-7]）

对于{2，3，5，7}，答案是 1。对于每个其他数字，使用观察 3，如果可能的话，尝试找到可能的最小值。
以下是上述方法的实现。

## C++

```
// CPP program to find the minimum number of single
// digit prime numbers required which when summed
// equals to a given number N.
#include <bits/stdc++.h>
using namespace std;

// function to check if i-th
// index is valid or not
bool check(int i, int val)
{
    if (i - val < 0)
        return false;
    return true;
}

// function to find the minimum number of single
// digit prime numbers required which when summed up
// equals to a given number N.
int MinimumPrimes(int n)
{
    int dp[n + 1];

    for (int i = 1; i <= n; i++)
        dp[i] = 1e9;

    dp[0] = dp[2] = dp[3] = dp[5] = dp[7] = 1;
    for (int i = 1; i <= n; i++) {

        if (check(i, 2))
            dp[i] = min(dp[i], 1 + dp[i - 2]);

        if (check(i, 3))
            dp[i] = min(dp[i], 1 + dp[i - 3]);

        if (check(i, 5))
            dp[i] = min(dp[i], 1 + dp[i - 5]);

        if (check(i, 7))
            dp[i] = min(dp[i], 1 + dp[i - 7]);
    }

    // Not possible
    if (dp[n] == (1e9))
        return -1;
    else
        return dp[n];
}

// Driver Code
int main()
{

    int n = 12;

    int minimal = MinimumPrimes(n);
    if (minimal != -1)
        cout << "Minimum number of single"
             << " digit primes required : "
             << minimal << endl;

    else
        cout << "Not possible";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum number
// of single digit prime numbers required
// which when summed equals to a given
// number N.

class Geeks {

// function to check if i-th
// index is valid or not
static boolean check(int i, int val)
{
    if (i - val < 0)
        return false;
    else
        return true;
}

// function to find the minimum number
// of single digit prime numbers required
// which when summed up equals to a given
// number N.
static double MinimumPrimes(int n)
{
    double[] dp;
    dp = new double[n+1];

    for (int i = 1; i <= n; i++)
        dp[i] = 1e9;

    dp[0] = dp[2] = dp[3] = dp[5] = dp[7] = 1;
    for (int i = 1; i <= n; i++) {

        if (check(i, 2))
            dp[i] = Math.min(dp[i], 1 + dp[i - 2]);

        if (check(i, 3))
            dp[i] = Math.min(dp[i], 1 + dp[i - 3]);

        if (check(i, 5))
            dp[i] = Math.min(dp[i], 1 + dp[i - 5]);

        if (check(i, 7))
            dp[i] = Math.min(dp[i], 1 + dp[i - 7]);
    }

    // Not possible
    if (dp[n] == (1e9))
        return -1;
    else
        return dp[n];
}

    // Driver Code
    public static void main(String args[])
    {

        int n = 12;
        int minimal = (int)MinimumPrimes(n);

        if (minimal != -1)
            System.out.println("Minimum number of single "+
                        "digit primes required: "+minimal);

        else
            System.out.println("Not Possible");

    }
}

// This code is contributed ankita_saini
```

## 蟒蛇 3

```
# Python3 program to find the minimum number
# of single digit prime numbers required 
# which when summed equals to a given 
# number N.

# function to check if i-th
# index is valid or not

def check(i,val):
    if i-val<0:
        return False
    return True

# function to find the minimum number of single
# digit prime numbers required which when summed up
# equals to a given number N.

def MinimumPrimes(n):
    dp=[10**9]*(n+1)
    dp[0]=dp[2]=dp[3]=dp[5]=dp[7]=1
    for i in range(1,n+1):
        if check(i,2):
            dp[i]=min(dp[i],1+dp[i-2])
        if check(i,3):
            dp[i]=min(dp[i],1+dp[i-3])
        if check(i,5):
            dp[i]=min(dp[i],1+dp[i-5])
        if check(i,7):
            dp[i]=min(dp[i],1+dp[i-7])

    # Not possible
    if dp[n]==10**9:
        return -1
    else:
        return dp[n]

# Driver Code
if __name__ == "__main__":
    n=12
    minimal=MinimumPrimes(n)
    if minimal!=-1:
        print("Minimum number of single digit primes required : ",minimal)
    else:
        print("Not possible")
#This code is contributed Saurabh Shukla
```

## C#

```
// C# program to find the
// minimum number of single
// digit prime numbers required
// which when summed equals to
// a given number N.
using System;

class GFG
{

// function to check if i-th
// index is valid or not
static Boolean check(int i,
                     int val)
{
    if (i - val < 0)
        return false;
    else
        return true;
}

// function to find the
// minimum number of single
// digit prime numbers
// required which when summed
// up equals to a given
// number N.
static double MinimumPrimes(int n)
{
    double[] dp;
    dp = new double[n + 1];

    for (int i = 1; i <= n; i++)
        dp[i] = 1e9;

    dp[0] = dp[2] = dp[3] = dp[5] = dp[7] = 1;
    for (int i = 1; i <= n; i++)
    {
        if (check(i, 2))
            dp[i] = Math.Min(dp[i], 1 +
                             dp[i - 2]);

        if (check(i, 3))
            dp[i] = Math.Min(dp[i], 1 +
                             dp[i - 3]);

        if (check(i, 5))
            dp[i] = Math.Min(dp[i], 1 +
                             dp[i - 5]);

        if (check(i, 7))
            dp[i] = Math.Min(dp[i], 1 +
                             dp[i - 7]);
    }

    // Not possible
    if (dp[n] == (1e9))
        return -1;
    else
        return dp[n];
}

// Driver Code
public static void Main(String []args)
{
    int n = 12;
    int minimal = (int)MinimumPrimes(n);

    if (minimal != -1)
        Console.WriteLine("Minimum number of single " +
                            "digit primes required: " +
                                              minimal);
    else
        Console.WriteLine("Not Possible");

}
}

// This code is contributed
// by Ankita_Saini
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the minimum
// number of single digit prime
// numbers required which when summed
// equals to a given number N.

// function to check if i-th
// index is valid or not
function check($i, $val)
{
    if ($i - $val < 0)
        return false;
    return true;
}

// function to find the minimum
// number of single digit prime
// numbers required which when
// summed up equals to a given
// number N.
function MinimumPrimes($n)
{

    for ($i = 1; $i<= $n; $i++)
        $dp[$i] = 1e9;

    $dp[0] = $dp[2] = $dp[3] = $dp[5] = $dp[7] = 1;
    for ($i = 1; $i <= $n; $i++)
    {

        if (check($i, 2))
            $dp[$i] = min($dp[$i], 1 +
                          $dp[$i - 2]);

        if (check($i, 3))
            $dp[$i] = min($dp[$i], 1 +
                          $dp[$i - 3]);

        if (check($i, 5))
            $dp[$i] = min($dp[$i], 1 +
                          $dp[$i - 5]);

        if (check($i, 7))
            $dp[$i] = min($dp[$i], 1 +
                          $dp[$i - 7]);
    }

    // Not possible
    if ($dp[$n] == (1e9))
        return -1;
    else
        return $dp[$n];
}

// Driver Code
$n = 12;

$minimal = MinimumPrimes($n);
if ($minimal != -1)
{
    echo("Minimum number of single " .
           "digit primes required :");
    echo( $minimal );
}
else
{
    echo("Not possible");
}

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the minimum
// number of single digit prime
// numbers required which when summed
// equals to a given number N.

// function to check if i-th
// index is valid or not
function check(i, val)
{
    if (i - val < 0)
        return false;
    return true;
}

// function to find the minimum
// number of single digit prime
// numbers required which when
// summed up equals to a given
// number N.
function MinimumPrimes(n)
{
    let dp = new Array(n + 1)

    for (let i = 1; i<= n; i++)
        dp[i] = 1e9;

    dp[0] = dp[2] = dp[3] = dp[5] = dp[7] = 1;
    for (let i = 1; i <= n; i++)
    {

        if (check(i, 2))
            dp[i] = Math.min(dp[i], 1 +
                          dp[i - 2]);

        if (check(i, 3))
            dp[i] = Math.min(dp[i], 1 +
                          dp[i - 3]);

        if (check(i, 5))
            dp[i] = Math.min(dp[i], 1 +
                          dp[i - 5]);

        if (check(i, 7))
            dp[i] = Math.min(dp[i], 1 +
                          dp[i - 7]);
    }

    // Not possible
    if (dp[n] == (1e9))
        return -1;
    else
        return dp[n];
}

// Driver Code
let n = 12;

let minimal = MinimumPrimes(n);
if (minimal != -1)
{
    document.write("Minimum number of single "  + "digit primes required :");
    document.write( minimal );
}
else
{
    document.write("Not possible");
}

// This code is contributed
// by gfgking

</script>
```

**Output:** 

```
Minimum number of single digit primes required : 2
```

**时间复杂度:**O(N)
T3】注:如果是多个查询，可以预先计算 dp[]数组，我们可以回答 O(1)中的每个查询。