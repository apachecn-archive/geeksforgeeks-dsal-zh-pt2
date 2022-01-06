# 产品没有重复质因数的子阵计数

> 原文:[https://www . geesforgeks . org/count-subarrays-谁的产品不重复-质因数/](https://www.geeksforgeeks.org/count-subarrays-whose-product-doesnt-repeating-prime-factor/)

给定一个整数数组。求结果数素分解中所有元素乘积不含重复素因子的子阵总数。
**例:**

```
Input: 2 3 9
Output: 3
Explanation:
Total sub-array are:-
{2}, {3}, {9}, {2, 3}, {3, 9}, {2, 3, 9}

Subarray which violets the property are:-
{9}       -> {3 * 3}, Since 3 is a repeating prime
             factor in prime decomposition of 9
{3, 9}    -> {3 * 3 * 3}, 3 is a repeating prime 
             factor in prime decomposition of 27
{2, 3, 9} -> {2 * 3 * 3 * 3}, 3 is repeating 
             prime factor in prime decomposition 
             of 54
Hence total subarray remains which satisfies our
condition are 3.

Input: 2, 3, 5, 15, 7, 2
Output: 12
```

一种**天真的方法**是一个循环一个循环地运行，生成所有的子阵列，然后取所有元素的乘积，这样它的素分解就不包含重复的元素。这种方法肯定会很慢，并且会导致数组元素的大值溢出。
一种**有效的**方法是使用厄拉多塞筛的素因子分解。

> 想法是使用筛子存储所有值的[最小质因数(SPF)(直到最大值)。我们通过递归地将给定的数除以它的最小素因子直到它变成 1 来计算给定数的素因子分解。](https://www.geeksforgeeks.org/prime-factorization-using-sieve-olog-n-multiple-queries/)

1.  假设 **ind[]** 是一个数组，使得 ind[i]在 arr[]中存储质因数 I 的最后一个索引，并且**“last _ ind”**跟踪任何除数的最后一个索引。
2.  现在从左向右遍历(0 到 n-1)。对于数组[i]的特定元素，使用上述方法找到质因数，并用最新的索引**‘I+1’**初始化所有的因数。
3.  但是在执行步骤 2 之前，我们用数组[i]的每个除数的 ind[]更新变量**‘last _ ind’**。
4.  由于变量“last_ind”包含数组[i]的任何除数的最后一个索引(小于 I)，我们可以保证所有元素 **(last_ind+1，last_ind+2 … i)** 都不会有 arr[i]的任何重复质因数。因此我们的 ans 将是**(I–last _ ind+1)**
5.  对数组[]的剩余元素执行上述步骤，同时更新每个索引的答案。

## C++

```
// C++ program to count all sub-arrays whose
// product doesn't contain a repeating prime
// factor.
#include<bits/stdc++.h>
using namespace std;

const int MAXN = 1000001;
int spf[MAXN];

// Calculating SPF (Smallest Prime Factor) for
// every number till MAXN.
// Time Complexity : O(n log log n)
void sieve()
{
    // marking smallest prime factor for every
    // number to be itself.
    for (int i=1; i<MAXN; i++)
        spf[i] = i;

    // separately marking spf for every even
    // number as 2
    for (int i=4; i<MAXN; i+=2)
        spf[i] = 2;

    for (int i=3; i*i<MAXN; i++)
    {
        // checking if i is prime
        if (spf[i] == i)
        {
            // marking SPF for all numbers divisible
            // by i
            for (int j=i*i; j<MAXN; j+=i)

                // marking spf[j] if it is not
                // previously marked
                if (spf[j]==j)
                    spf[j] = i;
        }
    }
}

// Function to count all sub-arrays whose
// product doesn't contain a repeating prime
// factor.
int countSubArray(int arr[], int n)
{
    // ind[i] is going to store 1 + last index of
    // of an array element which has i as prime
    // factor.
    int ind[MAXN];
    memset(ind, -1, sizeof ind);

    int count = 0; // Initialize result
    int last_ind = 0; // It stores index
    for (int i=0; i < n; ++i)
    {
        while (arr[i] > 1)
        {
            int div = spf[arr[i]];

            // Fetch the last index of prime
            // divisor of element
            last_ind = max(last_ind, ind[div]);

            // Update the current divisor index
            ind[div] = i + 1;

            arr[i] /= div;
        }

        // Update result, we basically include
        // all required subarrays ending with
        // index arr[i].
        count += i - last_ind + 1;
    }
    return count;
}

// Driver code
int main()
{
    sieve();
    int arr[] = {2, 3, 9};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countSubArray(arr, n) << "\n";

    int arr1[] = {2, 3, 5, 15, 7, 2};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);
    cout << countSubArray(arr1, n1);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all sub-arrays whose
// product doesn't contain a repeating prime
// factor
import java.io.*;
import java.util.*;

class GFG
{
    public static int MAXN = 1000001;
    public static int[] spf = new int[MAXN];

    // Calculating SPF (Smallest Prime Factor) for
    // every number till MAXN.
    // Time Complexity : O(n log log n)
    static void sieve()
    {
        // marking smallest prime factor for every
        // number to be itself.
        for (int i=1; i<MAXN; i++)
            spf[i] = i;

        // separately marking spf for every even
        // number as 2
        for (int i=4; i<MAXN; i+=2)
            spf[i] = 2;

        for (int i=3; i*i<MAXN; i++)
        {
            // checking if i is prime
            if (spf[i] == i)
            {
                // marking SPF for all numbers divisible
                // by i
                for (int j=i*i; j<MAXN; j+=i)

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j]==j)
                        spf[j] = i;
            }
        }
    }

    // Function to count all sub-arrays whose
    // product doesn't contain a repeating prime
    // factor
    static int countSubArray(int arr[], int n)
    {
        // ind[i] is going to store 1 + last index of
        // of an array element which has i as prime
        // factor.
        int[] ind = new int[MAXN];
        Arrays.fill(ind, -1);

        int count = 0; // Initialize result
        int last_ind = 0; // It stores index
        for (int i=0; i < n; ++i)
        {
            while (arr[i] > 1)
            {
                int div = spf[arr[i]];

                // Fetch the last index of prime
                // divisor of element
                last_ind = Math.max(last_ind, ind[div]);

                // Update the current divisor index
                ind[div] = i + 1;

                arr[i] /= div;
            }

            // Update result, we basically include
            // all required subarrays ending with
            // index arr[i].
            count += i - last_ind + 1;
        }
        return count;
    }

    // driver program
    public static void main (String[] args)
    {
        sieve();
        int arr[] = {2, 3, 9};
        int n = arr.length;
        System.out.println(countSubArray(arr, n));

        int arr1[] = {2, 3, 5, 15, 7, 2};
        int n1 = arr1.length;
        System.out.println(countSubArray(arr1, n1));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 program to count all sub-arrays
# whose product does not contain a repeating
# prime factor.
from math import sqrt

MAXN = 1000001
spf = [0 for i in range(MAXN)]

# Calculating SPF (Smallest Prime Factor)
# for every number till MAXN.
# Time Complexity : O(n log log n)
def sieve():

    # marking smallest prime factor
    # for every number to be itself.
    for i in range(1, MAXN, 1):
        spf[i] = i

    # separately marking spf for
    # every even number as 2
    for i in range(4, MAXN, 2):
        spf[i] = 2

    k = int(sqrt(MAXN))
    for i in range(3, k, 1):

        # checking if i is prime
        if (spf[i] == i):

            # marking SPF for all numbers
            # divisible by i
            for j in range(i * i, MAXN, i):

                # marking spf[j] if it is
                # not previously marked
                if (spf[j] == j):
                    spf[j] = i

# Function to count all sub-arrays whose
# product doesn't contain a repeating
# prime factor.
def countSubArray(arr, n):

    # ind[i] is going to store 1 + last
    # index of an array element which
    # has i as prime factor.
    ind = [-1 for i in range(MAXN)]

    count = 0

    # Initialize result
    last_ind = 0

    # It stores index
    for i in range(0, n, 1):
        while (arr[i] > 1):
            div = spf[arr[i]]

            # Fetch the last index of prime
            # divisor of element
            last_ind = max(last_ind, ind[div])

            # Update the current divisor index
            ind[div] = i + 1

            arr[i] = int(arr[i] / div)

        # Update result, we basically include
        # all required subarrays ending with
        # index arr[i].
        count += i - last_ind + 1
    return count

# Driver code
if __name__ == '__main__':
    sieve()
    arr = [2, 3, 9]
    n = len(arr)
    print(countSubArray(arr, n))

    arr1 = [2, 3, 5, 15, 7, 2]
    n1 = len(arr1)
    print(countSubArray(arr1, n1))

# This code is contributed by
# Shashank_Sharma
```

## C#

```
// C# program to count all sub-arrays
// whose product doesn't contain a
// repeating prime factor
using System;

public class GFG  {

    public static int MAXN = 1000001;
    public static int[] spf = new int[MAXN];

    // Calculating SPF (Smallest Prime Factor)
    // for every number till MAXN.
    // Time Complexity : O(n log log n)
    static void sieve()
    {
        // marking smallest prime factor
        // for every number to be itself.
        for (int i = 1; i < MAXN; i++)
            spf[i] = i;

        // separately marking spf for
        // every even number as 2
        for (int i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (int i = 3; i * i < MAXN; i++)
        {
            // checking if i is prime
            if (spf[i] == i)
            {
                // marking SPF for all numbers divisible
                // by i
                for (int j = i * i; j < MAXN; j += i)

                    // marking spf[j] if it is
                    // not previously marked
                    if (spf[j] == j)
                        spf[j] = i;
            }
        }
    }

    // Function to count all sub-arrays
    // whose product doesn't contain
    // a repeating prime factor
    static int countSubArray(int []arr, int n)
    {

        // ind[i] is going to store 1 + last
        // index of an array element which
        // has i as prime factor.
        int[] ind = new int[MAXN];

        for(int i = 0; i < MAXN; i++)
        {
            ind[i] = -1;
        }

        int count = 0; // Initialize result
        int last_ind = 0; // It stores index
        for (int i = 0; i < n; ++i)
        {
            while (arr[i] > 1)
            {
                int div = spf[arr[i]];

                // Fetch the last index of prime
                // divisor of element
                last_ind = Math.Max(last_ind, ind[div]);

                // Update the current divisor index
                ind[div] = i + 1;

                arr[i] /= div;
            }

            // Update result, we basically include
            // all required subarrays ending with
            // index arr[i].
            count += i - last_ind + 1;
        }
        return count;
    }

    // Driver Code
    public static void Main ()
    {
        sieve();
        int []arr = {2, 3, 9};
        int n = arr.Length;
        Console.WriteLine(countSubArray(arr, n));

        int []arr1 = {2, 3, 5, 15, 7, 2};
        int n1 = arr1.Length;
        Console.WriteLine(countSubArray(arr1, n1));
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all sub-arrays whose
// product doesn't contain a repeating prime
// factor.
$MAXN = 1000001;
$spf = array_fill(0, $MAXN, NULL);

// Calculating SPF (Smallest Prime Factor)
// for every number till MAXN.
// Time Complexity : O(n log log n)
function sieve()
{
    global $spf, $MAXN;

    // marking smallest prime factor for
    // every number to be itself.
    for ($i = 1; $i < $MAXN; $i++)
        $spf[$i] = $i;

    // separately marking spf for every
    // even number as 2
    for ($i = 4; $i < $MAXN; $i += 2)
        $spf[$i] = 2;

    for ($i = 3; $i * $i < $MAXN; $i++)
    {
        // checking if i is prime
        if ($spf[$i] == $i)
        {
            // marking SPF for all numbers
            // divisible by i
            for ($j = $i * $i; $j < $MAXN; $j += $i)

                // marking spf[j] if it is not
                // previously marked
                if ($spf[$j] == $j)
                    $spf[$j] = $i;
        }
    }
}

// Function to count all sub-arrays whose
// product doesn't contain a repeating
// prime factor.
function countSubArray(&$arr, $n)
{
    global $MAXN, $spf;

    // ind[i] is going to store 1 + last index
    // of an array element which has i as prime
    // factor.
    $ind = array_fill(-1, $MAXN, NULL);

    $count = 0; // Initialize result
    $last_ind = 0; // It stores index
    for ($i = 0; $i < $n; ++$i)
    {
        while ($arr[$i] > 1)
        {
            $div = $spf[$arr[$i]];

            // Fetch the last index of prime
            // divisor of element
            $last_ind = max($last_ind, $ind[$div]);

            // Update the current divisor index
            $ind[$div] = $i + 1;
            if($div != 0)
            $arr[$i] /= $div;
        }

        // Update result, we basically include
        // all required subarrays ending with
        // index arr[i].
        $count += $i - $last_ind + 1;
    }
    return $count;
}

// Driver code
sieve();
$arr = array(2, 3, 9);
$n = sizeof($arr);
echo countSubArray($arr, $n) . "\n";

$arr1 = array(2, 3, 5, 15, 7, 2);
$n1 = sizeof($arr1);
echo countSubArray($arr1, $n1);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to count all sub-arrays whose
// product doesn't contain a repeating prime
// factor

    let MAXN = 1000001;
    let spf = new Array(MAXN);

     // Calculating SPF (Smallest Prime Factor) for
    // every number till MAXN.
    // Time Complexity : O(n log log n)
    function  sieve()
    {

        // marking smallest prime factor for every
        // number to be itself.
        for (let i = 1; i < MAXN; i++)
            spf[i] = i;

        // separately marking spf for every even
        // number as 2
        for (let i = 4; i < MAXN; i += 2)
            spf[i] = 2;

        for (let i = 3; i * i < MAXN; i++)
        {
            // checking if i is prime
            if (spf[i] == i)
            {
                // marking SPF for all numbers divisible
                // by i
                for (let j = i * i; j < MAXN; j += i)

                    // marking spf[j] if it is not
                    // previously marked
                    if (spf[j] == j)
                        spf[j] = i;
            }
        }
    }

     // Function to count all sub-arrays whose
    // product doesn't contain a repeating prime
    // factor
    function countSubArray(arr,n)
    {

        // ind[i] is going to store 1 + last index of
        // of an array element which has i as prime
        // factor.
        let ind = new Array(MAXN);
        for(let i = 0; i < ind.length; i++)
        {
            ind[i] = -1;
        }

        let count = 0; // Initialize result
        let last_ind = 0; // It stores index
        for (let i = 0; i < n; ++i)
        {
            while (arr[i] > 1)
            {
                let div = spf[arr[i]];

                // Fetch the last index of prime
                // divisor of element
                last_ind = Math.max(last_ind, ind[div]);

                // Update the current divisor index
                ind[div] = i + 1;

                arr[i] /= div;
            }

            // Update result, we basically include
            // all required subarrays ending with
            // index arr[i].
            count += i - last_ind + 1;
        }
        return count;
    }

    // driver program
    sieve();
    let arr = [2, 3, 9];
    let n = arr.length;
    document.write(countSubArray(arr, n)+"<br>");

    let arr1 = [2, 3, 5, 15, 7, 2];
    let n1 = arr1.length;
    document.write(countSubArray(arr1, n1));

    // This code is contributed by rag2127

</script>
```

**Output**

```
3
12
```

**时间复杂度:**O(MAX * log(log(MAX)+nlog(n))
**辅助空间:** O(MAX)
本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。