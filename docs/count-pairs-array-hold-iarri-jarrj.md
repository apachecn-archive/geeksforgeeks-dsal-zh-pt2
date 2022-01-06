# 计数数组中持有 i*arr[i] > j*arr[j]

的对

> 原文:[https://www . geesforgeks . org/count-pairs-array-hold-iarri-jarrj/](https://www.geeksforgeeks.org/count-pairs-array-hold-iarri-jarrj/)

给定整数数组 arr[0..n-1]，对中的所有对(arr[i]，arr[j])进行计数，使得 i*arr[i] > j*arr[j]，0 =< i < j < n。

**示例:**

```
Input : arr[] = {5 , 0, 10, 2, 4, 1, 6}
Output: 5
 Pairs which hold condition i*arr[i] > j*arr[j]
 are (10, 2) (10, 4) (10, 1) (2, 1) (4, 1)

Input  : arr[] = {8, 4, 2, 1}
Output : 2
```

一个**简单的解决方案**是运行两个循环。逐个选取数组中的每个元素，并为每个元素找到数组右侧满足保持条件的元素，然后递增计数器并最后返回计数器值。

以下是上述想法的实现:

## C++

```
// C++ program to count all pair that
// hold condition i*arr[i] > j*arr[j]
#include<iostream>
using namespace std;

// Return count of pair in given array
// such that  i*arr[i] > j*arr[j]
int CountPair(int arr[] , int n )
{
    int result = 0; // Initialize result

    for (int i=0; i<n; i++)
    {
        // Generate all pair and increment
        // counter if the hold given condition
        for (int j = i + 1; j < n; j++)
            if (i*arr[i] > j*arr[j] )
                result ++;
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = {5 , 0, 10, 2, 4, 1, 6} ;
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Count of Pairs : "
         << CountPair(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Code for Count pairs in an
// array that hold i*arr[i] > j*arr[j]
class GFG {

    // Return count of pair in given array
    // such that  i*arr[i] > j*arr[j]
    public static int CountPair(int arr[] , int n )
    {
        int result = 0; // Initialize result

        for (int i = 0; i < n; i++)
        {
            // Generate all pair and increment
            // counter if the hold given condition
            for (int j = i + 1; j < n; j++)
                if (i*arr[i] > j*arr[j] )
                    result ++;
        }
        return result;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {5 , 0, 10, 2, 4, 1, 6} ;
        int n = arr.length;
        System.out.println("Count of Pairs : " +
                            CountPair(arr, n));
    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 Code to Count pairs in an
# array that hold i*arr[i] > j*arr[j]

# Return count of pair in given array
# such that i*arr[i] > j*arr[j]
def CountPair(arr , n ):

    # Initialize result
    result = 0;

    for i in range (0, n):

        # Generate all pair and increment
        # counter if the hold given condition
        j = i + 1
        while(j < n):
            if (i * arr[i] > j * arr[j] ):
                result = result +1
            j = j + 1
    return result;

# Driver program to test above function */

arr = [5, 0, 10, 2, 4, 1, 6]
n = len(arr)
print("Count of Pairs : " , CountPair(arr, n))

# This code is contributed by Sam007.
```

## C#

```
// C# Code to Count pairs in an
// array that hold i*arr[i] > j*arr[j]
using System;

class GFG
{
    // Return count of pair in given array
    // such that i*arr[i] > j*arr[j]
    public static int CountPair(int []arr , int n )
    {
        // Initialize result
        int result = 0;

        for (int i = 0; i < n; i++)
        {
            // Generate all pair and increment
            // counter if the hold given condition
            for (int j = i + 1; j < n; j++)
                if (i*arr[i] > j*arr[j] )
                    result ++;
        }
        return result;
    }

    /* Driver program to test above function */
    public static void Main()
    {
        int []arr = {5, 0, 10, 2, 4, 1, 6};
        int n = arr.Length;
        Console.WriteLine("Count of Pairs : " +
                           CountPair(arr, n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all pair that
// hold condition i*arr[i] > j*arr[j]

// Return count of pair in given array
// such that i*arr[i] > j*arr[j]
function CountPair($arr , $n )
{

    // Initialize result
    $result = 0;

    for($i = 0; $i < $n; $i++)
    {

        // Generate all pair and increment
        // counter if the hold given condition
        for ($j = $i + 1; $j < $n; $j++)
            if ($i *  $arr[$i] > $j * $arr[$j] )
                $result ++;
    }
    return $result;
}

    // Driver code
    $arr = array(5, 0, 10, 2, 4, 1, 6) ;
    $n = sizeof($arr);
    echo "Count of Pairs : ",
    CountPair($arr, $n);

// This code is contributed by m_kit
?>
```

## java 描述语言

```
<script>

// JavaScript program  to Count pairs in an
// array that hold i*arr[i] > j*arr[j]

// Return count of pair in given array
// such that  i*arr[i] > j*arr[j]
function CountPair(arr, n)
{

    // Initialize result
    let result = 0;

    for(let i = 0; i < n; i++)
    {

        // Generate all pair and increment
        // counter if the hold given condition
        for(let j = i + 1; j < n; j++)
            if (i * arr[i] > j * arr[j] )
                result ++;
    }
    return result;
}

// Driver Code
let arr = [5 , 0, 10, 2, 4, 1, 6] ;
let n = arr.length;

document.write("Count of Pairs : " +
               CountPair(arr, n));

// This code is contributed by souravghosh0416 

</script>
```

**输出:**

```
Count of Pairs : 5
```

时间复杂度:O(n <sup>2</sup> )

这个问题的一个**高效解决方案**需要 O(n log n)时间。这个想法是基于一个关于这个问题的有趣事实，即在修改数组使得每个元素都与其索引相乘之后，这个问题转换成[在数组](https://www.geeksforgeeks.org/counting-inversions/)中计数反转。
算法:

```
Given an array 'arr' and it's size 'n'
1) First traversal array element, i goes from 0 to n-1
   a) Multiple each element with its index arr[i] = arr[i] * i 
2) After that step 1\. whole process is similar to Count Inversions in an array. 
```

在上述思想的实施下

## C++

```
// C++ program to count all pair that
// hold condition i*arr[i] > j*arr[j]
#include <bits/stdc++.h>
using namespace std;

/* This function merges two sorted arrays and
   returns inversion count in the arrays.*/
int merge(int arr[], int temp[], int left,
                       int mid, int right)
{
    int inv_count = 0;

    int i = left; /* index for left subarray*/
    int j = mid;  /* index for right subarray*/
    int k = left; /* index for resultant subarray*/
    while ((i <= mid - 1) && (j <= right))
    {
        if (arr[i] <= arr[j])
            temp[k++] = arr[i++];
        else
        {
            temp[k++] = arr[j++];

            inv_count = inv_count + (mid - i);
        }
    }

    /* Copy the remaining elements of left
     subarray (if there are any) to temp*/
    while (i <= mid - 1)
        temp[k++] = arr[i++];

    /* Copy the remaining elements of right
     subarray (if there are any) to temp*/
    while (j <= right)
        temp[k++] = arr[j++];

    /* Copy back the merged elements to original
      array*/
    for (i=left; i <= right; i++)
        arr[i] = temp[i];

    return inv_count;
}

/* An auxiliary recursive function that sorts
   the input array and returns the number of
   inversions in the array. */
int _mergeSort(int arr[], int temp[], int left,
                                      int right)
{
    int mid, inv_count = 0;
    if (right > left)
    {
        /* Divide the array into two parts and call
          _mergeSortAndCountInv() for each of
          the parts */
        mid = (right + left)/2;

        /* Inversion count will be sum of inversions in
           left-part, right-part and number of inversions
           in merging */
        inv_count  = _mergeSort(arr, temp, left, mid);
        inv_count += _mergeSort(arr, temp, mid+1, right);

        /*Merge the two parts*/
        inv_count += merge(arr, temp, left, mid+1, right);
    }

    return inv_count;
}

/* This function sorts the input array and
   returns the number of inversions in the
   array */
int countPairs(int arr[], int n)
{
    // Modify the array so that problem reduces to
    // count inversion problem.
    for (int i=0; i<n; i++)
        arr[i] = i*arr[i];

    // Count inversions using same logic as
    // below post
    // https://www.geeksforgeeks.org/counting-inversions/
    int temp[n];
    return _mergeSort(arr, temp, 0, n - 1);
}

// Driver code
int main()
{
    int arr[] = {5, 0, 10, 2, 4, 1, 6};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << "Count of Pairs : "
         << countPairs(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count all pair that
// hold condition i*arr[i] > j*arr[j]
import java.io.*;

class GFG
{
    // This function merges two sorted arrays and
    // returns inversion count in the arrays.
    static int merge(int arr[], int temp[], int left,
                                   int mid, int right)
    {
        int inv_count = 0;

        /* index for left subarray*/
        int i = left;

        /* index for right subarray*/
        int j = mid;
        /* index for resultant subarray*/
        int k = left;

        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
            {
                temp[k++] = arr[j++];

                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements of left
        subarray (if there are any) to temp*/
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        /* Copy the remaining elements of right
        subarray (if there are any) to temp*/
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements
        // to original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    /* An auxiliary recursive function
    that sorts the input array and
    returns the number of inversions
    in the array. */
    static int _mergeSort(int arr[], int temp[],
                               int left,int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and call
            _mergeSortAndCountInv() for each of
            the parts */
            mid = (right + left) / 2;

            // Inversion count will be sum of inversions in
            // left-part, right-part and number of inversions
            // in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid+1, right);

            /*Merge the two parts*/
            inv_count += merge(arr, temp, left, mid+1, right);
        }

        return inv_count;
    }

    // This function sorts the input array and
    // returns the number of inversions in the
    // array
    static int countPairs(int arr[], int n)
    {
        // Modify the array so that problem reduces to
        // count inversion problem.
        for (int i = 0; i < n; i++)
            arr[i] = i * arr[i];

        // Count inversions using same logic as
        // below post
        // https://www.geeksforgeeks.org/counting-inversions/
        int temp[] = new int [n];
        return _mergeSort(arr, temp, 0, n - 1);
    }

    // Driver code

    public static void main (String[] args)
    {
        int arr[] = {5, 0, 10, 2, 4, 1, 6};
        int n = arr.length;
        System.out.print( "Count of Pairs : "
                          + countPairs(arr, n)); 

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to count all
# pair that hold condition
# i*arr[i] > j*arr[j]

# This function merges two
# sorted arrays and returns
# inversion count in the arrays.
def merge(arr, temp, left, mid, right):

    inv_count = 0

    i = left # index for left subarray
    j = mid # index for right subarray
    k = left # index for resultant subarray
    while ((i <= mid - 1) and (j <= right)):

        if (arr[i] <= arr[j]):
            temp[k] = arr[i]
            i += 1
            k += 1
        else:

            temp[k] = arr[j]
            k += 1
            j += 1

            inv_count = inv_count + (mid - i)

    # Copy the remaining elements of left
    # subarray (if there are any) to temp
    while (i <= mid - 1):
        temp[k] = arr[i]
        i += 1
        k += 1

    # Copy the remaining elements of right
    # subarray (if there are any) to temp
    while (j <= right):
        temp[k] = arr[j]
        k += 1
        j += 1

    # Copy back the merged elements
    # to original array
    for i in range(left, right + 1):
        arr[i] = temp[i]

    return inv_count

# An auxiliary recursive function
# that sorts the input array and
# returns the number of inversions
# in the array.
def _mergeSort(arr, temp, left, right):

    inv_count = 0
    if (right > left):

        # Divide the array into two parts
        # and call _mergeSortAndCountInv()
        # for each of the parts
        mid = (right + left) // 2

        # Inversion count will be sum of
        # inversions in left-part, right-part x
        # and number of inversions in merging
        inv_count = _mergeSort(arr, temp, left, mid)
        inv_count += _mergeSort(arr, temp,
                                mid + 1, right)

        # Merge the two parts
        inv_count += merge(arr, temp, left,    
                           mid + 1, right)

    return inv_count

# This function sorts the input
# array and returns the number
# of inversions in the array
def countPairs(arr, n):

    # Modify the array so that problem
    # reduces to count inversion problem.
    for i in range(n):
        arr[i] = i * arr[i]

    # Count inversions using same
    # logic as below post
    # https://www.geeksforgeeks.org/counting-inversions/
    temp = [0] * n
    return _mergeSort(arr, temp, 0, n - 1)

# Driver code
if __name__ == "__main__":
    arr = [5, 0, 10, 2, 4, 1, 6]
    n = len(arr)
    print("Count of Pairs : ",
           countPairs(arr, n))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to count all pair that
// hold condition i*arr[i] > j*arr[j]
using System;

class GFG
{
    // This function merges two sorted arrays and
    // returns inversion count in the arrays.
    static int merge(int []arr, int []temp, int left,
                                int mid, int right)
    {
        int inv_count = 0;

        /* index for left subarray*/
        int i = left;

        /* index for right subarray*/
        int j = mid;
        /* index for resultant subarray*/
        int k = left;

        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
            {
                temp[k++] = arr[j++];

                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements of left
        subarray (if there are any) to temp*/
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        /* Copy the remaining elements of right
        subarray (if there are any) to temp*/
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements
        // to original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    /* An auxiliary recursive function
    that sorts the input array and
    returns the number of inversions
    in the array. */
    static int _mergeSort(int []arr, int []temp,
                            int left,int right)
    {
        int mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and call
            _mergeSortAndCountInv() for each of
            the parts */
            mid = (right + left) / 2;

            // Inversion count will be sum of inversions in
            // left-part, right-part and number of inversions
            // in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid+1, right);

            /*Merge the two parts*/
            inv_count += merge(arr, temp, left, mid+1, right);
        }

        return inv_count;
    }

    // This function sorts the input array and
    // returns the number of inversions in the
    // array
    static int countPairs(int []arr, int n)
    {
        // Modify the array so that problem reduces to
        // count inversion problem.
        for (int i = 0; i < n; i++)
            arr[i] = i * arr[i];

        // Count inversions using same logic as
        // below post
        // https://www.geeksforgeeks.org/counting-inversions/
        int []temp = new int [n];
        return _mergeSort(arr, temp, 0, n - 1);
    }

    // Driver code

    public static void Main ()
    {
        int []arr = {5, 0, 10, 2, 4, 1, 6};
        int n = arr.Length;
        Console.WriteLine( "Count of Pairs : "
                        + countPairs(arr, n));

    }
}

// This code is contributed by anuj_67.
```

## java 描述语言

```
<script>
// Javascript program to count all pair that
// hold condition i*arr[i] > j*arr[j]

    // This function merges two sorted arrays and
    // returns inversion count in the arrays.
    function merge(arr,temp,left,mid,right)
    {
        let inv_count = 0;

        /* index for left subarray*/
        let i = left;

        /* index for right subarray*/
        let j = mid;
        /* index for resultant subarray*/
        let k = left;

        while ((i <= mid - 1) && (j <= right))
        {
            if (arr[i] <= arr[j])
                temp[k++] = arr[i++];
            else
            {
                temp[k++] = arr[j++];

                inv_count = inv_count + (mid - i);
            }
        }

        /* Copy the remaining elements of left
        subarray (if there are any) to temp*/
        while (i <= mid - 1)
            temp[k++] = arr[i++];

        /* Copy the remaining elements of right
        subarray (if there are any) to temp*/
        while (j <= right)
            temp[k++] = arr[j++];

        // Copy back the merged elements
        // to original array
        for (i = left; i <= right; i++)
            arr[i] = temp[i];

        return inv_count;
    }

    /* An auxiliary recursive function
    that sorts the input array and
    returns the number of inversions
    in the array. */
    function _mergeSort(arr,temp,left,right)
    {
        let mid, inv_count = 0;
        if (right > left)
        {
            /* Divide the array into two parts and call
            _mergeSortAndCountInv() for each of
            the parts */
            mid = Math.floor((right + left) / 2);

            // Inversion count will be sum of inversions in
            // left-part, right-part and number of inversions
            // in merging
            inv_count = _mergeSort(arr, temp, left, mid);
            inv_count += _mergeSort(arr, temp, mid+1, right);

            /*Merge the two parts*/
            inv_count += merge(arr, temp, left, mid+1, right);
        }

        return inv_count;
    }

    // This function sorts the input array and
    // returns the number of inversions in the
    // array
    function countPairs(arr,n)
    {
        // Modify the array so that problem reduces to
        // count inversion problem.
        for (let i = 0; i < n; i++)
            arr[i] = i * arr[i];

        // Count inversions using same logic as
        // below post
        // https://www.geeksforgeeks.org/counting-inversions/
        let temp = new Array(n);
        for(let i=0;i<temp;i++)
        {
            temp[i]=0;
        }
        return _mergeSort(arr, temp, 0, n - 1);
    }

    // Driver code
    let arr=[5, 0, 10, 2, 4, 1, 6];
    let n = arr.length;
    document.write( "Count of Pairs : "
                          + countPairs(arr, n));
    // This code is contributed by rag2127
</script>
```

**输出:**

```
Count of Pairs : 5
```

**时间复杂度:** O(n log n)

本文由[**Nishant _ Singh(Pintu)**](https://practice.geeksforgeeks.org/user-profile.php?user=_code)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。