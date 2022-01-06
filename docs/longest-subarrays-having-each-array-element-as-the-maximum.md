# 每个阵列元素为最大值的最长子阵列

> 原文:[https://www . geeksforgeeks . org/最长子阵列-以每个阵列元素为最大值/](https://www.geeksforgeeks.org/longest-subarrays-having-each-array-element-as-the-maximum/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是为每个数组元素 **arr[i]** 找到最长的子数组，其中包含 arr[i]作为最大值。

**示例:**

> **输入:** arr[] = {1，2，3，0，1}
> **输出:** 1 2 5 1 2
> **解释:**
> 以 arr[0]为最大的最长子阵列为{1}
> 以 arr[1]为最大的最长子阵列为{1，2}
> 以 arr[2]为最大的最长子阵列为{1，2，3，0，1}
> 最长子阵列为 arr
> 
> **输入:** arr[] = {3，3，3，1，6，2 }
> T3】输出:【4 4 4 1 6 1

**方法:**思路是使用[双指针](https://www.geeksforgeeks.org/two-pointers-technique/)技术解决问题:

*   初始化两个指针，*左*和*右*。使得对于每个元素 **arr[i]** ，左边的**指向索引**【I–1，0】**，以连续的方式找到小于或等于 arr[i]的元素。一旦找到大于**arr【I】**的元素，指针就会停止。**
*   **类似地，**右侧**指向索引**【I+1，n–1】**以连续方式查找小于或等于**arr【I】**的元素，并停止查找大于 arr【I】的任何元素。**
*   **因此**arr【I】**最大的最大邻接子阵列长度为 **1 +右–左**。**
*   **对每个数组元素重复上述步骤。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length of
// Subarrays for each element of the array
// having it as the maximum
void solve(int n, int arr[])
{
    int i, ans = 0;
    for (i = 0; i < n; i++) {

        // Initialize the bounds
        int left = max(i - 1, 0);
        int right = min(n - 1, i + 1);

        // Iterate to find greater
        // element on the left
        while (left >= 0) {

            // If greater element is found
            if (arr[left] > arr[i]) {
                left++;
                break;
            }

            // Decrement left pointer
            left--;
        }

        // If boundary is exceeded
        if (left < 0)
            left++;

        // Iterate to find greater
        // element on the right
        while (right < n) {

            // If greater element is found
            if (arr[right] > arr[i]) {
                right--;
                break;
            }
            // Increment right pointer
            right++;
        }

        // If boundary is exceeded
        if (right >= n)
            right--;

        // Length of longest subarray where
        // arr[i] is the largest
        ans = 1 + right - left;

        // Print the answer
        cout << ans << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 1 };
    int n = sizeof arr / sizeof arr[0];

    solve(n, arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java Program to implement
// the above approach
import java.util.*;
class GFG{

// Function to find the maximum length of
// Subarrays for each element of the array
// having it as the maximum
static void solve(int n, int arr[])
{
    int i, ans = 0;
    for (i = 0; i < n; i++)
    {

        // Initialize the bounds
        int left = Math.max(i - 1, 0);
        int right = Math.min(n - 1, i + 1);

        // Iterate to find greater
        // element on the left
        while (left >= 0)
        {

            // If greater element is found
            if (arr[left] > arr[i])
            {
                left++;
                break;
            }

            // Decrement left pointer
            left--;
        }

        // If boundary is exceeded
        if (left < 0)
            left++;

        // Iterate to find greater
        // element on the right
        while (right < n)
        {

            // If greater element is found
            if (arr[right] > arr[i])
            {
                right--;
                break;
            }

            // Increment right pointer
            right++;
        }

        // If boundary is exceeded
        if (right >= n)
            right--;

        // Length of longest subarray where
        // arr[i] is the largest
        ans = 1 + right - left;

        // Print the answer
        System.out.print(ans + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 4, 2, 1 };
    int n = arr.length;

    solve(n, arr);
}
}

// This code is contributed by Rajput-Ji
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach

# Function to find the maximum length of
# Subarrays for each element of the array
# having it as the maximum
def solve(n, arr):

    ans = 0

    for i in range(n):

        # Initialise the bounds
        left = max(i - 1, 0)
        right = min(n - 1, i + 1)

        # Iterate to find greater
        # element on the left
        while left >= 0:

            # If greater element is found
            if arr[left] > arr[i]:
                left += 1
                break

            # Decrement left pointer
            left -= 1

        # If boundary is exceeded
        if left < 0:
            left += 1

        # Iterate to find greater
        # element on the right
        while right < n:

            # If greater element is found
            if arr[right] > arr[i]:
                right -= 1
                break

            # Increment right pointer
            right += 1

        # if boundary is exceeded
        if right >= n:
            right -= 1

        # Length of longest subarray where
        # arr[i] is the largest
        ans = 1 + right - left

        # Print the answer
        print(ans, end = " ")

# Driver code
arr = [ 4, 2, 1 ]
n = len(arr)

solve(n, arr)

# This code is contributed by Stuti Pathak
```

## **C#**

```
// C# Program to implement
// the above approach
using System;
class GFG{

// Function to find the maximum length of
// Subarrays for each element of the array
// having it as the maximum
static void solve(int n, int []arr)
{
    int i, ans = 0;
    for (i = 0; i < n; i++)
    {

        // Initialize the bounds
        int left = Math.Max(i - 1, 0);
        int right = Math.Min(n - 1, i + 1);

        // Iterate to find greater
        // element on the left
        while (left >= 0)
        {

            // If greater element is found
            if (arr[left] > arr[i])
            {
                left++;
                break;
            }

            // Decrement left pointer
            left--;
        }

        // If boundary is exceeded
        if (left < 0)
            left++;

        // Iterate to find greater
        // element on the right
        while (right < n)
        {

            // If greater element is found
            if (arr[right] > arr[i])
            {
                right--;
                break;
            }

            // Increment right pointer
            right++;
        }

        // If boundary is exceeded
        if (right >= n)
            right--;

        // Length of longest subarray where
        // arr[i] is the largest
        ans = 1 + right - left;

        // Print the answer
        Console.Write(ans + " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 4, 2, 1 };
    int n = arr.Length;

    solve(n, arr);
}
}

// This code is contributed by Princi Singh
```

## **java 描述语言**

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the maximum length of
// Subarrays for each element of the array
// having it as the maximum
function solve(n, arr)
{
    let i, ans = 0;
    for (i = 0; i < n; i++)
    {

        // Initialize the bounds
        let left = Math.max(i - 1, 0);
        let right = Math.min(n - 1, i + 1);

        // Iterate to find greater
        // element on the left
        while (left >= 0)
        {

            // If greater element is found
            if (arr[left] > arr[i])
            {
                left++;
                break;
            }

            // Decrement left pointer
            left--;
        }

        // If boundary is exceeded
        if (left < 0)
            left++;

        // Iterate to find greater
        // element on the right
        while (right < n)
        {

            // If greater element is found
            if (arr[right] > arr[i])
            {
                right--;
                break;
            }

            // Increment right pointer
            right++;
        }

        // If boundary is exceeded
        if (right >= n)
            right--;

        // Length of longest subarray where
        // arr[i] is the largest
        ans = 1 + right - left;

        // Print the answer
        document.write(ans + " ");
    }
}

// Driver Code

    let arr = [ 4, 2, 1 ];
    let n = arr.length;

    solve(n, arr);

</script>
```

****Output:** 

```
3 2 1
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***