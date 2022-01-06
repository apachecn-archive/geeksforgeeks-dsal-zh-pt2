# 最大和双离子子阵列

> 原文:[https://www.geeksforgeeks.org/maximum-sum-bitonic-subarray/](https://www.geeksforgeeks.org/maximum-sum-bitonic-subarray/)

给定一个包含 **n 个**数字的数组。问题是找到最大和的双调和子阵。双离子子阵列是元素先增加后减少的子阵列。严格递增或严格递减的子阵列也被认为是双子阵列。需要 O(n)的时间复杂度。

**示例:**

```
Input : arr[] = {5, 3, 9, 2, 7, 6, 4}
Output : 19
The subarray is {2, 7, 6, 4}.

Input : arr[] = {9, 12, 14, 8, 6, 5, 10, 20}
Output : 54
```

**方法:**问题与[最大和双调和子序列](https://www.geeksforgeeks.org/maximum-sum-bi-tonic-sub-sequence/)密切相关。我们创建了两个数组 **msis[]** 和 **msds[]** 。msis[i]存储以 arr[i]结尾的递增子阵列的和。msds[i]存储从 arr[i]开始的递减子阵列的和。现在，对于数组的每个索引 **i** ，最大和位子数组计算为**max(msis[I]+MSDS[I]-arr[I])**。

## C++

```
// C++ implementation to find the
// maximum sum bitonic subarray
#include <bits/stdc++.h>

using namespace std;

// function to find the maximum sum
// bitonic subarray
int maxSumBitonicSubArr(int arr[], int n)
{
    // 'msis[]' to store the maximum sum increasing subarray
    // up to each index of 'arr' from the beginning
    // 'msds[]' to store the maximum sum decreasing subarray
    // from each index of 'arr' up to the end
    int msis[n], msds[n];

    // to store the maximum sum
    // bitonic subarray
    int max_sum = INT_MIN;

    // building up the maximum sum increasing subarray
    // for each array index
    msis[0] = arr[0];
    for (int i=1; i<n; i++)
        if (arr[i] > arr[i-1])
            msis[i] = msis[i-1] + arr[i];
        else
            msis[i] = arr[i];   

    // building up the maximum sum decreasing subarray
    // for each array index
    msds[n-1] = arr[n-1];
    for (int i=n-2; i>=0; i--)
        if (arr[i] > arr[i+1])
            msds[i] = msds[i+1] + arr[i];
        else
            msds[i] = arr[i];

    // for each array index, calculating the maximum sum
    // of bitonic subarray of which it is a part of
    for (int i=0; i<n; i++)           
        // if true , then update 'max' bitonic
        // subarray sum
        if (max_sum < (msis[i] + msds[i] - arr[i]))
            max_sum = msis[i] + msds[i] - arr[i];

    // required maximum sum
    return max_sum;
}

// Driver program to test above
int main()
{
    int arr[] = {5, 3, 9, 2, 7, 6, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr, n);
    return 0;    
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// find the maximum sum
// bitonic subarray
class GFG
{

    // function to find the maximum
    // sum bitonic subarray
    static int maxSumBitonicSubArr(int arr[],
                                   int n)
    {

    // 'msis[]' to store the maximum
    // sum increasing subarray up to
    // each index of 'arr' from the
    // beginning 'msds[]' to store
    // the maximum sum decreasing
    // subarray from each index of
    // 'arr' up to the end
    int []msis = new int[n];
    int []msds = new int[n];

    // to store the maximum
    // sum bitonic subarray
    int max_sum = Integer.MIN_VALUE;

    // building up the maximum
    // sum increasing subarray
    // for each array index
    msis[0] = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > arr[i - 1])
            msis[i] = msis[i - 1] +
                       arr[i];
        else
            msis[i] = arr[i];

    // building up the maximum
    // sum decreasing subarray
    // for each array index
    msds[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        if (arr[i] > arr[i + 1])
            msds[i] = msds[i + 1] + arr[i];
        else
            msds[i] = arr[i];

    // for each array index,
    // calculating the maximum
    // sum of bitonic subarray
    // of which it is a part of
    for (int i = 0; i < n; i++)        

        // if true , then update
        // 'max' bitonic subarray sum
        if (max_sum < (msis[i] +
                       msds[i] - arr[i]))
            max_sum = msis[i] +
                      msds[i] - arr[i];

    // required maximum sum
    return max_sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = {5, 3, 9, 2, 7, 6, 4};
        int n = arr.length;
        System.out.println( "Maximum Sum = " +
                 maxSumBitonicSubArr(arr, n));
    }
}

// This code is contributed
// by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation
# to find the maximum sum
# bitonic subarray

# function to find the
# maximum sum bitonic subarray
def maxSumBitonicSubArr(arr, n):

    # 'msis[]' to store the maximum
    # sum increasing subarray up to
    # each index of 'arr' from the
    # beginning 'msds[]' to store
    # the maximum sum decreasing
    # subarray from each index of
    # 'arr' up to the end
    msis = [None] * n
    msds = [None] * n

    # to store the maximum
    # sum bitonic subarray
    max_sum = 0

    # building up the maximum
    # sum increasing subarray
    # for each array index
    msis[0] = arr[0]
    for i in range(1, n):
        if (arr[i] > arr[i - 1]):
            msis[i] = msis[i - 1] + arr[i]
        else:
            msis[i] = arr[i]

    # building up the maximum
    # sum decreasing subarray
    # for each array index
    msds[n - 1] = arr[n - 1]
    for i in range(n - 2, -1, -1):
        if (arr[i] > arr[i + 1]):
            msds[i] = msds[i + 1] + arr[i]
        else:
            msds[i] = arr[i]

    # for each array index,
    # calculating the maximum
    # sum of bitonic subarray
    # of which it is a part of
    for i in range(n):   

        # if true , then update
        # 'max' bitonic subarray sum
        if (max_sum < (msis[i] +
                       msds[i] - arr[i])):
            max_sum = (msis[i] +
                       msds[i] - arr[i])

    # required maximum sum
    return max_sum

# Driver Code
arr = [5, 3, 9, 2, 7, 6, 4];
n = len(arr)
print("Maximum Sum = "+
       str(maxSumBitonicSubArr(arr, n)))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation to find
// the maximum sum bitonic subarray
using System;

class GFG
{

    // function to find the maximum
    // sum bitonic subarray
    static int maxSumBitonicSubArr(int[] arr,
                                   int n)
    {
    // 'msis[]' to store the maximum
    // sum increasing subarray up to
    // each index of 'arr' from the
    // beginning 'msds[]' to store
    // the maximum sum decreasing
    // subarray from each index of
    // 'arr' up to the end
    int []msis = new int[n];
    int []msds = new int[n];

    // to store the maximum
    // sum bitonic subarray
    int max_sum = int.MinValue;

    // building up the maximum
    // sum increasing subarray
    // for each array index
    msis[0] = arr[0];
    for (int i = 1; i < n; i++)
        if (arr[i] > arr[i - 1])
            msis[i] = msis[i - 1] +
                       arr[i];
        else
            msis[i] = arr[i];

    // building up the maximum
    // sum decreasing subarray
    // for each array index
    msds[n - 1] = arr[n - 1];
    for (int i = n - 2; i >= 0; i--)
        if (arr[i] > arr[i + 1])
            msds[i] = msds[i + 1] +
                       arr[i];
        else
            msds[i] = arr[i];

    // for each array index, calculating
    // the maximum sum of bitonic subarray
    // of which it is a part of
    for (int i = 0; i < n; i++)   

        // if true , then update
        // 'max' bitonic subarray sum
        if (max_sum < (msis[i] +
                       msds[i] - arr[i]))
            max_sum = msis[i] +
                      msds[i] - arr[i];

    // required maximum sum
    return max_sum;
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = {5, 3, 9, 2, 7, 6, 4};
        int n = arr.Length;
        Console.Write("Maximum Sum = " +
           maxSumBitonicSubArr(arr, n));
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the
// maximum sum bitonic subarray

// function to find the maximum sum
// bitonic subarray
function maxSumBitonicSubArr($arr, $n)
{
    // 'msis[]' to store the maximum
    // sum increasing subarray up to
    // each index of 'arr' from the
    // beginning 'msds[]' to store
    // the maximum sum decreasing
    // subarray from each index of
    // 'arr' up to the end
    $msis = array();
    $msds = array();

    // to store the maximum
    // sum bitonic subarray
    $max_sum = PHP_INT_MIN;

    // building up the maximum
    // sum increasing subarray
    // for each array index
    $msis[0] = $arr[0];
    for ($i = 1; $i < $n; $i++)
        if ($arr[$i] > $arr[$i - 1])
            $msis[$i] = $msis[$i - 1] +
                              $arr[$i];
        else
            $msis[$i] = $arr[$i];

    // building up the maximum
    // sum decreasing subarray
    // for each array index
    $msds[$n - 1] = $arr[$n - 1];
    for ($i = $n - 2; $i >= 0; $i--)
        if ($arr[$i] > $arr[$i + 1])
            $msds[$i] = $msds[$i + 1] +
                              $arr[$i];
        else
            $msds[$i] = $arr[$i];

    // for each array index,
    // calculating the maximum sum
    // of bitonic subarray of which
    // it is a part of
    for ($i = 0; $i < $n; $i++)    
        // if true , then update
        // 'max' bitonic subarray sum
        if ($max_sum < ($msis[$i] +
                        $msds[$i] - $arr[$i]))
            $max_sum = $msis[$i] +
                       $msds[$i] - $arr[$i];

    // required maximum sum
    return $max_sum;
}

// Driver Code
$arr = array(5, 3, 9,
             2, 7, 6, 4);
$n = sizeof($arr);
echo "Maximum Sum = ",
      maxSumBitonicSubArr($arr, $n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

    // Javascript implementation to find
    // the maximum sum bitonic subarray

    // function to find the maximum
    // sum bitonic subarray
    function maxSumBitonicSubArr(arr, n)
    {
      // 'msis[]' to store the maximum
      // sum increasing subarray up to
      // each index of 'arr' from the
      // beginning 'msds[]' to store
      // the maximum sum decreasing
      // subarray from each index of
      // 'arr' up to the end
      let msis = new Array(n);
      msis.fill(0);
      let msds = new Array(n);
      msds.fill(0);

      // to store the maximum
      // sum bitonic subarray
      let max_sum = Number.MIN_VALUE;

      // building up the maximum
      // sum increasing subarray
      // for each array index
      msis[0] = arr[0];
      for (let i = 1; i < n; i++)
          if (arr[i] > arr[i - 1])
              msis[i] = msis[i - 1] + arr[i];
          else
              msis[i] = arr[i];

      // building up the maximum
      // sum decreasing subarray
      // for each array index
      msds[n - 1] = arr[n - 1];
      for (let i = n - 2; i >= 0; i--)
          if (arr[i] > arr[i + 1])
              msds[i] = msds[i + 1] + arr[i];
          else
              msds[i] = arr[i];

      // for each array index, calculating
      // the maximum sum of bitonic subarray
      // of which it is a part of
      for (let i = 0; i < n; i++)   

          // if true , then update
          // 'max' bitonic subarray sum
          if (max_sum < (msis[i] + msds[i] - arr[i]))
              max_sum = msis[i] + msds[i] - arr[i];

      // required maximum sum
      return max_sum;
    }

    let arr = [5, 3, 9, 2, 7, 6, 4];
    let n = arr.length;
    document.write("Maximum Sum = "
    + maxSumBitonicSubArr(arr, n));

</script>
```

**输出:**

```
Maximum Sum = 19
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

**空间优化解:**
可以恒记忆求解。事实上，由于我们正在寻找连续的子阵列，我们可以将初始阵列分成比特块，并比较它们的总和。

## C++

```
// C++ implementation to find the
// maximum sum bitonic subarray
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum sum bitonic
// subarray.
int maxSumBitonicSubArr(int arr[], int n)
{
    // to store the maximum sum
    // bitonic subarray
    int max_sum = INT_MIN;

    int i = 0;
    while (i < n) {

        // Find the longest increasing subarray
        // starting at i.
        int j = i;
        while (j+1 < n && arr[j] < arr[j+1])
            j++;

        // Now we know that a[i..j] is an
        // increasing subarray. Remove non-
        // positive elements from the left
        // side as much as possible.
        while (i < j && arr[i] <= 0)
            i++;

        // Find the longest decreasing subarray
        // starting at j.
        int k = j;
        while (k+1 < n && arr[k] > arr[k+1])
            k++;

        // Now we know that a[j..k] is a
        // decreasing subarray. Remove non-
        // positive elements from the right
        // side as much as possible.
        // last is needed to keep the last
        // seen element.
        int last = k;
        while (k > j && arr[k] <= 0)
            k--;

        // Compute the max sum of the
        // increasing part.
        int sum_inc =
               accumulate(arr+i, arr+j+1, 0);

        // Compute the max sum of the
        // decreasing part.
        int sum_dec =
               accumulate(arr+j, arr+k+1, 0);

        // The overall max sum is the sum of
        // both parts minus the peak element,
        // because it was counted twice.
        int sum_all = sum_inc + sum_dec - arr[j];

        max_sum = max({max_sum, sum_inc,
                       sum_dec, sum_all});

        // If the next element is equal to the
        // current, i.e. arr[i+1] == arr[i],
        // last == i.
        // To ensure the algorithm has progress,
        // get the max of last and i+1.
        i = max(last, i+1);
    }

    // required maximum sum
    return max_sum;
}

// Driver program to test above
int main()
{
    // The example from the article, the
    // answer is 19.
    int arr[] = {5, 3, 9, 2, 7, 6, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr, n)
         << endl;

    // Always increasing, the answer is 15.
    int arr2[] = {1, 2, 3, 4, 5};
    int n2 = sizeof(arr2) / sizeof(arr2[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr2, n2)
         << endl;

    // Always decreasing, the answer is 15.
    int arr3[] = {5, 4, 3, 2, 1};
    int n3 = sizeof(arr3) / sizeof(arr3[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr3, n3)
         << endl;

    // All are equal, the answer is 5.
    int arr4[] = {5, 5, 5, 5};
    int n4 = sizeof(arr4) / sizeof(arr4[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr4, n4)
         << endl;

    // The whole array is bitonic, but the answer is 7.
    int arr5[] = {-1, 0, 1, 2, 3, 1, 0, -1, -10};
    int n5 = sizeof(arr5) / sizeof(arr5[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr5, n5)
         << endl;

    // The answer is 4 (the tail).
    int arr6[] = {-1, 0, 1, 2, 0, -1, -2, 0, 1, 3};
    int n6 = sizeof(arr6) / sizeof(arr6[0]);
    cout << "Maximum Sum = "
         << maxSumBitonicSubArr(arr6, n6)
         << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum bitonic subarray
import java.util.*;

class GFG{

static int find_partial_sum(int arr[],
                            int start,
                            int end)
{
    int sum = 0;
    for(int i = start; i < end; i++)
        sum += arr[i];

    return sum;
}

// Function to find the maximum sum bitonic
// subarray.
static int maxSumBitonicSubArr(int arr[], int n)
{

    // To store the maximum sum
    // bitonic subarray
    int max_sum = -1000000;

    int i = 0;
    while (i < n)
    {

        // Find the longest increasing
        // subarray starting at i.
        int j = i;
        while (j + 1 < n && arr[j] < arr[j + 1])
            j++;

        // Now we know that a[i..j] is an
        // increasing subarray. Remove non-
        // positive elements from the left
        // side as much as possible.
        while (i < j && arr[i] <= 0)
            i++;

        // Find the longest decreasing subarray
        // starting at j.
        int k = j;
        while (k + 1 < n && arr[k] > arr[k + 1])
            k++;

        // Now we know that a[j..k] is a
        // decreasing subarray. Remove non-
        // positive elements from the right
        // side as much as possible.
        // last is needed to keep the last
        // seen element.
        int last = k;
        while (k > j && arr[k] <= 0)
            k--;

        // Compute the max sum of the
        // increasing part.
        int sum_inc = find_partial_sum(arr, i,
                                       j + 1);

        // Compute the max sum of the
        // decreasing part.
        int sum_dec = find_partial_sum(arr, j,
                                       k + 1);

        // The overall max sum is the sum of
        // both parts minus the peak element,
        // because it was counted twice.
        int sum_all = sum_inc + sum_dec - arr[j];

        max_sum = Math.max(Math.max(max_sum, sum_inc),
                           Math.max(sum_dec, sum_all));

        // If the next element is equal to the
        // current, i.e. arr[i+1] == arr[i],
        // last == i.
        // To ensure the algorithm has progress,
        // get the max of last and i+1.
        i = Math.max(last, i + 1);
    }

    // Required maximum sum
    return max_sum;
}

// Driver code
public static void main(String args[])
{

    // The example from the article, the
    // answer is 19.
    int arr[] = { 5, 3, 9, 2, 7, 6, 4 };
    int n = arr.length;
    System.out.println("Maximum sum = " +
           maxSumBitonicSubArr(arr, n));

    // Always increasing, the answer is 15.
    int arr2[] = { 1, 2, 3, 4, 5 };
    int n2 = arr2.length;
    System.out.println("Maximum sum = " +
           maxSumBitonicSubArr(arr2, n2));

    // Always decreasing, the answer is 15.
    int arr3[] = { 5, 4, 3, 2, 1 };
    int n3 = arr3.length;
    System.out.println("Maximum sum = " +
           maxSumBitonicSubArr(arr3, n3));

    // All are equal, the answer is 5.
    int arr4[] = { 5, 5, 5, 5 };
    int n4 = arr4.length;
    System.out.println("Maximum sum = " +
           maxSumBitonicSubArr(arr4, n4));

    // The whole array is bitonic,
    // but the answer is 7.
    int arr5[] = { -1, 0, 1, 2, 3,
                    1, 0, -1, -10 };
    int n5 = arr5.length;
    System.out.println("Maximum sum = " +
           maxSumBitonicSubArr(arr5, n5));

    // The answer is 4 (the tail).
    int arr6[] = { -1, 0, 1, 2, 0,
                   -1, -2, 0, 1, 3 };
    int n6 = arr6.length;
    System.out.println("Maximum sum = " +
            maxSumBitonicSubArr(arr6, n6));
}
}

// This code is contributed by amreshkumar3
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum sum bitonic subarray

# Function to find the maximum sum bitonic
# subarray.
def maxSumBitonicSubArr(arr, n):

    # to store the maximum sum
    # bitonic subarray
    max_sum = -10**9

    i = 0
    while (i < n):

        # Find the longest increasing subarray
        # starting at i.
        j = i
        while (j + 1 < n and arr[j] < arr[j + 1]):
            j += 1

        # Now we know that a[i..j] is an
        # increasing subarray. Remove non-
        # positive elements from the left
        # side as much as possible.
        while (i < j and arr[i] <= 0):
            i += 1

        # Find the longest decreasing subarray
        # starting at j.
        k = j
        while (k + 1 < n and arr[k] > arr[k + 1]):
            k += 1

        # Now we know that a[j..k] is a
        # decreasing subarray. Remove non-
        # positive elements from the right
        # side as much as possible.
        # last is needed to keep the last
        # seen element.
        last = k
        while (k > j and arr[k] <= 0):
            k -= 1

        # Compute the max sum of the
        # increasing part.
        nn = arr[i:j + 1]
        sum_inc = sum(nn)

        # Compute the max sum of the
        # decreasing part.
        nn = arr[j:k + 1]
        sum_dec = sum(nn)

        # The overall max sum is the sum of
        # both parts minus the peak element,
        # because it was counted twice.
        sum_all = sum_inc + sum_dec - arr[j]

        max_sum = max([max_sum, sum_inc,
                       sum_dec, sum_all])

        # If the next element is equal to the
        # current, i.e. arr[i+1] == arr[i],
        # last == i.
        # To ensure the algorithm has progress,
        # get the max of last and i+1.
        i = max(last, i + 1)

    # required maximum sum
    return max_sum

# Driver Code

# The example from the article, the
# answer is 19.
arr = [5, 3, 9, 2, 7, 6, 4]
n = len(arr)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr, n))

# Always increasing, the answer is 15.
arr2 = [1, 2, 3, 4, 5]
n2 = len(arr2)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr2, n2))

# Always decreasing, the answer is 15.
arr3 = [5, 4, 3, 2, 1]
n3 = len(arr3)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr3, n3))

# All are equal, the answer is 5.
arr4 = [5, 5, 5, 5]
n4 = len(arr4)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr4, n4))

