# 用第二小元素重复替换最大的数组元素

使所有数组元素相等

> 原文:[https://www . geesforgeks . org/make-all-array-elements-equal-by-reply-replace-最大的 array-element-with-second-mini-element/](https://www.geeksforgeeks.org/make-all-array-elements-equal-by-repeatedly-replacing-largest-array-element-with-the-second-smallest-element/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**arr【】**，任务是通过用第二大数组元素替换**最大的**数组元素来计算使所有数组元素相等所需的操作次数，第二大数组元素严格来说是小于最大数组元素的**。**

****示例:****

> ****输入:** arr[ ] = {1，1，2，2，3}
> **输出:** 4
> **说明:**使所有数组元素相等总共需要 4 次运算。
> **操作 1:** 将最大的元素(= arr[4] = 3)替换为次大的元素(= arr[2] = 2)。数组 arr[]修改为{1，1，2，2， **2** }。
> **操作 2:** 将最大的元素(= arr[2] = 2)替换为次大的元素(= arr[0] = 1)。数组 arr[]修改为{1，1， **1** ，2，2}
> **操作 3:** 用下一个最大的元素(= arr[0] = 1)替换最大的元素(= arr[3] = 2)。数组 arr[]修改为{1，1，1， **1** ，2}
> **操作 4:** 用下一个最大的元素(= arr[0] = 1)替换最大的元素(= arr[4] = 2)。数组 arr[]修改为{1，1，1，1， **1****
> 
> ****输入:** arr[ ] = {1，1，1 }
> T3】输出: 0**

****方法:**按照以下步骤解决问题:**

*   **初始化一个变量，说**值 _ 计数= 0** 和**运算 _ 计数= 0** 。**
*   **[按升序排列数组**arr[]**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。**
*   **[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，检查当前元素是否大于上一个元素。如果发现为真**，**则增加**值 _ 计数**至 **1** 。**
*   **每次迭代，在**运算 _ 计数**中加入**值 _ 计数**。**
*   **最后打印**运算 _ 计数**的值。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program to Make all array elements
// equal by perform certain operation
#include <bits/stdc++.h>
using namespace std;

// Function to count number of operations
// required to make all array elements equal
int operation(int arr[], int n)
{
    // Initialize the val_count
    // and operation_count by 0.
    int val_count = 0, operation_count = 0;

    // Sort the array in ascending order.
    sort(arr, arr + n);

    for (int i = 1; i < n; i++) {

        // Current element greater
        // than the previous element
        if (arr[i - 1] < arr[i]) {

            // If yes then update the
            // val_count by 1.
            val_count++;
        }

        // Add the value_count in operation_count.
        operation_count = operation_count + val_count;
    }
    // Return the operation_count
    return operation_count;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 1, 1, 2, 2, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << operation(arr, n);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.Arrays;
import java.io.*;

class GFG
{

  // Function to count number of operations
  // required to make all array elements equal
  static int operation(int arr[], int n)
  {

    // Initialize the val_count
    // and operation_count by 0.
    int val_count = 0, operation_count = 0;

    // Sort the array in ascending order.
    Arrays.sort(arr);

    for (int i = 1; i < n; i++) {

      // Current element greater
      // than the previous element
      if (arr[i - 1] < arr[i]) {

        // If yes then update the
        // val_count by 1.
        val_count++;
      }

      // Add the value_count in operation_count.
      operation_count = operation_count + val_count;
    }
    // Return the operation_count
    return operation_count;
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given Input
    int arr[] = { 1, 1, 2, 2, 3 };
    int n = arr.length;

    // Function Call
    System.out.println( operation(arr, n));
  }
}

// This code is contributed by Potta Lokesh
```

## **蟒蛇 3**

```
# Python3 program to Make all array elements
# equal by perform certain operation

# Function to count number of operations
# required to make all array elements equal
def operation(arr, n):

     # Initialize the val_count
    # and operation_count by 0.
    val_count = 0
    operation_count = 0

    # Sort the array in ascending order.
    arr.sort()
    for i in range(1, n):

         # Current element greater
        # than the previous element
        if arr[i-1] < arr[i]:

             # If yes then update the
            # val_count by 1.
            val_count += 1

        # Add the value_count in operation_count.  
        operation_count += val_count

    # Return the operation_count
    return operation_count

# Driver code
arr = [1, 1, 2, 2, 3]
n = len(arr)
print(operation(arr, n))

# This code is contributed by Parth Manchanda
```

## **C#**

```
// C# program for the above approach
using System;

public class GFG
{

  // Function to count number of operations
  // required to make all array elements equal
  static int operation(int []arr, int n)
  {

    // Initialize the val_count
    // and operation_count by 0.
    int val_count = 0, operation_count = 0;

    // Sort the array in ascending order.
    Array.Sort(arr);

    for (int i = 1; i < n; i++) {

      // Current element greater
      // than the previous element
      if (arr[i - 1] < arr[i]) {

        // If yes then update the
        // val_count by 1.
        val_count++;
      }

      // Add the value_count in operation_count.
      operation_count = operation_count + val_count;
    }

    // Return the operation_count
    return operation_count;
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given Input
    int []arr = { 1, 1, 2, 2, 3 };
    int n = arr.Length;

    // Function Call
    Console.WriteLine( operation(arr, n));
  }
}

// This code is contributed by Amit Katiyar
```

## **java 描述语言**

```
// Javascript program to Make all array elements
// equal by perform certain operation

// Function to count number of operations
// required to make all array elements equal
function operation(arr, n) {
  // Initialize the val_count
  // and operation_count by 0.
  let val_count = 0,
    operation_count = 0;

  // Sort the array in ascending order.
  arr.sort();

  for (let i = 1; i < n; i++) {
    // Current element greater
    // than the previous element
    if (arr[i - 1] < arr[i]) {
      // If yes then update the
      // val_count by 1.
      val_count++;
    }

    // Add the value_count in operation_count.
    operation_count = operation_count + val_count;
  }
  // Return the operation_count
  return operation_count;
}

// Driver Code

// Given Input
let arr = [1, 1, 2, 2, 3];
let n = arr.length;

// Function Call
document.write(operation(arr, n));

// This code is contributed by gfgking.
```

****Output:** 

```
4
```** 

*****时间复杂度:** O(NLogN)*
***辅助空间:** O(1)***