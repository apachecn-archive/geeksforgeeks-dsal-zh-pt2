# 统计特殊排列的数量

> 原文:[https://www . geeksforgeeks . org/count-特殊排列数/](https://www.geeksforgeeks.org/count-the-number-of-special-permutations/)

给定两个正整数 **n** 和 **k** ，任务是计算特殊排列的数量。一种特殊的排列 **P** 被定义为第一个 **n** 自然数的排列，其中至少存在**(n–k)**索引，使得 **P <sub>i</sub> = i** 。
**先决条件:** [错乱](https://www.geeksforgeeks.org/count-derangements-permutation-such-that-no-element-appears-in-its-original-position/)

**示例:**

> **输入:** n = 4，k = 2
> **输出:** 7
> {1，2，3，4}、{1，2，4，3}、{4，2，3，1}、{2，1，3，4}、{1，4，3，2}、{1，3，2，4}和{3，2，1，4}是唯一可能的特殊排列。
> 
> **输入:** n = 5，k = 3
> T3】输出: 31

**方法:**让函数**f<sub>x</sub>T5】表示存在精确的 **x** 索引的特殊排列的数量，使得 **P <sub>i</sub> = i** 。因此，所需的答案是:**

> f<sub>(n–k)</sub>+f<sub>(n–k+1)</sub>+f<sub>(n–k+2)</sub>+…+f<sub>(n–1)</sub>+f<sub>n</sub>

现在，可以通过从 **n** 中选择 **x** 指数来计算**f<sub>x</sub>T3，其中 **P <sub>i</sub> = i** 并计算**(n–I)**其他指数的混乱数量，至于它们**P<sub>I</sub>T17】不应等于 **i** ，然后将结果乘以 **<sup>n</sup>******

下面是上述方法的实现:

## C++

```
// C++ program to count the number
// of required permutations
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to return the number of ways
// to choose r objects out of n objects
int nCr(int n, int r)
{
    int ans = 1;
    if (r > n - r)
        r = n - r;
    for (int i = 0; i < r; i++) {
        ans *= (n - i);
        ans /= (i + 1);
    }
    return ans;
}

// Function to return the number
// of derangements of n
int countDerangements(int n)
{
    int der[n + 1];

    der[0] = 1;
    der[1] = 0;
    der[2] = 1;

    for (int i = 3; i <= n; i++)
        der[i] = (i - 1) * (der[i - 1]
                         + der[i - 2]);
    return der[n];
}

// Function to return the required
// number of permutations
ll countPermutations(int n, int k)
{
    ll ans = 0;
    for (int i = n - k; i <= n; i++) {

        // Ways to choose i indices from n indices
        int ways = nCr(n, i);

        // Dearangements of (n - i) indices
        ans += ways * countDerangements(n - i);
    }
    return ans;
}

// Driver Code to test above functions
int main()
{
    int n = 5, k = 3;
    cout << countPermutations(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of required permutations

public class GFG{

    // Function to return the number of ways
    // to choose r objects out of n objects
    static int nCr(int n, int r)
    {
        int ans = 1;
        if (r > n - r)
            r = n - r;
        for (int i = 0; i < r; i++) {
            ans *= (n - i);
            ans /= (i + 1);
        }
        return ans;
    }

    // Function to return the number
    // of derangements of n
    static int countDerangements(int n)
    {
        int der[] = new int[ n + 3];

        der[0] = 1;
        der[1] = 0;
        der[2] = 1;

        for (int i = 3; i <= n; i++)
            der[i] = (i - 1) * (der[i - 1]
                            + der[i - 2]);
        return der[n];
    }

    // Function to return the required
    // number of permutations
    static int countPermutations(int n, int k)
    {
        int ans = 0;
        for (int i = n - k; i <= n; i++) {

            // Ways to choose i indices from n indices
            int ways = nCr(n, i);

            // Dearangements of (n - i) indices
            //System.out.println(ans) ;
            ans += (ways * countDerangements(n- i));
        }
        return ans;
    }

    // Driver Code to test above functions
    public static void main(String []args)
    {
        int n = 5, k = 3;
        System.out.println(countPermutations(n, k)) ;
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python 3 program to count the number
# of required permutation

# function to return the number of ways
# to chooser objects out of n objects
def nCr(n, r):
    ans = 1
    if r > n - r:
        r = n - r
    for i in range(r):
        ans *= (n - i)
        ans /= (i + 1)
    return ans

# function to return the number of
# degrangemnets of n
def countDerangements(n):
    der = [0 for i in range(n + 3)]

    der[0] = 1
    der[1] = 0
    der[2] = 1

    for i in range(3, n + 1):
        der[i] = (i - 1) * (der[i - 1] +
                            der[i - 2])

    return der[n]

# function to return the required
# number of permutations
def countPermutations(n, k):
    ans = 0
    for i in range(n - k, n + 1):

        # ways to chose i indices
        # from n indices
        ways = nCr(n, i)

        # Dearrangements of (n-i) indices
        ans += ways * countDerangements(n - i)
    return ans

# Driver Code
n, k = 5, 3

print(countPermutations(n, k))

# This code is contributed by
# Mohit kumar 29 (IIIT gwalior)
```

## C#

```

// C# program to count the number
// of required permutations
using System;   
public class GFG{

    // Function to return the number of ways
    // to choose r objects out of n objects
    static int nCr(int n, int r)
    {
        int ans = 1;
        if (r > n - r)
            r = n - r;
        for (int i = 0; i < r; i++) {
            ans *= (n - i);
            ans /= (i + 1);
        }
        return ans;
    }

    // Function to return the number
    // of derangements of n
    static int countDerangements(int n)
    {
        int []der = new int[ n + 3];

        der[0] = 1;
        der[1] = 0;
        der[2] = 1;

        for (int i = 3; i <= n; i++)
            der[i] = (i - 1) * (der[i - 1]
                            + der[i - 2]);
        return der[n];
    }

    // Function to return the required
    // number of permutations
    static int countPermutations(int n, int k)
    {
        int ans = 0;
        for (int i = n - k; i <= n; i++) {

            // Ways to choose i indices from n indices
            int ways = nCr(n, i);

            // Dearangements of (n - i) indices
            //System.out.println(ans) ;
            ans += (ways * countDerangements(n- i));
        }
        return ans;
    }

    // Driver Code to test above functions
    public static void Main()
    {
        int n = 5, k = 3;
        Console.WriteLine(countPermutations(n, k)) ;
    }
}
// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count the number
// of required permutations

// Function to return the number of ways
// to choose r objects out of n objects
function nCr($n, $r)
{
    $ans = 1;
    if ($r > $n - $r)
        $r = $n - $r;
    for ($i = 0; $i < $r; $i++)
    {
        $ans *= ($n - $i);
        $ans /= ($i + 1);
    }
    return $ans;
}

// Function to return the number
// of derangements of n
function countDerangements($n)
{
    $der = array($n + 1);

    $der[0] = 1;
    $der[1] = 0;
    $der[2] = 1;

    for ($i = 3; $i <= $n; $i++)
        $der[$i] = ($i - 1) *
                   ($der[$i - 1] +
                    $der[$i - 2]);
    return $der[$n];
}

// Function to return the required
// number of permutations
function countPermutations($n, $k)
{
    $ans = 0;
    for ($i = $n - $k; $i <= $n; $i++)
    {

        // Ways to choose i indices
        // from n indices
        $ways = nCr($n, $i);

        // Dearangements of (n - i) indices
        $ans += $ways * countDerangements($n - $i);
    }
    return $ans;
}

// Driver Code
$n = 5;
$k = 3;
echo (countPermutations($n, $k));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

      // JavaScript program to count the number
      // of required permutations
      // Function to return the number of ways
      // to choose r objects out of n objects
      function nCr(n, r) {
        var ans = 1;
        if (r > n - r) r = n - r;
        for (var i = 0; i < r; i++) {
          ans *= n - i;
          ans /= i + 1;
        }
        return ans;
      }

      // Function to return the number
      // of derangements of n
      function countDerangements(n) {
        var der = [...Array(n + 1)];

        der[0] = 1;
        der[1] = 0;
        der[2] = 1;

        for (var i = 3; i <= n; i++)
          der[i] = (i - 1) * (der[i - 1] + der[i - 2]);
        return der[n];
      }

      // Function to return the required
      // number of permutations
      function countPermutations(n, k) {
        var ans = 0;
        for (var i = n - k; i <= n; i++) {
          // Ways to choose i indices from n indices
          var ways = nCr(n, i);

          // Dearangements of (n - i) indices
          ans += ways * countDerangements(n - i);
        }
        return ans;
      }

      // Driver Code to test above functions
      var n = 5,
        k = 3;
      document.write(countPermutations(n, k));

</script>
```

**Output:** 

```
31
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(N)