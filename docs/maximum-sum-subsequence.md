# 最大和子序列

> 原文:[https://www.geeksforgeeks.org/maximum-sum-subsequence/](https://www.geeksforgeeks.org/maximum-sum-subsequence/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到给定数组中存在的最大和[非空子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)。

**示例:**

> **输入:** arr[] = { 2，3，7，1，9 }
> **输出:** 22
> **解释:**
> 子序列{ arr[0]、arr[1]、arr[2]、arr[3]、arr[4]之和等于 22，是数组任意子序列的最大可能和。
> 因此，要求的输出是 22。
> 
> **输入:** arr[] = { -2，11，-4，2，-3，-10 }
> **输出:** 13
> **解释:**
> 子序列{ arr[1]，arr[3] }之和等于 13，是数组任意子序列的最大可能和。
> 因此，需要的输出是 13。

**天真法:**解决这个问题最简单的方法是[生成数组所有可能的非空子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)，计算数组每个子序列的和。最后，打印从子序列获得的最大和。

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效途径:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)计算数组的正元素之和并打印得到的和。按照以下步骤解决问题:

*   检查数组的[最大元素是否大于 **0** 。如果发现为真，则](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)[遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并打印数组所有正元素的和。
*   否则，打印数组中最大的[元素。](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum
// non-emepty subsequence sum
int MaxNonEmpSubSeq(int a[], int n)
{
    // Stores the maximum non-emepty
    // subsequence sum in an array
    int sum = 0;

    // Stores the largest element
    // in the array
    int max = *max_element(a, a + n);

    if (max <= 0) {

        return max;
    }

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // If a[i] is greater than 0
        if (a[i] > 0) {

            // Update sum
            sum += a[i];
        }
    }
    return sum;
}

// Driver Code
int main()
{
    int arr[] = { -2, 11, -4, 2, -3, -10 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << MaxNonEmpSubSeq(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

  // Function to print the maximum
  // non-emepty subsequence sum
  static int MaxNonEmpSubSeq(int a[], int n)
  {

    // Stores the maximum non-emepty
    // subsequence sum in an array
    int sum = 0;

    // Stores the largest element
    // in the array
    int max = a[0];
    for(int i = 1; i < n; i++)
    {
      if(max < a[i])
      {
        max = a[i];
      }
    }

    if (max <= 0)
    {    
      return max;
    }

    // Traverse the array
    for (int i = 0; i < n; i++)
    {

      // If a[i] is greater than 0
      if (a[i] > 0)
      {

        // Update sum
        sum += a[i];
      }
    }
    return sum;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { -2, 11, -4, 2, -3, -10 };
    int N = arr.length;

    System.out.println(MaxNonEmpSubSeq(arr, N));
  }
}

// This code is contributed by divyesh072019
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to print the maximum
# non-emepty subsequence sum
def MaxNonEmpSubSeq(a, n):

    # Stores the maximum non-emepty
    # subsequence sum in an array
    sum = 0

    # Stores the largest element
    # in the array
    maxm = max(a)

    if (maxm <= 0):
        return maxm

    # Traverse the array
    for i in range(n):

        # If a[i] is greater than 0
        if (a[i] > 0):

            # Update sum
            sum += a[i]

    return sum

# Driver Code
if __name__ == '__main__':

    arr = [ -2, 11, -4, 2, -3, -10 ]
    N = len(arr)

    print(MaxNonEmpSubSeq(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to print the maximum
// non-emepty subsequence sum
static int MaxNonEmpSubSeq(int[] a, int n)
{

    // Stores the maximum non-emepty
    // subsequence sum in an array
    int sum = 0;

    // Stores the largest element
    // in the array
    int max = a[0];
    for(int i = 1; i < n; i++)
    {
        if (max < a[i])
        {
            max = a[i];
        }
    }

    if (max <= 0)
    {
        return max;
    }

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // If a[i] is greater than 0
        if (a[i] > 0)
        {

            // Update sum
            sum += a[i];
        }
    }
    return sum;
}

// Driver Code
static void Main()
{
    int[] arr = { -2, 11, -4, 2, -3, -10 };
    int N = arr.Length;

    Console.WriteLine(MaxNonEmpSubSeq(arr, N));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

    // Javascript program to implement
    // the above approach

    // Function to print the maximum
    // non-emepty subsequence sum
    function MaxNonEmpSubSeq(a, n)
    {

        // Stores the maximum non-emepty
        // subsequence sum in an array
        let sum = 0;

        // Stores the largest element
        // in the array
        let max = a[0];
        for(let i = 1; i < n; i++)
        {
            if (max < a[i])
            {
                max = a[i];
            }
        }

        if (max <= 0)
        {
            return max;
        }

        // Traverse the array
        for(let i = 0; i < n; i++)
        {

            // If a[i] is greater than 0
            if (a[i] > 0)
            {

                // Update sum
                sum += a[i];
            }
        }
        return sum;
    }

    let arr = [ -2, 11, -4, 2, -3, -10 ];
    let N = arr.length;

    document.write(MaxNonEmpSubSeq(arr, N));

</script>
```

**Output:** 

```
13
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)