# The whole array is bitonic,
# but the answer is 7.
arr5 = [-1, 0, 1, 2, 3, 1, 0, -1, -10]
n5 = len(arr5)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr5, n5))

# The answer is 4 (the tail).
arr6 = [-1, 0, 1, 2, 0, -1, -2, 0, 1, 3]
n6 = len(arr6)
print("Maximum Sum = ",
       maxSumBitonicSubArr(arr6, n6))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation to find the
// maximum sum bitonic subarray
using System;

class GFG{

static int find_partial_sum(int []arr,
                            int start,
                            int end)
{
    int sum = 0;
    for(int i = start; i < end; i++)
        sum += arr[i];

    return sum;
}

// Function to find the maximum sum bitonic
// subarray.
static int maxSumBitonicSubArr(int []arr, int n)
{

    // To store the maximum sum
    // bitonic subarray
    int max_sum = -1000000;

    int i = 0;
    while (i < n)
    {

        // Find the longest increasing subarray
        // starting at i.
        int j = i;
        while (j + 1 < n && arr[j] < arr[j + 1])
            j++;

        // Now we know that a[i..j] is an
        // increasing subarray. Remove non-
        // positive elements from the left
        // side as much as possible.
        while (i < j && arr[i] <= 0)
            i++;

        // Find the longest decreasing subarray
        // starting at j.
        int k = j;
        while (k + 1 < n && arr[k] > arr[k + 1])
            k++;

        // Now we know that a[j..k] is a
        // decreasing subarray. Remove non-
        // positive elements from the right
        // side as much as possible.
        // last is needed to keep the last
        // seen element.
        int last = k;
        while (k > j && arr[k] <= 0)
            k--;

        // Compute the max sum of the
        // increasing part.
        int sum_inc = find_partial_sum(arr, i,
                                       j + 1);

        // Compute the max sum of the
        // decreasing part.
        int sum_dec = find_partial_sum(arr, j,
                                       k + 1);

        // The overall max sum is the sum of
        // both parts minus the peak element,
        // because it was counted twice.
        int sum_all = sum_inc + sum_dec - arr[j];

        max_sum = Math.Max(Math.Max(max_sum, sum_inc),
                           Math.Max(sum_dec, sum_all));

        // If the next element is equal to the
        // current, i.e. arr[i+1] == arr[i],
        // last == i.
        // To ensure the algorithm has progress,
        // get the max of last and i+1.
        i = Math.Max(last, i + 1);
    }

    // Required maximum sum
    return max_sum;
}

// Driver code
public static void Main()
{

    // The example from the article, the
    // answer is 19.
    int []arr = { 5, 3, 9, 2, 7, 6, 4 };
    int n = arr.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr, n));

    // Always increasing, the answer is 15.
    int []arr2 = { 1, 2, 3, 4, 5 };
    int n2 = arr2.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr2, n2));

    // Always decreasing, the answer is 15.
    int []arr3 = { 5, 4, 3, 2, 1 };
    int n3 = arr3.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr3, n3));

    // All are equal, the answer is 5.
    int []arr4 = { 5, 5, 5, 5 };
    int n4 = arr4.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr4, n4));

    // The whole array is bitonic,
    // but the answer is 7.
    int []arr5 = { -1, 0, 1, 2, 3,
                    1, 0, -1, -10 };
    int n5 = arr5.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr5, n5));

    // The answer is 4 (the tail).
    int []arr6 = { -1, 0, 1, 2, 0,
                   -1, -2, 0, 1, 3};
    int n6 = arr6.Length;
    Console.WriteLine("Maximum sum = " +
            maxSumBitonicSubArr(arr6, n6));
}
}

