# 通过翻转子阵列

最大化 0 的数量

> 原文:[https://www . geesforgeks . org/maximum-number-0s-fling-subarray/](https://www.geeksforgeeks.org/maximize-number-0s-flipping-subarray/)

给定一个二进制数组，在允许子数组翻转一次的情况下，找出数组中最大的零个数。翻转操作将所有 0 切换为 1，将 1 切换为 0。
示例:

```
Input :  arr[] = {0, 1, 0, 0, 1, 1, 0}
Output : 6
We can get 6 zeros by flipping the subarray {4, 5}

Input :  arr[] = {0, 0, 0, 1, 0, 1}
Output : 5
```

**方法 1(简单:O(n)<sup>2</sup>)**
一个简单的解决方法是考虑所有子阵，找到一个最大值为**(1 的计数)–(0 的计数)**的子阵。让这个值为 max_diff。最后，返回原始数组中零的计数加上 max_diff。

## C++

```
// C++ program to maximize number of zeroes in a
// binary array by at most one flip operation
#include<bits/stdc++.h>
using namespace std;

// A Kadane's algorithm based solution to find maximum
// number of 0s by flipping a subarray.
int findMaxZeroCount(bool arr[], int n)
{
    // Initialize max_diff = maximum of (Count of 0s -
    // count of 1s) for all subarrays.
    int max_diff = 0;

    // Initialize count of 0s in original array
    int orig_zero_count = 0;

    // Consider all Subarrays by using two nested two
    // loops
    for (int i=0; i<n; i++)
    {
        // Increment count of zeros
        if (arr[i] == 0)
            orig_zero_count++;

        // Initialize counts of 0s and 1s
        int count1 = 0, count0 = 0;

        // Consider all subarrays starting from arr[i]
        // and find the difference between 1s and 0s.
        // Update max_diff if required
        for (int j=i; j<n; j++)
        {
            (arr[j] == 1)? count1++ : count0++;
            max_diff = max(max_diff, count1 - count0);
        }
    }

    // Final result would be count of 0s in original
    // array plus max_diff.
    return orig_zero_count + max_diff;
}

// Driver program
int main()
{
    bool arr[] = {0, 1, 0, 0, 1, 1, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMaxZeroCount(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Maximize number of 0s by flipping
// a subarray
class GFG {

    // A Kadane's algorithm based solution to find maximum
    // number of 0s by flipping a subarray.
    public static int findMaxZeroCount(int arr[], int n)
    {
        // Initialize max_diff = maximum of (Count of 0s -
        // count of 1s) for all subarrays.
        int max_diff = 0;

        // Initialize count of 0s in original array
        int orig_zero_count = 0;

        // Consider all Subarrays by using two nested two
        // loops
        for (int i=0; i<n; i++)
        {
            // Increment count of zeros
            if (arr[i] == 0)
                orig_zero_count++;

            // Initialize counts of 0s and 1s
            int count1 = 0, count0 = 0;

            // Consider all subarrays starting from arr[i]
            // and find the difference between 1s and 0s.
            // Update max_diff if required
            for (int j = i; j < n; j ++)
            {
                if(arr[j] == 1)
                    count1++;
                else count0++;
                max_diff = Math.max(max_diff, count1 - count0);
            }
        }

        // Final result would be count of 0s in original
        // array plus max_diff.
        return orig_zero_count + max_diff;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {0, 1, 0, 0, 1, 1, 0};

        System.out.println(findMaxZeroCount(arr, arr.length));
    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to maximize number of
# zeroes in a binary array by at most
# one flip operation

# A Kadane's algorithm based solution
# to find maximum number of 0s by
# flipping a subarray.
def findMaxZeroCount(arr, n):

    # Initialize max_diff = maximum
    # of (Count of 0s - count of 1s)
    # for all subarrays.
    max_diff = 0

    # Initialize count of 0s in
    # original array
    orig_zero_count = 0

    # Consider all Subarrays by using
    # two nested two loops
    for i in range(n):

        # Increment count of zeros
        if arr[i] == 0:
            orig_zero_count += 1

        # Initialize counts of 0s and 1s
        count1, count0 = 0, 0

        # Consider all subarrays starting
        # from arr[i] and find the
        # difference between 1s and 0s.
        # Update max_diff if required
        for j in range(i, n):
            if arr[j] == 1:
                count1 += 1
            else:
                count0 += 1

            max_diff = max(max_diff, count1 -
                                     count0)

    # Final result would be count of 0s
    # in original array plus max_diff.
    return orig_zero_count + max_diff

# Driver code
arr = [ 0, 1, 0, 0, 1, 1, 0 ]
n = len(arr)

print(findMaxZeroCount(arr, n))

# This code is contributed by stutipathak31jan
```

## C#

```
// C# code for Maximize number of 0s by
// flipping a subarray
using System;

class GFG{

// A Kadane's algorithm based solution
// to find maximum number of 0s by
// flipping a subarray.
public static int findMaxZeroCount(int []arr,
                                   int n)
{

    // Initialize max_diff = maximum of
    // (Count of 0s - count of 1s) for
    // all subarrays.
    int max_diff = 0;

    // Initialize count of 0s in
    // original array
    int orig_zero_count = 0;

    // Consider all Subarrays by
    // using two nested two loops
    for(int i = 0; i < n; i++)
    {

        // Increment count of zeros
        if (arr[i] == 0)
            orig_zero_count++;

        // Initialize counts of 0s and 1s
        int count1 = 0, count0 = 0;

        // Consider all subarrays starting
        // from arr[i] and find the difference
        // between 1s and 0s.
        // Update max_diff if required
        for(int j = i; j < n; j ++)
        {
            if(arr[j] == 1)
                count1++;

            else count0++;
            max_diff = Math.Max(max_diff,
                                count1 - count0);
        }
    }

    // Final result would be count of 0s in original
    // array plus max_diff.
    return orig_zero_count + max_diff;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 0, 1, 0, 0, 1, 1, 0 };

    Console.WriteLine(
        findMaxZeroCount(arr, arr.Length));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// JavaScript program to maximize number of zeroes in a
// binary array by at most one flip operation

// A Kadane's algorithm based solution to find maximum
// number of 0s by flipping a subarray.
function findMaxZeroCount(arr, n)
{
    // Initialize max_diff = maximum of (Count of 0s -
    // count of 1s) for all subarrays.
    let max_diff = 0;

    // Initialize count of 0s in original array
    let orig_zero_count = 0;

    // Consider all Subarrays by using two nested two
    // loops
    for (let i=0; i<n; i++)
    {
        // Increment count of zeros
        if (arr[i] == 0)
            orig_zero_count++;

        // Initialize counts of 0s and 1s
        let count1 = 0, count0 = 0;

        // Consider all subarrays starting from arr[i]
        // and find the difference between 1s and 0s.
        // Update max_diff if required
        for (let j=i; j<n; j++)
        {
            (arr[j] == 1)? count1++ : count0++;
            max_diff = Math.max(max_diff, count1 - count0);
        }
    }

    // Final result would be count of 0s in original
    // array plus max_diff.
    return orig_zero_count + max_diff;
}

// Driver program
    let arr = [0, 1, 0, 0, 1, 1, 0];
    let n = arr.length;
    document.write(findMaxZeroCount(arr, n));

// This code is contributed by Surbhi Tyagi.

</script>
```

**输出:**

```
6
```

**方法二(高效:O(n))**
这个问题可以简化为[最大子阵求和问题](https://www.geeksforgeeks.org/largest-sum-contiguous-subarray/)。其思想是把每 0 看作-1，每 1 看作 1，求这个修正数组中最大子阵和的和。这个和是我们需要的 max _ diff(0 的计数–任何子阵列中 1 的计数)。最后，我们返回原始数组中的 max_diff 加上零的计数。

## C++

```
// C++ program to maximize number of zeroes in a
// binary array by at most one flip operation
#include<bits/stdc++.h>
using namespace std;

// A Kadane's algorithm based solution to find maximum
// number of 0s by flipping a subarray.
int findMaxZeroCount(bool arr[], int n)
{
    // Initialize count of zeros and maximum difference
    // between count of 1s and 0s in a subarray
    int orig_zero_count = 0;

    // Initiale overall max diff for any subarray
    int max_diff = 0;

    // Initialize current diff
    int curr_max = 0;

    for (int i=0; i<n; i++)
    {
        // Count of zeros in original array (Not related
        // to Kadane's algorithm)
        if (arr[i] == 0)
           orig_zero_count++;

        // Value to be considered for finding maximum sum
        int val = (arr[i] == 1)? 1 : -1;

        // Update current max and max_diff
        curr_max = max(val, curr_max + val);
        max_diff = max(max_diff, curr_max);
    }
    max_diff = max(0, max_diff);

    return orig_zero_count + max_diff;
}

// Driver program
int main()
{
    bool arr[] = {0, 1, 0, 0, 1, 1, 0};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMaxZeroCount(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for Maximize number of 0s by
// flipping a subarray
class GFG {

    // A Kadane's algorithm based solution to find maximum
    // number of 0s by flipping a subarray.
    public static int findMaxZeroCount(int arr[], int n)
    {
        // Initialize count of zeros and maximum difference
        // between count of 1s and 0s in a subarray
        int orig_zero_count = 0;

        // Initiale overall max diff for any subarray
        int max_diff = 0;

        // Initialize current diff
        int curr_max = 0;

        for (int i = 0; i < n; i ++)
        {
            // Count of zeros in original array (Not related
            // to Kadane's algorithm)
            if (arr[i] == 0)
               orig_zero_count ++;

            // Value to be considered for finding maximum sum
            int val = (arr[i] == 1)? 1 : -1;

            // Update current max and max_diff
            curr_max = Math.max(val, curr_max + val);
            max_diff = Math.max(max_diff, curr_max);
        }
        max_diff = Math.max(0, max_diff);

        return orig_zero_count + max_diff;
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {0, 1, 0, 0, 1, 1, 0};

        System.out.println(findMaxZeroCount(arr, arr.length));
    }
  }
// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to maximize number
# of zeroes in a binary array by at
# most one flip operation

# A Kadane's algorithm based solution
# to find maximum number of 0s by
# flipping a subarray.
def findMaxZeroCount(arr, n):

    # Initialize count of zeros and
    # maximum difference between count
    # of 1s and 0s in a subarray
    orig_zero_count = 0

    # Initialize overall max diff
    # for any subarray
    max_diff = 0

    # Initialize current diff
    curr_max = 0

    for i in range(n):

        # Count of zeros in original
        # array (Not related to
        # Kadane's algorithm)
        if arr[i] == 0:
            orig_zero_count += 1

        # Value to be considered for
        # finding maximum sum
        val = 1 if arr[i] == 1 else -1

        # Update current max and max_diff
        curr_max = max(val, curr_max + val)
        max_diff = max(max_diff, curr_max)

    max_diff = max(0, max_diff)

    return orig_zero_count + max_diff

# Driver code
arr = [ 0, 1, 0, 0, 1, 1, 0 ]
n = len(arr)

print(findMaxZeroCount(arr, n))

# This code is contributed by stutipathak31jan
```

## C#

```
// C# code for Maximize number of 0s by
// flipping a subarray
using System;
class GFG{

  // A Kadane's algorithm based solution to find maximum
  // number of 0s by flipping a subarray.
  public static int findMaxZeroCount(int []arr, int n)
  {
    // Initialize count of zeros and maximum difference
    // between count of 1s and 0s in a subarray
    int orig_zero_count = 0;

    // Initiale overall max diff for any subarray
    int max_diff = 0;

    // Initialize current diff
    int curr_max = 0;

    for (int i = 0; i < n; i ++)
    {
      // Count of zeros in original array (Not related
      // to Kadane's algorithm)
      if (arr[i] == 0)
        orig_zero_count ++;

      // Value to be considered for finding maximum sum
      int val = (arr[i] == 1)? 1 : -1;

      // Update current max and max_diff
      curr_max = Math.Max(val, curr_max + val);
      max_diff = Math.Max(max_diff, curr_max);
    }
    max_diff = Math.Max(0, max_diff);

    return orig_zero_count + max_diff;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    int []arr = {0, 1, 0, 0, 1, 1, 0};

    Console.WriteLine(findMaxZeroCount(arr, arr.Length));
  }
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// JavaScript program to
// maximize number of zeroes in a
// binary array by at most one flip operation

// A Kadane's algorithm
// based solution to find maximum
// number of 0s by flipping a subarray.
function findMaxZeroCount(arr, n)
{
    // Initialize count of
    // zeros and maximum difference
    // between count of 1s and 0s in
    // a subarray
    var orig_zero_count = 0;

    // Initiale overall max diff for any subarray
    var max_diff = 0;

    // Initialize current diff
    var curr_max = 0;

    for (var i=0; i<n; i++)
    {
        // Count of zeros in original array
        // (Not related to Kadane's algorithm)
        if (arr[i] == 0)
           orig_zero_count++;

        // Value to be considered for
        // finding maximum sum
        var val;
        if (arr[i] == 1)
        val=1;
        else
        val=-1;

        // Update current max and max_diff
        curr_max = Math.max(val, curr_max + val);
        max_diff = Math.max(max_diff, curr_max);
    }
    max_diff = Math.max(0, max_diff);

    return orig_zero_count + max_diff;
}

    var arr = [0, 1, 0, 0, 1, 1, 0];
    var n=7;
    document.write(findMaxZeroCount(arr, n));

    // This Code is Contributed by Harshit Srivastava

</script>
```

**输出:**

```
6
```

本文由 **Shivam Agrawal** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。