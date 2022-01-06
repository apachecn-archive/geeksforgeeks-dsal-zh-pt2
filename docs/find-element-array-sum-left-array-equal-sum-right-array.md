# 找到数组中的一个元素，使左数组的和等于右数组的和

> 原文:[https://www . geesforgeks . org/find-element-array-sum-left-array-equal-sum-right-array/](https://www.geeksforgeeks.org/find-element-array-sum-left-array-equal-sum-right-array/)

给定一个大小为 n 的数组，找到一个元素，将数组分成两个和相等的子数组。
**例:**

```
Input: 1 4 2 5
Output: 2
Explanation: If 2 is the partition, 
      subarrays are : {1, 4} and {5}

Input: 2 3 4 1 4 5
Output: 1
Explanation: If 1 is the partition, 
 Subarrays are : {2, 3, 4} and {4, 5}
```

**方法 1(简单)**
从第二个元素开始考虑每个元素。计算左边元素的总和和右边元素的总和。如果这两个和相同，则返回元素。

**方法 2(使用前缀和后缀数组:**

```
We form a prefix and suffix sum arrays

Given array: 1 4 2 5
Prefix Sum:  1  5 7 12
Suffix Sum:  12 11 7 5

Now, we will traverse both prefix arrays.
The index at which they yield equal result,
is the index where the array is partitioned 
with equal sum.
```

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int findElement(int arr[], int n)
{
    // Forming prefix sum array from 0
    int prefixSum[n];
    prefixSum[0] = arr[0];
    for (int i = 1; i < n; i++)
        prefixSum[i] = prefixSum[i - 1] + arr[i];

    // Forming suffix sum array from n-1
    int suffixSum[n];
    suffixSum[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        suffixSum[i] = suffixSum[i + 1] + arr[i];

    // Find the point where prefix and suffix
    // sums are same.
    for (int i = 1; i < n - 1; i++)
        if (prefixSum[i] == suffixSum[i])
            return arr[i];

    return -1;
}

// Driver code
int main()
{
    int arr[] = { 1, 4, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findElement(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an element
// such that sum of right side element
// is equal to sum of left side
public class GFG {

    // Finds an element in an array such that
    // left and right side sums are equal
    static int findElement(int arr[], int n)
    {
        // Forming prefix sum array from 0
        int[] prefixSum = new int[n];
        prefixSum[0] = arr[0];
        for (int i = 1; i < n; i++)
            prefixSum[i] = prefixSum[i - 1] + arr[i];

        // Forming suffix sum array from n-1
        int[] suffixSum = new int[n];
        suffixSum[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--)
            suffixSum[i] = suffixSum[i + 1] + arr[i];

        // Find the point where prefix and suffix
        // sums are same.
        for (int i = 1; i < n - 1; i++)
            if (prefixSum[i] == suffixSum[i])
                return arr[i];

        return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = { 1, 4, 2, 5 };
        int n = arr.length;
        System.out.println(findElement(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 Program to find an element
# such that sum of right side element
# is equal to sum of left side

# Function for Finds an element in
# an array such that left and right
# side sums are equal
def findElement(arr, n) :

    # Forming prefix sum array from 0
    prefixSum = [0] * n
    prefixSum[0] = arr[0]
    for i in range(1, n) :
        prefixSum[i] = prefixSum[i - 1] + arr[i]

    # Forming suffix sum array from n-1
    suffixSum = [0] * n
    suffixSum[n - 1] = arr[n - 1]
    for i in range(n - 2, -1, -1) :
        suffixSum[i] = suffixSum[i + 1] + arr[i]

    # Find the point where prefix
    # and suffix sums are same.
    for i in range(1, n - 1, 1) :
        if prefixSum[i] == suffixSum[i] :
            return arr[i]

    return -1

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 4, 2, 5]
    n = len(arr)
    print(findElement(arr, n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find an element
// such that sum of right side element
// is equal to sum of left side
using System;

class GFG
{

    // Finds an element in an
    // array such that left
    // and right side sums
    // are equal
    static int findElement(int []arr,
                           int n)
    {
        // Forming prefix sum
        // array from 0
        int[] prefixSum = new int[n];
        prefixSum[0] = arr[0];
        for (int i = 1; i < n; i++)
            prefixSum[i] = prefixSum[i - 1] +
                                     arr[i];

        // Forming suffix sum
        // array from n-1
        int[] suffixSum = new int[n];
        suffixSum[n - 1] = arr[n - 1];
        for (int i = n - 2; i >= 0; i--)
            suffixSum[i] = suffixSum[i + 1] +
                                     arr[i];

        // Find the point where prefix
        // and suffix sums are same.
        for (int i = 1; i < n - 1; i++)
            if (prefixSum[i] == suffixSum[i])
                return arr[i];

        return -1;
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 4, 2, 5 };
        int n = arr.Length;
        Console.WriteLine(findElement(arr, n));
    }
}

// This code is contributed by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
function findElement(&$arr, $n)
{
    // Forming prefix sum array from 0
    $prefixSum = array_fill(0, $n, NULL);
    $prefixSum[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
        $prefixSum[$i] = $prefixSum[$i - 1] +
                                    $arr[$i];

    // Forming suffix sum array from n-1
    $suffixSum = array_fill(0, $n, NULL);
    $suffixSum[$n - 1] = $arr[$n - 1];
    for ($i = $n - 2; $i >= 0; $i--)
        $suffixSum[$i] = $suffixSum[$i + 1] +
                                    $arr[$i];

    // Find the point where prefix
    // and suffix sums are same.
    for ($i = 1; $i < $n - 1; $i++)
        if ($prefixSum[$i] == $suffixSum[$i])
            return $arr[$i];

    return -1;
}

// Driver code
$arr = array( 1, 4, 2, 5 );
$n = sizeof($arr);
echo findElement($arr, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find an element
// such that sum of right side element
// is equal to sum of left side

    // Finds an element in an array such that
    // left and right side sums are equal
    function findElement(arr , n)
    {
        // Forming prefix sum array from 0
        var prefixSum = Array(n).fill(0);
        prefixSum[0] = arr[0];
        for (i = 1; i < n; i++)
            prefixSum[i] = prefixSum[i - 1] + arr[i];

        // Forming suffix sum array from n-1
        var suffixSum = Array(n).fill(0);
        suffixSum[n - 1] = arr[n - 1];
        for (i = n - 2; i >= 0; i--)
            suffixSum[i] = suffixSum[i + 1] + arr[i];

        // Find the point where prefix and suffix
        // sums are same.
        for (i = 1; i < n - 1; i++)
            if (prefixSum[i] == suffixSum[i])
                return arr[i];

        return -1;
    }

    // Driver code

        var arr = [ 1, 4, 2, 5 ];
        var n = arr.length;
        document.write(findElement(arr, n));

// This code contributed by umadevi9616

</script>
```

**Output**

```
2
```

**方法 3(空间有效)**
我们计算除了 right_sum 中的第一个元素之外的整个数组的和，认为它是划分元素。现在，我们从左到右遍历数组，从 right_sum 中减去一个元素，并向 left_sum 中添加一个元素。在 right_sum 等于 left_sum 的地方，我们得到了分区。

下面是实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to compute partition
int findElement(int arr[], int size)
{
    int right_sum = 0, left_sum = 0;

    // Computing right_sum
    for (int i = 1; i < size; i++)
        right_sum += arr[i];

    // Checking the point of partition
    // i.e. left_Sum == right_sum
    for (int i = 0, j = 1; j < size; i++, j++) {
        right_sum -= arr[j];
        left_sum += arr[i];

        if (left_sum == right_sum)
            return arr[i + 1];
    }

    return -1;
}

// Driver
int main()
{
    int arr[] = { 2, 3, 4, 1, 4, 5 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << findElement(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an element
// such that sum of right side element
// is equal to sum of left side
public class GFG {

    // Function to compute partition
    static int findElement(int arr[], int size)
    {
        int right_sum = 0, left_sum = 0;

        // Computing right_sum
        for (int i = 1; i < size; i++)
            right_sum += arr[i];

        // Checking the point of partition
        // i.e. left_Sum == right_sum
        for (int i = 0, j = 1; j < size; i++, j++) {
            right_sum -= arr[j];
            left_sum += arr[i];

            if (left_sum == right_sum)
                return arr[i + 1];
        }

        return -1;
    }

    // Driver
    public static void main(String args[])
    {
        int arr[] = { 2, 3, 4, 1, 4, 5 };
        int size = arr.length;
        System.out.println(findElement(arr, size));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 Program to find an element
# such that sum of right side element
# is equal to sum of left side

# Function to compute partition
def findElement(arr, size) :

    right_sum, left_sum = 0, 0

    # Computing right_sum
    for i in range(1, size) :
        right_sum += arr[i]

    i, j = 0, 1

    # Checking the point of partition
    # i.e. left_Sum == right_sum
    while j < size :
        right_sum -= arr[j]
        left_sum += arr[i]

        if left_sum == right_sum :
            return arr[i + 1]

        j += 1
        i += 1

    return -1

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 3, 4, 1, 4, 5]
    n = len(arr)
    print(findElement(arr, n))

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to find an
// element such that sum
// of right side element
// is equal to sum of
// left side
using System;

class GFG
{
    // Function to compute
    // partition
    static int findElement(int []arr,
                           int size)
    {
        int right_sum = 0,
            left_sum = 0;

        // Computing right_sum
        for (int i = 1; i < size; i++)
            right_sum += arr[i];

        // Checking the point
        // of partition i.e.
        // left_Sum == right_sum
        for (int i = 0, j = 1;
                 j < size; i++, j++)
        {
            right_sum -= arr[j];
            left_sum += arr[i];

            if (left_sum == right_sum)
                return arr[i + 1];
        }

        return -1;
    }

    // Driver Code
    public static void Main()
    {
        int []arr = {2, 3, 4, 1, 4, 5};
        int size = arr.Length;
        Console.WriteLine(findElement(arr, size));
    }
}

// This code is contributed
// by anuj_67.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Function to compute partition
function findElement(&$arr, $size)
{
    $right_sum = 0;
    $left_sum = 0;

    // Computing right_sum
    for ($i = 1; $i < $size; $i++)
        $right_sum += $arr[$i];

    // Checking the point of partition
    // i.e. left_Sum == right_sum
    for ($i = 0, $j = 1;
         $j < $size; $i++, $j++)
    {
        $right_sum -= $arr[$j];
        $left_sum += $arr[$i];

        if ($left_sum == $right_sum)
            return $arr[$i + 1];
    }

    return -1;
}

// Driver Code
$arr = array( 2, 3, 4, 1, 4, 5 );
$size = sizeof($arr);
echo findElement($arr, $size);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>
     // Function to compute partition
    function findElement(arr) {
        let right_sum = 0, left_sum = 0;

        // Computing right_sum
        for (let i = 1; i < arr.length; i++)
            right_sum += arr[i];

        // Checking the point of partition
        // i.e. left_Sum == right_sum
        for (let i = 0, j = 1; j < arr.length; i++, j++) {
            right_sum -= arr[j];
            left_sum += arr[i];

            if (left_sum === right_sum)
                return arr[i + 1];
        }

        return -1;
    }

    // Driver
    let arr = [ 2, 3, 4, 1, 4, 5 ];
    document.write(findElement(arr));

// This code is contributed by Surbhi Tyagi
</script>
```

**Output**

```
1
```

**方法 4(时空效率)**

```
We define two pointers i and j to traverse the array from left and right,
left_sum and right_sum to store sum from right and left respectively

If left_sum is lesser than increment i and if right_sum is lesser than decrement j 
and, find a position where left_sum == right_sum and i and j are next to each other
```

**注:**该解仅适用于数组只包含正元素的情况。

下面是上述方法的实现:

## C++

```
// C++ program to find an element
// such that sum of right side element
// is equal to sum of left side
#include<bits/stdc++.h>
using namespace std;

// Function to compute
// partition
int findElement(int arr[],
                int size)
{
  int right_sum = 0,
      left_sum = 0;

  // Maintains left
  // cumulative sum
  left_sum = 0;

  // Maintains right
  // cumulative sum
  right_sum = 0;
  int i = -1, j = -1;

  for(i = 0, j = size - 1;
      i < j; i++, j--)
  {
    left_sum += arr[i];
    right_sum += arr[j];

    // Keep moving i towards
    // center until left_sum
    //is found lesser than right_sum
    while(left_sum < right_sum &&
          i < j)
    {
      i++;
      left_sum += arr[i];
    }

    // Keep moving j towards
    // center until right_sum is
    // found lesser than left_sum
    while(right_sum < left_sum &&
          i < j)
    {
      j--;
      right_sum += arr[j];
    }
  }

  if(left_sum == right_sum && i == j)
    return arr[i];
  else
    return -1;
}

// Driver code
int main()
{
  int arr[] = {2, 3, 4,
               1, 4, 5};
  int size = sizeof(arr) /
             sizeof(arr[0]);
  cout << (findElement(arr, size));
}

// This code is contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find an element
// such that sum of right side element
// is equal to sum of left side
public class Gfg {

    // Function to compute partition
    static int findElement(int arr[], int size)
    {
        int right_sum = 0, left_sum = 0;
        // Maintains left cumulative sum
        left_sum = 0;

        // Maintains right cumulative sum
        right_sum=0;
        int i = -1, j = -1;

        for( i = 0, j = size-1 ; i < j ; i++, j-- ){
            left_sum += arr[i];
            right_sum += arr[j];

            // Keep moving i towards center until
            // left_sum is found lesser than right_sum
            while(left_sum < right_sum && i < j){
                i++;
                left_sum += arr[i];
            }
            // Keep moving j towards center until
            // right_sum is found lesser than left_sum
            while(right_sum < left_sum && i < j){
                j--;
                right_sum += arr[j];
            }
        }
        if(left_sum == right_sum && i == j)
            return arr[i];
        else
            return -1;
    }

    // Driver code
    public static void main(String args[])
    {
        int arr[] = {2, 3, 4, 1, 4, 5};
        int size = arr.length;
        System.out.println(findElement(arr, size));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find an element
# such that sum of right side element
# is equal to sum of left side

# Function to compute partition
def findElement(arr, size):

    # Maintains left cumulative sum
    left_sum = 0;

    # Maintains right cumulative sum
    right_sum = 0;
    i = 0; j = -1;
    j = size - 1;

    while(i < j):
        if(i < j):
            left_sum += arr[i];
            right_sum += arr[j];

            # Keep moving i towards center
            # until left_sum is found
            # lesser than right_sum
            while (left_sum < right_sum and
                   i < j):
                i += 1;
                left_sum += arr[i];

            # Keep moving j towards center
            # until right_sum is found
            # lesser than left_sum
            while (right_sum < left_sum and
                   i < j):
                j -= 1;
                right_sum += arr[j];
            j -= 1
            i += 1
    if (left_sum == right_sum && i == j):
        return arr[i];
    else:
        return -1;

# Driver code
if __name__ == '__main__':

    arr = [2, 3, 4,
           1, 4, 5];
    size = len(arr);
    print(findElement(arr, size));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program to find an element
// such that sum of right side element
// is equal to sum of left side
using System;

class GFG{

// Function to compute partition
static int findElement(int []arr, int size)
{
    int right_sum = 0, left_sum = 0;

    // Maintains left cumulative sum
    left_sum = 0;

    // Maintains right cumulative sum
    right_sum = 0;
    int i = -1, j = -1;

    for(i = 0, j = size - 1; i < j; i++, j--)
    {
        left_sum += arr[i];
        right_sum += arr[j];

        // Keep moving i towards center until
        // left_sum is found lesser than right_sum
        while (left_sum < right_sum && i < j)
        {
            i++;
            left_sum += arr[i];
        }

        // Keep moving j towards center until
        // right_sum is found lesser than left_sum
        while (right_sum < left_sum && i < j)
        {
            j--;
            right_sum += arr[j];
        }
    }
    if (left_sum == right_sum && i == j)
        return arr[i];
    else
        return -1;
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 2, 3, 4, 1, 4, 5 };
    int size = arr.Length;

    Console.WriteLine(findElement(arr, size));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program to find an element
// such that sum of right side element
// is equal to sum of left side

    // Function to compute partition
    function findElement(arr , size) {
        var right_sum = 0, left_sum = 0;
        // Maintains left cumulative sum
        left_sum = 0;

        // Maintains right cumulative sum
        right_sum = 0;
        var i = -1, j = -1;

        for (i = 0, j = size - 1; i < j; i++, j--) {
            left_sum += arr[i];
            right_sum += arr[j];

            // Keep moving i towards center until
            // left_sum is found lesser than right_sum
            while (left_sum < right_sum && i < j) {
                i++;
                left_sum += arr[i];
            }
            // Keep moving j towards center until
            // right_sum is found lesser than left_sum
            while (right_sum < left_sum && i < j) {
                j--;
                right_sum += arr[j];
            }
        }
        if (left_sum == right_sum && i == j)
            return arr[i];
        else
            return -1;
    }

    // Driver code

        var arr = [ 2, 3, 4, 1, 4, 5 ];
        var size = arr.length;
        document.write(findElement(arr, size));

// This code contributed by gauravrajput1
</script>
```

**Output**

```
1
```