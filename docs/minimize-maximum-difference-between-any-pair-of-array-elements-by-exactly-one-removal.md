# 将任意一对数组元素之间的最大差异精确地减少一次

> 原文:[https://www . geeksforgeeks . org/通过精确一次移除来最小化任何数组元素对之间的最大差异/](https://www.geeksforgeeks.org/minimize-maximum-difference-between-any-pair-of-array-elements-by-exactly-one-removal/)

给定一个由 **N** 个整数(N > 2)组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过移除恰好一个元素来最小化任意一对元素 **(arr[i]，arr[j])** 之间的最大差异。

**示例:**

> **输入:** arr[] = {1，3，4，7}
> **输出:** 3
> **解释:**
> 从数组中移除元素 7，将数组修改为{1，3，4}。
> 这里(4，1)的差值= 4–1 = 3，这是最小可能的最大差值。
> 
> **输入:** arr[] = {1，2，3，4}
> **输出:** 2

**天真方法:**解决给定问题的最简单方法是逐个移除每个元素，并检查哪一个元素给出了每对元素之间的最小[最大差异](https://www.geeksforgeeks.org/maximum-difference-between-a-pair-of-adjacent-elements-by-excluding-every-element-once/)。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N)*

**有效方法:**通过观察最大差值等于给定数组的最大值和[最小值元素之间的差值，也可以优化上述方法。因此，移除最大元素或移除最小元素总是给出最佳答案。](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)

因此，想法是[按照升序对给定的数组进行排序](https://www.geeksforgeeks.org/arrays-sort-in-java-with-examples/)并打印值**(arr[N–2]–arr[0])**和**(arr[N–1]–arr[1])**的最小值作为最小化的最大差值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum maximum
// difference after removing one element
int findMinDifference(int arr[], int n)
{
    // Stores the resultant minimized
    // maximum difference
    int ans = 0;

    // Sort the given array
    sort(arr, arr + n);

    // Find the minimum maximum
    // difference
    ans = min(arr[n - 2] - arr[0],
              arr[n - 1] - arr[1]);

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << findMinDifference(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {

  // Function to find the minimum maximum
  // difference after removing one element
  static int findMinDifference(int []arr, int n)
  {

    // Stores the resultant minimized
    // maximum difference
    int ans = 0;

    // Sort the given array
    Arrays.sort(arr);

    // Find the minimum maximum
    // difference
    ans = Math.min(arr[n - 2] - arr[0],
                   arr[n - 1] - arr[1]);

    // Return the result
    return ans;
  }

  // Driver Code

  public static void main (String[] args) {

    int []arr = { 1, 3, 4, 7 };
    int N = arr.length;

    System.out.println(findMinDifference(arr, N));
  }

}

// This code is contributed by unknown2108
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum maximum
# difference after removing one element
def findMinDifference(arr, n):

    # Stores the resultant minimized
    # maximum difference
    ans = 0

    # Sort the given array
    arr = sorted(arr)

    # Find the minimum maximum
    # difference
    ans = min(arr[n - 2] - arr[0],
              arr[n - 1] - arr[1])

    # Return the result
    return ans

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 3, 4, 7 ]
    N = len(arr)

    print (findMinDifference(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum maximum
// difference after removing one element
static int findMinDifference(int []arr, int n)
{

    // Stores the resultant minimized
    // maximum difference
    int ans = 0;

    // Sort the given array
    Array.Sort(arr);

    // Find the minimum maximum
    // difference
    ans = Math.Min(arr[n - 2] - arr[0],
                   arr[n - 1] - arr[1]);

    // Return the result
    return ans;
}

// Driver Code
public static void Main()
{
    int []arr = { 1, 3, 4, 7 };
    int N = arr.Length;

    Console.Write(findMinDifference(arr, N));
}
}

// This code is contributed by ipg2016107
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum maximum
// difference after removing one element
function findMinDifference(arr, n)
{

    // Stores the resultant minimized
    // maximum difference
    let ans = 0;

    // Sort the given array
    arr.sort(function(a,b){return a-b;});

    // Find the minimum maximum
    // difference
    ans = Math.min(arr[n - 2] - arr[0],
                   arr[n - 1] - arr[1]);

    // Return the result
    return ans;
}

// Driver Code
let arr=[1, 3, 4, 7];
let N = arr.length;
document.write(findMinDifference(arr, N));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*