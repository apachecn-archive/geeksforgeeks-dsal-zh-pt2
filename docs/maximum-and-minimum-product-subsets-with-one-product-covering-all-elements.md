# 最大和最小乘积子集

> 原文:[https://www . geesforgeks . org/最大和最小产品子集一个产品覆盖所有元素/](https://www.geeksforgeeks.org/maximum-and-minimum-product-subsets-with-one-product-covering-all-elements/)

给定一个集合，我们需要在集合的所有子集之间找到最大和最小可能乘积。

**示例:**

```
Input : arr[] = {4, -2, 5};
Output: Maximum product = 20 
        Minimum product = -40
Maximum product is obtained by multiplying
4 5
Minimum product is obtained by multiplying 
4, -2, 5

Input : arr[] = {-4, -2, 3, 7, 5, 0, 1};
Output: Maximum product = 840 
        Minimum product = -420
Maximum product is obtained by multiplying
-4, -2, 3, 7, 5
Minimum product is obtained by multiplying 
-4, 3, 7, 5 
```

由于数组可以有负值、零值和正值，如果攻击不当，这个问题会有很多边缘情况。下面给出的解决方案在当前索引和先前索引处保持最大乘积和最小乘积，并且在任何时刻，当前乘积根据当前元素的符号从先前最大值或先前最小值乘以当前元素中获取值。例如，如果我们正在寻找最大乘积，那么如果当前元素为正，则当前最大值将是先前最大值乘以当前值，否则如果当前元素为负，则先前最小值乘以当前值。同样的程序也适用于寻找最小乘积。

请看下面简单的代码来理解。

## C++

```
// C++ program to find maximum and minimum
// product from an array
#include <bits/stdc++.h>
using namespace std;

// method returns maximum and minimum obtainable
// product of array arr
pair<int, int> getMaxandMinProduct(int arr[], int n)
{
    // Initialize all products with arr[0]
    int curMaxProduct = arr[0];
    int curMinProduct = arr[0];
    int prevMaxProduct = arr[0];
    int prevMinProduct = arr[0];
    int maxProduct = arr[0];
    int minProduct = arr[0];

    // Process all elements after arr[0]
    for (int i = 1; i < n; ++i)
    {
        /* Current maximum product is maximum of following
            1) prevMax * curelement (when curelement is +ve)
            2) prevMin * curelement (when curelement is -ve)
            3) Element itself
            4) Previous max product */
        curMaxProduct = max(prevMaxProduct * arr[i],
                            max(prevMinProduct * arr[i],
                                arr[i]));
        curMaxProduct = max(curMaxProduct, prevMaxProduct);

        /* Current min product computation is Similar to
           that of current max product     */
        curMinProduct = min(prevMaxProduct * arr[i],
                            min(prevMinProduct * arr[i],
                                arr[i]));
        curMinProduct = min(curMinProduct, prevMinProduct);
        maxProduct = max(maxProduct, curMaxProduct);
        minProduct = min(minProduct, curMinProduct);

        // copy current values to previous values
        prevMaxProduct = curMaxProduct;
        prevMinProduct = curMinProduct;
    }

    return make_pair(minProduct, maxProduct);
}

//  driver code to test above methods
int main()
{
    int arr[] = {-4, -2, 3, 7, 5, 0, 1};
    int n = sizeof(arr) / sizeof(int);
    pair<int, int> product = getMaxandMinProduct(arr, n);
    printf("Minimum product is %d and "
            "Maximum product is %dn",
             product.first, product.second);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum and minimum
// product from an array
class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// method returns maximum and minimum obtainable
// product of array arr
static pair getMaxandMinProduct(int arr[], int n)
{
    // Initialize all products with arr[0]
    int curMaxProduct = arr[0];
    int curMinProduct = arr[0];
    int prevMaxProduct = arr[0];
    int prevMinProduct = arr[0];
    int maxProduct = arr[0];
    int minProduct = arr[0];

    // Process all elements after arr[0]
    for (int i = 1; i < n; ++i)
    {
        /* Current maximum product is maximum of following
            1) prevMax * curelement (when curelement is +ve)
            2) prevMin * curelement (when curelement is -ve)
            3) Element itself
            4) Previous max product */
        curMaxProduct = Math.max(prevMaxProduct * arr[i],
                        Math.max(prevMinProduct * arr[i],
                                                  arr[i]));
        curMaxProduct = Math.max(curMaxProduct,
                                 prevMaxProduct);

        /* Current min product computation is
        Similar to that of current max product */
        curMinProduct = Math.min(prevMaxProduct * arr[i],
                        Math.min(prevMinProduct * arr[i],
                                                  arr[i]));
        curMinProduct = Math.min(curMinProduct, prevMinProduct);
        maxProduct = Math.max(maxProduct, curMaxProduct);
        minProduct = Math.min(minProduct, curMinProduct);

        // copy current values to previous values
        prevMaxProduct = curMaxProduct;
        prevMinProduct = curMinProduct;
    }
    return new pair(minProduct, maxProduct);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = {-4, -2, 3, 7, 5, 0, 1};
    int n = arr.length;
    pair product = getMaxandMinProduct(arr, n);
    System.out.printf("Minimum product is %d and " +
                      "Maximum product is %d",
                       product.first, product.second);
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find maximum and
# minimum product from an array

# method returns maximum and minimum
# obtainable product of array arr
def getMaxandMinProduct(arr, n):

    # Initialize all products with arr[0]
    curMaxProduct = arr[0]
    curMinProduct = arr[0]
    prevMaxProduct = arr[0]
    prevMinProduct = arr[0]
    maxProduct = arr[0]
    minProduct = arr[0]

    # Process all elements after arr[0]
    for i in range(1, n):

        # Current maximum product is maximum of following
        # 1) prevMax * curelement (when curelement is +ve)
        # 2) prevMin * curelement (when curelement is -ve)
        # 3) Element itself
        # 4) Previous max product
        curMaxProduct = max(prevMaxProduct * arr[i],
                        max(prevMinProduct * arr[i], arr[i]))
        curMaxProduct = max(curMaxProduct, prevMaxProduct)

        # Current min product computation is Similar to
        # that of current max product
        curMinProduct = min(prevMaxProduct * arr[i],
                        min(prevMinProduct * arr[i], arr[i]))
        curMinProduct = min(curMinProduct, prevMinProduct)
        maxProduct = max(maxProduct, curMaxProduct)
        minProduct = min(minProduct, curMinProduct)

        # copy current values to previous values
        prevMaxProduct = curMaxProduct
        prevMinProduct = curMinProduct

    return (minProduct, maxProduct)

# Driver Code
if __name__ == "__main__":
    arr = [-4, -2, 3, 7, 5, 0, 1]
    n = len(arr)
    product = getMaxandMinProduct(arr, n)
    print("Minimum product is", product[0], "and",
          "Maximum product is", product[1])

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# program to find maximum and minimum
// product from an array
using System;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// method returns maximum and minimum
// obtainable product of array arr
static pair getMaxandMinProduct(int []arr,
                                int n)
{
    // Initialize all products with arr[0]
    int curMaxProduct = arr[0];
    int curMinProduct = arr[0];
    int prevMaxProduct = arr[0];
    int prevMinProduct = arr[0];
    int maxProduct = arr[0];
    int minProduct = arr[0];

    // Process all elements after arr[0]
    for (int i = 1; i < n; ++i)
    {
        /* Current maximum product is maximum of following
            1) prevMax * curelement (when curelement is +ve)
            2) prevMin * curelement (when curelement is -ve)
            3) Element itself
            4) Previous max product */
        curMaxProduct = Math.Max(prevMaxProduct * arr[i],
                        Math.Max(prevMinProduct * arr[i],
                                                  arr[i]));
        curMaxProduct = Math.Max(curMaxProduct,
                                 prevMaxProduct);

        /* Current min product computation is
        Similar to that of current max product */
        curMinProduct = Math.Min(prevMaxProduct * arr[i],
                        Math.Min(prevMinProduct * arr[i],
                                                  arr[i]));
        curMinProduct = Math.Min(curMinProduct,
                                 prevMinProduct);
        maxProduct = Math.Max(maxProduct, curMaxProduct);
        minProduct = Math.Min(minProduct, curMinProduct);

        // copy current values to previous values
        prevMaxProduct = curMaxProduct;
        prevMinProduct = curMinProduct;
    }
    return new pair(minProduct, maxProduct);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = {-4, -2, 3, 7, 5, 0, 1};
    int n = arr.Length;
    pair product = getMaxandMinProduct(arr, n);
    Console.Write("Minimum product is {0} and " +
                  "Maximum product is {1}",
                   product.first, product.second);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to find maximum and minimum
// product from an array

// method returns maximum and minimum obtainable
// product of array arr
function getMaxandMinProduct(arr, n)
{

    // Initialize all products with arr[0]
    let curMaxProduct = arr[0];
    let curMinProduct = arr[0];
    let prevMaxProduct = arr[0];
    let prevMinProduct = arr[0];
    let maxProduct = arr[0];
    let minProduct = arr[0];

    // Process all elements after arr[0]
    for(let i = 1; i < n; ++i)
    {

        /* Current maximum product is maximum of following
            1) prevMax * curelement (when curelement is +ve)
            2) prevMin * curelement (when curelement is -ve)
            3) Element itself
            4) Previous max product */
        curMaxProduct = Math.max(prevMaxProduct * arr[i],
                        Math.max(prevMinProduct * arr[i],
                                                  arr[i]));
        curMaxProduct = Math.max(curMaxProduct,
                                 prevMaxProduct);

        /* Current min product computation is Similar to
        that of current max product     */
        curMinProduct = Math.min(prevMaxProduct * arr[i],
                        Math.min(prevMinProduct * arr[i],
                                                  arr[i]));
        curMinProduct = Math.min(curMinProduct,
                                 prevMinProduct);
        maxProduct = Math.max(maxProduct, curMaxProduct);
        minProduct = Math.min(minProduct, curMinProduct);

        // Copy current values to previous values
        prevMaxProduct = curMaxProduct;
        prevMinProduct = curMinProduct;
    }
    return [minProduct, maxProduct];
}

// Driver code
let arr = [ -4, -2, 3, 7, 5, 0, 1 ];
let n = arr.length;
let product = getMaxandMinProduct(arr, n);

document.write("Minimum product is " + product[0] +
               " and Maximum product is " + product[1]);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Minimum product is -420 and Maximum product is 840
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。