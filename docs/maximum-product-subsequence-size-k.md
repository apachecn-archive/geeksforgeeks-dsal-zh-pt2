# 大小为 k 的子序列的最大乘积

> 原文:[https://www . geesforgeks . org/maximum-product-subserial-size-k/](https://www.geeksforgeeks.org/maximum-product-subsequence-size-k/)

给定一个由 n 个整数组成的数组 A[]，任务是找到一个大小为 k 的子序列，它的乘积在给定数组的所有可能的 k 个大小的子序列中是最大的。
约束

```
1 <= n <= 10^5
1 <= k <= n
```

**例:**

```
Input : A[] = {1, 2, 0, 3}, 
          k = 2
Output : 6
Explanation : Subsequence containing elements
{2, 3} gives maximum product : 2*3 = 6

Input : A[] = {1, 2, -1, -3, -6, 4}, 
          k = 4
Output : 144
Explanation : Subsequence containing {2, -3, 
-6, 4} gives maximum product : 2*(-3)*(-6)*4 
= 144
```

以下是这个问题中出现的不同情况。

*   **案例一:如果 A 的最大元素是 0，k 是奇数**这里如果子序列中不包含 0，那么乘积将小于 0，因为奇数个负整数的乘积给出一个负整数。因此 0 必须包含在子序列中。因为子序列中存在 0，所以子序列的乘积是 0。答案= 0。
*   **情况二:如果 A 的最大元素为负，k 为奇**。这里乘积将小于 0，
    因为奇数个负整数的乘积给出一个负整数。为了得到最大乘积，我们取最小(绝对值)k 个元素的乘积。从绝对值来看:| A[n-1]|>| A[n-2]|…>| A[0]|。因此我们取 A[n-1]，A[n-2]，A[n-3]，…。A[n-k]
    答案= A[n-1] * A[n-2] * …..*阿[不适用]
*   **情况三:如果 A 的最大元素为正，k 为奇**。在 k 大小的子序列中，如果所有元素都是< 0，那么乘积将小于 0，因为奇数个负整数的乘积给出了负整数。因此，子序列中至少有一个元素必须是正整数。为了得到最大乘积，最大正数应该出现在子序列中。现在我们需要给子序列增加 k-1 个元素。
    因为 k 是奇数，k-1 变成偶数。所以问题归结为案例四。答案= A[n-1] *案例四的答案。
*   **情况四:如果 k 为偶数**。因为 k 是偶数，所以我们总是在子序列中加一对。所以子序列中需要相加的总对是 k/2。为了简单起见，我们的新 k 是 k/2。现在，由于 A 被排序，具有最大乘积的对将总是 A[0]*A[1]或 A[n-1]*A[n-2]。如果对前面的陈述有疑问，考虑负数🙂

```
Now,
    if A[0]*A[1] > A[n-1]*A[n-2],
       second max product pair will be 
       either A[2]*A[3] OR A[n-1]*[n-2].
    else second max product pair will be
         either A[0]*A[1] OR A[n-3]*[n-4]. 
```

以下是上述解决方案
的实现

## C++

```
// C++ code to find maximum possible product of
// sub-sequence of size k from given array of n
// integers
#include <algorithm> // for sorting
#include <iostream>
using namespace std;

// Required function
int maxProductSubarrayOfSizeK(int A[], int n, int k)
{
    // sorting given input array
    sort(A, A + n);

    // variable to store final product of all element
    // of sub-sequence of size k
    int product = 1;

    // CASE I
    // If max element is 0 and
    // k is odd then max product will be 0
    if (A[n - 1] == 0 && (k & 1))
        return 0;

    // CASE II
    // If all elements are negative and
    // k is odd then max product will be
    // product of rightmost-subarray of size k
    if (A[n - 1] <= 0 && (k & 1)) {
        for (int i = n - 1; i >= n - k; i--)
            product *= A[i];
        return product;
    }

    // else
    // i is current left pointer index
    int i = 0;

    // j is current right pointer index
    int j = n - 1;

    // CASE III
    // if k is odd and rightmost element in
    // sorted array is positive then it
    // must come in subsequence
    // Multiplying A[j] with product and
    // correspondingly changing j
    if (k & 1) {
        product *= A[j];
        j--;
        k--;
    }

    // CASE IV
    // Now k is even
    // Now we deal with pairs
    // Each time a pair is multiplied to product
    // ie.. two elements are added to subsequence each time
    // Effectively k becomes half
    // Hence, k >>= 1 means k /= 2
    k >>= 1;

    // Now finding k corresponding pairs
    // to get maximum possible value of product
    for (int itr = 0; itr < k; itr++) {

        // product from left pointers
        int left_product = A[i] * A[i + 1];

        // product from right pointers
        int right_product = A[j] * A[j - 1];

        // Taking the max product from two choices
        // Correspondingly changing the pointer's position
        if (left_product > right_product) {
            product *= left_product;
            i += 2;
        }
        else {
            product *= right_product;
            j -= 2;
        }
    }

    // Finally return product
    return product;
}

// Driver Code to test above function
int main()
{
    int A[] = { 1, 2, -1, -3, -6, 4 };
    int n = sizeof(A) / sizeof(A[0]);
    int k = 4;
    cout << maxProductSubarrayOfSizeK(A, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum possible product of
// sub-sequence of size k from given array of n
// integers
import java.io.*;
import java.util.*;

class GFG {
    // Function to find maximum possible product
    static int maxProductSubarrayOfSizeK(int A[], int n, int k)
    {
        // sorting given input array
        Arrays.sort(A);

        // variable to store final product of all element
        // of sub-sequence of size k
        int product = 1;

        // CASE I
        // If max element is 0 and
        // k is odd then max product will be 0
        if (A[n - 1] == 0 && k % 2 != 0)
            return 0;

        // CASE II
        // If all elements are negative and
        // k is odd then max product will be
        // product of rightmost-subarray of size k
        if (A[n - 1] <= 0 && k % 2 != 0) {
            for (int i = n - 1; i >= n - k; i--)
                product *= A[i];
            return product;
        }

        // else
        // i is current left pointer index
        int i = 0;

        // j is current right pointer index
        int j = n - 1;

        // CASE III
        // if k is odd and rightmost element in
        // sorted array is positive then it
        // must come in subsequence
        // Multiplying A[j] with product and
        // correspondingly changing j
        if (k % 2 != 0) {
            product *= A[j];
            j--;
            k--;
        }

        // CASE IV
        // Now k is even
        // Now we deal with pairs
        // Each time a pair is multiplied to product
        // ie.. two elements are added to subsequence each time
        // Effectively k becomes half
        // Hence, k >>= 1 means k /= 2
        k >>= 1;

        // Now finding k corresponding pairs
        // to get maximum possible value of product
        for (int itr = 0; itr < k; itr++) {
            // product from left pointers
            int left_product = A[i] * A[i + 1];

            // product from right pointers
            int right_product = A[j] * A[j - 1];

            // Taking the max product from two choices
            // Correspondingly changing the pointer's position
            if (left_product > right_product) {
                product *= left_product;
                i += 2;
            }
            else {
                product *= right_product;
                j -= 2;
            }
        }

        // Finally return product
        return product;
    }

    // driver program
    public static void main(String[] args)
    {
        int A[] = { 1, 2, -1, -3, -6, 4 };
        int n = A.length;
        int k = 4;
        System.out.println(maxProductSubarrayOfSizeK(A, n, k));
    }
}

// Contributed by Pramod Kumar
```

## 蟒蛇 3

```
# Python 3 code to find maximum possible
# product of sub-sequence of size k from
# given array of n integers

# Required function
def maxProductSubarrayOfSizeK(A, n, k):

    # sorting given input array
    A.sort()

    # variable to store final product of
    # all element of sub-sequence of size k
    product = 1

    # CASE I
    # If max element is 0 and
    # k is odd then max product will be 0
    if (A[n - 1] == 0 and (k & 1)):
        return 0

    # CASE II
    # If all elements are negative and
    # k is odd then max product will be
    # product of rightmost-subarray of size k
    if (A[n - 1] <= 0 and (k & 1)) :
        for i in range(n - 1, n - k + 1, -1):
            product *= A[i]
        return product

    # else
    # i is current left pointer index
    i = 0

    # j is current right pointer index
    j = n - 1

    # CASE III
    # if k is odd and rightmost element in
    # sorted array is positive then it
    # must come in subsequence
    # Multiplying A[j] with product and
    # correspondingly changing j
    if (k & 1):
        product *= A[j]
        j-= 1
        k-=1

    # CASE IV
    # Now k is even. So, Now we deal with pairs
    # Each time a pair is multiplied to product
    # ie.. two elements are added to subsequence
    # each time. Effectively k becomes half
    # Hence, k >>= 1 means k /= 2
    k >>= 1

    # Now finding k corresponding pairs to get
    # maximum possible value of product
    for itr in range( k) :

        # product from left pointers
        left_product = A[i] * A[i + 1]

        # product from right pointers
        right_product = A[j] * A[j - 1]

        # Taking the max product from two
        # choices. Correspondingly changing
        # the pointer's position
        if (left_product > right_product) :
            product *= left_product
            i += 2

        else :
            product *= right_product
            j -= 2

    # Finally return product
    return product

# Driver Code
if __name__ == "__main__":

    A = [ 1, 2, -1, -3, -6, 4 ]
    n = len(A)
    k = 4
    print(maxProductSubarrayOfSizeK(A, n, k))

# This code is contributed by ita_c
```

## C#

```
// C# program to find maximum possible
// product of sub-sequence of size k
// from given array of n integers
using System;

class GFG {

    // Function to find maximum possible product
    static int maxProductSubarrayOfSizeK(int[] A, int n,
                                                  int k)
    {
        // sorting given input array
        Array.Sort(A);

        // variable to store final product of
        // all element of sub-sequence of size k
        int product = 1;
        int i;

        // CASE I
        // If max element is 0 and
        // k is odd then max product will be 0
        if (A[n - 1] == 0 && k % 2 != 0)
            return 0;

        // CASE II
        // If all elements are negative and
        // k is odd then max product will be
        // product of rightmost-subarray of size k
        if (A[n - 1] <= 0 && k % 2 != 0) {
            for (i = n - 1; i >= n - k; i--)
                product *= A[i];
            return product;
        }

        // else
        // i is current left pointer index
        i = 0;

        // j is current right pointer index
        int j = n - 1;

        // CASE III
        // if k is odd and rightmost element in
        // sorted array is positive then it
        // must come in subsequence
        // Multiplying A[j] with product and
        // correspondingly changing j
        if (k % 2 != 0) {
            product *= A[j];
            j--;
            k--;
        }

        // CASE IV
        // Now k is even
        // Now we deal with pairs
        // Each time a pair is multiplied to
        // product i.e.. two elements are added to
        // subsequence each time  Effectively k becomes half
        // Hence, k >>= 1 means k /= 2
        k >>= 1;

        // Now finding k corresponding pairs
        // to get maximum possible value of product
        for (int itr = 0; itr < k; itr++) {

            // product from left pointers
            int left_product = A[i] * A[i + 1];

            // product from right pointers
            int right_product = A[j] * A[j - 1];

            // Taking the max product from two choices
            // Correspondingly changing the pointer's position
            if (left_product > right_product) {
                product *= left_product;
                i += 2;
            }
            else {
                product *= right_product;
                j -= 2;
            }
        }

        // Finally return product
        return product;
    }

    // driver program
    public static void Main()
    {
        int[] A = { 1, 2, -1, -3, -6, 4 };
        int n = A.Length;
        int k = 4;
        Console.WriteLine(maxProductSubarrayOfSizeK(A, n, k));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find maximum possible product of
// sub-sequence of size k from given array of n
// integers

// Required function

function maxProductSubarrayOfSizeK($A, $n, $k)
{
    // sorting given input array
    sort($A);

    // variable to store final product of all element
    // of sub-sequence of size k
    $product = 1;

    // CASE I
    // If max element is 0 and
    // k is odd then max product will be 0
    if ($A[$n - 1] == 0 && ($k & 1))
        return 0;

    // CASE II
    // If all elements are negative and
    // k is odd then max product will be
    // product of rightmost-subarray of size k
    if ($A[$n - 1] <= 0 && ($k & 1))
    {
        for ($i = $n - 1; $i >= $n - $k; $i--)
            $product *= $A[$i];
        return $product;
    }

    // else
    // i is current left pointer index
    $i = 0;

    // j is current right pointer index
    $j = $n - 1;

    // CASE III
    // if k is odd and rightmost element in
    // sorted array is positive then it
    // must come in subsequence
    // Multiplying A[j] with product and
    // correspondingly changing j
    if ($k & 1)
    {
        $product *= $A[$j];
        $j--;
        $k--;
    }

    // CASE IV
    // Now k is even
    // Now we deal with pairs
    // Each time a pair is multiplied to product
    // ie.. two elements are added to subsequence each time
    // Effectively k becomes half
    // Hence, k >>= 1 means k /= 2
    $k >>= 1;

    // Now finding k corresponding pairs
    // to get maximum possible value of product
    for ($itr = 0; $itr < $k; $itr++)
    {

        // product from left pointers
        $left_product = $A[$i] * $A[$i + 1];

        // product from right pointers
        $right_product = $A[$j] * $A[$j - 1];

        // Taking the max product from two choices
        // Correspondingly changing the pointer's position
        if ($left_product > $right_product)
        {
            $product *= $left_product;
            $i += 2;
        }
        else
        {
            $product *= $right_product;
            $j -= 2;
        }
    }

    // Finally return product
    return $product;
}

    // Driver Code
    $A = array(1, 2, -1, -3, -6, 4 );
    $n = count($A);
    $k = 4;
    echo maxProductSubarrayOfSizeK($A, $n, $k);

// This code is contributed by ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find maximum possible
    // product of sub-sequence of size k
    // from given array of n integers

    // Function to find maximum possible product
    function maxProductSubarrayOfSizeK(A, n, k)
    {
        // sorting given input array
        A.sort(function(a, b){return a - b});

        // variable to store final product of
        // all element of sub-sequence of size k
        let product = 1;
        let i;

        // CASE I
        // If max element is 0 and
        // k is odd then max product will be 0
        if (A[n - 1] == 0 && k % 2 != 0)
            return 0;

        // CASE II
        // If all elements are negative and
        // k is odd then max product will be
        // product of rightmost-subarray of size k
        if (A[n - 1] <= 0 && k % 2 != 0) {
            for (i = n - 1; i >= n - k; i--)
                product *= A[i];
            return product;
        }

        // else
        // i is current left pointer index
        i = 0;

        // j is current right pointer index
        let j = n - 1;

        // CASE III
        // if k is odd and rightmost element in
        // sorted array is positive then it
        // must come in subsequence
        // Multiplying A[j] with product and
        // correspondingly changing j
        if (k % 2 != 0) {
            product *= A[j];
            j--;
            k--;
        }

        // CASE IV
        // Now k is even
        // Now we deal with pairs
        // Each time a pair is multiplied to
        // product i.e.. two elements are added to
        // subsequence each time  Effectively k becomes half
        // Hence, k >>= 1 means k /= 2
        k >>= 1;

        // Now finding k corresponding pairs
        // to get maximum possible value of product
        for (let itr = 0; itr < k; itr++) {

            // product from left pointers
            let left_product = A[i] * A[i + 1];

            // product from right pointers
            let right_product = A[j] * A[j - 1];

            // Taking the max product from two choices
            // Correspondingly changing the pointer's position
            if (left_product > right_product) {
                product *= left_product;
                i += 2;
            }
            else {
                product *= right_product;
                j -= 2;
            }
        }

        // Finally return product
        return product;
    }

    let A = [ 1, 2, -1, -3, -6, 4 ];
    let n = A.length;
    let k = 4;
    document.write(maxProductSubarrayOfSizeK(A, n, k));

</script>
```

**输出:**

```
144
```

**时间复杂度:O(n * log n)** O(n * log n)来自排序+ O(k)来自数组中一次遍历= O(n * log n)
**辅助空间:O(1)**
本文由 [**Pratik Chhajer**](http://www.pratikchhajer.me/) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。