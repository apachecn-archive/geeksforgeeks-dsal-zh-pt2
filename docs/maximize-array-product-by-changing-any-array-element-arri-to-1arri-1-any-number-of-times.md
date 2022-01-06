# 通过将任意数组元素 arr[i]更改为(-1)* arr[I]–1 任意次来最大化数组乘积

> 原文:[https://www . geeksforgeeks . org/最大化-数组-产品-通过改变任意数组元素-arri-to-1 arri-1-任意次数/](https://www.geeksforgeeks.org/maximize-array-product-by-changing-any-array-element-arri-to-1arri-1-any-number-of-times/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过将每个数组元素 **arr[i]** 更改为**(-1)* arr[I]–1**任意多次来修改数组元素，以使数组的乘积最大化。

**示例:**

> ***输入:** arr[] = {-3，0，1}*
> ***输出:** 2 -1 -2*
> ***解释:***
> *对数组元素执行以下操作可使乘积最大化:*
> *对 arr[0]应用该操作一次，arr[0]=(-1)*(-3)–1 = 2。*
> *对 arr[1]应用操作一次，arr[1]= 0–1 =-1。*
> *对 arr[2]进行一次操作，arr[2]=-1–1 =-2。*
> *修改后的数组是{2，-1，-2}带产品 4，这是最大可能。*
> 
> ***输入:** arr[] = {-9，2，0，1，-5，3，16}*
> ***输出:** -9 -3 -1 -2 -5 -4 16*

**方法:**给定的问题可以基于以下观察来解决:

*   为了使乘积最大，元素的绝对值应该更高，因为运算减少了负元素的绝对值。因此，给定的操作应该只应用于正值。
*   如果元素的数量是奇数，那么对最高绝对值的元素执行运算，因为奇数个负数的乘积是负数。因此，将产品的一个正数更改为正数和最大值。
*   对负数执行运算会减少其绝对值。因此，找到具有最大绝对值的元素，并对其应用一次操作，因为这将使乘积减少最少。

按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，对于每个元素 **arr[i]** ，检查 **arr[i] ≥ 0** 。如果发现为真，则更新**arr[I]=(-1)* arr[I]–1**。否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   数组遍历后，[检查 **N** 的值是否为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)。如果发现为真，则找到绝对值最大的元素，并对其应用一次操作。
*   完成以上步骤后，打印修改后的数组 **arr[]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find array with maximum
// product by changing array
// elements to (-1)arr[i] - 1
void findArrayWithMaxProduct(int arr[],
                             int N)
{
    // Traverse the array
    for (int i = 0; i < N; i++)

        // Applying the operation on
        // all the positive elements
        if (arr[i] >= 0) {
            arr[i] = -arr[i] - 1;
        }

    if (N % 2 == 1) {

        // Stores maximum element in array
        int max_element = -1;

        // Stores index of maximum element
        int index = -1;

        for (int i = 0; i < N; i++)

            // Check if current element
            // is greater than the
            // maximum element
            if (abs(arr[i]) > max_element) {

                max_element = abs(arr[i]);

                // Find index of the
                // maximum element
                index = i;
            }

        // Perform the operation on the
        // maximum element
        arr[index] = -arr[index] - 1;
    }

    // Print the elements of the array
    for (int i = 0; i < N; i++)
        printf("%d ", arr[i]);
}

// Driver Code
int main()
{
    int arr[] = { -3, 0, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findArrayWithMaxProduct(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
class GFG
{

  // Function to find array with maximum
  // product by changing array
  // elements to (-1)arr[i] - 1
  static void findArrayWithMaxProduct(int arr[], int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)

      // Applying the operation on
      // all the positive elements
      if (arr[i] >= 0)
      {
        arr[i] = -arr[i] - 1;
      }

    if (N % 2 == 1)
    {

      // Stores maximum element in array
      int max_element = -1;

      // Stores index of maximum element
      int index = -1;

      for (int i = 0; i < N; i++)

        // Check if current element
        // is greater than the
        // maximum element
        if (Math.abs(arr[i]) > max_element) {

          max_element = Math.abs(arr[i]);

          // Find index of the
          // maximum element
          index = i;
        }

      // Perform the operation on the
      // maximum element
      arr[index] = -arr[index] - 1;
    }

    // Print the elements of the array
    for (int i = 0; i < N; i++)
      System.out.print(arr[i] + " ");
  }

  // Driver Code
  public static void main(String[] args)
  {
    int arr[] = { -3, 0, 1 };
    int N = arr.length;

    // Function Call
    findArrayWithMaxProduct(arr, N);
  }
}

// This code is contributed by jithin.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find array with maximum
# product by changing array
# elements to (-1)arr[i] - 1
def findArrayWithMaxProduct(arr, N):

    # Traverse the array
    for i in range(N):

        # Applying the operation on
        # all the positive elements
        if (arr[i] >= 0):
            arr[i] = -arr[i] - 1
    if (N % 2 == 1):

        # Stores maximum element in array
        max_element = -1

        # Stores index of maximum element
        index = -1
        for i in range(N):

            # Check if current element
            # is greater than the
            # maximum element
            if (abs(arr[i]) > max_element):
                max_element = abs(arr[i])

                # Find index of the
                # maximum element
                index = i

        # Perform the operation on the
        # maximum element
        arr[index] = -arr[index] - 1

    # Prthe elements of the array
    for i in arr:
        print(i, end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [-3, 0, 1]
    N = len(arr)

    # Function Call
    findArrayWithMaxProduct(arr, N)

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

  // Function to find array with maximum
  // product by changing array
  // elements to (-1)arr[i] - 1
  static void findArrayWithMaxProduct(int[] arr, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)

      // Applying the operation on
      // all the positive elements
      if (arr[i] >= 0)
      {
        arr[i] = -arr[i] - 1;
      }

    if (N % 2 == 1)
    {

      // Stores maximum element in array
      int max_element = -1;

      // Stores index of maximum element
      int index = -1;
      for (int i = 0; i < N; i++)

        // Check if current element
        // is greater than the
        // maximum element
        if (Math.Abs(arr[i]) > max_element) {

          max_element = Math.Abs(arr[i]);

          // Find index of the
          // maximum element
          index = i;
        }

      // Perform the operation on the
      // maximum element
      arr[index] = -arr[index] - 1;
    }

    // Print the elements of the array
    for (int i = 0; i < N; i++)
      Console.Write(arr[i] + " ");
  }

// Driver Code
static public void Main()
{
    int[] arr = { -3, 0, 1 };
    int N = arr.Length;

    // Function Call
    findArrayWithMaxProduct(arr, N);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
      // JavaScript program for the above approach
      // Function to find array with maximum
      // product by changing array
      // elements to (-1)arr[i] - 1
      function findArrayWithMaxProduct(arr, N)
      {

        // Traverse the array
        for (var i = 0; i < N; i++)

          // Applying the operation on
          // all the positive elements
          if (arr[i] >= 0) {
            arr[i] = -arr[i] - 1;
          }

        if (N % 2 === 1)
        {

          // Stores maximum element in array
          var max_element = -1;

          // Stores index of maximum element
          var index = -1;
          for (var i = 0; i < N; i++)

            // Check if current element
            // is greater than the
            // maximum element
            if (Math.abs(arr[i]) > max_element)
            {
              max_element = Math.abs(arr[i]);

              // Find index of the
              // maximum element
              index = i;
            }

          // Perform the operation on the
          // maximum element
          arr[index] = -arr[index] - 1;
        }

        // Print the elements of the array
        for (var i = 0; i < N; i++) document.write(arr[i] + " ");
      }

      // Driver Code
      var arr = [-3, 0, 1];
      var N = arr.length;

      // Function Call
      findArrayWithMaxProduct(arr, N);

      // This code is contributed by rdtank.
    </script>
```

**Output:** 

```
2 -1 -2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)