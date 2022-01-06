# 通过最多 K 次替换来最小化数组的最大值和最小值之间的差异

> 原文:[https://www . geeksforgeeks . org/最小化最多 k 个替换的最大和最小阵列之间的差异/](https://www.geeksforgeeks.org/minimize-difference-between-maximum-and-minimum-of-array-by-at-most-k-replacements/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**和一个**T5】整数 **K** ，任务是选择数组中最多 K 个**元素**，并用任意数字替换。最多执行**K 次替换后，求数组最大值和最小值的最小差。****

**示例:**

> **输入:** arr[] = {1，4，6，11，15}，k = 3
> **输出:** 2
> **解释:**
> k = 1，arr = {4，4，6，11，15}，arr[0]替换为 4
> k = 2，arr = {4，4，6，4，15}，arr[3]替换为 4
> k = 3，arr = {4，4，6，6
> 
> **输入:** arr[] = {1，4，6，11，15}，k = 2
> **输出:** 5
> **解释:**
> k = 1，arr = {1，4，6，6，15}，arr[3]替换为 6
> k = 2，arr = {1，4，6，6，6}，arr[4]替换为 6
> Max–Min = 6–1 = 5

**方法:**思路是用[两个指针](https://www.geeksforgeeks.org/two-pointers-technique/)的概念。以下是步骤:

1.  [给定数组排序](https://www.geeksforgeeks.org/sorting-algorithms/)。
2.  保持两个指针，一个指向数组的最后一个元素，另一个指向数组的第**K**元素。
3.  迭代数组 **K + 1** 次，每次求两个指针指向的元素的差。
4.  每次找到差异时，跟踪变量中可能的最小差异，并在最后返回该值。

以下是上述方法的实现:

## C++

```
// C++ program of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum difference
// between the maximum and the minimum
// elements arr[] by at most K replacements
int maxMinDifference(int arr[], int n, int k)
{
    // Check if turns are more than
    // or equal to n-1 then simply
    // return zero
    if (k >= n - 1)
        return 0;

    // Sort the array
    sort(arr, arr + n);

    // Set difference as the
    // maximum possible difference
    int ans = arr[n - 1] - arr[0];

    // Iterate over the array to
    // track the minimum difference
    // in k turns
    for (int i = k, j = n - 1;
         i >= 0; --i, --j) {

        ans = min(arr[j] - arr[i], ans);
    }

    // Return the answer
    return ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 4, 6, 11, 15 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K replacements
    int K = 3;

    // Function Call
    cout << maxMinDifference(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the approach
import java.io.*;
import java.util.Arrays;
class GFG{

// Function to find minimum difference
// between the maximum and the minimum
// elements arr[] by at most K replacements
static int maxMinDifference(int arr[], int n, int k)
{
    // Check if turns are more than
    // or equal to n-1 then simply
    // return zero
    if (k >= n - 1)
        return 0;

    // Sort the array
    Arrays.sort(arr);

    // Set difference as the
    // maximum possible difference
    int ans = arr[n - 1] - arr[0];

    // Iterate over the array to
    // track the minimum difference
    // in k turns
    for (int i = k, j = n - 1;
             i >= 0; --i, --j)
    {
        ans = Math.min(arr[j] - arr[i], ans);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    // Given array arr[]
    int arr[] = { 1, 4, 6, 11, 15 };
    int N = arr.length;

    // Given K replacements
    int K = 3;

    // Function Call
    System.out.print(maxMinDifference(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum difference
# between the maximum and the minimum
# elements arr[] by at most K replacements
def maxMinDifference(arr, n, k):

    # Check if turns are more than
    # or equal to n-1 then simply
    # return zero
    if(k >= n - 1):
        return 0

    # Sort the array
    arr.sort()

    # Set difference as the
    # maximum possible difference
    ans = arr[n - 1] - arr[0]

    # Iterate over the array to
    # track the minimum difference
    # in k turns
    i = k
    j = n - 1
    while i >= 0:
        ans = min(arr[j] - arr[i], ans)
        i -= 1
        j -= 1

    # Return the answer
    return ans

# Driver code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 1, 4, 6, 11, 15 ]
    N = len(arr)

    # Given K replacements
    K = 3

    # Function Call
    print(maxMinDifference(arr, N, K))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program of the approach
using System;
class GFG{

// Function to find minimum difference
// between the maximum and the minimum
// elements arr[] by at most K replacements
static int maxMinDifference(int []arr, int n, int k)
{
    // Check if turns are more than
    // or equal to n-1 then simply
    // return zero
    if (k >= n - 1)
        return 0;

    // Sort the array
    Array.Sort(arr);

    // Set difference as the
    // maximum possible difference
    int ans = arr[n - 1] - arr[0];

    // Iterate over the array to
    // track the minimum difference
    // in k turns
    for (int i = k, j = n - 1;
             i >= 0; --i, --j)
    {
        ans = Math.Min(arr[j] - arr[i], ans);
    }

    // Return the answer
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    // Given array arr[]
    int [] arr = new  int[] { 1, 4, 6, 11, 15 };
    int N = arr.Length;

    // Given K replacements
    int K = 3;

    // Function Call
    Console.Write(maxMinDifference(arr, N, K));
}
}

// This code is contributed by Ritik Bansal
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find minimum difference
// between the maximum and the minimum
// elements arr[] by at most K replacements
function maxMinDifference(arr, n, k)
{
    // Check if turns are more than
    // or equal to n-1 then simply
    // return zero
    if (k >= n - 1)
        return 0;

    // Sort the array
    arr.sort((a, b) => a - b);

    // Set difference as the
    // maximum possible difference
    let ans = arr[n - 1] - arr[0];

    // Iterate over the array to
    // track the minimum difference
    // in k turns
    for (let i = k, j = n - 1;
             i >= 0; --i, --j)
    {
        ans = Math.min(arr[j] - arr[i], ans);
    }

    // Return the answer
    return ans;
}

// Driver Code

   // Given array arr[]
    let arr = [ 1, 4, 6, 11, 15 ];
    let N = arr.length;

    // Given K replacements
    let K = 3;

    // Function Call
    document.write(maxMinDifference(arr, N, K));

</script>
```

**Output:** 

```
2
```

**时间复杂度:***O(N * log<sub>2</sub>N)*
**辅助空间:** *O(1)*