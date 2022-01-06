# 具有增加的连续元素的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长连续元素子数组长度/](https://www.geeksforgeeks.org/length-of-longest-subarray-with-increasing-contiguous-elements/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** ，任务是从[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)中找出最长的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度，该子数组由连续的数字以递增的顺序组成。

**示例:**

> **输入:** arr[] = {2，3，4，6，7，8，9，10}
> **输出:** 5
> **说明:**子阵{6，7，8，9，10}是满足给定条件的最长子阵。因此，所需的输出为 5。
> 
> **输入:** arr[] = {4，5，1，2，3，4，9，10，11，12 }
> T3】输出: 4

**天真法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个索引 ***i*** ，从超索引开始遍历，从 **i** 开始寻找满足给定条件的最长子数组的长度。将 I 移至不满足条件的索引，并从该索引中进行检查。最后，打印获得的这种子阵列的最大长度。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subarray
// with increasing contiguous elements
int maxiConsecutiveSubarray(int arr[], int N)
{

    // Stores the length of
    // required longest subarray
    int maxi = 0;

    for (int i = 0; i < N - 1; i++) {

        // Stores the length of length of longest
        // such subarray from ith index
        int cnt = 1, j;

        for (j = i; j < N; j++) {

            // If consecutive elements are
            // increasing and differ by 1
            if (arr[j + 1] == arr[j] + 1) {
                cnt++;
            }

            // Otherwise
            else {
                break;
            }
        }

        // Update the longest subarray
        // obtained so far
        maxi = max(maxi, cnt);
        i = j;
    }

    // Return the length obtained
    return maxi;
}

// Driver Code
int main()
{
    int N = 11;
    int arr[] = { 1, 3, 4, 2, 3, 4,
                  2, 3, 5, 6, 7 };

    cout << maxiConsecutiveSubarray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG{

// Function to find the longest subarray
// with increasing contiguous elements
public static int maxiConsecutiveSubarray(int arr[],
                                          int N)
{

    // Stores the length of
    // required longest subarray
    int maxi = 0;

    for(int i = 0; i < N - 1; i++)
    {

        // Stores the length of length of
        // longest such subarray from ith
        // index
        int cnt = 1, j;

        for(j = i; j < N - 1; j++)
        {

            // If consecutive elements are
            // increasing and differ by 1
            if (arr[j + 1] == arr[j] + 1)
            {
                cnt++;
            }

            // Otherwise
            else
            {
                break;
            }
        }

        // Update the longest subarray
        // obtained so far
        maxi = Math.max(maxi, cnt);
        i = j;
    }

    // Return the length obtained
    return maxi;
}

// Driver Code
public static void main(String args[])
{
    int N = 11;
    int arr[] = { 1, 3, 4, 2, 3, 4,
                  2, 3, 5, 6, 7 };

    System.out.println(maxiConsecutiveSubarray(arr, N));
}
}

// This code is contributed by hemanth gadarla
```

## 蟒蛇 3

```
# Python3 implementation for
# the above approach

# Function to find the longest
# subarray with increasing
# contiguous elements
def maxiConsecutiveSubarray(arr, N):

    # Stores the length of
    # required longest subarray
    maxi = 0;

    for i in range(N - 1):
        # Stores the length of
        # length of longest such
        # subarray from ith index
        cnt = 1;

        for j in range(i, N - 1):

            # If consecutive elements are
            # increasing and differ by 1
            if (arr[j + 1] == arr[j] + 1):
                cnt += 1;

            # Otherwise
            else:
                break;

        # Update the longest subarray
        # obtained so far
        maxi = max(maxi, cnt);
        i = j;

    # Return the length obtained
    return maxi;

# Driver Code
if __name__ == '__main__':

    N = 11;
    arr = [1, 3, 4, 2, 3,
           4, 2, 3, 5, 6, 7];

    print(maxiConsecutiveSubarray(arr, N));

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation for the
// above approach
using System;
class GFG{

// Function to find the longest
// subarray with increasing
// contiguous elements
public static int maxiConsecutiveSubarray(int []arr,
                                          int N)
{   
  // Stores the length of
  // required longest subarray
  int maxi = 0;

  for(int i = 0; i < N - 1; i++)
  {
    // Stores the length of
    // length of longest such
    // subarray from ith index
    int cnt = 1, j;

    for(j = i; j < N - 1; j++)
    {
      // If consecutive elements are
      // increasing and differ by 1
      if (arr[j + 1] == arr[j] + 1)
      {
        cnt++;
      }

      // Otherwise
      else
      {
        break;
      }
    }

    // Update the longest subarray
    // obtained so far
    maxi = Math.Max(maxi, cnt);
    i = j;
  }

  // Return the length
  // obtained
  return maxi;
}

// Driver Code
public static void Main(String []args)
{
  int N = 11;
  int []arr = {1, 3, 4, 2, 3, 4,
               2, 3, 5, 6, 7};
  Console.WriteLine(
          maxiConsecutiveSubarray(arr, N));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the longest subarray
// with increasing contiguous elements
function maxiConsecutiveSubarray(arr, N)
{

    // Stores the length of
    // required longest subarray
    let maxi = 0;

    for(let i = 0; i < N - 1; i++)
    {

        // Stores the length of length of
        // longest such subarray from ith
        // index
        let cnt = 1, j;

        for(j = i; j < N - 1; j++)
        {

            // If consecutive elements are
            // increasing and differ by 1
            if (arr[j + 1] == arr[j] + 1)
            {
                cnt++;
            }

            // Otherwise
            else
            {
                break;
            }
        }

        // Update the longest subarray
        // obtained so far
        maxi = Math.max(maxi, cnt);
        i = j;
    }

    // Return the length obtained
    return maxi;
}

    // Driver Code

    let  N = 11;
    let arr = [ 1, 3, 4, 2, 3, 4,
                  2, 3, 5, 6, 7 ];

    document.write(maxiConsecutiveSubarray(arr, N));

</script>
```

**Output**

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)