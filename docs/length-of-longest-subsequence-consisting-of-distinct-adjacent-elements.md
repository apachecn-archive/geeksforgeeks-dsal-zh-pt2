# 由不同的相邻元素组成的最长子序列的长度

> 原文:[https://www . geesforgeks . org/最长子序列长度-由不同的相邻元素组成/](https://www.geeksforgeeks.org/length-of-longest-subsequence-consisting-of-distinct-adjacent-elements/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到数组 **arr[]** 中最长的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，使得子序列中所有相邻的元素都不同。

**示例:**

> **输入:** arr[] = {4，2，3，4，3}
> **输出:** 5
> **解释:**
> 相邻元素不相等的最长子序列是{4，2，3，4，3}。子序列的长度是 5。
> 
> **输入:** arr[] = {7，8，1，2，2，5，5，1}
> **输出:** 6
> **解释:**相邻元素不相等的最长子序列是{7，8，1，2，5，1}。子序列的长度是 5。

**天真方法:**最简单的方法是[生成给定数组的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，并打印所有相邻元素都不同的子序列的最大长度。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**按照以下步骤解决问题:

*   初始化**计数**到 **1** 存储最长[子序列](https://www.geeksforgeeks.org/tag/subsequence/)的长度。
*   [在索引**【1，N-1】**上遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个元素，检查当前元素是否等于前一个元素。如果发现不相等，则按 **1** 递增**计数**。
*   完成上述步骤后，打印**计数**的值作为子序列的最大可能长度。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the length of
// longest subsequence having different
// adjacent elements
void longestSubsequence(int arr[], int N)
{
    // Stores the length of the
    // longest subsequence
    int count = 1;

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // If previous and current
        // element are not same
        if (arr[i] != arr[i - 1]) {

            // Increment the count
            count++;
        }
    }

    // Print the maximum length
    cout << count << endl;
}

// Driver Code
int main()
{
    int arr[] = { 7, 8, 1, 2, 2, 5, 5, 1 };

    // Size of Array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    longestSubsequence(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;

class GFG{

// Function that finds the length of
// longest subsequence having different
// adjacent elements
static void longestSubsequence(int arr[],
                               int N)
{
  // Stores the length of the
  // longest subsequence
  int count = 1;

  // Traverse the array
  for (int i = 1; i < N; i++)
  {
    // If previous and current
    // element are not same
    if (arr[i] != arr[i - 1])
    {
      // Increment the count
      count++;
    }
  }

  // Print the maximum length
  System.out.println(count);
}

// Driver Code
public static void main(String args[])
{
  int arr[] = {7, 8, 1, 2,
               2, 5, 5, 1};

  // Size of Array
  int N = arr.length;

  // Function Call
  longestSubsequence(arr, N);
}
}

// This code is contributed by bgangwar59
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the length of
# longest subsequence having different
# adjacent elements
def longestSubsequence(arr, N):

    # Stores the length of the
    # longest subsequence
    count = 1

    # Traverse the array
    for i in range(1, N, 1):

        # If previous and current
        # element are not same
        if (arr[i] != arr[i - 1]):

            # Increment the count
            count += 1

    # Print the maximum length
    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 7, 8, 1, 2, 2, 5, 5, 1 ]

    # Size of Array
    N = len(arr)

    # Function Call
    longestSubsequence(arr, N)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the
// above approach
using System;

class GFG{

// Function that finds the length of
// longest subsequence having different
// adjacent elements
static void longestSubsequence(int[] arr,
                               int N)
{

  // Stores the length of the
  // longest subsequence
  int count = 1;

  // Traverse the array
  for(int i = 1; i < N; i++)
  {

    // If previous and current
    // element are not same
    if (arr[i] != arr[i - 1])
    {

      // Increment the count
      count++;
    }
  }

  // Print the maximum length
  Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
  int[] arr = { 7, 8, 1, 2,
                2, 5, 5, 1 };

  // Size of Array
  int N = arr.Length;

  // Function Call
  longestSubsequence(arr, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function that finds the length of
// longest subsequence having different
// adjacent elements
function longestSubsequence(arr, N)
{
  // Stores the length of the
  // longest subsequence
  let count = 1;

  // Traverse the array
  for (let i = 1; i < N; i++)
  {
    // If previous and current
    // element are not same
    if (arr[i] != arr[i - 1])
    {
      // Increment the count
      count++;
    }
  }

  // Prlet the maximum length
  document.write(count);
}

// Driver Code

    let arr = [7, 8, 1, 2,
               2, 5, 5, 1];

  // Size of Array
  let N = arr.length;

  // Function Call
  longestSubsequence(arr, N);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)