# 将环形数组的所有元素减少到 0 所需的最小减 1 次数

> 原文:[https://www . geesforgeks . org/将循环数组的所有元素减少到 0 所需的最小减 1 次数/](https://www.geeksforgeeks.org/minimum-number-of-decrements-by-1-required-to-reduce-all-elements-of-a-circular-array-to-0/)

给定一个由 **N** 个整数组成的[圆形数组](https://www.geeksforgeeks.org/circular-array/) [](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]** ，任务是找到将圆形数组的所有元素减少到 **0** 的最小操作数。在每次操作中，将当前元素减少 **1** ( *从第一个元素*开始)并移动到下一个元素。

**示例:**

> **输入:** arr[] = {2，0，2}
> **输出:** 6
> **解释:**
> 执行以下操作:
> 
> 1.  将数组元素 arr[0]减少 1 将数组修改为{ **1** ，0，2}并移动到下一个元素 arr[1]。
> 2.  什么也不做，转到下一个元素，即 arr[2]。
> 3.  将数组元素 arr[2]减少 1 将数组修改为{1，0， **1** }并移动到下一个元素 arr[0]。
> 4.  将数组元素 arr[0]减少 1 将数组修改为{ **0** ，0，1}并移动到下一个元素 arr[1]。
> 5.  什么也不做，转到下一个元素，即 arr[2]。
> 6.  将数组元素 arr[2]减少 1 会将数组修改为{0，0， **0** }并移动到下一个元素 arr[0]。
> 
> 经过上述操作，环形数组的所有数组元素都已减少到 0。因此，所需的最小操作数是 6。
> 
> **输入:** arr[] = {0，3，1，3，2}
> **输出:** 14

**天真方法:**解决给定问题的最简单方法是[通过执行给定的操作以循环顺序遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，直到所有数组元素都是 **0** ，并记录所执行的操作的计数。完成上述步骤后，打印执行的操作数。

***时间复杂度:** O(N*M)，其中 **M** 是* [*阵的最大元素*](https://www.geeksforgeeks.org/c-program-find-largest-element-array/) *。*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以通过找到[最大数组元素](https://www.geeksforgeeks.org/program-find-minimum-maximum-element-array/)的最后一个索引并相应地找到所需的最小运算次数来优化。按照以下步骤解决问题:

*   初始化两个变量，比如 **pos** 和 **M** ，分别存储最大元素和最大元素的[最后一个索引。](https://www.geeksforgeeks.org/python-maximum-minimum-elements-position-list/)
*   [使用变量 **i** 遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，如果 **arr[i]** 的值至少为 **M** ，则将 **M** 的值修改为 **arr[i]** ，将 **pos** 修改为 **i** 。
*   完成上述步骤后，打印**(MX–1)* N+pos+1**的值作为最小步数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find minimum operation
// require to make all elements 0
void minimumOperations(int arr[], int N)
{
    // Stores the maximum element and
    // its position in the array
    int mx = 0, pos = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Update the maximum element
        // and its index
        if (arr[i] >= mx) {
            mx = arr[i];
            pos = i;
        }
    }

    // Print the minimum number of
    // operations required
    cout << (mx - 1) * N + pos + 1;
}

// Driver Code
int main()
{
    int arr[] = { 2, 0, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);

    minimumOperations(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

  // Function to find minimum operation
  // require to make all elements 0
  static void minimumOperations(int arr[], int N)
  {

    // Stores the maximum element and
    // its position in the array
    int mx = 0, pos = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Update the maximum element
      // and its index
      if (arr[i] >= mx) {
        mx = arr[i];
        pos = i;
      }
    }

    // Print the minimum number of
    // operations required
    System.out.println((mx - 1) * N + pos + 1);
  }

  // Driver Code
  public static void main (String[] args)
  {
    int arr[] = { 2, 0, 2 };
    int N = arr.length;

    minimumOperations(arr, N);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find minimum operation
# require to make all elements 0
def minimumOperations(arr, N):

    # Stores the maximum element and
    # its position in the array
    mx = 0
    pos = 0

    # Traverse the array
    for i in range(N):

        # Update the maximum element
        # and its index
        if (arr[i] >= mx):
            mx = arr[i]
            pos = i

    # Print the minimum number of
    # operations required
    print((mx - 1) * N + pos + 1)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 0, 2 ]
    N = len(arr)

    minimumOperations(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

  // Function to find minimum operation
  // require to make all elements 0
  static void minimumOperations(int[] arr, int N)
  {

    // Stores the maximum element and
    // its position in the array
    int mx = 0, pos = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Update the maximum element
      // and its index
      if (arr[i] >= mx) {
        mx = arr[i];
        pos = i;
      }
    }

    // Print the minimum number of
    // operations required
    Console.Write((mx - 1) * N + pos + 1);
  }

// Driver Code
public static void Main()
{
    int[] arr = { 2, 0, 2 };
    int N = arr.Length;

    minimumOperations(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>

// JavaScript code for above approach

  // Function to find minimum operation
  // require to make all elements 0
  function minimumOperations(arr, N)
  {

    // Stores the maximum element and
    // its position in the array
    let mx = 0, pos = 0;

    // Traverse the array
    for (let i = 0; i < N; i++) {

      // Update the maximum element
      // and its index
      if (arr[i] >= mx) {
        mx = arr[i];
        pos = i;
      }
    }

    // Print the minimum number of
    // operations required
    document.write((mx - 1) * N + pos + 1);
  }

// Driver Code
    let arr = [ 2, 0, 2 ];
    let N = arr.length;

    minimumOperations(arr, N);

    // This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)