# 前缀和后缀乘积相等的索引计数

> 原文:[https://www . geesforgeks . org/indexs-count-of-prefix-后缀-product-equal/](https://www.geeksforgeeks.org/count-of-indices-for-which-the-prefix-and-suffix-product-are-equal/)

给定整数的[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]** ，任务是找到[前缀积](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)和[后缀积](https://www.geeksforgeeks.org/tag/suffix/)相等的索引数。

**示例:**

> **输入:**arr**=【4，-5，1，1，-2，5，-2】
> **输出:** 2
> **说明:**前缀和后缀乘积相等的指数如下:
> At 指数 2 前缀和后缀乘积为 20
> At 指数 3 前缀和后缀乘积为 20**
> 
> ****输入:** arr = [5，0，4，-1，-3，0]
> **输出:** 3
> **说明:**前缀和后缀乘积相等的指数如下:
> At 索引 1 前缀和后缀乘积为 0
> At 索引 2 前缀和后缀乘积为 0
> At 索引 3 前缀和后缀乘积为 0
> At 索引 4 前缀和后缀乘积为 0
> At 索引 5 前缀和后缀乘积为 0**

****天真方法:**给定的问题可以通过以下方式解决:[从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr** 并计算前缀乘积直到该索引，然后[从右到左迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** 并计算后缀乘积，然后检查前缀和后缀乘积是否相等。
**时间复杂度:** O(N^2)**

****高效方法:**上述方法可以通过使用  [<u>散列</u>](https://www.geeksforgeeks.org/hashing-data-structure/) 技术来解决。按照以下步骤解决问题:**

*   **[从右向左遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr** ，在每个索引处将产品存储到一个辅助数组 **prod****
*   **[从左到右迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr** ，在每个索引处计算前缀乘积**
*   **对于获得的每个前缀乘积，检查**产品**中是否存在相同值的后缀乘积

    *   如果是，则将计数 **res** 增加 1** 
*   **返回获得的结果 **res****

**下面是上述方法的实现:**

## **C++**

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate number of
// equal prefix and suffix product
// till the same indices
int equalProdPreSuf(vector<int>& arr)
{

    // Initialize a variable
    // to store the result
    int res = 0;

    // Initialize variables to
    // calculate prefix and suffix sums
    int preProd = 1, sufProd = 1;

    // Length of array arr
    int len = arr.size();

    // Initialize an auxiliary array to
    // store suffix product at every index
    vector<int> prod(len, 0);

    // Traverse the array from right to left
    for (int i = len - 1; i >= 0; i--) {

        // Multiply the current
        // element to sufSum
        sufProd *= arr[i];

        // Store the value in prod
        prod[i] = sufProd;
    }

    // Iterate the array from left to right
    for (int i = 0; i < len; i++) {

        // Multiply the current
        // element to preProd
        preProd *= arr[i];

        // If prefix product is equal to
        // suffix product prod[i] then
        // increment res by 1
        if (preProd == prod[i]) {

            // Increment the result
            res++;
        }
    }

    // Return the answer
    return res;
}

// Driver code
int main()
{

    // Initialize the array
    vector<int> arr = { 4, 5, 1, 1, -2, 5, -2 };

    // Call the function and
    // print its result
    cout << equalProdPreSuf(arr);

    return 0;
}

    // This code is contributed by rakeshsahni
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    // Function to calculate number of
    // equal prefix and suffix product
    // till the same indices
    public static int equalProdPreSuf(int[] arr)
    {

        // Initialize a variable
        // to store the result
        int res = 0;

        // Initialize variables to
        // calculate prefix and suffix sums
        int preProd = 1, sufProd = 1;

        // Length of array arr
        int len = arr.length;

        // Initialize an auxiliary array to
        // store suffix product at every index
        int[] prod = new int[len];

        // Traverse the array from right to left
        for (int i = len - 1; i >= 0; i--) {

            // Multiply the current
            // element to sufSum
            sufProd *= arr[i];

            // Store the value in prod
            prod[i] = sufProd;
        }

        // Iterate the array from left to right
        for (int i = 0; i < len; i++) {

            // Multiply the current
            // element to preProd
            preProd *= arr[i];

            // If prefix product is equal to
            // suffix product prod[i] then
            // increment res by 1
            if (preProd == prod[i]) {

                // Increment the result
                res++;
            }
        }

        // Return the answer
        return res;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Initialize the array
        int[] arr = { 4, 5, 1, 1, -2, 5, -2 };

        // Call the function and
        // print its result
        System.out.println(equalProdPreSuf(arr));
    }
}
```

## **蟒蛇 3**

```
# Python Program to implement
# the above approach

# Function to calculate number of
# equal prefix and suffix product
# till the same indices
def equalProdPreSuf(arr):

    # Initialize a variable
    # to store the result
    res = 0

    # Initialize variables to
    # calculate prefix and suffix sums
    preProd = 1
    sufProd = 1

    # Length of array arr
    Len = len(arr)

    # Initialize an auxiliary array to
    # store suffix product at every index
    prod = [0] * Len

    # Traverse the array from right to left
    for i in range(Len-1, 0, -1):

        # Multiply the current
        # element to sufSum
        sufProd *= arr[i]

        # Store the value in prod
        prod[i] = sufProd

    # Iterate the array from left to right
    for i in range(Len):

        # Multiply the current
        # element to preProd
        preProd *= arr[i]

        # If prefix product is equal to
        # suffix product prod[i] then
        # increment res by 1
        if (preProd == prod[i]):

            # Increment the result
            res += 1

    # Return the answer
    return res

# Driver code

# Initialize the array
arr = [4, 5, 1, 1, -2, 5, -2]

# Call the function and
# print its result
print(equalProdPreSuf(arr))

# This code is contributed by gfgking.
```

## **C#**

```
// C# implementation for the above approach
using System;

class GFG {

    // Function to calculate number of
    // equal prefix and suffix product
    // till the same indices
    public static int equalProdPreSuf(int[] arr)
    {

        // Initialize a variable
        // to store the result
        int res = 0;

        // Initialize variables to
        // calculate prefix and suffix sums
        int preProd = 1, sufProd = 1;

        // Length of array arr
        int len = arr.Length;

        // Initialize an auxiliary array to
        // store suffix product at every index
        int[] prod = new int[len];

        // Traverse the array from right to left
        for (int i = len - 1; i >= 0; i--) {

            // Multiply the current
            // element to sufSum
            sufProd *= arr[i];

            // Store the value in prod
            prod[i] = sufProd;
        }

        // Iterate the array from left to right
        for (int i = 0; i < len; i++) {

            // Multiply the current
            // element to preProd
            preProd *= arr[i];

            // If prefix product is equal to
            // suffix product prod[i] then
            // increment res by 1
            if (preProd == prod[i]) {

                // Increment the result
                res++;
            }
        }

        // Return the answer
        return res;
    }

    // Driver code
    public static void Main(String[] args)
    {

        // Initialize the array
        int[] arr = { 4, 5, 1, 1, -2, 5, -2 };

        // Call the function and
        // print its result
        Console.Write(equalProdPreSuf(arr));
    }
}

// This code is contributed by gfgking.
```

## **java 描述语言**

```
<script>

       // JavaScript Program to implement
       // the above approach

       // Function to calculate number of
       // equal prefix and suffix product
       // till the same indices
       function equalProdPreSuf(arr) {

           // Initialize a variable
           // to store the result
           let res = 0;

           // Initialize variables to
           // calculate prefix and suffix sums
           let preProd = 1, sufProd = 1;

           // Length of array arr
           let len = arr.length;

           // Initialize an auxiliary array to
           // store suffix product at every index
           let prod = new Array(len).fill(0);

           // Traverse the array from right to left
           for (let i = len - 1; i >= 0; i--) {

               // Multiply the current
               // element to sufSum
               sufProd *= arr[i];

               // Store the value in prod
               prod[i] = sufProd;
           }

           // Iterate the array from left to right
           for (let i = 0; i < len; i++) {

               // Multiply the current
               // element to preProd
               preProd *= arr[i];

               // If prefix product is equal to
               // suffix product prod[i] then
               // increment res by 1
               if (preProd == prod[i]) {

                   // Increment the result
                   res++;
               }
           }

           // Return the answer
           return res;
       }

       // Driver code

       // Initialize the array
       let arr = [4, 5, 1, 1, -2, 5, -2];

       // Call the function and
       // print its result
       document.write(equalProdPreSuf(arr));

   // This code is contributed by Potta Lokesh
   </script>
```

****Output**

```
2
```** 

****时间复杂度:**O(N)
T3】辅助空间: O(N)**