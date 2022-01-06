# 符号交替的最大长度子序列和最大和

> 原文:[https://www . geeksforgeeks . org/最大长度子序列带交替符号和最大和/](https://www.geeksforgeeks.org/maximum-length-subsequence-with-alternating-sign-and-maximum-sum/)

给定大小为 n 的**数组 arr[]** ，该数组具有除零之外的正整数和负整数。任务是找到具有最大大小和最大和的交替符号的子序列，也就是说，在子序列中，每个相邻元素的符号是相反的，例如，如果第一个元素是正的，那么第二个元素必须是负的，然后是另一个正整数，以此类推。
**例:**

```
Input: arr[] = {2, 3, 7, -6, -4}
Output: 7 -4
Explanation:
Possible subsequences are [2, -6] [2, -4] [3, -6] [3, -4] [7, -6] [7, -4].
Out of these [7, -4] has the maximum sum. 

Input: arr[] = {-4, 9, 4, 11, -5, -17, 9, -3, -5, 2}
Output: -4 11 -5 9 -3 2  
```

**方法:**
解决上述问题的主要思路是**从由相同符号组成的数组的线段**中找到最大元素，这意味着我们必须在连续的正元素和连续的负元素中选择最大元素。由于我们想要最大的尺寸，我们将只从每个片段中提取一个元素，并且为了最大化总和，我们需要提取每个片段的最大元素。
**下面是上述方法的实现:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to find the
// subsequence with alternating sign
// having maximum size and maximum sum.

#include <bits/stdc++.h>
using namespace std;

// Function to find the subsequence
// with alternating sign having
// maximum size and maximum sum.
void findSubsequence(int arr[], int n)
{
    int sign[n] = { 0 };

    // Find whether each element
    // is positive or negative
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0)
            sign[i] = 1;
        else
            sign[i] = -1;
    }

    int k = 0;
    int result[n] = { 0 };

    // Find the required subsequence
    for (int i = 0; i < n; i++) {

        int cur = arr[i];
        int j = i;

        while (j < n && sign[i] == sign[j]) {

            // Find the maximum element
            // in the specified range
            cur = max(cur, arr[j]);
            ++j;
        }

        result[k++] = cur;

        i = j - 1;
    }

    // print the result
    for (int i = 0; i < k; i++)
        cout << result[i] << " ";
    cout << "\n";
}

// Driver code
int main()
{
    // array declaration
    int arr[] = { -4, 9, 4, 11, -5, -17, 9, -3, -5, 2 };

    // size of array
    int n = sizeof(arr) / sizeof(arr[0]);

    findSubsequence(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// subsequence with alternating sign
// having maximum size and maximum sum.
class GFG{

// Function to find the subsequence
// with alternating sign having
// maximum size and maximum sum.
static void findSubsequence(int arr[], int n)
{
    int sign[] = new int[n];

    // Find whether each element
    // is positive or negative
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0)
            sign[i] = 1;
        else
            sign[i] = -1;
    }

    int k = 0;
    int result[] = new int[n];

    // Find the required subsequence
    for (int i = 0; i < n; i++) {

        int cur = arr[i];
        int j = i;

        while (j < n && sign[i] == sign[j]) {

            // Find the maximum element
            // in the specified range
            cur = Math.max(cur, arr[j]);
            ++j;
        }

        result[k++] = cur;

        i = j - 1;
    }

    // print the result
    for (int i = 0; i < k; i++)
        System.out.print(result[i]+ " ");
    System.out.print("\n");
}

// Driver code
public static void main(String[] args)
{
    // array declaration
    int arr[] = { -4, 9, 4, 11, -5, -17, 9, -3, -5, 2 };

    // size of array
    int n = arr.length;

    findSubsequence(arr, n);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation to find the
# subsequence with alternating sign
# having maximum size and maximum sum.

# Function to find the subsequence
# with alternating sign having
# maximum size and maximum sum.
def findSubsequence(arr, n):
    sign = [0]*n

    # Find whether each element
    # is positive or negative
    for i in range(n):
        if (arr[i] > 0):
            sign[i] = 1
        else:
            sign[i] = -1

    k = 0
    result = [0]*n

    # Find the required subsequence
    i = 0
    while i < n:

        cur = arr[i]
        j = i

        while (j < n and sign[i] == sign[j]):

            # Find the maximum element
            # in the specified range
            cur = max(cur, arr[j])
            j += 1

        result[k] = cur
        k += 1

        i = j - 1
        i += 1

    # print the result
    for i in range(k):
        print(result[i],end=" ")

# Driver code
if __name__ == '__main__':
    # array declaration
    arr=[-4, 9, 4, 11, -5, -17, 9, -3, -5, 2]

    # size of array
    n = len(arr)

    findSubsequence(arr, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to find the
// subsequence with alternating sign
// having maximum size and maximum sum.
using System;

public class GFG{

// Function to find the subsequence
// with alternating sign having
// maximum size and maximum sum.
static void findSubsequence(int []arr, int n)
{
    int []sign = new int[n];

    // Find whether each element
    // is positive or negative
    for (int i = 0; i < n; i++) {
        if (arr[i] > 0)
            sign[i] = 1;
        else
            sign[i] = -1;
    }

    int k = 0;
    int []result = new int[n];

    // Find the required subsequence
    for (int i = 0; i < n; i++) {

        int cur = arr[i];
        int j = i;

        while (j < n && sign[i] == sign[j]) {

            // Find the maximum element
            // in the specified range
            cur = Math.Max(cur, arr[j]);
            ++j;
        }

        result[k++] = cur;

        i = j - 1;
    }

    // print the result
    for (int i = 0; i < k; i++)
        Console.Write(result[i]+ " ");
    Console.Write("\n");
}

// Driver code
public static void Main(String[] args)
{
    // array declaration
    int []arr = { -4, 9, 4, 11, -5, -17, 9, -3, -5, 2 };

    // size of array
    int n = arr.Length;

    findSubsequence(arr, n);
}
}
// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// subsequence with alternating sign
// having maximum size and maximum sum.

// Function to find the subsequence
// with alternating sign having
// maximum size and maximum sum.
function findSubsequence(arr, n)
{
    let sign = Array.from({length: n}, (_, i) => 0);

    // Find whether each element
    // is positive or negative
    for (let i = 0; i < n; i++)
    {
        if (arr[i] > 0)
            sign[i] = 1;
        else
            sign[i] = -1;
    }

    let k = 0;
    let result = Array.from({length: n}, (_, i) => 0);

    // Find the required subsequence
    for (let i = 0; i < n; i++) {

        let cur = arr[i];
        let j = i;

        while (j < n && sign[i] == sign[j]) {

            // Find the maximum element
            // in the specified range
            cur = Math.max(cur, arr[j]);
            ++j;
        }

        result[k++] = cur;

        i = j - 1;
    }

    // prlet the result
    for (let i = 0; i < k; i++)
        document.write(result[i]+ " ");
    document.write("<br/>");
}

// Driver Code

    // array declaration
    let arr = [ -4, 9, 4, 11, -5, -17, 9, -3, -5, 2 ];

    // size of array
    let n = arr.length;

    findSubsequence(arr, n);

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
-4 11 -5 9 -3 2
```

**时间复杂度:** O(N)

**辅助空间:** O(N)