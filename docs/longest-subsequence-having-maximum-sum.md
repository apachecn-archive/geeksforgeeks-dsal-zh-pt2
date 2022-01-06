# 具有最大和的最长子序列

> 原文:[https://www . geesforgeks . org/最长子序列具有最大和/](https://www.geeksforgeeks.org/longest-subsequence-having-maximum-sum/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定数组中找到最长的非空[子序列，其和最大。](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)

**示例:**

> **输入:** arr[] = { 1，2，-4，-2，3，0 }
> **输出:** 1 2 3 0
> **解释:**
> 子序列{ 1，2，3，0 }的元素之和为 6，这是最大可能的和。
> 因此，要求的输出是 1 2 3 0
> 
> **输入:** arr[] = { -10，-6，-2，-3，-4 }
> 输出: -2

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)的所有可能的子序列，并计算它们的和。用最大和打印所有子序列中最长的。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**有效途径:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化一个变量，比如说 **maxm** ，来存储给定数组的[最大元素。](https://www.geeksforgeeks.org/how-to-find-the-maximum-element-of-an-array-using-stl-in-c/)
*   如果 **maxm < 0** ，则打印 **maxm** 的值。
*   否则，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并打印所有正数组元素。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subsequence
// from the given array with maximum sum
void longestSubWithMaxSum(int arr[], int N)
{
    // Stores the largest element
    // of the array
    int Max = *max_element(arr,
                           arr + N);

    // If Max is less than 0
    if (Max < 0) {

        // Print the largest element
        // of the array
        cout << Max;
        return;
    }

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If arr[i] is greater
        // than or equal to 0
        if (arr[i] >= 0) {

            // Print elements of
            // the subsequence
            cout << arr[i] << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, -4, -2, 3, 0 };

    int N = sizeof(arr) / sizeof(arr[0]);

    longestSubWithMaxSum(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the longest subsequence
// from the given array with maximum sum
static void longestSubWithMaxSum(int arr[], int N)
{

    // Stores the largest element
    // of the array
    int Max = Arrays.stream(arr).max().getAsInt();

    // If Max is less than 0
    if (Max < 0)
    {

        // Print the largest element
        // of the array
        System.out.print(Max);
        return;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is greater
        // than or equal to 0
        if (arr[i] >= 0)
        {

            // Print elements of
            // the subsequence
            System.out.print(arr[i] + " ");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, -4, -2, 3, 0 };
    int N = arr.length;

    longestSubWithMaxSum(arr, N);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the longest subsequence
# from the given array with maximum sum
def longestSubWithMaxSum(arr, N):

    # Stores the largest element
    # of the array
    Max = max(arr)

    # If Max is less than 0
    if (Max < 0) :

        # Print the largest element
        # of the array
        print(Max)
        return

    # Traverse the array
    for i in range(N):

        # If arr[i] is greater
        # than or equal to 0
        if (arr[i] >= 0) :

            # Print elements of
            # the subsequence
            print(arr[i], end = " ")

# Driver code
arr = [ 1, 2, -4, -2, 3, 0 ]

N = len(arr)

longestSubWithMaxSum(arr, N)

# This code is contributed divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the longest subsequence
// from the given array with maximum sum
static void longestSubWithMaxSum(int []arr,
                                 int N)
{

    // Stores the largest element
    // of the array
    int Max = arr[0];

    for(int i = 1; i < N; i++)
    {
        if (Max < arr[i])
            Max = arr[i];
    }

    // If Max is less than 0
    if (Max < 0)
    {

        // Print the largest element
        // of the array
        Console.Write(Max);
        return;
    }

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If arr[i] is greater
        // than or equal to 0
        if (arr[i] >= 0)
        {

            // Print elements of
            // the subsequence
            Console.Write(arr[i] + " ");
        }
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, -4, -2, 3, 0 };
    int N = arr.Length;

    longestSubWithMaxSum(arr, N);
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the longest subsequence
// from the given array with maximum sum
function longestSubWithMaxSum(arr, N)
{    

    // Stores the largest element
    // of the array
    let Max = Math.max(...arr);

    // If Max is less than 0
    if (Max < 0)
    {

        // Print the largest element
        // of the array
        document.write(Max);
        return;
    }

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // If arr[i] is greater
        // than or equal to 0
        if (arr[i] >= 0)
        {

            // Print the elements of
            // the subsequence
            document.write(arr[i] + " ");
        }
    }
}

// Driver code
let arr = [ 1, 2, -4, -2, 3, 0 ];
let N = arr.length;

longestSubWithMaxSum(arr, N);

// This code is contributed by avijitmondal1998

</script>
```

**Output:** 

```
1 2 3 0
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)