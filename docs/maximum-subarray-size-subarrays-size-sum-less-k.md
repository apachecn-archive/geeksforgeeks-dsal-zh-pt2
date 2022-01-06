# 最大子阵列大小，使得该大小的所有子阵列的总和小于 k

> 原文:[https://www . geesforgeks . org/maximum-subarray-size-subarray-size-sum-less-k/](https://www.geeksforgeeks.org/maximum-subarray-size-subarrays-size-sum-less-k/)

给定一个由 **n** 个正整数和一个正整数 **k** 组成的数组，任务是找到最大子阵列大小，使得该大小的所有子阵列的元素之和小于或等于 k

**例:**

```
Input :  arr[] = {1, 2, 3, 4} and k = 8.
Output : 2
Sum of subarrays of size 1: 1, 2, 3, 4.
Sum of subarrays of size 2: 3, 5, 7.
Sum of subarrays of size 3: 6, 9.
Sum of subarrays of size 4: 10.
So, maximum subarray size such that all subarrays of that size have the sum of elements less than 8 is 2.

Input :  arr[] = {1, 2, 10, 4} and k = 8.
Output : -1
There is an array element with value greater than k, so subarray sum cannot be less than k.

Input :  arr[] = {1, 2, 10, 4} and K = 14
Output : 2
```

**简单方法:**首先，所需的子阵列尺寸必须介于 **1 到 n** 之间。现在，由于所有数组元素都是正整数，我们可以说任何子数组的前缀和都应该严格递增。因此，我们可以说

```
if arr[i] + arr[i + 1] + ..... + arr[j - 1] + arr[j] <= K
then arr[i] + arr[i + 1] + ..... + arr[j - 1] <= K, as arr[j] is a positive integer.
```

*   Execute [method of bisection](https://www.geeksforgeeks.org/binary-search/) in the range of 1 to n, and find the highest subarray size, so that all subarrays of this size have the sum of elements less than or equal to k.

下面是上述方法的实现:

## C++

```
// C++ program to find maximum
// subarray size, such that all
// subarrays of that size have
// sum less than K.
#include<bits/stdc++.h>
using namespace std;

// Search for the maximum length of
// required subarray.
int bsearch(int prefixsum[], int n,
                             int k)
{
    // Initialize result
    int ans = -1;

    // Do Binary Search for largest
    // subarray size
    int left = 1, right = n;
    while (left <= right)
    {
        int mid = (left + right) / 2;

        // Check for all subarrays after mid
        int i;
        for (i = mid; i <= n; i++)
        {
            // Checking if all the subarrays
            //  of a size less than k.
            if (prefixsum[i] - prefixsum[i - mid] > k)
                break;
        }

        // All subarrays of size mid have
        // sum less than or equal to k
        if (i == n + 1)
        {
            left = mid + 1;
            ans = mid;
        }

        // We found a subarray of size mid
        // with sum greater than k
        else
            right = mid - 1;
    }
    return ans;
}

// Return the maximum subarray size,
// such that all subarray of that size
// have sum less than K.
int maxSize(int arr[], int n, int k)
{
    // Initialize prefix sum array as 0.
    int prefixsum[n + 1];
    memset(prefixsum, 0, sizeof(prefixsum));

    // Finding prefix sum of the array.
    for (int i = 0; i < n; i++)
        prefixsum[i + 1] = prefixsum[i] +
                           arr[i];

    return bsearch(prefixsum, n, k);
}

// Driver code
int main()
{
    int arr[] = {1, 2, 10, 4};
    int n = sizeof(arr) / sizeof(arr[0]);
    int k = 14;
    cout << maxSize(arr, n, k) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum
// subarray size, such that all
// subarrays of that size have
// sum less than K.
import java.util.Arrays;

class GFG
{

    // Search for the maximum length
    // of required subarray.
    static int bsearch(int prefixsum[],
                       int n, int k)
    {
        // Initialize result
        int ans = -1;

        // Do Binary Search for largest
        // subarray size
        int left = 1, right = n;

        while (left <= right)
        {
            int mid = (left + right) / 2;

            // Check for all subarrays after mid
            int i;
            for (i = mid; i <= n; i++)
            {

                // Checking if all the subarrays
                // of a size is less than k.
                if (prefixsum[i] - prefixsum[i - mid] > k)
                    break;
            }

            // All subarrays of size mid have
            // sum less than or equal to k
            if (i == n + 1)
            {
                left = mid + 1;
                ans = mid;
            }

            // We found a subarray of size mid
            // with sum greater than k
            else
                right = mid - 1;
        }

        return ans;
    }

    // Return the maximum subarray size, such
    // that all subarray of that size have
    // sum less than K.
    static int maxSize(int arr[], int n, int k)
    {

        // Initialize prefix sum array as 0.
        int prefixsum[] = new int[n + 1];
        Arrays.fill(prefixsum, 0);

        // Finding prefix sum of the array.
        for (int i = 0; i < n; i++)
            prefixsum[i + 1] = prefixsum[i] + arr[i];

        return bsearch(prefixsum, n, k);
    }

    // Driver code
    public static void main(String arg[])
    {
        int arr[] = { 1, 2, 10, 4 };
        int n = arr.length;
        int k = 14;
        System.out.println(maxSize(arr, n, k));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python3 program to find maximum
# subarray size, such that all
# subarrays of that size have
# sum less than K.

# Search for the maximum length of
# required subarray.
def bsearch(prefixsum, n, k):

    # Initialize result
    # Do Binary Search for largest
    # subarray size
    ans, left, right = -1, 1, n

    while (left <= right):

        # Check for all subarrays after mid
        mid = (left + right)//2

        for i in range(mid, n + 1):

            # Checking if all the subarray of
            # a size is less than k.
            if (prefixsum[i] - prefixsum[i - mid] > k):
                i = i - 1
                break
        i = i + 1
        if (i == n + 1):
            left = mid + 1
            ans = mid
        # We found a subarray of size mid with sum
        # greater than k
        else:
            right = mid - 1

    return ans;

# Return the maximum subarray size, such
# that all subarray of that size have
# sum less than K.
def maxSize(arr, n, k):
    prefixsum = [0 for x in range(n + 1)]

    # Finding prefix sum of the array.
    for i in range(n):
        prefixsum[i + 1] = prefixsum[i] + arr[i]

    return bsearch(prefixsum, n, k);

# Driver Code
arr = [ 1, 2, 10, 4 ]
n = len(arr)
k = 14
print (maxSize(arr, n, k))

# This code is contributed by Afzal
```

## C#

```
// C# program to find maximum
// subarray size, such that all
// subarrays of that size have
// sum less than K.
using System;

class GFG {

    // Search for the maximum length
    // of required subarray.
    static int bsearch(int []prefixsum,
                          int n, int k)
    {

        // Initialize result
        int ans = -1;

        // Do Binary Search for
        // largest subarray size
        int left = 1, right = n;

        while (left <= right)
        {
            int mid = (left + right) / 2;

            // Check for all subarrays
            // after mid
            int i;
            for (i = mid; i <= n; i++)
            {

                // Checking if all the
                // subarrays of a size is
                // less than k.
                if (prefixsum[i] -
                     prefixsum[i - mid] > k)
                    break;
            }

            // All subarrays of size mid have
            // sum less than or equal to k
            if (i == n + 1)
            {
                left = mid + 1;
                ans = mid;
            }

            // We found a subarray of size mid
            // with sum greater than k
            else
                right = mid - 1;
        }

        return ans;
    }

    // Return the maximum subarray size, such
    // that all subarray of that size have
    // sum less than K.
    static int maxSize(int []arr, int n, int k)
    {

        // Initialize prefix sum array as 0.
        int []prefixsum = new int[n + 1];
        for(int i=0;i<n+1;i++)
        prefixsum[i]=0;

        // Finding prefix sum of the array.
        for (int i = 0; i < n; i++)
            prefixsum[i + 1] = prefixsum[i]
                                     + arr[i];

        return bsearch(prefixsum, n, k);
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 1, 2, 10, 4 };
        int n = arr.Length;
        int k = 14;

        Console.Write(maxSize(arr, n, k));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum subarray
// size, such that all subarrays of that
// size have sum less than K.

// Search for the maximum length of
// required subarray.
function bsearch(&$prefixsum, $n, $k)
{
    // Initialize result
    $ans = -1;

    // Do Binary Search for largest
    // subarray size
    $left = 1;
    $right = $n;
    while ($left <= $right)
    {
        $mid = intval(($left + $right) / 2);

        // Check for all subarrays after mid
        for ($i = $mid; $i <= $n; $i++)
        {
            // Checking if all the subarrays
            // of a size less than k.
            if ($prefixsum[$i] - $prefixsum[$i -
                                 $mid] > $k)
                break;
        }

        // All subarrays of size mid have
        // sum less than or equal to k
        if ($i == $n + 1)
        {
            $left = $mid + 1;
            $ans = $mid;
        }

        // We found a subarray of size mid
        // with sum greater than k
        else
            $right = $mid - 1;
    }
    return $ans;
}

// Return the maximum subarray size,
// such that all subarray of that size
// have sum less than K.
function maxSize(&$arr, $n, $k)
{
    // Initialize prefix sum array as 0.
    $prefixsum = array_fill(0, $n + 1, NULL);

    // Finding prefix sum of the array.
    for ($i = 0; $i < $n; $i++)
        $prefixsum[$i + 1] = $prefixsum[$i] +
                             $arr[$i];

    return bsearch($prefixsum, $n, $k);
}

// Driver code
$arr = array(1, 2, 10, 4);
$n = sizeof($arr);
$k = 14;
echo maxSize($arr, $n, $k) . "\n";

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// javascript program to find maximum
// subarray size, such that all
// subarrays of that size have
// sum less than K.

    // Search for the maximum length
    // of required subarray.
    function bsearch(prefixsum , n , k)
    {
        // Initialize result
        var ans = -1;

        // Do Binary Search for largest
        // subarray size
        var left = 1, right = n;

        while (left <= right) {
            var mid = parseInt((left + right) / 2);

            // Check for all subarrays after mid
            var i;
            for (i = mid; i <= n; i++) {

                // Checking if all the subarrays
                // of a size is less than k.
                if (prefixsum[i] - prefixsum[i - mid] > k)
                    break;
            }

            // All subarrays of size mid have
            // sum less than or equal to k
            if (i == n + 1) {
                left = mid + 1;
                ans = mid;
            }

            // We found a subarray of size mid
            // with sum greater than k
            else
                right = mid - 1;
        }

        return ans;
    }

    // Return the maximum subarray size, such
    // that all subarray of that size have
    // sum less than K.
    function maxSize(arr , n , k) {

        // Initialize prefix sum array as 0.
        var prefixsum = Array(n + 1).fill(0);

        // Finding prefix sum of the array.
        for (i = 0; i < n; i++)
            prefixsum[i + 1] = prefixsum[i] + arr[i];

        return bsearch(prefixsum, n, k);
    }

    // Driver code
        var arr = [ 1, 2, 10, 4 ];
        var n = arr.length;
        var k = 14;
        document.write(maxSize(arr, n, k));

// This code contributed by Rajput-Ji

</script>
```

**Output**

```
2
```

***时间复杂度:** O(n log n)*

**高效方法:**该方法使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决给定的问题。

*   The method is to find **the minimum subarray size** whose sum is greater than the integer K ..
*   Increase the window size from the end where the sum of the window is greater than k.
*   Now, if the sub-array size is smaller than the already stored sub-array size (in the variable ans), the sub-array size is stored.
*   Now, decrease the subarray size from the beginning. The variable ans will store the minimum subarray size with sum greater than K ..
*   Finally, **(ans-1)** is the actual answer. Then, the subarray size -1 is the maximum subarray size, so that the sum of all subarrays of this size will be less than or equal to k.

下面是上述方法的实现:

## c++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the
// largest size subarray
void func(vector<int> arr,
          int k, int n)
{
    // Variable declaration
    int ans = n;
    int sum = 0;
    int start = 0;

    // Loop till N
    for (int end = 0; end < n; end++)
    {
        // Sliding window from left
        sum += arr[end];

        while (sum > k) {
            // Sliding window from right
            sum -= arr[start];
            start++;

            // Storing sub-array size - 1
            // for which sum was greater than k
            ans = min(ans, end - start + 1);

            // Sum will be 0 if start>end
            // because all elements are positive
            // start>end only when arr[end]>k i.e,
            // there is an array element with
            // value greater than k, so sub-array
            // sum cannot be less than k.
            if (sum == 0)
                break;
        }
        if (sum == 0) {
            ans = -1;
            break;
        }
    }

    // Print the answer
    cout << ans;
}

// Driver code
int main()
{
    vector<int> arr{ 1, 2, 3, 4 };
    int k = 8;
    int n = arr.size();

    // Function call
    func(arr, k, n);

    return 0;
}
```

## Java

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to find the
// largest size subarray
public static void func(int arr[],
                        int k, int n)
{

    // Variable declaration
    int ans = n;
    int sum = 0;
    int start = 0;

    // Loop till N
    for(int end = 0; end < n; end++)
    {

        // Sliding window from left
        sum += (int)arr[end];

        while (sum > k)
        {

            // Sliding window from right
            sum -= (int)arr[start];
            start++;

            // Storing sub-array size - 1
            // for which sum was greater than k
            ans = Math.min(ans, end - start + 1);

            // Sum will be 0 if start>end
            // because all elements are positive
            // start>end only when arr[end]>k i.e,
            // there is an array element with
            // value greater than k, so sub-array
            // sum cannot be less than k.
            if (sum == 0)
                break;
        }

        if (sum == 0)
        {
            ans = -1;
            break;
        }
    }

    // Print the answer
    System.out.println(ans);
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 3, 4 };
    int k = 8;
    int n = arr.length;

    // Function call
    func(arr, k, n);
}
}

// This code is contributed by rag2127
```

## python 3

```
# Python3 program for the above approach

# Function to find the
# largest size subarray
def func(arr, k, n):

    # Variable declaration
    ans = n
    Sum = 0
    start = 0

    # Loop till N
    for end in range(n):

        # Sliding window from left
        Sum += arr[end]

        while (Sum > k):

            # Sliding window from right
            Sum -= arr[start]
            start += 1

            # Storing sub-array size - 1
            # for which sum was greater than k
            ans = min(ans, end - start + 1)

            # Sum will be 0 if start>end
            # because all elements are positive
            # start>end only when arr[end]>k i.e,
            # there is an array element with
            # value greater than k, so sub-array
            # sum cannot be less than k.
            if (Sum == 0):
                break

        if (Sum == 0):
            ans = -1
            break

    # Print the answer
    print(ans)

# Driver code
arr = [ 1, 2, 3, 4 ]
k = 8
n = len(arr)

# Function call
func(arr, k, n)

# This code is contributed by avanitrachhadiya2155
```

## c#

```
// C# program for the above approach
using System;
using System.Collections;

class GFG{

// Function to find the
// largest size subarray
static void func(ArrayList arr,
                 int k, int n)
{

    // Variable declaration
    int ans = n;
    int sum = 0;
    int start = 0;

    // Loop till N
    for(int end = 0; end < n; end++)
    {

        // Sliding window from left
        sum += (int)arr[end];

        while (sum > k)
        {

            // Sliding window from right
            sum -= (int)arr[start];
            start++;

            // Storing sub-array size - 1
            // for which sum was greater than k
            ans = Math.Min(ans, end - start + 1);

            // Sum will be 0 if start>end
            // because all elements are positive
            // start>end only when arr[end]>k i.e,
            // there is an array element with
            // value greater than k, so sub-array
            // sum cannot be less than k.
            if (sum == 0)
                break;
        }
        if (sum == 0)
        {
            ans = -1;
            break;
        }
    }

    // Print the answer
    Console.Write(ans);
}

// Driver code
public static void Main(string[] args)
{
    ArrayList arr = new ArrayList(){ 1, 2, 3, 4 };
    int k = 8;
    int n = arr.Count;

    // Function call
    func(arr, k, n);
}
}

// This code is contributed by rutvik_56
```

## Javascript

```
<script>
// Javascript program for the above approach

// Function to find the
// largest size subarray
function func(arr, k, n)
{
    // Variable declaration
    let ans = n;
    let sum = 0;
    let start = 0;

    // Loop till N
    for (let end = 0; end < n; end++)
    {
        // Sliding window from left
        sum += arr[end];

        while (sum > k) {
            // Sliding window from right
            sum -= arr[start];
            start++;

            // Storing sub-array size - 1
            // for which sum was greater than k
            ans = Math.min(ans, end - start + 1);

            // Sum will be 0 if start>end
            // because all elements are positive
            // start>end only when arr[end]>k i.e,
            // there is an array element with
            // value greater than k, so sub-array
            // sum cannot be less than k.
            if (sum == 0)
                break;
        }
        if (sum == 0) {
            ans = -1;
            break;
        }
    }

    // Print the answer
    document.write(ans);
}

// Driver code
    let arr = [ 1, 2, 3, 4 ];
    let k = 8;
    let n = arr.length;

    // Function call
    func(arr, k, n);

</script>
```

**输出**

***时间复杂度:** O(N)*