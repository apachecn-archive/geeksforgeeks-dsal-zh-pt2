# 二进制数组中第二长的连续 1 序列的长度

> 原文:[https://www . geesforgeks . org/二进制数组中第二长连续 1 序列的长度/](https://www.geeksforgeeks.org/length-of-second-longest-sequence-of-consecutive-1s-in-a-binary-array/)

给定一个大小为 **N** 的二进制[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找出数组中第二个[最长的连续 1 序列](https://www.geeksforgeeks.org/length-longest-consecutive-1s-binary-representation/)的长度。

**示例:**

> **输入:** arr[] = {1，1，1，0，0，1，0，1，1，1，1，0，0}
> **输出:** 4 3
> **解释:**
> 连续 1 的最长序列是 4 即{arr[7]，… arr[10]}。
> 第二长的连续序列是 3，即{arr[0]，… arr[2]}。
> 
> **输入:** arr[] = {1，0，1 }
> T3】输出: 1 0

**方法:**思路是[遍历给定的二进制数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并跟踪到目前为止遇到的最大和第二大长度的连续一个。以下是步骤:

1.  初始化变量 **maxi** 、 **count** 和 **second_max** 分别存储连续 1 的最长、当前和第二长序列的长度..
2.  迭代给定数组两次。
3.  首先，[从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。每遇到 1 个，则增加**计数**，并与目前最大值进行比较。如果遇到 0，将计数重置为 0。
4.  在第二次遍历中，按照上述过程找到所需的连续 1 的第二长计数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// and second maximum length
void FindMax(int arr[], int N)
{
    // Initialise maximum length
    int maxi = -1;

    // Initialise second maximum length
    int maxi2 = -1;

    // Initialise count
    int count = 0;

    // Iterate over the array
    for (int i = 0; i < N; ++i) {

        // If sequence ends
        if (arr[i] == 0)

            // Reset count
            count = 0;

        // Otherwise
        else {

            // Increase length
            // of current sequence
            count++;

            // Update maximum
            maxi = max(maxi, count);
        }
    }

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // If sequence continues
        if (arr[i] == 1) {

            // Increase length
            // of current sequence
            count++;

            // Update second max
            if (count > maxi2 && count < maxi) {
                maxi2 = count;
            }
        }

        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;
    }

    maxi = max(maxi, 0);
    maxi2 = max(maxi2, 0);

    // Print the result
    cout << maxi2;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    FindMax(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function to find maximum
// and second maximum length
static void FindMax(int arr[], int N)
{

    // Initialise maximum length
    int maxi = -1;

    // Initialise second maximum length
    int maxi2 = -1;

    // Initialise count
    int count = 0;

    // Iterate over the array
    for(int i = 0; i < N; ++i)
    {

        // If sequence ends
        if (arr[i] == 0)

            // Reset count
            count = 0;

        // Otherwise
        else
        {

            // Increase length
            // of current sequence
            count++;

            // Update maximum
            maxi = Math.max(maxi, count);
        }
    }

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // If sequence continues
        if (arr[i] == 1)
        {

            // Increase length
            // of current sequence
            count++;

            // Update second max
            if (count > maxi2 &&
                count < maxi)
            {
                maxi2 = count;
            }
        }

        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;
    }

    maxi = Math.max(maxi, 0);
    maxi2 = Math.max(maxi2, 0);

    // Print the result
    System.out.println( maxi2);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 1, 1, 0, 0, 1, 1 };
    int n = arr.length;

    FindMax(arr, n);
}
}

// This code is contributed by Stream_Cipher
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find maximum
# and second maximum length
def FindMax(arr, N):

    # Initialise maximum length
    maxi = -1

    # Initialise second maximum length
    maxi2 = -1

    # Initialise count
    count = 0

    # Iterate over the array
    for i in range(N):

        # If sequence ends
        if (arr[i] == 0):

            # Reset count
            count = 0

        # Otherwise
        else:

            # Increase length
            # of current sequence
            count += 1

            # Update maximum
            maxi = max(maxi, count)

    # Traverse the given array
    for i in range(N):

        # If sequence continues
        if (arr[i] == 1):

            # Increase length
            # of current sequence
            count += 1

            # Update second max
            if (count > maxi2 and
                count < maxi):
                maxi2 = count

        # Reset count when 0 is found
        if (arr[i] == 0):
            count = 0

    maxi = max(maxi, 0)
    maxi2 = max(maxi2, 0)

    # Print the result
    print(maxi2)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, 1, 1, 0, 0, 1, 1]
    N = len(arr)

    # Function Call
    FindMax(arr, N)

# This code is contributed by Mohit Kumar29
```

## C#

```
// C# implementation of the above approach
using System.Collections.Generic;
using System;

class GFG{

// Function to find maximum
// and second maximum length
static void FindMax(int []arr, int N)
{

    // Initialise maximum length
    int maxi = -1;

    // Initialise second maximum length
    int maxi2 = -1;

    // Initialise count
    int count = 0;

    // Iterate over the array
    for(int i = 0; i < N; ++i)
    {

        // If sequence ends
        if (arr[i] == 0)

            // Reset count
            count = 0;

        // Otherwise
        else
        {

            // Increase length
            // of current sequence
            count++;

            // Update maximum
            maxi = Math.Max(maxi, count);
        }
    }

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // If sequence continues
        if (arr[i] == 1)
        {

            // Increase length
            // of current sequence
            count++;

            // Update second max
            if (count > maxi2 &&
                count < maxi)
            {
                maxi2 = count;
            }
        }

        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;
    }

    maxi = Math.Max(maxi, 0);
    maxi2 = Math.Max(maxi2, 0);

    // Print the result
    Console.WriteLine( maxi2);
}

// Driver code
public static void Main()
{
    int []arr = { 1, 1, 1, 0, 0, 1, 1 };
    int n = arr.Length;

    FindMax(arr, n);
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find maximum
// and second maximum length
function FindMax(arr, N)
{

    // Initialise maximum length
    let maxi = -1;

    // Initialise second maximum length
    let maxi2 = -1;

    // Initialise count
    let count = 0;

    // Iterate over the array
    for(let i = 0; i < N; ++i)
    {

        // If sequence ends
        if (arr[i] == 0)

            // Reset count
            count = 0;

        // Otherwise
        else
        {

            // Increase length
            // of current sequence
            count++;

            // Update maximum
            maxi = Math.max(maxi, count);
        }
    }

    // Traverse the given array
    for(let i = 0; i < N; i++)
    {

        // If sequence continues
        if (arr[i] == 1)
        {

            // Increase length
            // of current sequence
            count++;

            // Update second max
            if (count > maxi2 &&
                count < maxi)
            {
                maxi2 = count;
            }
        }

        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;
    }

    maxi = Math.max(maxi, 0);
    maxi2 = Math.max(maxi2, 0);

    // Prlet the result
    document.write( maxi2);
}

// Driver code

    let arr = [ 1, 1, 1, 0, 0, 1, 1 ];
    let n = arr.length;

    FindMax(arr, n);

     // This code is contributed by target_2.
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*