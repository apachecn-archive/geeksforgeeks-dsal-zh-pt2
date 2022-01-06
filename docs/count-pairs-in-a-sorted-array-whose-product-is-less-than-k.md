# 对乘积小于 k 的排序数组中的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-in-a-sorted-array-其产品小于-k/](https://www.geeksforgeeks.org/count-pairs-in-a-sorted-array-whose-product-is-less-than-k/)

给定一个排序的整数数组和数字 k，任务是对乘积小于 x 的数组中的对进行计数。
**示例:**

> **输入:** A = {2，3，5，6}，k = 16
> **输出:** 4
> 对积小于 16: (2，3)，(2，5)，(2，6)，(3，5)
> T7】输入: A = {2，3，4，6，9}，k = 20
> **输出:** 6
> 对积小于 20: (2，3)，(2，4)，(2)

这个问题的一个**简单解决方案**运行两个循环，一个接一个地生成所有对，并检查当前对的乘积是否小于 x。
这个问题的一个**有效解决方案**是在 l 和 r 变量中取指数的初值和终值。考虑以下两种情况:

> *   **Case-I:**
>     Let's consider I < J and A [I] * A [J] < K, and then we can say A [I] * A [J-1] < K as A [J-1] < A [J]
> *   **case-ii:**
>     Let's consider i k, and then we can say a [I] * a [j+1] > k as a [j+1] > a [j] For ordered arrays,
>     is similar to a [I] * a [j+].

上面的问题类似于[在和小于 x](https://www.geeksforgeeks.org/count-pairs-array-whose-sum-less-x/) 的排序数组中计数对，唯一不同的是求对的乘积而不是和。
**下面是解决这个问题的算法:**

```
1) Initialize two variables l and r to find the candidate 
   elements in the sorted array.
       (a) l = 0
       (b) r = n - 1
2) Initialize : result = 0
2) Loop while l < r.

    // If current left and current
    // right have product smaller than x,
    // the all elements from l+1 to r
    // form a pair with current
    (a) If (arr[l] * arr[r] < x)  
          result = result + (r - l)    
          l++;  

    (b) Else
            r--;

3) Return result
```

**下面是上面算法的实现:**

## C++

```
// C++ program to find number of pairs with
// product less than k in a sorted array
#include <bits/stdc++.h>
using namespace std;

// Function to count the pairs
int fun(int A[], int n, int k)
{
    // count to keep count of
    // number of pairs with product
    // less than k
    int count = 0;
    int i = 0;
    int j = n - 1;

    // Traverse the array
    while (i < j) {

        // If product is less than k
        // then count that pair
        // and increment 'i'
        if (A[i] * A[j] < k) {
            count += (j - i);
            i++;
        }

        // Else decrement 'j'
        else {
            j--;
        }
    }

    // Return count of pairs
    return count;
}

// Driver code
int main()
{

    int A[] = { 2, 3, 4, 6, 9 };
    int n = sizeof(A) / sizeof(int);
    int k = 20;
    cout << "Number of pairs with product less than "
         << k << " = " << fun(A, n, k) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find number
// of pairs with product less
// than k in a sorted array
class GFG
{

// Function to count the pairs
static int fun(int A[],
               int n, int k)
{
    // count to keep count of
    // number of pairs with
    // product less than k
    int count = 0;
    int i = 0;
    int j = n - 1;

    // Traverse the array
    while (i < j)
    {

        // If product is less than
        // k then count that pair
        // and increment 'i'
        if (A[i] * A[j] < k)
        {
            count += (j - i);
            i++;
        }

        // Else decrement 'j'
        else
        {
            j--;
        }
    }

    // Return count of pairs
    return count;
}

// Driver code
public static void main(String args[])
{
    int A[] = {2, 3, 4, 6, 9};
    int n = A.length;
    int k = 20;

    System.out.println("Number of pairs with " +
                     "product less than 20 = " +
                                  fun(A, n, k));
}
}

// This code is contributed
// by Kirti_Mangal
```

## 计算机编程语言

```
# Python program to find number of pairs with
# product less than k in a sorted array

def fun(A, k):
    # count to keep count of number
    # of pairs with product less than k
    count = 0
    n = len(A)
    # Left pointer pointing to leftmost part
    i = 0

    # Right pointer pointing to rightmost part
    j = n-1

    # While left and right pointer don't meet
    while i < j:
        if A[i]*A[j] < k:
            count += (j-i)
            # Increment the left pointer
            i+= 1
        else:
            # Decrement the right pointer
            j-= 1
    return count

# Driver code to test above function
A = [2, 3, 4, 6, 9]
k = 20
print("Number of pairs with product less than ",
k, " = ", fun(A, k))
```

## C#

```
// C# program to find number
// of pairs with product less
// than k in a sorted array
using System;

class GFG
{

// Function to count the pairs
static int fun(int []A,
               int n, int k)
{
    // count to keep count of
    // number of pairs with
    // product less than k
    int count = 0;
    int i = 0;
    int j = n - 1;

    // Traverse the array
    while (i < j)
    {

        // If product is less than
        // k then count that pair
        // and increment 'i'
        if (A[i] * A[j] < k)
        {
            count += (j - i);
            i++;
        }

        // Else decrement 'j'
        else
        {
            j--;
        }
    }

    // Return count of pairs
    return count;
}

// Driver code
public static void Main()
{
    int []A = {2, 3, 4, 6, 9};
    int n = A.Length;
    int k = 20;

    Console.WriteLine("Number of pairs with " +
                    "product less than 20 = " +
                                 fun(A, n, k));
}
}

// This code is contributed
// by Subhadeep
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of
// pairs with product less than k
// in a sorted array

// Function to count the pairs
function fun($A, $n, $k)
{
    // count to keep count of
    // number of pairs with product
    // less than k
    $count = 0;
    $i = 0;
    $j = ($n - 1);

    // Traverse the array
    while ($i < $j)
    {

        // If product is less than k
        // then count that pair
        // and increment 'i'
        if ($A[$i] * $A[$j] < $k)
        {
            $count += ($j - $i);
            $i++;
        }

        // Else decrement 'j'
        else
        {
            $j--;
        }
    }

    // Return count of pairs
    return $count;
}

// Driver code
$A = array( 2, 3, 4, 6, 9 );
$n = sizeof($A);
$k = 20;
echo "Number of pairs with product less than ",
           $k , " = " , fun($A, $n, $k) , "\n";

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript program to find number
    // of pairs with product less
    // than k in a sorted array

    // Function to count the pairs
    function fun(A, n, k)
    {
        // count to keep count of
        // number of pairs with
        // product less than k
        let count = 0;
        let i = 0;
        let j = n - 1;

        // Traverse the array
        while (i < j)
        {

            // If product is less than
            // k then count that pair
            // and increment 'i'
            if (A[i] * A[j] < k)
            {
                count += (j - i);
                i++;
            }

            // Else decrement 'j'
            else
            {
                j--;
            }
        }

        // Return count of pairs
        return count;
    }

    let A = [2, 3, 4, 6, 9];
    let n = A.length;
    let k = 20;

    document.write("Number of pairs with " +
                    "product less than 20 = " +
                                 fun(A, n, k));

</script>
```

**Output:** 

```
Number of pairs with product less than 20 = 6
```

**时间复杂度:** O(N)