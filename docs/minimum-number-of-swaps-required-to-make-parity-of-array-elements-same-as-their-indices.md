# 使数组元素的奇偶性与其索引相同所需的最小交换次数

> 原文:[https://www . geeksforgeeks . org/最小交换次数-需要进行数组元素奇偶校验-与它们的索引相同/](https://www.geeksforgeeks.org/minimum-number-of-swaps-required-to-make-parity-of-array-elements-same-as-their-indices/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到使所有数组元素的奇偶性(即*偶数*或*奇数*)与其各自的索引相同所需的最小交换次数。如果无法做到，则打印**-1”**。

**示例:**

> **输入:** arr[] = {3，2，7，6}
> **输出:** 2
> **解释:**
> 交换{arr[0]，arr[1]}和{arr[2]，arr[3]}。数组 arr[]修改为{2，3，6，7}。
> 现在每个奇数和偶数元素分别处于奇数和偶数索引。
> 因此，所需的最少互换数量为 2。
> 
> **输入:** arr[] = {7}
> **输出:** -1

**方法:**按照以下步骤解决问题:

*   用 **0** 初始化变量**偶数**和**奇数**，以存储偶数和奇数的[计数](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)。
*   使用变量 **i** 遍历数组 **arr[]** ，并执行以下操作:
    *   如果**arr【I】**和 **i** 的宇称相同，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   检查 **i** 是否为偶数。如果发现为真，则通过将值增加 **1** 来更新**甚至**。
    *   否则，通过将值增加 **1** 来更新**奇数**。
*   完成上述步骤后，如果**偶数**和**奇数**的值不相等，则打印 **-1** 。
*   否则，打印**甚至**的值作为所需的最小交换次数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum number
// of swaps required to make the parity
// of array elements same as their indices
void minimumSwaps(int arr[], int N)
{
    // Stores count of even
    // and odd array elements
    int even = 0, odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Check if indices and
        // array elements are not
        // of the same parity
        if (arr[i] % 2 != i % 2) {

            // If index is even
            if (i % 2 == 0) {

                // Update even
                even++;
            }
            else {

                // Update odd
                odd++;
            }
        }
    }

    // Condition for not possible
    if (even != odd) {

        cout << -1;
    }

    // Otherwise
    else {
        cout << even;
    }
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 7, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    minimumSwaps(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // Function to count the minimum number
  // of swaps required to make the parity
  // of array elements same as their indices
  static void minimumSwaps(int arr[], int N)
  {

    // Stores count of even
    // and odd array elements
    int even = 0, odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Check if indices and
      // array elements are not
      // of the same parity
      if (arr[i] % 2 != i % 2) {

        // If index is even
        if (i % 2 == 0) {

          // Update even
          even++;
        }
        else {

          // Update odd
          odd++;
        }
      }
    }

    // Condition for not possible
    if (even != odd) {

      System.out.println(-1);
    }

    // Otherwise
    else {
      System.out.println(even);
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    int arr[] = { 3, 2, 7, 6 };
    int N = arr.length;

    minimumSwaps(arr, N);
  }
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum number
# of swaps required to make the parity
# of array elements same as their indices
def minimumSwaps(arr, N):

    # Stores count of even
    # and odd array elements
    even, odd = 0, 0

    # Traverse the array
    for i in range(N):

        # Check if indices and
        # array elements are not
        # of the same parity
        if (arr[i] % 2 != i % 2):

            # If index is even
            if (i % 2 == 0):

                # Update even
                even += 1
            else:
                # Update odd
                odd += 1

    # Condition for not possible
    if (even != odd):
        print(-1)

    # Otherwise
    else:
        print(even)

# Driver Code
if __name__ == '__main__':
    arr = [3, 2, 7, 6]
    N = len(arr)

    minimumSwaps(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

  // Function to count the minimum number
  // of swaps required to make the parity
  // of array elements same as their indices
  static void minimumSwaps(int[] arr, int N)
  {

    // Stores count of even
    // and odd array elements
    int even = 0, odd = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Check if indices and
      // array elements are not
      // of the same parity
      if (arr[i] % 2 != i % 2) {

        // If index is even
        if (i % 2 == 0) {

          // Update even
          even++;
        }
        else {

          // Update odd
          odd++;
        }
      }
    }

    // Condition for not possible
    if (even != odd) {

      Console.WriteLine(-1);
    }

    // Otherwise
    else {
      Console.WriteLine(even);
    }
  }

  // Driver Code
  public static void Main()
  {
    int[] arr = { 3, 2, 7, 6 };
    int N = arr.Length;

    minimumSwaps(arr, N);
  }
}

// This code is contributed by souravghosh0416.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the minimum number
// of swaps required to make the parity
// of array elements same as their indices
function minimumSwaps(arr, N)
{

    // Stores count of even
    // and odd array elements
    let even = 0, odd = 0;

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Check if indices and
        // array elements are not
        // of the same parity
        if (arr[i] % 2 != i % 2)
        {

            // If index is even
            if (i % 2 == 0)
            {

                // Update even
                even++;
            }
            else
            {

                // Update odd
                odd++;
            }
        }
    }

    // Condition for not possible
    if (even != odd)
    {
        document.write(-1);
    }

    // Otherwise
    else
    {
        document.write(even);
    }
}

// Driver code
let arr = [ 3, 2, 7, 6 ];
let N = arr.length;

minimumSwaps(arr, N);

// This code is contributed by target_2

</script>
```

**Output:** 

```
2
```

***时间复杂度:*** *O(N)*
***辅助空间:*** *O(1)*