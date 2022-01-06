# 异或值为奇数的最长子序列的长度

> 原文:[https://www . geeksforgeeks . org/最长子序列长度-其-xor-值为奇数/](https://www.geeksforgeeks.org/length-of-longest-subsequence-whose-xor-value-is-odd/)

给定一个由 **N** 个正整数组成的数组 **arr[]** ，任务是找出最长子序列的长度，使得子序列中所有整数的[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为奇数。

**示例:**

> **输入:** N = 7，arr[] = {2，3，4，1，5，6，7}
> **输出:** 6
> **说明:** *最大长度的子序列为{2* ，3，4，5，6，7 *}*
> *，所有元素异或为 1。*
> *其他子序列也存在。*
> 
> **输入:** N = 4，arr[] = {2，4，6，8}
> **输出:** 0
> **解释:**没有可能的子序列存在。

**天真方法:**天真的想法是[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，并检查任何子序列的按位异或是否为奇数。如果存在按位异或为奇数的子序列，则打印这些子序列中的最大长度。

**时间复杂度:***O(N * 2<sup>N</sup>)*
T7】辅助空间: *O(1)*

**高效方法:**优化上述幼稚方法的思路是[统计给定数组](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)中奇数和偶数元素的个数，并求出最长子序列的长度，如下所示:

1.  计算**arr【】**中偶数和奇数元素的数量。
2.  如果奇数值的计数等于数组大小，即 **N** ，那么我们有两种可能的情况:
    1.  如果数组的大小是奇数，那么最大长度将等于 **N**
    2.  否则最大长度将等于**N–1**。
3.  如果偶数值的计数等于数组大小，那么最大长度将为零。
4.  现在，如果两种类型的元素都出现在给定的数组中，那么最大长度将包括所有偶数元素，对于奇数元素，如果奇数值的计数为奇数，我们将包括所有偶数元素，否则我们将包括**奇数–1**元素。
5.  在上述步骤之后，打印最长子序列的最大长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function for find max XOR subsequence
// having odd value
int maxXORSubsequence(int arr[], int n)
{

    // Initialize odd and even count
    int odd = 0, even = 0;

    // Count the number of odd and even
    // numbers in given array
    for (int i = 0; i < n; i++) {
        if (arr[i] & 1)
            odd++;
        else
            even++;
    }

    int maxlen;

    if (odd == n) {

        // if all values are odd
        // in given array
        if (odd % 2 == 0)
            maxlen = n - 1;
        else
            maxlen = n;
    }
    else if (even == n) {

        // if all values are even
        // in given array
        maxlen = 0;
    }
    else {

        // if both odd and even are
        // present in given array
        if (odd % 2 == 0)
            maxlen = even + odd - 1;
        else
            maxlen = even + odd;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 3, 4, 5, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maxXORSubsequence(arr, n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function for find max XOR subsequence
// having odd value
static int maxXORSubsequence(int arr[], int n)
{

    // Initialize odd and even count
    int i, odd = 0, even = 0;

    // Count the number of odd and even
    // numbers in given array
    for(i = 0; i < n; i++)
    {
        if ((arr[i] & 1) != 0)
            odd++;
        else
            even++;
    }

    int maxlen;

    if (odd == n)
    {

        // If all values are odd
        // in given array
        if (odd % 2 == 0)
            maxlen = n - 1;
        else
            maxlen = n;
    }
    else if (even == n)
    {

        // If all values are even
        // in given array
        maxlen = 0;
    }
    else
    {

        // If both odd and even are
        // present in given array
        if (odd % 2 == 0)
            maxlen = even + odd - 1;
        else
            maxlen = even + odd;
    }
    return maxlen;
}

// Driver Code
public static void main (String []args)
{

    // Given array arr[]
    int arr[] = { 2, 3, 4, 5, 6, 7 };
    int n = arr.length;

    // Function Call
    System.out.print( maxXORSubsequence(arr, n));
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function for find max XOR subsequence
# having odd value
def maxXorSubsequence(arr, n):

    # Initialize odd and even count
    odd = 0
    even = 0

    # Count the number of odd and even
    # numbers in given array
    for i in range(0, n):
        if arr[i] % 2 != 0:
            odd += 1
        else:
            even += 1
    if odd == n:

        # If all values are odd
        # in given array
        if odd % 2 == 0:
            maxlen = n - 1
        else:
            maxlen = n

    elif even == n:

        # If all values are even
        # in given array
        maxlen = 0
    else:

        # If both odd and even are
        # present in given array
        if odd % 2 == 0:
            maxlen = even + odd - 1
        else:
            maxlen = even + odd

    return maxlen

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 2, 3, 4, 5, 6, 7 ]
    n = len(arr)

    # Function Call
    print(maxXorSubsequence(arr,n))

# This code is contributed by virusbuddah_
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function for find max XOR subsequence
// having odd value
static int maxXORSubsequence(int[] arr, int n)
{

    // Initialize odd and even count
    int i, odd = 0, even = 0;

    // Count the number of odd and even
    // numbers in given array
    for(i = 0; i < n; i++)
    {
        if ((arr[i] & 1) != 0)
            odd++;
        else
            even++;
    }

    int maxlen;

    if (odd == n)
    {

        // If all values are odd
        // in given array
        if (odd % 2 == 0)
            maxlen = n - 1;
        else
            maxlen = n;
    }
    else if (even == n)
    {

        // If all values are even
        // in given array
        maxlen = 0;
    }
    else
    {

        // If both odd and even are
        // present in given array
        if (odd % 2 == 0)
            maxlen = even + odd - 1;
        else
            maxlen = even + odd;
    }
    return maxlen;
}

// Driver Code
public static void Main (string []args)
{

    // Given array arr[]
    int []arr = { 2, 3, 4, 5, 6, 7 };
    int n = arr.Length;

    // Function Call
    Console.Write( maxXORSubsequence(arr, n));
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function for find max XOR subsequence
// having odd value
function maxXORSubsequence(arr, n)
{

    // Initialize odd and even count
    let odd = 0, even = 0;

    // Count the number of odd and even
    // numbers in given array
    for(let i = 0; i < n; i++)
    {
        if ((arr[i] & 1) != 0)
            odd++;
        else
            even++;
    }

    let maxlen;

    if (odd == n)
    {

        // If all values are odd
        // in given array
        if (odd % 2 == 0)
            maxlen = n - 1;
        else
            maxlen = n;
    }
    else if (even == n)
    {

        // If all values are even
        // in given array
        maxlen = 0;
    }
    else
    {

        // If both odd and even are
        // present in given array
        if (odd % 2 == 0)
            maxlen = even + odd - 1;
        else
            maxlen = even + odd;
    }
    return maxlen;
}

// Driver code

// Given array arr[]
let arr = [ 2, 3, 4, 5, 6, 7 ];
let n = arr.length;

// Function Call
document.write(maxXORSubsequence(arr, n));

// This code is contributed by divyesh072019

</script>
```

**Output:**

```
6
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*