# 大小为 K 的子阵列中谷元素的最大计数数量

> 原文:[https://www . geeksforgeeks . org/最大计数-大小为 k 的子阵列中的谷元素数/](https://www.geeksforgeeks.org/maximum-count-number-of-valley-elements-in-a-subarray-of-size-k/)

给定一个数组 **arr[]** ，任务是选择一个大小为 **K** 的[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，它包含相对于相邻元素的最大数量的谷点。
**一个元素 arr[i]被称为谷点，如果它的两个相邻元素都大于它，即** ![  ](img/0faf5aa5dcca41fbedb26b2cadf9f952.png "Rendered by QuickLaTeX.com") **和** ![  ](img/0faf5aa5dcca41fbedb26b2cadf9f952.png "Rendered by QuickLaTeX.com") **。**

**示例:**

> **输入:** arr[] = {5，4，6，4，5，2，3，1}，K = 7 the
> 
> **输出:**3
> T3】说明:T5】在子阵 arr[0-6] = {5，4，6，4，5，2，3}
> 子阵中有 3 个谷点，最大。
> 
> **输入:** arr[] = {2，1，4，2，3，4，1，2}，K = 4
> **输出:** 1
> **说明:**
> 在子阵 arr[0-3] = {2，1，4，2}
> 子阵中只有一个谷点，是最大的。

**方法:**思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)来解决这个问题。
以下是该方法步骤的说明:

*   求大小为 k 的第一个子数组中谷点的总数。
*   迭代所有可能子阵的起始点，即数组的 **N-K** 点，应用[包含和排除](https://www.geeksforgeeks.org/inclusion-exclusion-various-applications/)原理计算当前窗口的谷点个数。
*   在每一步，更新最终答案以计算每个子阵列的全局最大值。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum number of valley elements
// in the subarrays of size K

#include<bits/stdc++.h>
using namespace std;

// Function to find the valley elements
// in the array which contains
// in the subarrays of the size K
void minpoint(int arr[],int n, int k)
{
    int min_point = 0;
    for (int i = 1; i < k-1 ; i++)
    {
        // Increment min_point
        // if element at index i
        // is smaller than element
        // at index i + 1 and i-1
        if(arr[i] < arr[i - 1] && arr[i] < arr[i + 1])
            min_point += 1;
    }
    // final_point to maintain maximum
    // of min points of subarray
    int final_point = min_point;

    // Iterate over array
    // from kth element
    for(int i = k ; i < n; i++)
    {
        // Leftmost element of subarray
        if(arr[i - ( k - 1 )] < arr[i - ( k - 1 ) + 1]&&
        arr[i - ( k - 1 )] < arr[i - ( k - 1 ) - 1])
            min_point -= 1;

        // Rightmost element of subarray
        if(arr[i - 1] < arr[i] && arr[i - 1] < arr[i - 2])
            min_point += 1;

        // if new subarray have greater
        // number of min points than previous
        // subarray, then final_point is modified
        if(min_point > final_point)
            final_point = min_point;
    }

    // Max minimum points in
    // subarray of size k
    cout<<(final_point);
}

// Driver Code
int main()
{
    int arr[] = {2, 1, 4, 2, 3, 4, 1, 2};
    int n = sizeof(arr)/sizeof(arr[0]);
    int k = 4;
    minpoint(arr, n, k);
    return 0;
}
// This code contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum number of valley elements
// in the subarrays of size K
class GFG{

// Function to find the valley elements
// in the array which contains
// in the subarrays of the size K
static void minpoint(int arr[], int n, int k)
{
    int min_point = 0;
    for(int i = 1; i < k - 1; i++)
    {

       // Increment min_point
       // if element at index i
       // is smaller than element
       // at index i + 1 and i-1
       if(arr[i] < arr[i - 1] &&
          arr[i] < arr[i + 1])
          min_point += 1;
    }

    // final_point to maintain maximum
    // of min points of subarray
    int final_point = min_point;

    // Iterate over array
    // from kth element
    for(int i = k ; i < n; i++)
    {

       // Leftmost element of subarray
       if(arr[i - ( k - 1 )] < arr[i - ( k - 1 ) + 1] &&
          arr[i - ( k - 1 )] < arr[i - ( k - 1 ) - 1])
          min_point -= 1;

       // Rightmost element of subarray
       if(arr[i - 1] < arr[i] &&
          arr[i - 1] < arr[i - 2])
          min_point += 1;

       // If new subarray have greater
       // number of min points than previous
       // subarray, then final_point is modified
       if(min_point > final_point)
          final_point = min_point;
    }

    // Max minimum points in
    // subarray of size k
    System.out.println(final_point);
}

// Driver Code
public static void main (String[] args)
{
    int arr[] = { 2, 1, 4, 2, 3, 4, 1, 2 };
    int n = arr.length;
    int k = 4;

    minpoint(arr, n, k);
}
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum number of valley elements
# in the subarrays of size K

# Function to find the valley elements
# in the array which contains
# in the subarrays of the size K
def minpoint(arr, n, k):
    min_point = 0
    for i in range(1, k-1):

        # Increment min_point
        # if element at index i
        # is smaller than element
        # at index i + 1 and i-1
        if(arr[i] < arr[i - 1] and arr[i] < arr[i + 1]):
            min_point += 1

    # final_point to maintain maximum
    # of min points of subarray
    final_point = min_point

    # Iterate over array
    # from kth element
    for i in range(k, n):

        # Leftmost element of subarray
        if(arr[i - ( k - 1 )] < arr[i - ( k - 1 ) + 1] and\
           arr[i - ( k - 1 )] < arr[i - ( k - 1 ) - 1]):
            min_point -= 1

        # Rightmost element of subarray
        if(arr[i - 1] < arr[i] and arr[i - 1] < arr[i - 2]):
            min_point += 1

        # if new subarray have greater
        # number of min points than previous
        # subarray, then final_point is modified
        if(min_point > final_point):
            final_point = min_point

    # Max minimum points in
    # subarray of size k
    print(final_point)

# Driver Code
if __name__ == "__main__":
    arr = [2, 1, 4, 2, 3, 4, 1, 2]
    n = len(arr)
    k = 4
    minpoint(arr, n, k)
```

## C#

```
// C# implementation to find the
// maximum number of valley elements
// in the subarrays of size K
using System;

class GFG{

// Function to find the valley elements
// in the array which contains
// in the subarrays of the size K
static void minpoint(int []arr, int n, int k)
{
    int min_point = 0;
    for(int i = 1; i < k - 1; i++)
    {

       // Increment min_point
       // if element at index i
       // is smaller than element
       // at index i + 1 and i-1
       if(arr[i] < arr[i - 1] &&
          arr[i] < arr[i + 1])
          min_point += 1;
    }

    // final_point to maintain maximum
    // of min points of subarray
    int final_point = min_point;

    // Iterate over array
    // from kth element
    for(int i = k ; i < n; i++)
    {

       // Leftmost element of subarray
       if(arr[i - ( k - 1 )] < arr[i - ( k - 1 ) + 1] &&
          arr[i - ( k - 1 )] < arr[i - ( k - 1 ) - 1])
          min_point -= 1;

       // Rightmost element of subarray
       if(arr[i - 1] < arr[i] &&
          arr[i - 1] < arr[i - 2])
          min_point += 1;

       // If new subarray have greater
       // number of min points than previous
       // subarray, then final_point is modified
       if(min_point > final_point)
          final_point = min_point;
    }

    // Max minimum points in
    // subarray of size k
    Console.WriteLine(final_point);
}

// Driver Code
public static void Main (string[] args)
{
    int []arr = { 2, 1, 4, 2, 3, 4, 1, 2 };
    int n = arr.Length;
    int k = 4;

    minpoint(arr, n, k);
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// maximum number of valley elements
// in the subarrays of size K

// Function to find the valley elements
// in the array which contains
// in the subarrays of the size K
function minpoint(arr, n, k) {
    let min_point = 0;
    for (let i = 1; i < k - 1; i++) {
        // Increment min_point
        // if element at index i
        // is smaller than element
        // at index i + 1 and i-1
        if (arr[i] < arr[i - 1] && arr[i] < arr[i + 1])
            min_point += 1;
    }
    // final_point to maintain maximum
    // of min points of subarray
    let final_point = min_point;

    // Iterate over array
    // from kth element
    for (let i = k; i < n; i++) {
        // Leftmost element of subarray
        if (arr[i - (k - 1)] < arr[i - (k - 1) + 1] &&
            arr[i - (k - 1)] < arr[i - (k - 1) - 1])
            min_point -= 1;

        // Rightmost element of subarray
        if (arr[i - 1] < arr[i] && arr[i - 1] < arr[i - 2])
            min_point += 1;

        // if new subarray have greater
        // number of min points than previous
        // subarray, then final_point is modified
        if (min_point > final_point)
            final_point = min_point;
    }

    // Max minimum points in
    // subarray of size k
    document.write(final_point);
}

// Driver Code

let arr = [2, 1, 4, 2, 3, 4, 1, 2];
let n = arr.length;
let k = 4;
minpoint(arr, n, k);

// This code contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*T4】