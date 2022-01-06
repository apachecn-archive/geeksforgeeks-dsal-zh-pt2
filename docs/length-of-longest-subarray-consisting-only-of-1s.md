# 仅由 1s 组成的最长子阵列的长度

> 原文:[https://www . geeksforgeeks . org/最长子阵列长度-仅由-1s 组成/](https://www.geeksforgeeks.org/length-of-longest-subarray-consisting-only-of-1s/)

给定一个由二进制值组成的大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是在移除单个数组元素后找到仅由 **1** s 组成的最长非空子数组。

**示例:**

> **输入:** arr[] = {1，1，1 }
> T3】输出: 2
> 
> **输入:** arr[] = {0，0，0 }
> T3】输出: 0

**方法:**按照以下步骤解决问题:

*   初始化三个变量， **newLen = 0** ， **prevLen = 0** ， **maxLen = 0** 。
*   [通过在开头添加零来遍历数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **arr[]** :
    *   **如果 arr[i] = 1:** 将两个**纽伦** & **prevLen** 增加 **1** 。
    *   否则:
        *   将最大值赋给变量 **maxLen** 。
        *   设置 **prevLen = newLen** 和 **newLen = 0** 。
*   打印**maxLen**if**maxLen<len(arr)**。
*   否则，打印**maxLen–1**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to find the length of
// longest subarray containing only 1s
int longestSubarrayUtil(vector<int> arr, int n)
{
    int neww = 0, old = 0, m = 0;

    // Traverse the array
    for(int x = 0; x <= n; x++)
    {

        // If array element is 1
        if (arr[x] == 1)
        {

            // Increment both by 1
            neww += 1;
            old += 1;
        }
        else
        {

            // Assign maximum value
            m = max(m, old);

            //Assign new to old
            // and set new to zero
            old = neww;
            neww = 0;
        }
    }

    // Return the final length
    if (m < n)
    {
        return m;
    }
    else return m - 1;
}

// Function to find length of the
// longest subarray containing only 1's
void longestSubarray(vector<int> arr, int n)
{

    // Stores the length of longest
    // subarray consisting of 1s
    int len = longestSubarrayUtil(arr, n);

    // Print the length
    // of the subarray
    cout << len;
}

// Driver code
int main()
{

    // Given array
    vector<int> arr = {1, 1, 1};
    int n = arr.size();

    // Append 0 at beginning
    for(int i = n; i >= 0; i--)
    {
        arr[i] = arr[i - 1];
    }
    arr[0] = 0;

    // Function call to find the longest
    // subarray containing only 1's
    longestSubarray(arr, n);
}

// This code is contributed by SoumikMondal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Utility function to find the length of
// longest subarray containing only 1s
static int longestSubarrayUtil(int [] arr, int n)
{
    int neww = 0, old = 0, m = 0;

    // Traverse the array
    for(int x = 0; x <n; x++)
    {

        // If array element is 1
        if (arr[x] == 1)
        {

            // Increment both by 1
            neww += 1;
            old += 1;
        }
        else
        {

            // Assign maximum value
            m = Math.max(m, old);

            //Assign new to old
            // and set new to zero
            old = neww;
            neww = 0;
        }
    }
    m = Math.max(m, old);
    // Return the final length
    if(m<n)
        return m;
    else
        return m-1;
}

// Function to find length of the
// longest subarray containing only 1's
static void longestSubarray(int []arr, int n)
{

    // Stores the length of longest
    // subarray consisting of 1s
    int len = longestSubarrayUtil(arr, n);

    // Print the length
    // of the subarray
    System.out.print(len);
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int arr[] = {1, 1, 1};
    int n = arr.length;

    // Function call to find the longest
    // subarray containing only 1's
    longestSubarray(arr, n);
}
}

// This ode is contributed by amreshkumar3.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Utility function to find the length of
# longest subarray containing only 1s
def longestSubarrayUtil(arr):

    new, old, m = 0, 0, 0

    # Traverse the array
    for x in arr+[0]:

        # If array element is 1
        if x == 1:

            # Increment both by 1
            new += 1
            old += 1
        else:

            # Assign maximum value
            m = max(m, old)

            # Assign new to old
            # and set new to zero
            old, new = new, 0

    # Return the final length
    return m if m < len(arr) else m - 1

# Function to find length of the
# longest subarray containing only 1's
def longestSubarray(arr):

    # Stores the length of longest
    # subarray consisting of 1s
    len = longestSubarrayUtil(arr)

    # Print the length
    # of the subarray
    print(len)

# Given array
arr = [1, 1, 1]

# Function call to find the longest
# subarray containing only 1's
longestSubarray(arr)
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Utility function to find the length of
// longest subarray containing only 1s
function longestSubarrayUtil(arr, n)
{
    var neww = 0, old = 0, m = 0;

    // Traverse the array
    for(var x = 0; x <= n; x++)
    {

        // If array element is 1
        if (arr[x] == 1)
        {

            // Increment both by 1
            neww += 1;
            old += 1;
        }
        else
        {

            // Assign maximum value
            m = Math.max(m, old);

            //Assign new to old
            // and set new to zero
            old = neww;
            neww = 0;
        }
    }

    // Return the final length
    if (m < n)
    {
        return m;
    }
    else
    {
        return m - 1;
    }
}

// Function to find length of the
// longest subarray containing only 1's
function longestSubarray(arr, n)
{

    // Stores the length of longest
    // subarray consisting of 1s
    var len = longestSubarrayUtil(arr, n);

    // Print the length
    // of the subarray
    document.write( len);
}

// Driver code
// Given array
var arr = [1, 1, 1];
var n = arr.length;

// Append 0 at beginning
for(var i = n-1; i >= 0; i--)
{
    arr[i] = arr[i - 1];
}
arr[0] = 0;

// Function call to find the longest
// subarray containing only 1's
longestSubarray(arr, n);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)