// This code is contributed by amreshkumar3
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// maximum sum bitonic subarray

    function find_partial_sum(arr,start,end)
    {
        let sum = 0;
    for(let i = start; i < end; i++)
        sum += arr[i];

    return sum;
    }

// Function to find the maximum sum bitonic
// subarray.
function maxSumBitonicSubArr(arr,n)
{
    // To store the maximum sum
    // bitonic subarray
    let max_sum = -1000000;

    let i = 0;
    while (i < n)
    {

        // Find the longest increasing
        // subarray starting at i.
        let j = i;
        while (j + 1 < n && arr[j] < arr[j + 1])
            j++;

        // Now we know that a[i..j] is an
        // increasing subarray. Remove non-
        // positive elements from the left
        // side as much as possible.
        while (i < j && arr[i] <= 0)
            i++;

        // Find the longest decreasing subarray
        // starting at j.
        let k = j;
        while (k + 1 < n && arr[k] > arr[k + 1])
            k++;

        // Now we know that a[j..k] is a
        // decreasing subarray. Remove non-
        // positive elements from the right
        // side as much as possible.
        // last is needed to keep the last
        // seen element.
        let last = k;
        while (k > j && arr[k] <= 0)
            k--;

        // Compute the max sum of the
        // increasing part.
        let sum_inc = find_partial_sum(arr, i,
                                       j + 1);

        // Compute the max sum of the
        // decreasing part.
        let sum_dec = find_partial_sum(arr, j,
                                       k + 1);

        // The overall max sum is the sum of
        // both parts minus the peak element,
        // because it was counted twice.
        let sum_all = sum_inc + sum_dec - arr[j];

        max_sum = Math.max(Math.max(max_sum, sum_inc),
                           Math.max(sum_dec, sum_all));

        // If the next element is equal to the
        // current, i.e. arr[i+1] == arr[i],
        // last == i.
        // To ensure the algorithm has progress,
        // get the max of last and i+1.
        i = Math.max(last, i + 1);
    }

    // Required maximum sum
    return max_sum;
}

