# 递增子序列的最大乘积

> 原文:[https://www . geesforgeks . org/maximum-product-递增-subsequel/](https://www.geeksforgeeks.org/maximum-product-increasing-subsequence/)

给定一个数字数组，求该数组中一个递增子序列的数字相乘所得的最大乘积。
**注:**单个数字应该是大小为 1 的递增子序列。
示例:

```
Input : arr[] = { 3, 100, 4, 5, 150, 6 }
Output : 45000
Maximum product is 45000 formed by the 
increasing subsequence 3, 100, 150\. Note
that the longest increasing subsequence 
is different {3, 4, 5, 6}

Input : arr[] = { 10, 22, 9, 33, 21, 50, 41, 60 }
Output : 21780000
Maximum product is 21780000 formed by the 
increasing subsequence 10, 22, 33, 50, 60.

```

先决条件:[最长递增子序列](https://www.geeksforgeeks.org/longest-increasing-subsequence/)
**方法:**使用动态方法维护表 mpis[]。mpis[i]的值存储以 arr[i]结尾的乘积最大乘积递增子序列。最初，递增子序列表的所有值都被初始化为 arr[i]。我们使用类似于 [LIS 问题](https://www.geeksforgeeks.org/longest-increasing-subsequence/)的递归方法来寻找结果。

## C++

```
/* Dynamic programming C++ implementation of maximum
   product of an increasing subsequence */
#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Returns product of maximum product increasing
// subsequence.
ll lis(ll arr[], ll n)
{
    ll mpis[n];

    /* Initialize MPIS values */
    for (int i = 0; i < n; i++)
        mpis[i] = arr[i];

    /* Compute optimized MPIS values considering
       every element as ending element of sequence */
    for (int i = 1; i < n; i++)
        for (int j = 0; j < i; j++)
            if (arr[i] > arr[j] && mpis[i] < (mpis[j] * arr[i]))
                mpis[i] = mpis[j] * arr[i];

    /* Pick maximum of all product values */
    return *max_element(mpis, mpis + n);
}

/* Driver program to test above function */
int main()
{
    ll arr[] = { 3, 100, 4, 5, 150, 6 };
    ll n = sizeof(arr) / sizeof(arr[0]);
    printf("%lld", lis(arr, n));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/* Dynamic programming Java implementation
of maximum product of an increasing
subsequence */
import java.util.Arrays;
import java.util.Collections;

class GFG {

    // Returns product of maximum product
    // increasing subsequence.
    static int lis(int[] arr, int n)
    {
        int[] mpis = new int[n];
        int max = Integer.MIN_VALUE;

        /* Initialize MPIS values */
        for (int i = 0; i < n; i++)
            mpis[i] = arr[i];

        /* Compute optimized MPIS values
        considering every element as ending
        element of sequence */
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] && mpis[i]
                         < (mpis[j] * arr[i]))
                    mpis[i] = mpis[j] * arr[i];

        /* Pick maximum of all product values
        using for loop*/
        for (int k = 0; k < mpis.length; k++)
        {
            if (mpis[k] > max) {
                max = mpis[k];
            }
        }

        return max;
    }

    // Driver program to test above function
    static public void main(String[] args)
    {

        int[] arr = { 3, 100, 4, 5, 150, 6 };
        int n = arr.length;

        System.out.println(lis(arr, n));
    }
}

// This code is contributed by parashar.
```

<gfg-tab role="tab" slot="tab" id="gfg-tab-2">蟒 3 高光=</gfg-tab><gfg-panel role="tabpanel" slot="panel" id="gfg-panel-2" data-code-lang="Python3"></gfg-panel>

```
 # Dynamic programming Python3 implementation
# of maximum product of an increasing
# subsequence 

# Returns product of maximum product
# increasing subsequence.
def lis (arr, n ):
    mpis =[0] * (n)

    # Initialize MPIS values
    for i in range(n):
        mpis[i] = arr[i]

    # Compute optimized MPIS values
    # considering every element as 
    # ending element of sequence
    for i in range(1, n):
        for j in range(i):
            if (arr[i] > arr[j] and
                    mpis[i] < (mpis[j] * arr[i])):
                        mpis[i] = mpis[j] * arr[i]

    # Pick maximum of all product values 
    return max(mpis)

# Driver code to test above function
arr = [3, 100, 4, 5, 150, 6]
n = len(arr)
print( lis(arr, n))

# This code is contributed by "Sharad_Bhardwaj". 
```

## C#

```
/* Dynamic programming C# implementation
of maximum product of an increasing
subsequence */
using System;
using System.Linq;

public class GFG {

    // Returns product of maximum product
    // increasing subsequence.
    static long lis(long[] arr, long n)
    {
        long[] mpis = new long[n];

        /* Initialize MPIS values */
        for (int i = 0; i < n; i++)
            mpis[i] = arr[i];

        /* Compute optimized MPIS values considering
        every element as ending element of sequence */
        for (int i = 1; i < n; i++)
            for (int j = 0; j < i; j++)
                if (arr[i] > arr[j] && mpis[i] < (mpis[j] * arr[i]))
                    mpis[i] = mpis[j] * arr[i];

        /* Pick maximum of all product values */
        return mpis.Max();
    }

    /* Driver program to test above function */
    static public void Main()
    {

        long[] arr = { 3, 100, 4, 5, 150, 6 };
        long n = arr.Length;

        Console.WriteLine(lis(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?PHP

/* Dynamic programming PHP implementation of maximum
   product of an increasing subsequence */

// Returns product of maximum product increasing
// subsequence.
function lis(&$arr,  $n)
{
    $mpis = array_fill(0,$n, NULL);

    /* Initialize MPIS values */
    for ($i = 0; $i < $n; $i++)
        $mpis[$i] = $arr[$i];

    /* Compute optimized MPIS values considering
       every element as ending element of sequence */
    for ($i = 1; $i < $n; $i++)
        for ($j = 0; $j < $i; $j++)
            if ($arr[$i] > $arr[$j] && $mpis[$i] < ($mpis[$j] * $arr[$i]))
                $mpis[$i] = $mpis[$j] * $arr[$i];

    /* Pick maximum of all product values */
    return max($mpis);
}

/* Driver program to test above function */

    $arr = array ( 3, 100, 4, 5, 150, 6 );
    $n = sizeof($arr) / sizeof($arr[0]);
    echo lis($arr, $n);
    return 0;
?>
```

## java 描述语言

```
<script>

// JavaScript program implementation
of maximum product of an increasing

    // Returns product of maximum product
    // increasing subsequence.
    function lis(arr, n)
    {
        let mpis = [];
        let max = Number.MIN_VALUE;

        /* Initialize MPIS values */
        for (let i = 0; i < n; i++)
            mpis[i] = arr[i];

        /* Compute optimized MPIS values
        considering every element as ending
        element of sequence */
        for (let i = 1; i < n; i++)
            for (let j = 0; j < i; j++)
                if (arr[i] > arr[j] && mpis[i]
                         < (mpis[j] * arr[i]))
                    mpis[i] = mpis[j] * arr[i];

        /* Pick maximum of all product values
        using for loop*/
        for (let k = 0; k < mpis.length; k++)
        {
            if (mpis[k] > max)
            {
                max = mpis[k];
            }
        }
        return max;
    }

// Driver Code
    let arr = [ 3, 100, 4, 5, 150, 6 ];
        let n = arr.length;
        document.write(lis(arr, n));

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
 45000
```

**时间复杂度:**o(n^2)
T3】辅助空间: O(n)