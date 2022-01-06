# 奇数和偶数元素相等的最长子阵列长度

> 原文:[https://www . geeksforgeeks . org/奇数和偶数元素相等的最长子阵列长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-equal-number-of-odd-and-even-elements/)

给定一个整数数组 **arr[]** ，任务是找到奇数和偶数元素相等的最长子数组的长度。

**示例:**

> **输入:** arr[] = {1，2，1，2}
> **输出:** 4
> **解释:**
> 给定阵列中的子阵列是–
> { {1}、{1，2}、{1，2，1}、{1，2，1，2}、{2}、{2，1 }、{2，1，2}、{1}、{ 1，2}、{2}}
> 其中
> 
> **输入:** arr[] = {12，4，7，8，9，2，11，0，2，13 }
> T3】输出: 8

**天真法:**简单的解决方法是逐个考虑所有子阵，检查子阵中奇偶元素的个数，从那些子阵中找出最大值。
T3】时间复杂度: O(N <sup>2</sup> )

**高效方法:**思路是将奇数元素视为 1，偶数元素视为-1，返回和等于 0 的最长子数组的长度。使用[这个](https://www.geeksforgeeks.org/find-subarray-with-given-sum-in-array-of-integers/)方法可以找到给定和的子阵。
**时间复杂度:** O(N)
以下是上述方法的实现:

## C++

```
// C++ program to find the length
// of the longest sub-array with an
// equal number of odd and even elements
#include <bits/stdc++.h>
using namespace std;

// Function that returns the length of
// the longest sub-array with an equal
// number of odd and even elements
int maxSubarrayLength(int* A, int N)
{
    // Initialize variable to store result
    int maxLen = 0;

    // Initialize variable to store sum
    int curr_sum = 0;

    // Create an empty map to store
    // index of the sum
    unordered_map<int, int> hash;

    // Loop through the array
    for (int i = 0; i < N; i++) {
        if (A[i] % 2 == 0)
            curr_sum -= 1;
        else
            curr_sum += 1;

        // Check if number of even and
        // odd elements are equal
        if (curr_sum == 0)
            maxLen = max(maxLen, i + 1);

        // If curr_sum already exists in map
        // we have a subarray with 0 sum, i.e,
        // equal number of odd and even number
        if (hash.find(curr_sum) != hash.end())
            maxLen = max(maxLen,
                        i - hash[curr_sum]);

        // Store the index of the sum
        else
            hash[curr_sum] = i;
    }
    return maxLen;
}

// Driver Code
int main()
{
    int arr[] = { 12, 4, 7, 8, 9, 2,
                        11, 0, 2, 13 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxSubarrayLength(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length
// of the longest sub-array with an
// equal number of odd and even elements
import java.util.*;

class GFG
{

// Function that returns the length of
// the longest sub-array with an equal
// number of odd and even elements
static int maxSubarrayLength(int []A, int N)
{
    // Initialize variable to store result
    int maxLen = 0;

    // Initialize variable to store sum
    int curr_sum = 0;

    // Create an empty map to store
    // index of the sum
    HashMap<Integer,Integer> hash = new HashMap<Integer,Integer>();

    // Loop through the array
    for (int i = 0; i < N; i++)
    {
        if (A[i] % 2 == 0)
            curr_sum -= 1;
        else
            curr_sum += 1;

        // Check if number of even and
        // odd elements are equal
        if (curr_sum == 0)
            maxLen = Math.max(maxLen, i + 1);

        // If curr_sum already exists in map
        // we have a subarray with 0 sum, i.e,
        // equal number of odd and even number
        if (hash.containsKey(curr_sum))
            maxLen = Math.max(maxLen,
                        i - hash.get(curr_sum));

        // Store the index of the sum
        else {
            hash.put(curr_sum, i);
        }
    }
    return maxLen;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 12, 4, 7, 8, 9, 2,
                        11, 0, 2, 13 };
    int n = arr.length;

    System.out.print(maxSubarrayLength(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the length
# of the longest sub-array with an
# equal number of odd and even elements

# Function that returns the length of
# the longest sub-array with an equal
# number of odd and even elements
def maxSubarrayLength(A, N) :

    # Initialize variable to store result
    maxLen = 0;

    # Initialize variable to store sum
    curr_sum = 0;

    # Create an empty map to store
    # index of the sum
    hash = {};

    # Loop through the array
    for i in range(N) :
        if (A[i] % 2 == 0) :
            curr_sum -= 1;
        else :
            curr_sum += 1;

        # Check if number of even and
        # odd elements are equal
        if (curr_sum == 0) :
            maxLen = max(maxLen, i + 1);

        # If curr_sum already exists in map
        # we have a subarray with 0 sum, i.e,
        # equal number of odd and even number
        if curr_sum in hash :
            maxLen = max(maxLen, i - hash[curr_sum]);

        # Store the index of the sum
        else :
            hash[curr_sum] = i;

    return maxLen;

# Driver Code
if __name__ == "__main__" :

    arr = [ 12, 4, 7, 8, 9, 2, 11, 0, 2, 13 ];
    n = len(arr);

    print(maxSubarrayLength(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the length
// of the longest sub-array with an
// equal number of odd and even elements
using System;
using System.Collections.Generic;

class GFG
{

// Function that returns the length of
// the longest sub-array with an equal
// number of odd and even elements
static int maxSubarrayLength(int []A, int N)
{
    // Initialize variable to store result
    int maxLen = 0;

    // Initialize variable to store sum
    int curr_sum = 0;

    // Create an empty map to store
    // index of the sum
    Dictionary<int, int> hash = new Dictionary<int, int>();

    // Loop through the array
    for (int i = 0; i < N; i++)
    {
        if (A[i] % 2 == 0)
            curr_sum -= 1;
        else
            curr_sum += 1;

        // Check if number of even and
        // odd elements are equal
        if (curr_sum == 0)
            maxLen = Math.Max(maxLen, i + 1);

        // If curr_sum already exists in map
        // we have a subarray with 0 sum, i.e,
        // equal number of odd and even number
        if (hash.ContainsKey(curr_sum))
            maxLen = Math.Max(maxLen,
                        i - hash[curr_sum]);

        // Store the index of the sum
        else {
            hash.Add(curr_sum, i);
        }
    }
    return maxLen;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 12, 4, 7, 8, 9, 2,
                        11, 0, 2, 13 };
    int n = arr.Length;
    Console.Write(maxSubarrayLength(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to find the length
// of the longest sub-array with an
// equal number of odd and even elements

// Function that returns the length of
// the longest sub-array with an equal
// number of odd and even elements
function maxSubarrayLength(A, N)
{
    // Initialize variable to store result
    var maxLen = 0;

    // Initialize variable to store sum
    var curr_sum = 0;

    // Create an empty map to store
    // index of the sum
    var hash = new Map();

    // Loop through the array
    for (var i = 0; i < N; i++) {
        if (A[i] % 2 == 0)
            curr_sum -= 1;
        else
            curr_sum += 1;

        // Check if number of even and
        // odd elements are equal
        if (curr_sum == 0)
            maxLen = Math.max(maxLen, i + 1);

        // If curr_sum already exists in map
        // we have a subarray with 0 sum, i.e,
        // equal number of odd and even number
        if (hash.has(curr_sum))
            maxLen = Math.max(maxLen,
                        i - hash.get(curr_sum));

        // Store the index of the sum
        else
            hash.set(curr_sum, i);
    }
    return maxLen;
}

// Driver Code
var arr = [12, 4, 7, 8, 9, 2,
                    11, 0, 2, 13 ];
var n = arr.length;
document.write( maxSubarrayLength(arr, n));

</script>
```

**Output:** 

```
8
```