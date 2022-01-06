# 形成几何级数的最长子阵列

> 原文:[https://www . geesforgeks . org/long-subarray-forming-a-geometric-progress-gp/](https://www.geeksforgeeks.org/longest-subarray-forming-a-geometic-progression-gp/)

给定一个由不同数字组成的排序数组**arr[]**，任务是找出形成[几何级数](https://en.wikipedia.org/wiki/Geometric_progression)的最长子阵列的长度。

**示例:**

> **输入:** arr[]={1，2，4，7，14，28，56，89}
> **输出:** 4
> **解释:**
> 子阵{1，2，4}和{7，14，28，56}组成一个 GP。
> 因为{7，14，28，56}是他最长的，所以需要的输出是 4。
> 
> **输入:** arr[]={3，6，7，12，24，28，56}
> **输出:** 2

**天真方法:**解决问题最简单的方法是[生成所有可能的子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，对于每个子阵，检查是否形成 GP。不断更新找到的这种子阵列的最大长度。最后，打印获得的最大长度。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过以下步骤进行优化:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)选择一对相邻元素，即**arr【I】**和**arr【I+1】**，作为几何级数的前两项。
*   如果 **arr[i+1]** 不能被 **arr[i]** 整除，则不能考虑为公比。否则，将 **arr[i+1] / arr[i]** 作为当前几何级数的公比。
*   如果后续元素具有相同的公共比率，则增加并存储**几何级数**的长度。否则，更新公共比率，使其等于新的相邻元素对的比率。
*   最后，返回形成**几何级数**的最长子阵列的长度作为输出。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the length of
// the longest subarray forming a
// GP in a sorted array
int longestGP(int A[], int N)
{
    // Base Case
    if (N < 2)
        return N;

    // Stores the length of GP
    // and the common ratio
    int length = 1, common_ratio = 1;

    // Stores the maximum
    // length of the GP
    int maxlength = 1;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Check if the common ratio
        // is valid for GP
        if (A[i + 1] % A[i] == 0) {

            // If the current common ratio
            // is equal to previous common ratio
            if (A[i + 1] / A[i] == common_ratio) {

                // Increment the length of the GP
                length = length + 1;

                // Store the max length of GP
                maxlength
                    = max(maxlength, length);
            }

            // Otherwise
            else {

                // Update the common ratio
                common_ratio = A[i + 1] / A[i];

                // Update the length of GP
                length = 2;
            }
        }
        else {

            // Store the max length of GP
            maxlength
                = max(maxlength, length);

            // Update the length of GP
            length = 1;
        }
    }

    // Store the max length of GP
    maxlength = max(maxlength, length);

    // Return the max length of GP
    return maxlength;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 4, 7, 14, 28, 56, 89 };

    // Length of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << longestGP(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to return the length of
// the longest subarray forming a
// GP in a sorted array
static int longestGP(int A[], int N)
{

    // Base Case
    if (N < 2)
        return N;

    // Stores the length of GP
    // and the common ratio
    int length = 1, common_ratio = 1;

    // Stores the maximum
    // length of the GP
    int maxlength = 1;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {

        // Check if the common ratio
        // is valid for GP
        if (A[i + 1] % A[i] == 0)
        {

            // If the current common ratio
            // is equal to previous common ratio
            if (A[i + 1] / A[i] == common_ratio)
            {

                // Increment the length of the GP
                length = length + 1;

                // Store the max length of GP
                maxlength = Math.max(maxlength, length);
            }

            // Otherwise
            else
            {

                // Update the common ratio
                common_ratio = A[i + 1] / A[i];

                // Update the length of GP
                length = 2;
            }
        }
        else
        {

            // Store the max length of GP
            maxlength = Math.max(maxlength, length);

            // Update the length of GP
            length = 1;
        }
    }

    // Store the max length of GP
    maxlength = Math.max(maxlength, length);

    // Return the max length of GP
    return maxlength;
}

// Driver code
public static void main (String[] args)
{

    // Given array    
    int arr[] = { 1, 2, 4, 7, 14, 28, 56, 89 };

    // Length of the array
    int N = arr.length;

    // Function call
    System.out.println(longestGP(arr, N));
}
}

