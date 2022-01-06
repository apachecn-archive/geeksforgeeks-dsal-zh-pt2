# 通过执行给定操作的最小次数

使数组元素相等

> 原文:[https://www . geesforgeks . org/通过执行给定操作使数组元素相等-最小次数/](https://www.geeksforgeeks.org/make-the-array-elements-equal-by-performing-given-operations-minimum-number-of-times/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过执行以下操作最少次数来使所有数组元素相等:

*   将任何后缀数组的所有数组元素增加 1。
*   将任何后缀数组的所有元素减 1。
*   用另一个替换任何数组元素。

**示例:**

> **输入:** arr[] = {99，96，97，95}
> **输出:** 3
> **解释:**
> **操作 1:** 用一个 <sub>2</sub> 代替一个 <sub>1</sub> ，即 99 → 96。arr[]数组修改为{96，96，97，95}。
> **操作 2:** 将后缀{ a <sub>4</sub> 增加 2，即 95 → 97。arr[]数组修改为{96，96，97，97}。
> **操作 3:** 将后缀{ a <sub>3</sub> 减 1，即 97 → 96。arr[]数组修改为{96，96，96，96}。
> 因此，所需的操作总数为 3。
> 
> **输入:** arr[] = {1，-1，0，1，1}
> **输出:** 2

**方法:**想法是找到所有元素相等的数组的实际和与[和之间的差，然后选择要执行的操作，使得它导致最小的操作计数。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

*   初始化一个变量，比如 **totOps** ，来存储使所有数组元素相等所需的实际操作。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并存储所有连续元素对之间的差，并将它们的和存储在**合计**中。
*   初始化一个变量，比如 **maxOps** ，来存储所需操作的最大计数。
*   现在，找到改变元素时发生的最大变化，并将其存储在**最大值**变量中。有三种情况:
    *   对于第一个元素，即 **arr[1]** ，改变 **arr[1]** 的最佳方式是使其成为 **arr[2]** 。
    *   对于最后一个元素，即**arr【N】**，改变**arr【N】**的最佳方式是将其变为**arr【N-1】**。
    *   对于元素的其余部分，更改 **arr[i]** 会影响**arr[I-1]**和 **arr[i+1]** ，因此，最大的更改是**ABS(arr[I]<sub>–arr[I+1])+ABS(arr[I]<sub>–arr[I-1])–ABS(arr[I-1]</sub></sub>**
*   因此，所需的最小操作等于**总操作数**和**最大操作数**之间的差值。

下面是上述方法的实现:

## C++

```
// C++ Program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// operations of given type required
// to make the array elements equal
void minOperation(int a[], int N)
{
    // Stores the total count of operations
    int totOps = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++) {

        // Update difference between
        // pairs of adjacent elements
        totOps += abs(a[i] - a[i + 1]);
    }

    // Store the maximum count of operations
    int maxOps
        = max(abs(a[0] - a[1]),
              abs(a[N - 1] - a[N - 2]));

    for (int i = 1; i < N - 1; i++) {

        // Rest of the elements
        maxOps
            = max(maxOps, abs(a[i] - a[i - 1])
                              + abs(a[i] - a[i + 1])
                              - abs(a[i - 1] - a[i + 1]));
    }

    // Total Operation - Maximum Operation
    cout << totOps - maxOps << endl;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, -1, 0, 1, 1 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    minOperation(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;
class GFG
{

  // Function to calculate the minimum
  // operations of given type required
  // to make the array elements equal
  static void minOperation(int a[], int N)
  {

    // Stores the total count of operations
    int totOps = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++)
    {

      // Update difference between
      // pairs of adjacent elements
      totOps += Math.abs(a[i] - a[i + 1]);
    }

    // Store the maximum count of operations
    int maxOps
      = Math.max(Math.abs(a[0] - a[1]),
                 Math.abs(a[N - 1] - a[N - 2]));

    for (int i = 1; i < N - 1; i++)
    {

      // Rest of the elements
      maxOps = Math.max(
        maxOps,
        Math.abs(a[i] - a[i - 1])
        + Math.abs(a[i] - a[i + 1])
        - Math.abs(a[i - 1] - a[i + 1]));
    }

    // Total Operation - Maximum Operation
    System.out.println(totOps - maxOps);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int[] arr = { 1, -1, 0, 1, 1 };

    // Size of the array
    int N = arr.length;

    minOperation(arr, N);
  }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python3 Program for the above approach

# Function to calculate the minimum
# operations of given type required
# to make the array elements equal
def minOperation(a, N):

    # Stores the total count of operations
    totOps = 0

    # Traverse the array
    for i in range(N - 1):

        # Update difference between
        # pairs of adjacent elements
        totOps += abs(a[i] - a[i + 1])

    # Store the maximum count of operations
    maxOps = max(abs(a[0] - a[1]), abs(a[N - 1] - a[N - 2]))
    for i in range(1, N - 1):

        # Rest of the elements
        maxOps = max(maxOps, abs(a[i] - a[i - 1]) +
                     abs(a[i] - a[i + 1])- abs(a[i - 1] - a[i + 1]))

    # Total Operation - Maximum Operation
    print (totOps - maxOps)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [1, -1, 0, 1, 1]

    # Size of the array
    N = len(arr)
    minOperation(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# Program for the above approach
using System;
public class GFG {

  // Function to calculate the minimum
  // operations of given type required
  // to make the array elements equal
  static void minOperation(int[] a, int N)
  {
    // Stores the total count of operations
    int totOps = 0;

    // Traverse the array
    for (int i = 0; i < N - 1; i++)
    {

      // Update difference between
      // pairs of adjacent elements
      totOps += Math.Abs(a[i] - a[i + 1]);
    }

    // Store the maximum count of operations
    int maxOps
      = Math.Max(Math.Abs(a[0] - a[1]),
                 Math.Abs(a[N - 1] - a[N - 2]));

    for (int i = 1; i < N - 1; i++)
    {

      // Rest of the elements
      maxOps = Math.Max(
        maxOps,
        Math.Abs(a[i] - a[i - 1])
        + Math.Abs(a[i] - a[i + 1])
        - Math.Abs(a[i - 1] - a[i + 1]));
    }

    // Total Operation - Maximum Operation
    Console.WriteLine(totOps - maxOps);
  }

  // Driver Code
  static public void Main()
  {

    // Given array
    int[] arr = { 1, -1, 0, 1, 1 };

    // Size of the array
    int N = arr.Length;

    minOperation(arr, N);
  }
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>
// javascript Program for the above approach

    // Function to calculate the minimum
    // operations of given type required
    // to make the array elements equal
    function minOperation(a , N) {

        // Stores the total count of operations
        var totOps = 0;

        // Traverse the array
        for (i = 0; i < N - 1; i++) {

            // Update difference between
            // pairs of adjacent elements
            totOps += Math.abs(a[i] - a[i + 1]);
        }

        // Store the maximum count of operations
        var maxOps = Math.max(Math.abs(a[0] - a[1]), Math.abs(a[N - 1] - a[N - 2]));

        for (i = 1; i < N - 1; i++) {

            // Rest of the elements
            maxOps = Math.max(maxOps,
                    Math.abs(a[i] - a[i - 1]) + Math.abs(a[i] - a[i + 1]) - Math.abs(a[i - 1] - a[i + 1]));
        }

        // Total Operation - Maximum Operation
        document.write(totOps - maxOps);
    }

    // Driver Code

        // Given array
        var arr = [ 1, -1, 0, 1, 1 ];

        // Size of the array
        var N = arr.length;

        minOperation(arr, N);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)