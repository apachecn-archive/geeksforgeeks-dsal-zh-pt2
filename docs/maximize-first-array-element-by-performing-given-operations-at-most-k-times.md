# 通过最多执行 K 次给定操作最大化第一个数组元素

> 原文:[https://www . geeksforgeeks . org/通过最多执行 k 次给定操作来最大化第一个数组元素/](https://www.geeksforgeeks.org/maximize-first-array-element-by-performing-given-operations-at-most-k-times/)

给定一个大小为 **N** 整数 **K** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过最多执行以下操作 **K** 次来找到数组的最大第一个元素:

1.  选择一对指数 **i** 和**j**T4(0≤I，j ≤ N-1) 使得**| I-j | = 1**和 **arr <sub>i</sub> > 0** 。
2.  在这两个指标上设置**arr<sub>I</sub>= arr<sub>I</sub>1**和**arr<sub>j</sub>= arr<sub>j</sub>+1**。

**示例:**

> **输入:** arr[ ] = {1，0，3，2}，K = 5
> **输出:** 3
> **解释:**
> 可能的操作集合之一可以是:
> 操作 1:选择 **i = 3** 和 **j = 2** 。因此，数组修改为{1，1，2，2}。
> 操作 2:选择 **i = 3** 和 **j = 2** 。因此，数组修改为{1，2，1，2}。
> 操作 3:选择 **i = 2** 和 **j = 1** 。因此，数组修改为{2，1，1，2}。
> 操作 4:选择 **i = 2** 和 **j = 1** 。因此，数组修改为{3，0，1，2}。
> 
> **输入:** arr[] = {5，1}，K = 2
> T3】输出: 6

**方法:**按照以下步骤解决问题:

1.  在任何时候，最好选择最接近数组第一个元素的索引 **i** 和 **j** ，以及 **i > j** 。
2.  因此，对于每个操作，[从左到右遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并将元素移向第一个元素。
3.  如果所有元素都在某个点的第一个位置，停止遍历并打印第一个数组元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to maximize
// the first array element
int getMax(int arr[], int N, int K)
{

    // Traverse the array
    for (int i = 1; i < N; i++) {

        // Initialize cur_val to a[i]
        int cur_val = arr[i];

        // If all operations
        // are not over yet
        while (K >= i) {

            // If current value is
            // greater than zero
            if (cur_val > 0) {

                // Incrementing first
                // element of array by 1
                arr[0] = arr[0] + 1;

                // Decrementing current
                // value of array by 1
                cur_val = cur_val - 1;

                // Decrementing number
                // of operations by i
                K = K - i;
            }

            // If current value is
            // zero, then break
            else
                break;
        }
    }

    // Print first array element
    cout << arr[0];
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 0, 3, 2 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given K
    int K = 5;

    // Prints the maximum
    // possible value of the
    // first array element
    getMax(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

  // Function to maximize
  // the first array element
  static void getMax(int arr[], int N, int K)
  {

    // Traverse the array
    for (int i = 1; i < N; i++)
    {

      // Initialize cur_val to a[i]
      int cur_val = arr[i];

      // If all operations
      // are not over yet
      while (K >= i)
      {

        // If current value is
        // greater than zero
        if (cur_val > 0)
        {

          // Incrementing first
          // element of array by 1
          arr[0] = arr[0] + 1;

          // Decrementing current
          // value of array by 1
          cur_val = cur_val - 1;

          // Decrementing number
          // of operations by i
          K = K - i;
        }

        // If current value is
        // zero, then break
        else
          break;
      }
    }

    // Print first array element
    System.out.print(arr[0]);
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 1, 0, 3, 2 };

    // Size of the array
    int N = arr.length;

    // Given K
    int K = 5;

    // Prints the maximum
    // possible value of the
    // first array element
    getMax(arr, N, K);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to maximize
# the first array element
def getMax(arr, N, K):

    # Traverse the array
    for i in range(1, N, 1):

        # Initialize cur_val to a[i]
        cur_val = arr[i]

        # If all operations
        # are not over yet
        while (K >= i):

            # If current value is
            # greater than zero
            if (cur_val > 0):

                # Incrementing first
                # element of array by 1
                arr[0] = arr[0] + 1

                # Decrementing current
                # value of array by 1
                cur_val = cur_val - 1

                # Decrementing number
                # of operations by i
                K = K - i

            # If current value is
            # zero, then break
            else:
                break

    # Print first array element
    print(arr[0])

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 0, 3, 2 ]

    # Size of the array
    N = len(arr)

    # Given K
    K = 5

    # Prints the maximum
    # possible value of the
    # first array element
    getMax(arr, N, K)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to maximize
// the first array element
static void getMax(int[] arr, int N,
                   int K)
{

    // Traverse the array
    for(int i = 1; i < N; i++)
    {

        // Initialize cur_val to a[i]
        int cur_val = arr[i];

        // If all operations
        // are not over yet
        while (K >= i)
        {

            // If current value is
            // greater than zero
            if (cur_val > 0)
            {

                // Incrementing first
                // element of array by 1
                arr[0] = arr[0] + 1;

                // Decrementing current
                // value of array by 1
                cur_val = cur_val - 1;

                // Decrementing number
                // of operations by i
                K = K - i;
            }

            // If current value is
            // zero, then break
            else
                break;
        }
    }

    // Print first array element
    Console.Write(arr[0]);
} 

// Driver code
static void Main()
{

    // Given array
    int[] arr = { 1, 0, 3, 2 };

    // Size of the array
    int N = arr.Length;

    // Given K
    int K = 5;

    // Prints the maximum
    // possible value of the
    // first array element
    getMax(arr, N, K);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
// javascript program for the above approach   
// Function to maximize
    // the first array element
    function getMax(arr , N , K) {

        // Traverse the array
        for (i = 1; i < N; i++) {

            // Initialize cur_val to a[i]
            var cur_val = arr[i];

            // If all operations
            // are not over yet
            while (K >= i) {

                // If current value is
                // greater than zero
                if (cur_val > 0) {

                    // Incrementing first
                    // element of array by 1
                    arr[0] = arr[0] + 1;

                    // Decrementing current
                    // value of array by 1
                    cur_val = cur_val - 1;

                    // Decrementing number
                    // of operations by i
                    K = K - i;
                }

                // If current value is
                // zero, then break
                else
                    break;
            }
        }

        // Print first array element
        document.write(arr[0]);
    }

    // Driver Code

        // Given array
        var arr = [ 1, 0, 3, 2 ];

        // Size of the array
        var N = arr.length;

        // Given K
        var K = 5;

        // Prints the maximum
        // possible value of the
        // first array element
        getMax(arr, N, K);

// This code is contributed by aashish1995
</script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)