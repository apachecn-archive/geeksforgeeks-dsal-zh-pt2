# 尽量减少加减偶数，使所有数组元素等于 K

> 原文:[https://www . geesforgeks . org/minimum-加减奇数-偶数-使所有数组元素等于-k/](https://www.geeksforgeeks.org/minimize-adding-odd-and-subtracting-even-numbers-to-make-all-array-elements-equal-to-k/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** 和一个整数 **K** ，任务是通过多次执行以下操作，找到使所有数组元素等于 **K** 所需的最小操作数:

*   将 **arr[i]** 转换为 **arr[i] + X** ，其中 **X** 为[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。
*   将 **arr[i]** 转换为**arr[I]–Y**，其中 **Y** 为[偶数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。

**示例:**

> **输入:** arr[] = {8，7，2，1，3}，K = 5
> **输出:** 8
> **解释:**要使给定数组的所有元素等于 K(= 5)，需要执行以下操作:
> arr[0] = arr[0] + X，X = 1
> arr[0]= arr[0]–Y，Y = 4
> arr[1]= arr[1]–Y，Y = 2 【T11 X = 3
> arr[3] = arr[3] + X，X = 1
> arr[4] = arr[4] + X，X = 1
> arr[4] = arr[4] + X，X = 1
> 
> **输入:** arr[] = {1，2，3，4，5，6，7}，K = 3
> **输出:** 9

**方法:**使用[贪婪技术](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。以下是观察结果:

> 偶数+偶数=偶数
> 偶数+奇数=奇数
> 奇数+奇数=偶数
> 奇数+偶数=奇数

按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下条件。
    *   如果 **K > arr[i]和(K–arr[I])% 2 = = 0**，则在 **arr[i]** 中加上两个奇数 **(X)** 。因此，总共需要 **2** 次操作。
    *   如果 **K > arr[i]和(K–arr[I])% 2！= 0** 然后在**arr【I】**中加上一个奇数 **(X)** 。因此，总共需要 **1** 次操作。
    *   如果 **K < arr[i]和(arr[I]–arr[I])% 2 = = 0**那么将一个偶数 **(Y)** 减去 **arr[i]** 。因此，总共需要 **1** 次操作。
    *   如果 **K < arr[i]和(K–arr[I])% 2！= 0** 然后在**arr【I】**中加上一个奇数 **(X)** ，从**arr【I】**中减去一个偶数 **(Y)** 。因此，总共需要 **2** 次操作。
*   最后，打印使所有数组元素等于 **K** 所需的操作总数。

下面是上述方法的实现

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum operations
// required to make array elements equal to K
int MinOperation(int arr[], int N, int K)
{
    // Stores minimum count of operations
    int cntOpe = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // If K is greater than arr[i]
        if (K > arr[i]) {

            // If (K - arr[i]) is even
            if ((K - arr[i]) % 2 == 0) {

                // Update cntOpe
                cntOpe += 2;
            }
            else {

                // Update cntOpe
                cntOpe += 1;
            }
        }

        // If K is less than arr[i]
        else if (K < arr[i]) {

            // If (arr[i] - K) is even
            if ((K - arr[i]) % 2 == 0) {

                // Update cntOpe
                cntOpe += 1;
            }
            else {

                // Update cntOpe
                cntOpe += 2;
            }
        }
    }

    return cntOpe;
}

// Driver Code
int main()
{
    int arr[] = { 8, 7, 2, 1, 3 };
    int K = 5;
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << MinOperation(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG{

// Function to find the minimum
// operations required to make
// array elements equal to K
public static int MinOperation(int arr[],
                               int N, int K)
{
  // Stores minimum count of
  // operations
  int cntOpe = 0;

  // Traverse the given array
  for (int i = 0; i < N; i++)
  {
    // If K is greater than
    // arr[i]
    if (K > arr[i])
    {
      // If (K - arr[i]) is even
      if ((K - arr[i]) % 2 == 0)
      {
        // Update cntOpe
        cntOpe += 2;
      }
      else
      {
        // Update cntOpe
        cntOpe += 1;
      }
    }

    // If K is less than
    // arr[i]
    else if (K < arr[i])
    {
      // If (arr[i] - K) is
      // even
      if ((K - arr[i]) % 2 == 0)
      {
        // Update cntOpe
        cntOpe += 1;
      }
      else
      {
        // Update cntOpe
        cntOpe += 2;
      }
    }
  }

  return cntOpe;
}

// Driver code
public static void main(String[] args)
{
  int arr[] = {8, 7, 2, 1, 3};
  int K = 5;
  int N = arr.length;
  System.out.println(
  MinOperation(arr, N, K));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the minimum operations
# required to make array elements equal to K
def MinOperation(arr, N, K):

    # Stores minimum count of operations
    cntOpe = 0

    # Traverse the given array
    for i in range(N):

        # If K is greater than arr[i]
        if (K > arr[i]):

            # If (K - arr[i]) is even
            if ((K - arr[i]) % 2 == 0):

                # Update cntOpe
                cntOpe += 2

            else:

                # Update cntOpe
                cntOpe += 1

        # If K is less than arr[i]
        elif (K < arr[i]):

            # If (arr[i] - K) is even
            if ((K - arr[i]) % 2 == 0):

                # Update cntOpe
                cntOpe += 1

            else:

                # Update cntOpe
                cntOpe += 2

    return cntOpe

# Driver Code
arr = [ 8, 7, 2, 1, 3 ]
K = 5
N = len(arr)

print(MinOperation(arr, N, K))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to find the minimum
// operations required to make
// array elements equal to K
public static int MinOperation(int []arr,
                               int N, int K)
{

  // Stores minimum count of
  // operations
  int cntOpe = 0;

  // Traverse the given array
  for(int i = 0; i < N; i++)
  {

    // If K is greater than
    // arr[i]
    if (K > arr[i])
    {

      // If (K - arr[i]) is even
      if ((K - arr[i]) % 2 == 0)
      {

        // Update cntOpe
        cntOpe += 2;
      }
      else
      {

        // Update cntOpe
        cntOpe += 1;
      }
    }

    // If K is less than
    // arr[i]
    else if (K < arr[i])
    {

      // If (arr[i] - K) is
      // even
      if ((K - arr[i]) % 2 == 0)
      {

        // Update cntOpe
        cntOpe += 1;
      }
      else
      {

        // Update cntOpe
        cntOpe += 2;
      }
    }
  }
  return cntOpe;
}

// Driver code
public static void Main(String[] args)
{
  int []arr = {8, 7, 2, 1, 3};
  int K = 5;
  int N = arr.Length;

  Console.WriteLine(
  MinOperation(arr, N, K));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

// Function to find the minimum
// operations required to make
// array elements equal to K
function MinOperation(arr, N, K)
{
  // Stores minimum count of
  // operations
  let cntOpe = 0;

  // Traverse the given array
  for (let i = 0; i < N; i++)
  {
    // If K is greater than
    // arr[i]
    if (K > arr[i])
    {
      // If (K - arr[i]) is even
      if ((K - arr[i]) % 2 == 0)
      {
        // Update cntOpe
        cntOpe += 2;
      }
      else
      {
        // Update cntOpe
        cntOpe += 1;
      }
    }

    // If K is less than
    // arr[i]
    else if (K < arr[i])
    {
      // If (arr[i] - K) is
      // even
      if ((K - arr[i]) % 2 == 0)
      {
        // Update cntOpe
        cntOpe += 1;
      }
      else
      {
        // Update cntOpe
        cntOpe += 2;
      }
    }
  }

  return cntOpe;
}

    // Driver Code

    let arr = [8, 7, 2, 1, 3];
  let K = 5;
  let N = arr.length;
  document.write(
  MinOperation(arr, N, K));

</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)