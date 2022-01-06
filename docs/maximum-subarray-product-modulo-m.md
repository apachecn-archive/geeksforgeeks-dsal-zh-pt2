# 最大子阵列乘积模 M

> 原文:[https://www . geesforgeks . org/maximum-subarray-product-modal-m/](https://www.geeksforgeeks.org/maximum-subarray-product-modulo-m/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个正整数 **M** ，任务是求[最大子阵积](https://www.geeksforgeeks.org/maximum-product-subarray-set-3/) [模](https://www.geeksforgeeks.org/modulo-1097-1000000007/) **M** 和最大积[子阵](https://www.geeksforgeeks.org/tag/subarray/)的最小长度。

**示例:**

> **输入:** arr[] = {2，3，4，2}，N = 4，M = 5
> **输出:**
> 最大子阵积为 4
> 最大积子阵的最小长度为 1
> **说明:**
> 长度为 1 的子阵分别为{{2}、{3}、{4}、{2}，它们的积模 M(= 5)分别为{2，3，4，2}。
> 长度为 2 的子阵分别为{{2，3}、{3，4}、{4，2}，乘积模 M(= 5)分别为{1，2，3}。
> 长度为 3 的子阵分别为{{2，3，4}，{3，4，2}}乘积模 M(= 5)分别为{4，4 }。
> 长度为 4 的子阵为{2，3，4，2}，乘积 modlo M(= 5)为 3。
> 因此，最大子阵积 mod M(= 5)为 4，最小可能长度为 1。
> 
> **输入:** arr[] = {5，5，5}，N = 3，M = 7
> **输出:**
> 最大子阵积为 6
> 最大积子阵的最小长度为 3

**天真法:**最简单的方法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵，计算其乘积模 **M** ，并打印该子阵的最大子阵乘积和最小长度。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效途径:**上述途径可以通过将**arr【j】**乘以范围**【I，j–1】**内预先计算的子阵列乘积，计算范围**【I，j】**内的子阵列乘积来优化。按照以下步骤解决问题:

*   初始化两个变量，比如 ans 和 length，以存储最大子阵列乘积和最大乘积子阵列的最小长度。
*   迭代范围[0，N–1]并执行以下步骤:
    *   初始化一个变量，比如 product，来存储 subarr { arr[I]，…，arr[j]}的乘积。
    *   迭代范围[i，N-1]并通过乘以 arr[j]更新乘积，即(乘积* arr[j]) % M。
    *   在每次迭代中，更新 ans if ans< product and then update length, if length >(j–I+1)。
*   最后，打印 ans 中获得的最大子阵列乘积和具有最大乘积长度的子阵列的最小长度。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum subarray product
// modulo M and minimum length of the subarray
void maxModProdSubarr(int arr[], int n, int M)
{

    // Stores maximum subarray product modulo
    // M and minimum length of the subarray
    int ans = 0;

    // Stores the minimum length of
    // subarray having maximum product
    int length = n;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Stores the product of a subarray
        int product = 1;

        // Calculate Subarray whose start
        // index is i
        for (int j = i; j < n; j++) {

            // Multiply product by arr[i]
            product = (product * arr[i]) % M;

            // If product greater than ans
            if (product > ans) {

                // Update ans
                ans = product;
                if (length > j - i + 1) {

                    // Update length
                    length = j - i + 1;
                }
            }
        }
    }

    // Print maximum subarray product mod M
    cout << "Maximum subarray product is "
         << ans << endl;

    // Print minimum length of subarray
    // having maximum product
    cout << "Minimum length of the maximum product "
         << "subarray is " << length << endl;
}

// Drivers Code
int main()
{
    int arr[] = { 2, 3, 4, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int M = 5;

    maxModProdSubarr(arr, N, M);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find maximum subarray product
// modulo M and minimum length of the subarray
static void maxModProdSubarr(int arr[], int n, int M)
{

    // Stores maximum subarray product modulo
    // M and minimum length of the subarray
    int ans = 0;

    // Stores the minimum length of
    // subarray having maximum product
    int length = n;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Stores the product of a subarray
        int product = 1;

        // Calculate Subarray whose start
        // index is i
        for(int j = i; j < n; j++)
        {

            // Multiply product by arr[i]
            product = (product * arr[i]) % M;

            // If product greater than ans
            if (product > ans)
            {

                // Update ans
                ans = product;

                if (length > j - i + 1)
                {

                    // Update length
                    length = j - i + 1;
                }
            }
        }
    }

    // Print maximum subarray product mod M
    System.out.println(
        "Maximum subarray product is " + ans);

    // Print minimum length of subarray
    // having maximum product
    System.out.println(
        "Minimum length of the maximum " +
        "product subarray is " + length);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 2 };
    int N = arr.length;
    int M = 5;

    maxModProdSubarr(arr, N, M);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for above approach

# Function to find maximum subarray product
# modulo M and minimum length of the subarray
def maxModProdSubarr(arr, n, M):

    # Stores maximum subarray product modulo
    # M and minimum length of the subarray
    ans = 0

    # Stores the minimum length of
    # subarray having maximum product
    length = n

    # Traverse the array
    for i in range(n):

        # Stores the product of a subarray
        product = 1

        # Calculate Subarray whose start
        # index is i
        for j in range(i, n, 1):

            # Multiply product by arr[i]
            product = (product * arr[i]) % M

            # If product greater than ans
            if (product > ans):

                # Update ans
                ans = product
                if (length > j - i + 1):

                    # Update length
                    length = j - i + 1

    # Print maximum subarray product mod M
    print("Maximum subarray product is", ans)

    # Print minimum length of subarray
    # having maximum product
    print("Minimum length of the maximum product subarray is",length)

# Drivers Code
if __name__ == '__main__':
    arr =  [2, 3, 4, 2]
    N = len(arr)
    M = 5
    maxModProdSubarr(arr, N, M)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find maximum subarray product
// modulo M and minimum length of the subarray
static void maxModProdSubarr(int[] arr, int n,
                             int M)
{

    // Stores maximum subarray product modulo
    // M and minimum length of the subarray
    int ans = 0;

    // Stores the minimum length of
    // subarray having maximum product
    int length = n;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Stores the product of a subarray
        int product = 1;

        // Calculate Subarray whose start
        // index is i
        for(int j = i; j < n; j++)
        {

            // Multiply product by arr[i]
            product = (product * arr[i]) % M;

            // If product greater than ans
            if (product > ans)
            {

                // Update ans
                ans = product;

                if (length > j - i + 1)
                {

                    // Update length
                    length = j - i + 1;
                }
            }
        }
    }

    // Print maximum subarray product mod M
    Console.WriteLine(
        "Maximum subarray product is " + ans);

    // Print minimum length of subarray
    // having maximum product
    Console.WriteLine(
        "Minimum length of the maximum " +
        "product subarray is " + length);
}

// Driver code
static void Main()
{
    int[] arr = { 2, 3, 4, 2 };
    int N = arr.Length;
    int M = 5;

    maxModProdSubarr(arr, N, M);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to find maximum subarray product
    // modulo M and minimum length of the subarray
    function maxModProdSubarr(arr , n , M)
    {

        // Stores maximum subarray product modulo
        // M and minimum length of the subarray
        var ans = 0;

        // Stores the minimum length of
        // subarray having maximum product
        var length = n;

        // Traverse the array
        for (i = 0; i < n; i++) {

            // Stores the product of a subarray
            var product = 1;

            // Calculate Subarray whose start
            // index is i
            for (j = i; j < n; j++) {

                // Multiply product by arr[i]
                product = (product * arr[i]) % M;

                // If product greater than ans
                if (product > ans) {

                    // Update ans
                    ans = product;

                    if (length > j - i + 1) {

                        // Update length
                        length = j - i + 1;
                    }
                }
            }
        }

        // Print maximum subarray product mod M
        document.write("Maximum subarray product is " + ans+"<br/>");

        // Print minimum length of subarray
        // having maximum product
        document.write("Minimum length of the maximum " + "product subarray is " + length);
    }

    // Driver Code
        var arr = [ 2, 3, 4, 2 ];
        var N = arr.length;
        var M = 5;

        maxModProdSubarr(arr, N, M);

// This code is contributed by umadevi9616.
</script>
```

Output: 

```
Maximum subarray product is 4
Minimum length of the maximum product subarray is 1
```

***时间复杂度:O(N<sup>2</sup>)***
***辅助空间:O(1)***