// This code is contributed by jana_sayantan   
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to return the length of
# the longest subarray forming a
# GP in a sorted array
def longestGP(A, N):

    # Base Case
    if (N < 2):
        return N

    # Stores the length of GP
    # and the common ratio
    length = 1
    common_ratio = 1

    # Stores the maximum
    # length of the GP
    maxlength = 1

    # Traverse the array
    for i in range(N - 1):

        # Check if the common ratio
        # is valid for GP
        if (A[i + 1] % A[i] == 0):

            # If the current common ratio
            # is equal to previous common ratio
            if (A[i + 1] // A[i] == common_ratio):

                # Increment the length of the GP
                length = length + 1

                # Store the max length of GP
                maxlength = max(maxlength, length)

            # Otherwise
            else:

                # Update the common ratio
                common_ratio = A[i + 1] // A[i]

                # Update the length of GP
                length = 2

        else:

            # Store the max length of GP
            maxlength = max(maxlength, length)

            # Update the length of GP
            length = 1

    # Store the max length of GP
    maxlength = max(maxlength, length)

    # Return the max length of GP
    return maxlength

# Driver Code

# Given array
arr = [ 1, 2, 4, 7, 14, 28, 56, 89 ]

# Length of the array
N = len(arr)

# Function call
print(longestGP(arr, N))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to return the length of
// the longest subarray forming a
// GP in a sorted array
static int longestGP(int []A, int N)
{    
    // Base Case
    if (N < 2)
        return N;

    // Stores the length of GP
    // and the common ratio
    int length = 1, common_ratio = 1;

    // Stores the maximum
    // length of the GP
    int maxlength = 1;

    // Traverse the array
    for(int i = 0; i < N - 1; i++)
    {
        // Check if the common ratio
        // is valid for GP
        if (A[i + 1] % A[i] == 0)
        {
            // If the current common ratio
            // is equal to previous common ratio
            if (A[i + 1] / A[i] == common_ratio)
            {
                // Increment the length of the GP
                length = length + 1;

                // Store the max length of GP
                maxlength = Math.Max(maxlength,
                                     length);
            }

            // Otherwise
            else
            {               
                // Update the common ratio
                common_ratio = A[i + 1] /
                               A[i];

                // Update the length of GP
                length = 2;
            }
        }
        else
        {
            // Store the max length of GP
            maxlength = Math.Max(maxlength,
                                 length);

            // Update the length of GP
            length = 1;
        }
    }

    // Store the max length of GP
    maxlength = Math.Max(maxlength,
                         length);

    // Return the max length of GP
    return maxlength;
}

// Driver code
public static void Main(String[] args)
{    
    // Given array    
    int []arr = {1, 2, 4, 7,
                 14, 28, 56, 89};

    // Length of the array
    int N = arr.Length;

    // Function call
    Console.WriteLine(longestGP(arr, N));
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to return the length of
// the longest subarray forming a
// GP in a sorted array
function longestGP(A, N)
{

    // Base Case
    if (N < 2)
        return N;

    // Stores the length of GP
    // and the common ratio
    let length = 1, common_ratio = 1;

    // Stores the maximum
    // length of the GP
    let maxlength = 1;

    // Traverse the array
    for(let i = 0; i < N - 1; i++)
    {

        // Check if the common ratio
        // is valid for GP
        if (A[i + 1] % A[i] == 0)
        {

            // If the current common ratio
            // is equal to previous common ratio
            if (A[i + 1] / A[i] == common_ratio)
            {

                // Increment the length of the GP
                length = length + 1;

                // Store the max length of GP
                maxlength = Math.max(maxlength, length);
            }

            // Otherwise
            else
            {

                // Update the common ratio
                common_ratio = A[i + 1] / A[i];

                // Update the length of GP
                length = 2;
            }
        }
        else
        {

            // Store the max length of GP
            maxlength = Math.max(maxlength, length);

            // Update the length of GP
            length = 1;
        }
    }

    // Store the max length of GP
    maxlength = Math.max(maxlength, length);

    // Return the max length of GP
    return maxlength;
}

// Driver code

    // Given array    
    let arr = [ 1, 2, 4, 7, 14, 28, 56, 89 ];

    // Length of the array
    let N = arr.length;

    // Function call
    document.write(longestGP(arr, N));

  // This code is contributed by code_hunt.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*
***空间复杂度:** O(1)*