# 找出一个元素，将阵列分成两个子阵列，乘积相等

> 原文:[https://www . geeksforgeeks . org/find-一个元素，该元素用等积将数组分成两个子数组/](https://www.geeksforgeeks.org/find-an-element-which-divides-the-array-in-two-subarrays-with-equal-product/)

给定一个大小为 n 的数组，找到一个元素，这个元素将数组分成两个乘积相等的子数组。如果没有这样的分区，则打印-1。

**示例:**

```
Input : 1 4 2 1 4
Output : 2
If 2 is the partition, 
subarrays are : {1, 4} and {1, 4}

Input : 2, 3, 4, 1, 4, 6
Output : 1
If 1 is the partition, 
Subarrays are : {2, 3, 4} and {4, 6}
```

一个简单的解决方案是从第二个元素开始考虑每个元素。计算左边元素的乘积和右边元素的乘积。如果这两个产品相同，则返回元素。
T3】时间复杂度: O(N <sup>2</sup>

一个更好的解决方案是使用前缀和后缀产品数组。从 0 遍历到 n-1 <sup>第</sup>个索引，在这个索引处，它们产生一个相等的结果，这个索引是用一个相等的乘积来划分数组的。
**时间复杂度:** O(N)
**辅助空间:** O(N)

## C++

```
// C++ program to find an element which divides
// the array in two sub-arrays with equal product.
#include <bits/stdc++.h>
using namespace std;

// Function to find the index
int findElement(int arr[], int n)
{
    // Forming prefix sum array from 0
    int prefixMul[n];
    prefixMul[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefixMul[i] = prefixMul[i - 1] * arr[i];

    // Forming suffix sum array from n-1
    int suffixMul[n];
    suffixMul[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixMul[i] = suffixMul[i + 1] * arr[i];

    // Find the point where prefix and suffix
    // sums are same.
    for (int i = 1; i < n - 1; i++)
        if (prefixMul[i] == suffixMul[i])
            return arr[i];

    return -1;
}
// Driver code
int main()
{
    int arr[] = { 2, 3, 4, 1, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findElement(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an element
// which divides the array in two
// sub-arrays with equal product.
class GFG
{

// Function to find
// the index
static int findElement(int arr[],
                       int n)
{
    // Forming prefix
    // sum array from 0
    int prefixMul[] = new int[n];
    prefixMul[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefixMul[i] = prefixMul[i - 1] *
                                  arr[i];

    // Forming suffix sum
    // array from n-1
    int suffixMul[] = new int[n];
    suffixMul[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixMul[i] = suffixMul[i + 1] *
                                  arr[i];

    // Find the point where prefix
    // and suffix sums are same.
    for (int i = 1; i < n - 1; i++)
        if (prefixMul[i] == suffixMul[i])
            return arr[i];

    return -1;
}

// Driver code
public static void main(String args[])
{
    int arr[] = {2, 3, 4,
                 1, 4, 6};

    int n = arr.length;
    System.out.println(findElement(arr, n));

}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find an element 
# which divides the array in two 
# sub-arrays with equal product.

# Function to find the index
def findElement(arr, n):
    # Forming prefix sum array from 0
    prefixMul = []
    prefixMul.append(arr[0])
    for i in range(1, n):
        prefixMul.append(prefixMul[i-1]*arr[i])

    # Forming suffix sum array from n-1
    suffixMul = [None for i in range(0, n)]
    suffixMul[n-1] = arr[n-1]
    for i in range(n-2, -1, -1):
        suffixMul[i] = suffixMul[i+1]*arr[i]

    # Find the point where prefix and suffix
    # sums are same.
    for i in range(1, n-1):
        if prefixMul[i] == suffixMul[i]:
            return arr[i]

    return -1

# Driver Code
arr = [2, 3, 4, 1, 4, 6]
n = len(arr)
print(findElement(arr, n))

# This code is contributed by SamyuktaSHegde
```

## C#

```
// C# program to find an element
// which divides the array in two
// sub-arrays with equal product.
using System;

class GFG
{
    // Function to find
    // the index
    static int findElement(int []arr,
                           int n)
    {
    // Forming prefix
    // sum array from 0
    int []prefixMul = new int[n];
    prefixMul[0] = arr[0];

    for (int i = 1; i < n; i++)
        prefixMul[i] = prefixMul[i - 1] *
                                  arr[i];

    // Forming suffix sum
    // array from n-1
    int []suffixMul = new int[n];
    suffixMul[n - 1] = arr[n - 1];

    for (int i = n - 2; i >= 0; i--)
        suffixMul[i] = suffixMul[i + 1] *
                                  arr[i];

    // Find the point where prefix
    // and suffix sums are same.
    for (int i = 1; i < n - 1; i++)
        if (prefixMul[i] == suffixMul[i])
            return arr[i];

    return -1;
}

// Driver code
public static void Main()
{
    int []arr = {2, 3, 4, 1, 4, 6};

    int n = arr.Length;
    Console.Write(findElement(arr, n));
}
}

// This code is contributed
// by shiv_bhakt
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an
// element which divides
// the array in two sub-
// arrays with equal product.

// Function to find the index
function findElement($arr, $n)
{
    // Forming prefix
    // sum array from 0
    $prefixMul;
    $prefixMul[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $prefixMul[$i] = $prefixMul[$i - 1] *
                         $arr[$i];

    // Forming suffix
    // sum array from n-1
    $suffixMul;
    $suffixMul[$n - 1] = $arr[$n - 1];
    for ($i = $n - 2; $i >= 0; $i--)
        $suffixMul[$i] = $suffixMul[$i + 1] *
                         $arr[$i];

    // Find the point where
    // prefix and suffix sums
    // are same.
    for ($i = 1; $i < $n - 1; $i++)
        if ($prefixMul[$i] == $suffixMul[$i])
            return $arr[$i];

    return -1;
}

// Driver code
$arr = array( 2, 3, 4, 1, 4, 6 );
$n = sizeof($arr) / sizeof($arr[0]);
echo findElement($arr, $n);

// This code is contributed
// by shiv_bhakt
?>
```

## java 描述语言

```
<script>
    // javascript program to find an element which divides
    // the array in two sub-arrays with equal product.

    // Function to find the index
    function findElement(arr,n)
    {
        // Forming prefix sum array from 0
        let prefixMul= new Array(n);
        prefixMul.fill(0);
        prefixMul[0] = arr[0];
        for (let i = 1; i < n; i++)
            prefixMul[i] = prefixMul[i - 1] * arr[i];

        // Forming suffix sum array from n-1
        let suffixMul=new Array(n);
        suffixMul.fill(0);
        suffixMul[0] = arr[0];
        suffixMul[n - 1] = arr[n - 1];
        for (let i = n - 2; i >= 0; i--)
            suffixMul[i] = suffixMul[i + 1] * arr[i];

        // Find the point where prefix and suffix
        // sums are same.
        for (let i = 1; i < n - 1; i++)
            if (prefixMul[i] == suffixMul[i])
                return arr[i];

        return -1;
    }

    let arr = [2, 3, 4, 1, 4, 6 ];
    let n = arr.length;
    document.write(findElement(arr, n));

    // This code is contributed by vaibhavrabadiya117.
</script>
```

**Output:** 

```
1
```

一个**有效的**解决方案将是计算除了 right_mul 中的第一个元素之外的整个数组的乘积，将其视为分区元素。现在，我们从左到右遍历数组，将一个元素从 right_mul 分割，并将一个元素乘以 left_mul。右 mul 等于左 mul 的点，我们得到分区。

**时间复杂度:**O(N)
T3】辅助空间: O(1)

## C++

```
// C++ program to find an element which divides
// the array in two sub-arrays with equal product.
#include <bits/stdc++.h>
using namespace std;

// Function to compute partition
int findElement(int arr[], int size)
{
    int right_mul = 1, left_mul = 1;

    // Computing right_sum
    for (int i = 1; i < size; i++)
        right_mul *= arr[i];

    // Checking the point of partition
    // i.e. left_Sum == right_sum
    for (int i = 0, j = 1; j < size; i++, j++) {
        right_mul /= arr[j];
        left_mul *= arr[i];

        if (left_mul == right_mul)
            return arr[i + 1];
    }

    return -1;
}
// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 1, 4, 6 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << findElement(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an
// element which divides the
// array in two sub-arrays
// with equal product.
class GFG
{

// Function to
// compute partition
static int findElement(int arr[],
                       int size)
{
    int right_mul = 1,
        left_mul = 1;

    // Computing right_sum
    for (int i = 1; i < size; i++)
        right_mul *= arr[i];

    // Checking the point of
    // partition i.e. left_Sum
    // == right_sum
    for (int i = 0, j = 1;
             j < size; i++, j++)
    {
        right_mul /= arr[j];
        left_mul *= arr[i];

        if (left_mul == right_mul)
            return arr[i + 1];
    }

    return -1;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = {2, 3, 4, 1, 4, 6};
    int size = arr.length;
    System.out.println(findElement(arr,
                                   size));
}
}
// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python program to find an element which divides
# the array in two sub-arrays with equal product.

# Function to compute partition
def findElement(arr, size):

    right_mul = 1;
    left_mul = 1;

    # Computing right_sum
    for i in range(1,size):
        right_mul = right_mul *arr[i];
    # Checking the point of partition
    # i.e. left_Sum == right_sum
    for i, j in zip(range(0,size), range(1, size, 1)):   
        right_mul =right_mul / arr[j];
        left_mul = left_mul * arr[i];

        if (left_mul == right_mul):
            return arr[i + 1];

    return -1;

# Driver Code

arr = [ 2, 3, 4, 1, 4, 6,];
size = len(arr) ;
print(findElement(arr, size));

#This code is contributed by Shivi_Aggarwal
```

## C#

```
// C# program to find an
// element which divides the
// array in two sub-arrays
// with equal product.
using System;

class GFG
{
// Function to
// compute partition
static int findElement(int []arr,
                       int size)
{
    int right_mul = 1,
        left_mul = 1;

    // Computing right_sum
    for (int i = 1; i < size; i++)
        right_mul *= arr[i];

    // Checking the point of
    // partition i.e. left_Sum
    // == right_sum
    for (int i = 0, j = 1;
            j < size; i++, j++)
    {
        right_mul /= arr[j];
        left_mul *= arr[i];

        if (left_mul == right_mul)
            return arr[i + 1];
    }

    return -1;
}

// Driver Code
public static void Main()
{
    int []arr = new int[] {2, 3, 4,
                           1, 4, 6};
    int size = arr.Length;
    Console.Write(findElement(arr, size));
}
}

// This code is contributed
// by shiv_bhakt.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find an
// element which divides
// the array in two sub-
// arrays with equal product.

// Function to compute partition
function findElement($arr, $size)
{
    $right_mul = 1;
    $left_mul = 1;

    // Computing right_sum
    for ($i = 1; $i < $size; $i++)
        $right_mul *= $arr[$i];

    // Checking the point
    // of partition i.e.
    // left_Sum == right_sum
    for ($i = 0, $j = 1;
         $j < $size; $i++, $j++)
    {
        $right_mul /= $arr[$j];
        $left_mul *= $arr[$i];

        if ($left_mul == $right_mul)
            return $arr[$i + 1];
    }

    return -1;
}

// Driver Code
$arr = array(2, 3, 4, 1, 4, 6);
$size = sizeof($arr) /
        sizeof($arr[0]);
echo findElement($arr, $size);

// This code is contributed
// by shiv_bhakt.
?>
```

## java 描述语言

```
<script>
// javascript program to find an
// element which divides the
// array in two sub-arrays
// with equal product.    // Function to
    // compute partition
    function findElement(arr , size) {
        var right_mul = 1, left_mul = 1;

        // Computing right_sum
        for (i = 1; i < size; i++)
            right_mul *= arr[i];

        // Checking the point of
        // partition i.e. left_Sum
        // == right_sum
        for (i = 0, j = 1; j < size; i++, j++) {
            right_mul /= arr[j];
            left_mul *= arr[i];

            if (left_mul == right_mul)
                return arr[i + 1];
        }

        return -1;
    }

    // Driver Code

        var arr = [ 2, 3, 4, 1, 4, 6 ];
        var size = arr.length;
        document.write(findElement(arr, size));

// This code contributed by umadevi9616
</script>
```

**Output :** 

```
1
```