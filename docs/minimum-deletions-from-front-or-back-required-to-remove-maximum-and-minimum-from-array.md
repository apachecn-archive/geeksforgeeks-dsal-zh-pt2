# 从阵列中移除最大值和最小值所需的前部或后部最小删除量

> 原文:[https://www . geeksforgeeks . org/最小-从前部或后部删除-需要从阵列中删除最大值和最小值/](https://www.geeksforgeeks.org/minimum-deletions-from-front-or-back-required-to-remove-maximum-and-minimum-from-array/)

给定一个由整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是找到从 **arr[]** 中删除初始最小和最大元素所需的最小删除量。
**注意:**删除可以从阵列的正面或背面进行。

**示例:**

> **输入:** arr[] = {5，7，2，4，3}
> **输出:** 3
> **解释:**初始最小值= 2，初始最大值= 7
> 从 arr[]中删除前 3 会将 arr[]更新为{2，4，3}，其中没有初始最大值和最小值元素。
> 因此，至少需要 3 次操作。
> 
> **输入:** arr[] = {2，-1，3，5，8，-7 }
> T3】输出: 2

**逼近:**给定的问题可以用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。按照以下步骤解决给定的问题。

*   初始化两个变量 **mn** 、 **mx** 分别存储最小和最大元素。
*   使用两个变量 **minIndex，maxIndex** 来存储最小和最大元素的最后一次出现。
*   用 **i** 迭代 **arr[]**
    *   更新 **mn = min(mn，arr[i])**
    *   更新 **mx =最大值(mx，arr[i])**
*   使用两个变量，比如 minIndex 和 maxIndex 来存储最小和最大元素的最后一次出现。
*   用 I 迭代 arr[]
    *   如果 **arr[i] = mn** ，那么更新**minidex = I**
    *   如果 **arr[i] = mx** ，那么更新 **maxIndex =** i
*   计算所有删除的情况，并存储在变量 **x，y，z** 中。
*   返回 **x，y，z** 中的最小值作为最终答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum deletions to
// remove initial minimum and maximum
int minDeletions(int *arr, int N)
{
    // To store initial minimum and maximum
    int mn = INT_MAX, mx = INT_MIN;

    // Iterate and find min and max in arr[]
    for(int i = 0; i < N; i++) {
        mn = min(mn, arr[i]);
        mx = max(mx, arr[i]);
    }

    // To store indices of last min and max
    int minIndex, maxIndex;
    for(int i = 0; i < N; i++) {
        if(arr[i] == mn) minIndex = i;
        if(arr[i] == mx) maxIndex = i;
    }

    int temp = max(minIndex, maxIndex);
    minIndex = min(minIndex, maxIndex);
    maxIndex = temp;

    // Calculating all possible case of
    // deletion operations
    int x = N - maxIndex + minIndex + 1;
    int y = N - minIndex;
    int z = maxIndex + 1;

    // Return minimum among all the three cases
    return min({x, y, z});
}

// Driver Code
int main()
{
    int N = 6;
    int arr[] = {2, -1, 9, 7, -2, 3};

    cout << minDeletions(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;
class GFG
{

    // Function to calculate minimum deletions to
    // remove initial minimum and maximum
    static int minDeletions(int arr[], int N)
    {

        // To store initial minimum and maximum
        int mn = Integer.MAX_VALUE, mx = Integer.MIN_VALUE;

        // Iterate and find min and max in arr[]
        for (int i = 0; i < N; i++) {
            mn = Math.min(mn, arr[i]);
            mx = Math.max(mx, arr[i]);
        }

        // To store indices of last min and max
        int minIndx = 0, maxIndx = 0;
        for (int i = 0; i < N; i++) {
            if (arr[i] == mn)
                minIndx = i;
            if (arr[i] == mx)
                maxIndx = i;
        }

        int temp = Math.max(minIndx, maxIndx);
        minIndx = Math.min(minIndx, maxIndx);
        maxIndx = temp;

        // Calculating all possible case of
        // deletion operations
        int x = N - maxIndx + minIndx + 1;
        int y = N - minIndx;
        int z = maxIndx + 1;

        // Return minimum among all the three cases
        return Math.min(x, Math.min(y, z));
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 2, -1, 9, 7, -2, 3 };
        int N = 6;
        System.out.println(minDeletions(arr, N));
    }
}

// This code is contributed by dwivediyash
```

## 蟒蛇 3

```
# python program for the above approach
INT_MIN = -2147483648
INT_MAX = 2147483647

# Function to calculate minimum deletions to
# remove initial minimum and maximum
def minDeletions(arr, N):

        # To store initial minimum and maximum
    mn = INT_MAX
    mx = INT_MIN

    # Iterate and find min and max in arr[]
    for i in range(0, N):
        mn = min(mn, arr[i])
        mx = max(mx, arr[i])

        # To store indices of last min and max
    minIndex = 0
    maxIndex = 0
    for i in range(0, N):
        if(arr[i] == mn):
            minIndex = i
        if(arr[i] == mx):
            maxIndex = i

    temp = max(minIndex, maxIndex)
    minIndex = min(minIndex, maxIndex)
    maxIndex = temp

    # Calculating all possible case of
    # deletion operations
    x = N - maxIndex + minIndex + 1
    y = N - minIndex
    z = maxIndex + 1

    # Return minimum among all the three cases
    return min({x, y, z})

# Driver Code
if __name__ == "__main__":

    N = 6
    arr = [2, -1, 9, 7, -2, 3]

    print(minDeletions(arr, N))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to calculate minimum deletions to
    // remove initial minimum and maximum
    static int minDeletions(int[] arr, int N)
    {

        // To store initial minimum and maximum
        int mn = int.MaxValue, mx = int.MinValue;

        // Iterate and find min and max in arr[]
        for (int i = 0; i < N; i++) {
            mn = Math.Min(mn, arr[i]);
            mx = Math.Max(mx, arr[i]);
        }

        // To store indices of last min and max
        int minIndx = 0, maxIndx = 0;
        for (int i = 0; i < N; i++) {
            if (arr[i] == mn)
                minIndx = i;
            if (arr[i] == mx)
                maxIndx = i;
        }

        int temp = Math.Max(minIndx, maxIndx);
        minIndx = Math.Min(minIndx, maxIndx);
        maxIndx = temp;

        // Calculating all possible case of
        // deletion operations
        int x = N - maxIndx + minIndx + 1;
        int y = N - minIndx;
        int z = maxIndx + 1;

        // Return minimum among all the three cases
        return Math.Min(x, Math.Min(y, z));
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 2, -1, 9, 7, -2, 3 };
        int N = 6;
        Console.Write(minDeletions(arr, N));
    }
}

