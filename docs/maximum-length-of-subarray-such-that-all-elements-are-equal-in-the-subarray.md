# 子阵列的最大长度，使得子阵列中的所有元素相等

> 原文:[https://www . geesforgeks . org/子阵列最大长度-这样子阵列中的所有元素都是相等的/](https://www.geeksforgeeks.org/maximum-length-of-subarray-such-that-all-elements-are-equal-in-the-subarray/)

给定一个由 N 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到包含相似元素的最大长度子数组。
**例:**

> **输入:** arr[] = {1，2，3，4，5，5，5，5，2，2，1，1}
> **输出:** 5
> **解释:**
> 子阵列{5，5，5，5，5，5}的最大长度为 5，元素相同。
> **输入:** arr[] = {1，2，3，4}
> **输出:** 1
> **解释:**
> 所有相同的元素子阵列都是{1}、{2}、{3}和长度为 1 的{4}。

**方法:**思路是遍历数组存储相同元素的子阵的**最大长度**和**当前长度**。以下是步骤:

1.  遍历数组并检查当前元素是否等于下一个元素，然后增加当前长度变量的值。
2.  现在，将当前长度与最大长度进行比较，以更新子阵列的最大长度。
3.  如果当前元素不等于下一个元素，则将长度重置为 **1** ，并对数组的所有元素继续此操作。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the longest
// subarray with same element
int longest_subarray(int arr[], int d)
{

    int i = 0, j = 1, e = 0;

    for (i = 0; i < d - 1; i++) {

        // Check if the elements
        // are same then we can
        // increment the length
        if (arr[i] == arr[i + 1]) {
            j = j + 1;
        }
        else {

            // Reinitialize j
            j = 1;
        }

        // Compare the maximum
        // length e with j
        if (e < j) {
            e = j;
        }
    }

    // Return max length
    return e;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << longest_subarray(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the longest
// subarray with same element
static int longest_subarray(int arr[], int d)
{
    int i = 0, j = 1, e = 0;

    for(i = 0; i < d - 1; i++)
    {

       // Check if the elements
       // are same then we can
       // increment the length
       if (arr[i] == arr[i + 1])
       {
           j = j + 1;
       }
       else
       {

           // Reinitialize j
           j = 1;
       }

       // Compare the maximum
       // length e with j
       if (e < j)
       {
           e = j;
       }
    }

    // Return max length
    return e;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;

    // Function Call
    System.out.print(longest_subarray(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the longest
# subarray with same element
def longest_subarray(arr, d):

    (i, j, e) = (0, 1, 0)

    for i in range(d - 1):

        # Check if the elements
        # are same then we can
        # increment the length
        if arr[i] == arr[i + 1]:
            j += 1
        else:

            # Reinitialize j
            j = 1

        # Compare the maximum
        # length e with j
        if e < j:
            e = j

    # Return max length
    return e

# Driver code

# Given list arr[]
arr = [ 1, 2, 3, 4 ]
N = len(arr)

# Function call
print(longest_subarray(arr, N))

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the longest
// subarray with same element
static int longest_subarray(int []arr, int d)
{
    int i = 0, j = 1, e = 0;

    for(i = 0; i < d - 1; i++)
    {

       // Check if the elements
       // are same then we can
       // increment the length
       if (arr[i] == arr[i + 1])
       {
           j = j + 1;
       }
       else
       {

           // Reinitialize j
           j = 1;
       }

       // Compare the maximum
       // length e with j
       if (e < j)
       {
           e = j;
       }
    }

    // Return max length
    return e;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    // Function Call
    Console.Write(longest_subarray(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to find the longest
    // subarray with same element
    function longest_subarray(arr , d)
    {
        var i = 0, j = 1, e = 0;

        for (i = 0; i < d - 1; i++)
        {

            // Check if the elements
            // are same then we can
            // increment the length
            if (arr[i] == arr[i + 1])
            {
                j = j + 1;
            }
            else
            {

                // Reinitialize j
                j = 1;
            }

            // Compare the maximum
            // length e with j
            if (e < j) {
                e = j;
            }
        }

        // Return max length
        return e;
    }

    // Driver Code

        // Given array arr
        var arr = [ 1, 2, 3, 4 ];
        var N = arr.length;

        // Function Call
        document.write(longest_subarray(arr, N));

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
1
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*