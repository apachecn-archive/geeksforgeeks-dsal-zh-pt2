# 最大产品子阵列|第 3 套

> 原文:[https://www . geesforgeks . org/maximum-product-subarray-set-3/](https://www.geeksforgeeks.org/maximum-product-subarray-set-3/)

给定同时包含正整数和负整数的数组 A[]，求最大乘积子数组。
**例:**

```
Input: A[] = { 6, -3, -10, 0, 2 }
Output: 180  // The subarray is {6, -3, -10}

Input: A[] = {-1, -3, -10, 0, 60 }
Output: 60  // The subarray is {60}

Input: A[] = { -2, -3, 0, -2, -40 }
Output: 80  // The subarray is {-2, -40}
```

其思想是从左到右遍历数组，保持两个变量 minVal 和 maxVal，代表最小和最大乘积值，直到数组的第 I 个索引。现在，如果数组的第 I 个元素是负的，这意味着 minVal 和 maxVal 的值将被交换，因为 maxVal 的值将通过乘以一个负数而变得最小。现在，比较一下 minVal 和 maxVal。
minVal 和 maxVal 的值分别取决于当前索引元素或当前索引元素与前一个 minVal 和 maxVal 的乘积。
以下是上述方法的实施:

## C++

```
// C++ program to find maximum product subarray
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum product subarray
int maxProduct(int* arr, int n)
{
    // Variables to store maximum and minimum
    // product till ith index.
    int minVal = arr[0];
    int maxVal = arr[0];

    int maxProduct = arr[0];

    for (int i = 1; i < n; i++) {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if (arr[i] < 0)
            swap(maxVal, minVal);

        // maxVal and minVal stores the
        // product of subarray ending at arr[i].
        maxVal = max(arr[i], maxVal * arr[i]);
        minVal = min(arr[i], minVal * arr[i]);

        // Max Product of array.
        maxProduct = max(maxProduct, maxVal);
    }

    // Return maximum product found in array.
    return maxProduct;
}

// Driver Code
int main()
{
    int arr[] = { -1, -3, -10, 0, 60 };

    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Maximum Subarray product is "
         << maxProduct(arr, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum product subarray
import java.io.*;

class GFG {

    // Function to find maximum product subarray
    static int maxProduct(int arr[], int n)
    {

        // Variables to store maximum and minimum
        // product till ith index.
        int minVal = arr[0];
        int maxVal = arr[0];

        int maxProduct = arr[0];

        for (int i = 1; i < n; i++)
        {

            // When multiplied by -ve number,
            // maxVal becomes minVal
            // and minVal becomes maxVal.
            if (arr[i] < 0)
            {
                int temp = maxVal;
                maxVal = minVal;
                minVal =temp;

            }

            // maxVal and minVal stores the
            // product of subarray ending at arr[i].
            maxVal = Math.max(arr[i], maxVal * arr[i]);
            minVal = Math.min(arr[i], minVal * arr[i]);

            // Max Product of array.
            maxProduct = Math.max(maxProduct, maxVal);
        }

        // Return maximum product found in array.
        return maxProduct;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int arr[] = { -1, -3, -10, 0, 60 };
        int n = arr.length;

        System.out.println( "Maximum Subarray product is "
                                    + maxProduct(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 蟒蛇 3

```
# Python 3 program to find maximum
# product subarray

# Function to find maximum
# product subarray
def maxProduct(arr, n):

    # Variables to store maximum and
    # minimum product till ith index.
    minVal = arr[0]
    maxVal = arr[0]

    maxProduct = arr[0]

    for i in range(1, n, 1):

        # When multiplied by -ve number,
        # maxVal becomes minVal
        # and minVal becomes maxVal.
        if (arr[i] < 0):
            temp = maxVal
            maxVal = minVal
            minVal = temp

        # maxVal and minVal stores the
        # product of subarray ending at arr[i].
        maxVal = max(arr[i], maxVal * arr[i])
        minVal = min(arr[i], minVal * arr[i])

        # Max Product of array.
        maxProduct = max(maxProduct, maxVal)

    # Return maximum product
    # found in array.
    return maxProduct

# Driver Code
if __name__ == '__main__':
    arr = [-1, -3, -10, 0, 60]

    n = len(arr)

    print("Maximum Subarray product is",
                     maxProduct(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find
// maximum product subarray
using System;

class GFG
{

    // Function to find maximum
    // product subarray
    static int maxProduct(int []arr,
                          int n)
    {

        // Variables to store
        // maximum and minimum
        // product till ith index.
        int minVal = arr[0];
        int maxVal = arr[0];

        int maxProduct = arr[0];

        for (int i = 1; i < n; i++)
        {

            // When multiplied by -ve
            // number, maxVal becomes
            // minVal and minVal
            // becomes maxVal.
            if (arr[i] < 0)
            {
                int temp = maxVal;
                maxVal = minVal;
                minVal = temp;

            }

            // maxVal and minVal stores
            // the product of subarray
            // ending at arr[i].
            maxVal = Math.Max(arr[i],
                              maxVal * arr[i]);
            minVal = Math.Min(arr[i],
                              minVal * arr[i]);

            // Max Product of array.
            maxProduct = Math.Max(maxProduct,
                                  maxVal);
        }

        // Return maximum product
        // found in array.
        return maxProduct;
    }

    // Driver Code
    public static void Main ()
    {
        int []arr = {-1, -3, -10, 0, 60};
        int n = arr.Length;

        Console.WriteLine("Maximum Subarray " +
                                "product is " +
                           maxProduct(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum
// product subarray

// Function to find maximum
// product subarray
function maxProduct(&$arr, $n)
{
    // Variables to store maximum and
    // minimum product till ith index.
    $minVal = $arr[0];
    $maxVal = $arr[0];

    $maxProduct = $arr[0];

    for ($i = 1; $i < $n; $i++)
    {

        // When multiplied by -ve number,
        // maxVal becomes minVal
        // and minVal becomes maxVal.
        if ($arr[$i] < 0)
        {
            $temp = $maxVal;
            $maxVal = $minVal;
            $minVal = $temp;
        }

        // maxVal and minVal stores the
        // product of subarray ending at arr[i].
        $maxVal = max($arr[$i], $maxVal * $arr[$i]);
        $minVal = min($arr[$i], $minVal * $arr[$i]);

        // Max Product of array.
        $maxProduct = max($maxProduct, $maxVal);
    }

    // Return maximum product found in array.
    return $maxProduct;
}

// Driver Code
$arr = array( -1, -3, -10, 0, 60 );
$n = sizeof($arr);
echo "Maximum Subarray product is " .
         maxProduct($arr, $n) . "\n";

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// Javascript program to find maximum product subarray

    // Function to find maximum product subarray
    function maxProduct(arr,n)
    {
        // Variables to store maximum and minimum
        // product till ith index.
        let minVal = arr[0];
        let maxVal = arr[0];

        let maxProduct = arr[0];

        for (let i = 1; i < n; i++)
        {

            // When multiplied by -ve number,
            // maxVal becomes minVal
            // and minVal becomes maxVal.
            if (arr[i] < 0)
            {
                let temp = maxVal;
                maxVal = minVal;
                minVal =temp;

            }

            // maxVal and minVal stores the
            // product of subarray ending at arr[i].
            maxVal = Math.max(arr[i], maxVal * arr[i]);
            minVal = Math.min(arr[i], minVal * arr[i]);

            // Max Product of array.
            maxProduct = Math.max(maxProduct, maxVal);
        }

        // Return maximum product found in array.
        return maxProduct;
    }

     // Driver Code
    let arr=[ -1, -3, -10, 0, 60 ];
    let n = arr.length;
    document.write( "Maximum Subarray product is "
                                    + maxProduct(arr, n));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Maximum Sub array product is 60
```

**时间复杂度** : O( n )
**辅助空间** : O( 1 )
**相关文章** :

*   [最大产品子阵列|第 1 套](https://www.geeksforgeeks.org/maximum-product-subarray/)
*   [最大乘积子阵|集合 2(使用两个遍历)](https://www.geeksforgeeks.org/maximum-product-subarray-set-2-using-two-traversals/)