// This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate minimum deletions to
// remove initial minimum and maximum
function minDeletions(arr, N)
{

  // To store initial minimum and maximum
  let mn = Number.MAX_SAFE_INTEGER,
    mx = Number.MIN_SAFE_INTEGER;

  // Iterate and find min and max in arr[]
  for (let i = 0; i < N; i++) {
    mn = Math.min(mn, arr[i]);
    mx = Math.max(mx, arr[i]);
  }

  // To store indices of last min and max
  let minIndex, maxIndex;
  for (let i = 0; i < N; i++) {
    if (arr[i] == mn) minIndex = i;
    if (arr[i] == mx) maxIndex = i;
  }

  let temp = Math.max(minIndex, maxIndex);
  minIndex = Math.min(minIndex, maxIndex);
  maxIndex = temp;

  // Calculating all possible case of
  // deletion operations
  let x = N - maxIndex + minIndex + 1;
  let y = N - minIndex;
  let z = maxIndex + 1;

  // Return minimum among all the three cases
  return Math.min(x, Math.min(y, z));
}

// Driver Code

let N = 6;
let arr = [2, -1, 9, 7, -2, 3];

document.write(minDeletions(arr, N));

// This code is contributed by gfgking.
</script>
```

**Output**

```
4
```

**时间复杂度:** O(N)

**辅助空间:** O(1)