// The example from the article, the
// answer is 19.
let arr = [ 5, 3, 9, 2, 7, 6, 4 ];
let n = arr.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr, n)+"<br>");

// Always increasing, the answer is 15.
let arr2 = [ 1, 2, 3, 4, 5 ];
let n2 = arr2.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr2, n2)+"<br>");

// Always decreasing, the answer is 15.
let arr3 = [ 5, 4, 3, 2, 1 ];
let n3 = arr3.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr3, n3)+"<br>");

// All are equal, the answer is 5.
let arr4 = [ 5, 5, 5, 5 ];
let n4 = arr4.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr4, n4)+"<br>");

// The whole array is bitonic,
// but the answer is 7.
let arr5 = [ -1, 0, 1, 2, 3,
              1, 0, -1, -10 ];
let n5 = arr5.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr5, n5)+"<br>");

// The answer is 4 (the tail).
let arr6 = [ -1, 0, 1, 2, 0,
              -1, -2, 0, 1, 3 ];
let n6 = arr6.length;
document.write("Maximum sum = " +
                   maxSumBitonicSubArr(arr6, n6)+"<br>");

// This code is contributed by patel2127
</script>
```

**输出:**

```
Maximum Sum = 19
Maximum Sum = 15
Maximum Sum = 15
Maximum Sum = 5
Maximum Sum = 7
Maximum Sum = 4
```

感谢 **Andrey Khayrutdinov** 提出这个解决方案。
本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。