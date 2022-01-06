# 鸡蛋掉落难题(二项式系数和二分搜索法解)

> 原文:[https://www . geesforgeks . org/eggs-dropping-拼图-二项式-系数和二进制-搜索-解答/](https://www.geeksforgeeks.org/eggs-dropping-puzzle-binomial-coefficient-and-binary-search-solution/)

给定 n 个鸡蛋和 k 个楼层，找到最坏情况下所需的最小试验次数，以找到所有楼层都安全的楼层。如果从地板上掉下一个鸡蛋不会打破鸡蛋，那么地板是安全的。请看 [n 蛋 k 层。](https://www.geeksforgeeks.org/dynamic-programming-set-11-egg-dropping-puzzle/)完整的语句

**例**

```
Input : n = 2, k = 10
Output : 4
We first try from 4-th floor. Two cases arise,
(1) If egg breaks, we have one egg left so we
    need three more trials.
(2) If egg does not break, we try next from 7-th
    floor. Again two cases arise.
We can notice that if we choose 4th floor as first
floor, 7-th as next floor and 9 as next of next floor,
we never exceed more than 4 trials.

Input : n = 2\. k = 100
Output : 14
```

我们已经讨论了 [2 个鸡蛋和 k 层](https://www.geeksforgeeks.org/egg-dropping-puzzle-with-2-eggs-and-k-floors/)的问题。我们还讨论了一个[动态规划解决方案](https://www.geeksforgeeks.org/egg-dropping-puzzle-dp-11/)来寻找解决方案。动态规划解决方案基于问题的递归性质。让我们从不同的角度来看讨论的递归公式。

**我们可以用 x 审判覆盖多少层？**
当我们掉了一个鸡蛋，就会出现两种情况。

1.  如果鸡蛋破了，那么剩下的就是 x-1 试验和 n-1 鸡蛋。
2.  如果鸡蛋没有破裂，那么我们就剩下 x-1 试验和 n 个鸡蛋

```
Let maxFloors(x, n) be the maximum number of floors 
that we can cover with x trials and n eggs. From above 
two cases, we can write.

maxFloors(x, n) = maxFloors(x-1, n-1) + maxFloors(x-1, n) + 1
For all x >= 1 and n >= 1

Base cases : 
We can't cover any floor with 0 trials or 0 eggs
maxFloors(0, n) = 0
maxFloors(x, 0) = 0

Since we need to cover k floors, 
maxFloors(x, n) >= k           ----------(1)

The above recurrence simplifies to following,
Refer this for proof.

maxFloors(x, n) = &Sum;xCi
                  1 <= i <= n   ----------(2)
Here C represents Binomial Coefficient.

From above two equations, we can say.
&Sum;xCj  >= k
1 <= i <= n
Basically we need to find minimum value of x
that satisfies above inequality. We can find
such x using Binary Search.
```

## C++

```
// C++ program to find minimum
// number of trials in worst case.
#include <bits/stdc++.h>

using namespace std;

// Find sum of binomial coefficients xCi
// (where i varies from 1 to n).
int binomialCoeff(int x, int n, int k)
{
    int sum = 0, term = 1;
    for (int i = 1; i <= n; ++i) {
        term *= x - i + 1;
        term /= i;
        sum += term;
          if(sum>k)
          return sum;
    }
    return sum;
}

// Do binary search to find minimum
// number of trials in worst case.
int minTrials(int n, int k)
{
    // Initialize low and high as 1st
    // and last floors
    int low = 1, high = k;

    // Do binary search, for every mid,
    // find sum of binomial coefficients and
    // check if the sum is greater than k or not.
    while (low < high) {
        int mid = (low + high) / 2;
        if (binomialCoeff(mid, n, k) < k)
            low = mid + 1;
        else
            high = mid;
    }

    return low;
}

/* Driver code*/
int main()
{
    cout << minTrials(2, 10);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// number of trials in worst case.
class Geeks {

// Find sum of binomial coefficients xCi
// (where i varies from 1 to n). If the sum
// becomes more than K
static int binomialCoeff(int x, int n, int k)
{
    int sum = 0, term = 1;
    for (int i = 1; i <= n && sum < k; ++i) {
        term *= x - i + 1;
        term /= i;
        sum += term;
    }
    return sum;
}

// Do binary search to find minimum
// number of trials in worst case.
static int minTrials(int n, int k)
{
    // Initialize low and high as 1st
    //and last floors
    int low = 1, high = k;

    // Do binary search, for every mid,
    // find sum of binomial coefficients and
    // check if the sum is greater than k or not.
    while (low < high) {
        int mid = (low + high) / 2;
        if (binomialCoeff(mid, n, k) < k)
            low = mid + 1;
        else
            high = mid;
    }

    return low;
}

/* Driver code*/
public static void main(String args[])
{
    System.out.println(minTrials(2, 10));
}
}

// This code is contributed by ankita_saini
```

## 蟒蛇 3

```
# Python3 program to find minimum
# number of trials in worst case.

# Find sum of binomial coefficients
# xCi (where i varies from 1 to n).
# If the sum becomes more than K
def binomialCoeff(x, n, k):

    sum = 0;
    term = 1;
    i = 1;
    while(i <= n and sum < k):
        term *= x - i + 1;
        term /= i;
        sum += term;
        i += 1;
    return sum;

# Do binary search to find minimum
# number of trials in worst case.
def minTrials(n, k):

    # Initialize low and high as
    # 1st and last floors
    low = 1;
    high = k;

    # Do binary search, for every
    # mid, find sum of binomial
    # coefficients and check if
    # the sum is greater than k or not.
    while (low < high):

        mid = int((low + high) / 2);
        if (binomialCoeff(mid, n, k) < k):
            low = mid + 1;
        else:
            high = mid;

    return int(low);

# Driver Code
print(minTrials(2, 10));

# This code is contributed
# by mits
```

## C#

```
// C# program to find minimum
// number of trials in worst case.
using System;

class GFG
{

// Find sum of binomial coefficients
// xCi (where i varies from 1 to n).
// If the sum becomes more than K
static int binomialCoeff(int x,
                         int n, int k)
{
    int sum = 0, term = 1;
    for (int i = 1;
             i <= n && sum < k; ++i)
    {
        term *= x - i + 1;
        term /= i;
        sum += term;
    }
    return sum;
}

// Do binary search to find minimum
// number of trials in worst case.
static int minTrials(int n, int k)
{
    // Initialize low and high
    // as 1st and last floors
    int low = 1, high = k;

    // Do binary search, for every
    // mid, find sum of binomial
    // coefficients and check if the
    // sum is greater than k or not.
    while (low < high)
    {
        int mid = (low + high) / 2;
        if (binomialCoeff(mid, n, k) < k)
            low = mid + 1;
        else
            high = mid;
    }

    return low;
}

// Driver Code
public static void Main()
{
    Console.WriteLine(minTrials(2, 10));
}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum
// number of trials in worst case.

// Find sum of binomial coefficients
// xCi (where i varies from 1 to n).
// If the sum becomes more than K
function binomialCoeff($x, $n, $k)
{
    $sum = 0; $term = 1;
    for ($i = 1; $i <= $n &&
         $sum < $k; ++$i)
    {
        $term *= $x - $i + 1;
        $term /= $i;
        $sum += $term;
    }
    return $sum;
}

// Do binary search to find minimum
// number of trials in worst case.
function minTrials($n, $k)
{
    // Initialize low and high as
    // 1st and last floors
    $low = 1; $high = $k;

    // Do binary search, for every
    // mid, find sum of binomial
    // coefficients and check if
    // the sum is greater than k or not.
    while ($low < $high)
    {
        $mid = ($low + $high) / 2;
        if (binomialCoeff($mid, $n, $k) < $k)
            $low = $mid + 1;
        else
            $high = $mid;
    }

    return (int)$low;
}

// Driver Code
echo minTrials(2, 10);

// This code is contributed
// by Akanksha Rai(Abby_akku)
?>
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// number of trials in worst case.

// Find sum of binomial coefficients xCi
// (where i varies from 1 to n). If the sum
// becomes more than K
function binomialCoeff(x, n, k)
{
    var sum = 0, term = 1;
    for(var i = 1; i <= n && sum < k; ++i)
    {
        term *= x - i + 1;
        term /= i;
        sum += term;
    }
    return sum;
}

// Do binary search to find minimum
// number of trials in worst case.
function minTrials(n, k)
{

    // Initialize low and high as 1st
    //and last floors
    var low = 1, high = k;

    // Do binary search, for every mid,
    // find sum of binomial coefficients and
    // check if the sum is greater than k or not.
    while (low < high)
    {
        var mid = parseInt((low + high) / 2);
        if (binomialCoeff(mid, n, k) < k)
            low = mid + 1;
        else
            high = mid;
    }
    return low;
}

// Driver code
document.write(minTrials(2, 10));

// This code is contributed by shivanisinghss2110

</script>
```

**Output**

```
4
```

**时间复杂度:** O(n Log k)