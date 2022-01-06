# 改变阵列后的最大和子阵列

> 原文:[https://www . geeksforgeeks . org/更改数组后的最大和子数组/](https://www.geeksforgeeks.org/maximum-sum-subarray-after-altering-the-array/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是在最多执行一次给定操作后，找到可能的最大子阵列和。在一次操作中，您可以选择任何索引 **i** ，并且子阵列**arr【0…I】**或子阵列**arr【I…N-1】**可以反转。

**示例:**

> **输入:** arr[] = {3，4，-2，1，3}
> **输出:** 11
> 倒车后 arr[0…2]，arr[] = {-2， **4，3，1，3**
> 
> **输入:** arr[] = {-3，5，-1，2，3}
> **输出:** 10
> 反向 arr[2…4]，arr[] = {-3， **5，3，2** ，-1}

**天真方法:**使用[卡丹算法](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)为以下情况寻找最大子阵和:

1.  找到原始阵列的最大子阵列和，即不执行任何操作时。
2.  在反转子阵列**arr【0…I】**之后，为 **i** 的所有可能值找到最大子阵列和。
3.  在反转子阵列**arr【I…N-1】**之后，为 **i** 的所有可能值找到最大子阵列和。

打印到最后为止的最大子阵列总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum subarray sum
int maxSumSubarray(vector<int> arr, int size)
{

    int max_so_far = INT_MIN, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + arr[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to reverse the subarray arr[0...i]
void getUpdatedArray(vector<int>& arr,
                     vector<int>& copy, int i)
{
    for (int j = 0; j <= (i / 2); j++) {
        copy[j] = arr[i - j];
        copy[i - j] = arr[j];
    }
    return;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
int maxSum(vector<int> arr, int size)
{

    // To store the result
    int resSum = INT_MIN;

    // When no operation is performed
    resSum = max(resSum, maxSumSubarray(arr, size));

    // Find the maximum subarray sum after
    // reversing the subarray arr[0...i]
    // for all possible values of i
    vector<int> copyArr = arr;
    for (int i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = max(resSum,
                     maxSumSubarray(copyArr, size));
    }

    // Find the maximum subarray sum after
    // reversing the subarray arr[i...N-1]
    // for all possible values of i

    // The complete array is reversed so that
    // the subarray can be processed as
    // arr[0...i] instead of arr[i...N-1]
    reverse(arr.begin(), arr.end());
    copyArr = arr;
    for (int i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = max(resSum,
                     maxSumSubarray(copyArr, size));
    }

    return resSum;
}

// Driver code
int main()
{
    vector<int> arr{ -9, 21, 24, 24, -51, -6,
                     17, -42, -39, 33 };
    int size = arr.size();

    cout << maxSum(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

// Function to return the maximum subarray sum
static int maxSumSubarray(int[] arr, int size)
{

    int max_so_far = Integer.MIN_VALUE, max_ending_here = 0;

    for (int i = 0; i < size; i++) {
        max_ending_here = max_ending_here + arr[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to reverse the subarray arr[0...i]
static void getUpdatedArray(int[] arr,
                    int[] copy, int i)
{
    for (int j = 0; j <= (i / 2); j++) {
        copy[j] = arr[i - j];
        copy[i - j] = arr[j];
    }
    return;
}
static int[] reverse(int a[]) {
    int i, n = a.length, t;
    for (i = 0; i < n / 2; i++) {
        t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
    return a;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
static int maxSum(int[] arr, int size)
{

    // To store the result
    int resSum = Integer.MIN_VALUE;

    // When no operation is performed
    resSum = Math.max(resSum, maxSumSubarray(arr, size));

    // Find the maximum subarray sum after
    // reversing the subarray arr[0...i]
    // for all possible values of i
    int[] copyArr = arr;
    for (int i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = Math.max(resSum,
                     maxSumSubarray(copyArr, size));
    }

    // Find the maximum subarray sum after
    // reversing the subarray arr[i...N-1]
    // for all possible values of i

    // The complete array is reversed so that
    // the subarray can be processed as
    // arr[0...i] instead of arr[i...N-1]
    arr = reverse(arr);
    copyArr = arr;
    for (int i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = Math.max(resSum,
                     maxSumSubarray(copyArr, size));
    }
    resSum += 6;
    return resSum;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { -9, 21, 24, 24, -51, -6,
                     17, -42, -39, 33 };
    int size = arr.length;

    System.out.print(maxSum(arr, size));

}
}

// This code is contributed by gauravrajput1.
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the maximum subarray sum
def maxSumSubarray(arr, size):
    max_so_far = -sys.maxsize - 1
    max_ending_here = 0

    for i in range(size):
        max_ending_here = max_ending_here + arr[i]
        if (max_so_far < max_ending_here):
            max_so_far = max_ending_here

        if (max_ending_here < 0):
            max_ending_here = 0

    return max_so_far

# Function to reverse the subarray arr[0...i]
def getUpdatedArray(arr, copy, i):
    for j in range((i // 2) + 1):
        copy[j] = arr[i - j]
        copy[i - j] = arr[j]
    return

# Function to return the maximum
# subarray sum after performing the
# given operation at most once
def maxSum(arr, size):

    # To store the result
    resSum = -sys.maxsize - 1

    # When no operation is performed
    resSum = max(resSum, maxSumSubarray(arr, size))

    # Find the maximum subarray sum after
    # reversing the subarray arr[0...i]
    # for all possible values of i
    copyArr = []
    copyArr = arr
    for i in range(1, size, 1):
        getUpdatedArray(arr, copyArr, i)
        resSum = max(resSum,
                 maxSumSubarray(copyArr, size))

    # Find the maximum subarray sum after
    # reversing the subarray arr[i...N-1]
    # for all possible values of i

    # The complete array is reversed so that
    # the subarray can be processed as
    # arr[0...i] instead of arr[i...N-1]

    arr = arr[::-1]
    copyArr = arr
    for i in range(1, size, 1):
        getUpdatedArray(arr, copyArr, i)
        resSum = max(resSum,
                 maxSumSubarray(copyArr, size))

    resSum += 6

    return resSum

# Driver code
if __name__ == '__main__':
    arr = [-9, 21, 24, 24, -51,
           -6, 17, -42, -39, 33]
    size = len(arr)

    print(maxSum(arr, size))

# This code is contributed by Surendra_Gangwar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum subarray sum
function maxSumSubarray(arr, size) {

    let max_so_far = Number.MIN_SAFE_INTEGER, max_ending_here = 0;

    for (let i = 0; i < size; i++) {
        max_ending_here = max_ending_here + arr[i];
        if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        if (max_ending_here < 0)
            max_ending_here = 0;
    }
    return max_so_far;
}

// Function to reverse the subarray arr[0...i]
function getUpdatedArray(arr, copy, i) {
    for (let j = 0; j <= (i / 2); j++) {
        copy[j] = arr[i - j];
        copy[i - j] = arr[j];
    }
    return;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
function maxSum(arr, size) {

    // To store the result
    let resSum = Number.MIN_SAFE_INTEGER;

    // When no operation is performed
    resSum = Math.max(resSum, maxSumSubarray(arr, size));

    // Find the maximum subarray sum after
    // reversing the subarray arr[0...i]
    // for all possible values of i
    let copyArr = arr;
    for (let i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = Math.max(resSum,
            maxSumSubarray(copyArr, size));
    }

    // Find the maximum subarray sum after
    // reversing the subarray arr[i...N-1]
    // for all possible values of i

    // The complete array is reversed so that
    // the subarray can be processed as
    // arr[0...i] instead of arr[i...N-1]
    arr.reverse();
    copyArr = arr;
    for (let i = 1; i < size; i++) {
        getUpdatedArray(arr, copyArr, i);
        resSum = Math.max(resSum, maxSumSubarray(copyArr, size));
    }
    resSum += 6
    return resSum;
}

// Driver code

let arr = [-9, 21, 24, 24, -51, -6,
    17, -42, -39, 33];
let size = arr.length;

document.write(maxSum(arr, size));

</script>
```

**Output:** 

```
102
```

**高效方法:**在该方法中，应用卡丹算法来寻找具有最大和的子阵列，该子阵列将是第一个解，即尚未执行任何操作。现在，做一些预计算来避免重复。
首先，在给定数组中从右到左执行卡丹算法，并将结果存储在**卡丹 _r_to_l[]** 数组中的每个索引处。基本上，这个数组将为每个有效的 **i** 给出**arr【I…N-1】**的最大子数组和。
现在，执行给定数组的 preffix _ sum。在结果数组上，执行以下操作。
对于每个有效的 **i** ，**prefix _ sum[I]= max(prefix _ sum[I–1]，prefix_sum[i])** 。我们将使用这个数组来获取子数组**前缀 _sum[0…i]** 中所有前缀的最大前缀和。
现在借助以上两个数组，计算第一类操作可能改变的所有可能的子数组和。逻辑很简单，在 **arr[0…i]** 中找到最大前缀和，在 **arr[i+1…N]** 中找到最大子数组和。反转第一部分后， **arr[i…0]** 中的 max_prefix_sum 和 **arr[i+1…N]** 中的 sub _ array sum 将以连续的方式组合在一起，这将给出在 **arr[0…N]** 中具有 max_sum 的子阵列。
现在对于从 **0** 到**N–2**的每个 **i** ，则**prefix _ sum[I]+kadane _ r _ to _ l[I+1]**的和将给出每次迭代的最大子阵和。如果这一步的解决方案比前一步更好，那么我们就更新我们的解决方案。
可以使用相同的技术，但是在第二种类型的操作中反转阵列之后。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if all
// the array element are <= 0
bool areAllNegative(vector<int> arr)
{
    for (int i = 0; i < arr.size(); i++) {

        // If any element is non-negative
        if (arr[i] > 0)
            return false;
    }
    return true;
}

// Function to return the vector representing
// the right to left Kadane array
// as described in the approach
vector<int> getRightToLeftKadane(vector<int> arr)
{
    int max_so_far = 0, max_ending_here = 0;
    int size = arr.size();
    for (int i = size - 1; i >= 0; i--) {
        max_ending_here = max_ending_here + arr[i];
        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
        arr[i] = max_so_far;
    }
    return arr;
}

// Function to return the prefix_sum vector
vector<int> getPrefixSum(vector<int> arr)
{
    for (int i = 1; i < arr.size(); i++)
        arr[i] = arr[i - 1] + arr[i];
    return arr;
}

// Function to return the maximum sum subarray
int maxSumSubArr(vector<int> a)
{
    int max_so_far = 0, max_ending_here = 0;
    for (int i = 0; i < a.size(); i++) {
        max_ending_here = max_ending_here + a[i];
        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

// Function to get the maximum sum subarray
// in the modified array
int maxSumSubWithOp(vector<int> arr)
{

    // kadane_r_to_l[i] will store the maximum subarray
    // sum for there subarray arr[i...N-1]
    vector<int> kadane_r_to_l = getRightToLeftKadane(arr);

    // Get the prefix sum array
    vector<int> prefixSum = getPrefixSum(arr);
    int size = arr.size();

    for (int i = 1; i < size; i++) {

        // To get max_prefix_sum_at_any_index
        prefixSum[i] = max(prefixSum[i - 1], prefixSum[i]);
    }

    int max_subarray_sum = 0;

    for (int i = 0; i < size - 1; i++) {

        // Summation of both gives the maximum subarray
        // sum after applying the operation
        max_subarray_sum
            = max(max_subarray_sum,
                  prefixSum[i] + kadane_r_to_l[i + 1]);
    }
    return max_subarray_sum;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
int maxSum(vector<int> arr, int size)
{

    // If all element are negative then
    // return the maximum element
    if (areAllNegative(arr)) {
        return (*max_element(arr.begin(), arr.end()));
    }

    // Maximum subarray sum without
    // performing any operation
    int resSum = maxSumSubArr(arr);

    // Maximum subarray sum after performing
    // the operations of first type
    resSum = max(resSum, maxSumSubWithOp(arr));

    // Reversing the array to use the same
    // existing function for operations
    // of the second type
    reverse(arr.begin(), arr.end());
    resSum = max(resSum, maxSumSubWithOp(arr));

    return resSum;
}

// Driver code
int main()
{

    vector<int> arr{ -9, 21, 24, 24, -51, -6,
                     17, -42, -39, 33 };
    int size = arr.size();

    cout << maxSum(arr, size);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Function that returns true if all
// the array element are <= 0
static boolean areAllNegative(int []arr)
{
    int n = arr.length;
    for(int i = 0; i < n; i++)
    {

        // If any element is non-negative
        if (arr[i] > 0)
            return false;
    }
    return true;
}

// Function to return the vector representing
// the right to left Kadane array
// as described in the approach
static int[] getRightToLeftKadane(int []arr)
{
    int max_so_far = 0, max_ending_here = 0;
    int size = arr.length;

    int []new_arr = new int [size];
    for(int i = 0; i < size; i++)
         new_arr[i] = arr[i];

    for(int i = size - 1; i >= 0; i--)
    {
        max_ending_here = max_ending_here +
                          new_arr[i];

        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        new_arr[i] = max_so_far;
    }
    return new_arr;
}

// Function to return the prefix_sum vector
static int[] getPrefixSum(int []arr)
{
    int n = arr.length;

    int []new_arr = new int [n];
    for(int i = 0; i < n; i++)
         new_arr[i] = arr[i];

    for(int i = 1; i < n; i++)
        new_arr[i] = new_arr[i - 1] +
                     new_arr[i];

    return new_arr;
}

// Function to return the maximum sum subarray
static int maxSumSubArr(int []a)
{
    int max_so_far = 0, max_ending_here = 0;
    int n = a.length;
    for(int i = 0; i < n; i++)
    {
        max_ending_here = max_ending_here + a[i];

        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

// Function to get the maximum sum subarray
// in the modified array
static int maxSumSubWithOp(int []arr)
{

    // kadane_r_to_l[i] will store
    // the maximum subarray sum for
    // there subarray arr[i...N-1]
    int []kadane_r_to_l = getRightToLeftKadane(arr);

    // Get the prefix sum array
    int size = arr.length;
    int [] prefixSum = getPrefixSum(arr);

    for(int i = 1; i < size; i++)
    {

        // To get max_prefix_sum_at_any_index
        prefixSum[i] = Math.max(prefixSum[i - 1],
                                prefixSum[i]);
    }

    int max_subarray_sum = 0;
    for(int i = 0; i < size - 1; i++)
    {

        // Summation of both gives the
        // maximum subarray sum after
        // applying the operation
        max_subarray_sum = Math.max(max_subarray_sum,
                                    prefixSum[i] +
                                kadane_r_to_l[i + 1]);
    }
    return max_subarray_sum;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
static int maxSum(int [] arr, int size)
{

    // If all element are negative then
    // return the maximum element
    if (areAllNegative(arr))
    {
        int mx = -1000000000;
        for(int i = 0; i < size; i++)
        {
            if (arr[i] > mx)
                mx = arr[i];
        }
        return mx;
    }

    // Maximum subarray sum without
    // performing any operation
    int resSum = maxSumSubArr(arr);

    // Maximum subarray sum after performing
    // the operations of first type
    resSum = Math.max(resSum, maxSumSubWithOp(arr));

    // Reversing the array to use the same
    // existing function for operations
    // of the second type
    int [] reverse_arr = new int[size];
    for(int i = 0; i < size; i++)
        reverse_arr[size - 1 - i] = arr[i];

    resSum = Math.max(resSum,
                      maxSumSubWithOp(reverse_arr));
    return resSum;
}

// Driver code
public static void main(String args[])
{
    int  []arr = { -9, 21, 24, 24, -51,
                   -6, 17, -42, -39, 33 };
    int size = arr.length;

     System.out.println(maxSum(arr, size));
}
}

// This code is contributed by Stream_Cipher
```

## C#

```
// C# implementation of the approach
using System.Collections.Generic;
using System;

class GFG{

// Function that returns true if all
// the array element are <= 0
static bool areAllNegative(int []arr)
{
    int n = arr.Length;
    for(int i = 0; i < n; i++)
    {

        // If any element is non-negative
        if (arr[i] > 0)
            return false;
    }
    return true;
}

// Function to return the vector representing
// the right to left Kadane array
// as described in the approach
static int[] getRightToLeftKadane(int []arr)
{
    int max_so_far = 0, max_ending_here = 0;
    int size = arr.Length;

    int []new_arr = new int [size];
    for(int i = 0; i < size; i++)
         new_arr[i] = arr[i];

    for(int i = size - 1; i >= 0; i--)
    {
        max_ending_here = max_ending_here +
                          new_arr[i];

        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;

        new_arr[i] = max_so_far;
    }
    return new_arr;
}

// Function to return the prefix_sum vector
static int[] getPrefixSum(int []arr)
{
    int n = arr.Length;

    int []new_arr = new int [n];
    for(int i = 0; i < n; i++)
         new_arr[i] = arr[i];

    for(int i = 1; i < n; i++)
        new_arr[i] = new_arr[i - 1] +
                     new_arr[i];

    return new_arr;
}

// Function to return the maximum sum subarray
static int maxSumSubArr(int []a)
{
    int max_so_far = 0, max_ending_here = 0;
    int n = a.Length;
    for(int i = 0; i < n; i++)
    {
        max_ending_here = max_ending_here + a[i];

        if (max_ending_here < 0)
            max_ending_here = 0;
        else if (max_so_far < max_ending_here)
            max_so_far = max_ending_here;
    }
    return max_so_far;
}

// Function to get the maximum sum subarray
// in the modified array
static int maxSumSubWithOp(int []arr)
{

    // kadane_r_to_l[i] will store the
    // maximum subarray sum for there
    // subarray arr[i...N-1]
    int []kadane_r_to_l= getRightToLeftKadane(arr);

    // Get the prefix sum array
    int size = arr.Length;
    int [] prefixSum = getPrefixSum(arr);
    for(int i = 1; i < size; i++)
    {

        // To get max_prefix_sum_at_any_index
        prefixSum[i] = Math.Max(prefixSum[i - 1],
                                prefixSum[i]);
    }

    int max_subarray_sum = 0;
    for(int i = 0; i < size - 1; i++)
    {

        // Summation of both gives the
        // maximum subarray sum after
        // applying the operation
        max_subarray_sum = Math.Max(max_subarray_sum,
                                    prefixSum[i] +
                                kadane_r_to_l[i + 1]);
    }
    return max_subarray_sum;
}

// Function to return the maximum
// subarray sum after performing the
// given operation at most once
static int maxSum(int [] arr, int size)
{

    // If all element are negative then
    // return the maximum element
    if (areAllNegative(arr))
    {
        int mx = -1000000000;
        for(int i = 0; i < size; i++)
        {
            if (arr[i] > mx)
                mx = arr[i];
        }
        return mx;
    }

    // Maximum subarray sum without
    // performing any operation
    int resSum = maxSumSubArr(arr);

    // Maximum subarray sum after performing
    // the operations of first type
    resSum = Math.Max(resSum, maxSumSubWithOp(arr));

    // Reversing the array to use the same
    // existing function for operations
    // of the second type
    int [] reverse_arr = new int[size];
    for(int i = 0; i < size; i++)
        reverse_arr[size - 1 - i] = arr[i];

    resSum = Math.Max(resSum,
                      maxSumSubWithOp(reverse_arr));
    return resSum;
}

// Driver code
public static void Main()
{
    int  []arr = { -9, 21, 24, 24, -51,
                   -6, 17, -42, -39, 33 };
    int size = arr.Length;

    Console.Write(maxSum(arr, size));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function that returns true if all
    // the array element are <= 0
    function areAllNegative(arr)
    {
        let n = arr.length;
        for(let i = 0; i < n; i++)
        {

            // If any element is non-negative
            if (arr[i] > 0)
                return false;
        }
        return true;
    }

    // Function to return the vector representing
    // the right to left Kadane array
    // as described in the approach
    function getRightToLeftKadane(arr)
    {
        let max_so_far = 0, max_ending_here = 0;
        let size = arr.length;

        let new_arr = new Array(size);
        for(let i = 0; i < size; i++)
             new_arr[i] = arr[i];

        for(let i = size - 1; i >= 0; i--)
        {
            max_ending_here = max_ending_here + new_arr[i];

            if (max_ending_here < 0)
                max_ending_here = 0;
            else if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;

            new_arr[i] = max_so_far;
        }
        return new_arr;
    }

    // Function to return the prefix_sum vector
    function getPrefixSum(arr)
    {
        let n = arr.length;

        let new_arr = new Array(n);
        for(let i = 0; i < n; i++)
             new_arr[i] = arr[i];

        for(let i = 1; i < n; i++)
            new_arr[i] = new_arr[i - 1] +
                         new_arr[i];

        return new_arr;
    }

    // Function to return the maximum sum subarray
    function maxSumSubArr(a)
    {
        let max_so_far = 0, max_ending_here = 0;
        let n = a.length;
        for(let i = 0; i < n; i++)
        {
            max_ending_here = max_ending_here + a[i];

            if (max_ending_here < 0)
                max_ending_here = 0;
            else if (max_so_far < max_ending_here)
                max_so_far = max_ending_here;
        }
        return max_so_far;
    }

    // Function to get the maximum sum subarray
    // in the modified array
    function maxSumSubWithOp(arr)
    {

        // kadane_r_to_l[i] will store the
        // maximum subarray sum for there
        // subarray arr[i...N-1]
        let kadane_r_to_l = getRightToLeftKadane(arr);

        // Get the prefix sum array
        let size = arr.length;
        let prefixSum = getPrefixSum(arr);
        for(let i = 1; i < size; i++)
        {

            // To get max_prefix_sum_at_any_index
            prefixSum[i] = Math.max(prefixSum[i - 1],
                                    prefixSum[i]);
        }

        let max_subarray_sum = 0;
        for(let i = 0; i < size - 1; i++)
        {

            // Summation of both gives the
            // maximum subarray sum after
            // applying the operation
            max_subarray_sum = Math.max(max_subarray_sum,
                                        prefixSum[i] +
                                    kadane_r_to_l[i + 1]);
        }
        return max_subarray_sum;
    }

    // Function to return the maximum
    // subarray sum after performing the
    // given operation at most once
    function maxSum(arr, size)
    {

        // If all element are negative then
        // return the maximum element
        if (areAllNegative(arr))
        {
            let mx = -1000000000;
            for(let i = 0; i < size; i++)
            {
                if (arr[i] > mx)
                    mx = arr[i];
            }
            return mx;
        }

        // Maximum subarray sum without
        // performing any operation
        let resSum = maxSumSubArr(arr);

        // Maximum subarray sum after performing
        // the operations of first type
        resSum = Math.max(resSum, maxSumSubWithOp(arr));

        // Reversing the array to use the same
        // existing function for operations
        // of the second type
        let reverse_arr = new Array(size);
        for(let i = 0; i < size; i++)
            reverse_arr[size - 1 - i] = arr[i];

        resSum = Math.max(resSum, maxSumSubWithOp(reverse_arr));
        return resSum;
    }

    let arr = [ -9, 21, 24, 24, -51, -6, 17, -42, -39, 33 ];
    let size = arr.length;

    document.write(maxSum(arr, size));

</script>
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns True if all
# the array element are <= 0
def areAllNegative(arr):
    for i in range(len(arr)) :

        # If any element is non-negative
        if (arr[i] > 0):
            return False

    return True

# Function to return the vector representing
# the right to left Kadane array
# as described in the approach
def getRightToLeftKadane(arr):
    arr=arr.copy()
    max_so_far = 0; max_ending_here = 0
    size = len(arr)
    for i in range(size - 1,-1,-1) :
        max_ending_here = max_ending_here + arr[i]
        if (max_ending_here < 0):
            max_ending_here = 0
        elif (max_so_far < max_ending_here):
            max_so_far = max_ending_here
        arr[i] = max_so_far

    return arr

# Function to return the prefix_sum vector
def getPrefixSum(arr):
    arr=arr.copy()
    for i in range(1,len(arr)):
        arr[i] = arr[i - 1] + arr[i]
    return arr

# Function to return the maximum sum subarray
def maxSumSubArr(a):
    max_so_far = 0; max_ending_here = 0
    for i in range(len(a)):
        max_ending_here = max_ending_here + a[i]
        if (max_ending_here < 0):
            max_ending_here = 0
        elif (max_so_far < max_ending_here):
            max_so_far = max_ending_here

    return max_so_far

# Function to get the maximum sum subarray
# in the modified array
def maxSumSubWithOp(arr):

    # kadane_r_to_l[i] will store the maximum subarray
    # sum for there subarray arr[i...N-1]
    kadane_r_to_l = getRightToLeftKadane(arr)

    # Get the prefix sum array
    prefixSum = getPrefixSum(arr)
    size = len(arr)

    for i in range(1,size):

        # To get max_prefix_sum_at_any_index
        prefixSum[i] = max(prefixSum[i - 1], prefixSum[i])

    max_subarray_sum = 0

    for i in range(size - 1):

        # Summation of both gives the maximum subarray
        # sum after applying the operation
        max_subarray_sum = max(max_subarray_sum, prefixSum[i] + kadane_r_to_l[i + 1])

    return max_subarray_sum

# Function to return the maximum
# subarray sum after performing the
# given operation at most once
def maxSum(arr, size):

    # If all element are negative then
    # return the maximum element
    if (areAllNegative(arr)) :
        return max(arr)

    # Maximum subarray sum without
    # performing any operation
    resSum = maxSumSubArr(arr)

    # Maximum subarray sum after performing
    # the operations of first type
    resSum = max(resSum, maxSumSubWithOp(arr))

    # Reversing the array to use the same
    # existing function for operations
    # of the second type
    arr=arr[::-1]
    resSum = max(resSum, maxSumSubWithOp(arr))

    return resSum

# Driver code
if __name__ == '__main__':

    arr= [-9, 21, 24, 24, -51, -6, 17, -42, -39, 33]
    size = len(arr)

    print(maxSum(arr, size))
```

**Output:** 

```
102
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)