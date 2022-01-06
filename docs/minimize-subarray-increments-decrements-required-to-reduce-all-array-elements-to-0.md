# 最小化将所有阵列元素减少到 0 所需的子阵列增量/减量

> 原文:[https://www . geesforgeks . org/minimum-subarray-increments-reducts-需要将所有数组元素减少到 0/](https://www.geeksforgeeks.org/minimize-subarray-increments-decrements-required-to-reduce-all-array-elements-to-0/)

给定阵列 **arr[]，**选择任意[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)，并对子阵列的每个元素应用以下任意一个操作:

*   递增 1
*   递减 1

任务是打印将所有数组元素减少到 0 所需的最小数量的上述递增/递减操作。

**示例:**

> **输入:** arr[] = {1，3，4，1}
> **输出:** : 4
> **解释:**
> 将所有数组元素减为 0 的最佳步骤如下:
> **步骤 1:** 选择子数组【1，3，4，1】并将其转换为【0，2，3，0】，通过将每个元素减 1
> Array 修改为{0，2，3，0}
> **通过将每个元素递减 1
> 数组修改为{0，1，2，0}
> **第 3 步:**选择子数组[1，2]并将其转换为[0，1]，通过将每个元素递减 1
> 数组修改为{0，0，1，0}
> **第 4 步:**选择子数组[1]将其转换为[0]
> 数组修改为{0，0，0，0}
> 因此，最小数量**
> 
> **输入:** arr[] = {-2，0，-3，1，2}
> **输出** : 5
> **解释:**
> 将所有数组元素减为 0 的最佳步骤如下:
> **步骤 1:** 选择子数组[-2，0，-3]并将其转换为[-1，0，-2]，方法是将每个元素递增 1(除 0 之外)。
> 数组修改为{-1，0，-2，1，2}
> **步骤 2:** 选择子数组[-1，0，-2]并将其转换为[0，0，-1]，方法是将每个元素递增 1(除了 0)。
> 数组修改为{0，0，-1，1，2}
> **步骤 3:** 选择子数组[-1]将其转换为[0]
> 数组修改为{0，0，0，1，2}
> **步骤 4:** 选择子数组[1，2]并将其转换为[0，1]，方法是将每个元素减 1
> 数组修改为{0，0，0，0，1}
> **步骤**

**逼近:**解决问题，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)求最小负数和最大正数。它们的绝对值之和是所需的最小运算次数。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of operations required
int minOperation(int arr[], int N)
{
  int minOp = INT_MIN;
  int minNeg = 0, maxPos = 0;

  // Traverse the array
  for (int i = 0; i < N; i++)
  {
    // If array element
    // is negative
    if (arr[i] < 0)
    {
      if (arr[i] < minNeg)

        // Update minimum negative
        minNeg = arr[i];
    }
    else
    {
      if (arr[i] > maxPos)

        // Update maximum positive
        maxPos = arr[i];
    }
  }

  // Return minOp
  return abs(minNeg) + maxPos;
}

// Driver Code
int main()
{
  int arr[] = {1, 3, 4, 1};
  int N = sizeof(arr) / sizeof(arr[0]);
  cout << minOperation(arr, N);
}

//This code is contributed by Rajput-Ji
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the
// above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to count the minimum
    // number of operations required
    static int minOperation(int[] arr)
    {

        int minOp = Integer.MIN_VALUE;
        int minNeg = 0, maxPos = 0;

        // Traverse the array
        for (int i = 0; i < arr.length; i++) {

            // If array element
            // is negative
            if (arr[i] < 0) {
                if (arr[i] < minNeg)

                    // Update minimum negative
                    minNeg = arr[i];
            }
            else {
                if (arr[i] > maxPos)

                    // Update maximum positive
                    maxPos = arr[i];
            }
        }

        // Return minOp
        return Math.abs(minNeg) + maxPos;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 1, 3, 4, 1 };
        System.out.println(minOperation(arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program of the
# above approach

import sys

# Function to count the minimum
# number of operations required
def minOperation(arr):

    minOp = sys.maxsize
    minNeg = 0
    maxPos = 0

    # Traverse the array
    for i in range(len(arr)):

        # If array element
        # is negative
        if(arr[i] < 0):

            if (arr[i] < minNeg):

                # Update minimum negative
                minNeg = arr[i]
        else:
            if arr[i] > maxPos:

                # Update maximum position
                maxPos = arr[i]

    # Return minOp
    return abs(minNeg) + maxPos

# Driver code 
if __name__=="__main__":   
    arr=[1, 3, 4, 1]
    print(minOperation(arr))

# This code is contributed by Rutvik_56
```

## C#

```
// C# program of the
// above approach
using System;
class GFG{

// Function to count the minimum
// number of operations required
static int minOperation(int[] arr)
{

  int minOp = int.MinValue;
  int minNeg = 0, maxPos = 0;

  // Traverse the array
  for (int i = 0; i < arr.Length; i++)
  {
    // If array element
    // is negative
    if (arr[i] < 0)
    {
      if (arr[i] < minNeg)

        // Update minimum negative
        minNeg = arr[i];
    }
    else
    {
      if (arr[i] > maxPos)

        // Update maximum positive
        maxPos = arr[i];
    }
  }

  // Return minOp
  return Math.Abs(minNeg) + maxPos;
}

// Driver Code
public static void Main(String[] args)
{
  int []arr = {1, 3, 4, 1};
  Console.WriteLine(minOperation(arr));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

    // Function to count the minimum
    // number of operations required
    function minOperation(arr)
    {

        let minOp = Number.MIN_VALUE;
        let minNeg = 0, maxPos = 0;

        // Traverse the array
        for (let i = 0; i < arr.length; i++)
        {

            // If array element
            // is negative
            if (arr[i] < 0)
            {
                if (arr[i] < minNeg)

                    // Update minimum negative
                    minNeg = arr[i];
            }
            else
            {
                if (arr[i] > maxPos)

                    // Update maximum positive
                    maxPos = arr[i];
            }
        }

        // Return minOp
        return Math.abs(minNeg) + maxPos;
    }

// Driver code
    let arr = [ 1, 3, 4, 1 ];
    document.write(minOperation(arr));

     // This code is contributed by target_2.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)