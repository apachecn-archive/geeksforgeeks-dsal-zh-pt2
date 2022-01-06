# 计数具有偶数位“或”的子阵列

> 原文:[https://www . geesforgeks . org/count-subarrays-having-bitwise-or/](https://www.geeksforgeeks.org/count-subarrays-having-even-bitwise-or/)

给定一个由 **N** 个正整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的数量，这些子数组的元素的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为偶数。

**示例:**

> **输入:** arr[] = {1，5，4，2，6}
> **输出:** 6
> **解释:**
> 偶位运算的子阵为{4}、{2}、{6}、{2，6 }、{4，2}、{4，2，6 }。
> 因此，具有偶数位“或”的子阵列的数量是 6。
> 
> **输入:** arr[] ={2，5，6，8}
> **输出:** 4

**天真法:**解决问题最简单的方法是[生成所有子阵](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)，如果任一子阵的[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 为**甚至**，则增加此类子阵的个数。检查所有子阵列后，打印作为结果获得的**计数**。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效法:**通过观察子阵中的任何一个元素如果是**奇数**，那么肯定会使子阵的[T5【按位 OR】T7】为奇数，可以优化上述方法。因此，我们的想法是找出数组中偶数的连续段的长度，并将其贡献添加到总计数中。
按照以下步骤解决问题:](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)

*   初始化一个变量，比如说**计数**，以存储子阵列的总数，这些子阵列具有 [**位“或”**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 为偶数。
*   初始化一个变量，比如 **L** ，来存储相邻偶数元素的计数。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，并执行以下步骤:
    *   [如果当前元素为偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，那么将 **L** 的值增加 **1** 。
    *   否则，将值 **L * (L + 1) / 2** 添加到变量**计数**中，并将 **L** 更新为 **0** 。
*   如果 **L** 的值不为零，那么将 **L*(L + 1)/2** 加到变量**计数**中。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// subarrays having even Bitwise OR
int bitOr(int arr[], int N)
{
    // Store number of subarrays
    // having even bitwise OR
    int count = 0;

    // Store the length of the current
    // subarray having even numbers
    int length = 0;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // If the element is even
        if (arr[i] % 2 == 0) {

            // Increment size of the
            // current continuous sequence
// of even array elements
            length++;
        }

        // If arr[i] is odd
        else {

            // If length is non zero
            if (length != 0) {

                // Adding contribution of
                // subarrays consisting
                // only of even numbers
                count += ((length)
                          * (length + 1))
                         / 2;
            }

            // Make length of subarray as 0
            length = 0;
        }
    }

    // Add contribution of previous subarray
    count += ((length) * (length + 1)) / 2;

    // Return total count of subarrays
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 5, 4, 2, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << bitOr(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count the number of
// subarrays having even Bitwise OR
static int bitOr(int arr[], int N)
{

    // Store number of subarrays
    // having even bitwise OR
    int count = 0;

    // Store the length of the current
    // subarray having even numbers
    int length = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // If the element is even
        if (arr[i] % 2 == 0)
        {

            // Increment size of the
            // current continuous sequence
            // of even array elements
            length++;
        }

        // If arr[i] is odd
        else
        {

            // If length is non zero
            if (length != 0)
            {

                // Adding contribution of
                // subarrays consisting
                // only of even numbers
                count += ((length) * (length + 1)) / 2;
            }

            // Make length of subarray as 0
            length = 0;
        }
    }

    // Add contribution of previous subarray
    count += ((length) * (length + 1)) / 2;

    // Return total count of subarrays
    return count;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 5, 4, 2, 6 };
    int N = arr.length;

    // Function Call
    System.out.print(bitOr(arr, N));
}
}

// This code is contributed by splevel62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# subarrays having even Bitwise OR
def bitOr(arr, N):

    # Store number of subarrays
    # having even bitwise OR
    count = 0

    # Store the length of the current
    # subarray having even numbers
    length = 0

    # Traverse the array
    for i in range(N):

        # If the element is even
        if (arr[i] % 2 == 0):

            # Increment size of the
            # current continuous sequence
            # of even array elements
            length += 1

        # If arr[i] is odd
        else:

            # If length is non zero
            if (length != 0):

                # Adding contribution of
                # subarrays consisting
                # only of even numbers
                count += ((length) * (length + 1)) // 2

            # Make length of subarray as 0
            length = 0

    # Add contribution of previous subarray
    count += ((length) * (length + 1)) // 2

    # Return total count of subarrays
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 5, 4, 2, 6 ]
    N = len(arr)

    # Function Call
    print (bitOr(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to count the number of
  // subarrays having even Bitwise OR
  static int bitOr(int[] arr, int N)
  {

    // Store number of subarrays
    // having even bitwise OR
    int count = 0;

    // Store the length of the current
    // subarray having even numbers
    int length = 0;

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

      // If the element is even
      if (arr[i] % 2 == 0)
      {

        // Increment size of the
        // current continuous sequence
        // of even array elements
        length++;
      }

      // If arr[i] is odd
      else
      {

        // If length is non zero
        if (length != 0)
        {

          // Adding contribution of
          // subarrays consisting
          // only of even numbers
          count += ((length) * (length + 1)) / 2;
        }

        // Make length of subarray as 0
        length = 0;
      }
    }

    // Add contribution of previous subarray
    count += ((length) * (length + 1)) / 2;

    // Return total count of subarrays
    return count;
  }

  // Driver code
  static void Main()
  {
    int[] arr = { 1, 5, 4, 2, 6 };
    int N = arr.Length;

    // Function Call
    Console.Write(bitOr(arr, N));
  }
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// subarrays having even Bitwise OR
function bitOr(arr, N)
{
    // Store number of subarrays
    // having even bitwise OR
    var count = 0;

    // Store the length of the current
    // subarray having even numbers
    var length = 0;
    var i;

    // Traverse the array
    for (i = 0; i < N; i++) {

        // If the element is even
        if (arr[i] % 2 == 0) {

            // Increment size of the
            // current continuous sequence
// of even array elements
            length++;
        }

        // If arr[i] is odd
        else {

            // If length is non zero
            if (length != 0) {

                // Adding contribution of
                // subarrays consisting
                // only of even numbers
                count += Math.floor((length)
                          * (length + 1)
                         / 2);
            }

            // Make length of subarray as 0
            length = 0;
        }
    }

    // Add contribution of previous subarray
    count += Math.floor((length) * (length + 1) / 2);

    // Return total count of subarrays
    return count;
}

// Driver Code

    var arr = [1, 5, 4, 2, 6]
    var N = arr.length;

    // Function Call
    document.write(bitOr(arr, N));

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)