# 重复从一个元素中加 K，从其他元素中减 K，使数组相等的最小运算

> 原文:[https://www . geeksforgeeks . org/最小运算通过重复从一个元素中添加 k 并从其他元素中减去 k 来使数组相等/](https://www.geeksforgeeks.org/minimum-operations-to-make-array-equal-by-repeatedly-adding-k-from-an-element-and-subtracting-k-from-other/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和一个整数 **K，**的任务是找到使[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 的所有元素相等的最小操作数。在一个操作中，从一个元素中减去 **K** ，并将该 **K** 添加到另一个元素中。如果不可能，则打印 **-1** 。

**示例:**

> **输入** : arr[] = {5，8，11}，K = 3
> **输出:** 1
> **解释:**
> **运算 1:** 从 **arr[2](=11)** 中减去 **3** ，再加 3 至 **arr[0](=5)。**
> 现在，数组**arr【】**的所有元素都相等。
> 
> **输入** : arr[] = {1，2，3，4}，K = 2
> **输出** : -1

**逼近**:这个问题可以用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。首先检查[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的所有元素之和是否能被 **N** 整除。如果不能被整除，意味着不可能使[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的所有元素相等。否则，尝试加减 **K** 的值，使每个元素等于**arr[]/n 的和。**按照以下步骤解决这个问题:

*   将变量 **sum** 初始化为 **0** ，以存储[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**的所有元素的总和。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并将**和**更新为**和+ arr[i]。**
*   如果**总和% N i** 不等于 **0，**则打印 **-1** 和**返回。**
*   初始化一个变量**值除法**为**和/N** 存储这么多值，数组的每个元素**arr【】**被存储，**计数**为 **0** 以存储使所有数组元素相等所需的最小操作数。
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代
    *   如果**值除法–arr[I]% K**的 [abs](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/) 不等于 **0，**则打印 **-1** 和**返回。**
    *   更新**计数**为**计数+** [abs](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/) 的**值除法–arr[I/k .**
*   完成以上步骤后，打印**计数/2** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// operations to make all the elements of
// the array equal
void miniOperToMakeAllEleEqual(int arr[], int n, int k)
{
    // Store the sum of the array arr[]
    int sum = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++) {

        sum += arr[i];
    }

    // If it is not possible to make all
    // array element equal
    if (sum % n) {
        cout << -1;
        return;
    }

    int valueAfterDivision = sum / n;

    // Store the minimum number of operations needed
    int count = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++) {

        if (abs(valueAfterDivision - arr[i]) % k != 0) {
            cout << -1;
            return;
        }

        count += abs(valueAfterDivision - arr[i]) / k;
    }

    // Finally, print the minimum number operation
    // to make array elements equal
    cout << count / 2 << endl;
}

// Driver Code
int main()
{

    // Given Input
    int n = 3, k = 3;
    int arr[3] = { 5, 8, 11 };

    // Function Call
    miniOperToMakeAllEleEqual(arr, n, k);
    // This code is contributed by Potta Lokesh
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG
{

  // Function to find the minimum number of
  // operations to make all the elements of
  // the array equal
  static void miniOperToMakeAllEleEqual(int arr[], int n, int k)
  {
    // Store the sum of the array arr[]
    int sum = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++) {

      sum += arr[i];
    }

    // If it is not possible to make all
    // array element equal
    if (sum % n != 0) {
      System.out.println(-1);
      return;
    }

    int valueAfterDivision = sum / n;

    // Store the minimum number of operations needed
    int count = 0;

    // Traverse through the array
    for (int i = 0; i < n; i++) {

      if (Math.abs(valueAfterDivision - arr[i]) % k != 0) {
        System.out.println(-1);
        return;
      }

      count += Math.abs(valueAfterDivision - arr[i]) / k;
    }

    // Finally, print the minimum number operation
    // to make array elements equal
    System.out.println((int)count / 2);
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given Input
    int n = 3, k = 3;
    int arr[] = { 5, 8, 11 };

    // Function Call
    miniOperToMakeAllEleEqual(arr, n, k);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number of
# operations to make all the elements of
# the array equal
def miniOperToMakeAllEleEqual(arr, n, k):

    # Store the sum of the array arr[]
    sum = 0

    # Traverse through the array
    for i in range(n):
        sum += arr[i]

    # If it is not possible to make all
    # array element equal
    if (sum % n):
        print(-1)
        return

    valueAfterDivision = sum // n

    # Store the minimum number of operations needed
    count = 0

    # Traverse through the array
    for i in range(n):
        if (abs(valueAfterDivision - arr[i]) % k != 0):
            print(-1)
            return

        count += abs(valueAfterDivision - arr[i]) // k

    # Finally, print the minimum number operation
    # to make array elements equal
    print(count // 2)

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 3
    k = 3
    arr = [ 5, 8, 11 ]

    # Function Call
    miniOperToMakeAllEleEqual(arr, n, k)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG
{

    // Function to find the minimum number of
    // operations to make all the elements of
    // the array equal
    static void miniOperToMakeAllEleEqual(int[] arr, int n,
                                          int k)
    {
        // Store the sum of the array arr[]
        int sum = 0;

        // Traverse through the array
        for (int i = 0; i < n; i++) {

            sum += arr[i];
        }

        // If it is not possible to make all
        // array element equal
        if (sum % n != 0) {
            Console.WriteLine(-1);
            return;
        }

        int valueAfterDivision = sum / n;

        // Store the minimum number of operations needed
        int count = 0;

        // Traverse through the array
        for (int i = 0; i < n; i++) {

            if (Math.Abs(valueAfterDivision - arr[i]) % k
                != 0) {
                Console.WriteLine(-1);
                return;
            }

            count += Math.Abs(valueAfterDivision - arr[i])
                     / k;
        }

        // Finally, print the minimum number operation
        // to make array elements equal
        Console.WriteLine((int)count / 2);
    }

    static void Main()
    {
        // Given Input
        int n = 3, k = 3;
        int[] arr = { 5, 8, 11 };

        // Function Call
        miniOperToMakeAllEleEqual(arr, n, k);
    }
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>
       // JavaScript program for the above approach

       // Function to find the minimum number of
       // operations to make all the elements of
       // the array equal
       function miniOperToMakeAllEleEqual(arr, n, k)
       {

           // Store the sum of the array arr[]
           let sum = 0;

           // Traverse through the array
           for (let i = 0; i < n; i++) {

               sum += arr[i];
           }

           // If it is not possible to make all
           // array element equal
           if (sum % n) {
               document.write(-1);
               return;
           }

           let valueAfterDivision = sum / n;

           // Store the minimum number of operations needed
           let count = 0;

           // Traverse through the array
           for (let i = 0; i < n; i++) {

               if (Math.abs(valueAfterDivision - arr[i]) % k != 0) {
                   document.write(-1);
                   return;
               }

               count += Math.abs(valueAfterDivision - arr[i]) / k;
           }

           // Finally, print the minimum number operation
           // to make array elements equal
           document.write(Math.floor(count / 2));
       }

       // Driver Code

       // Given Input
       let n = 3, k = 3;
       let arr = [5, 8, 11];

       // Function Call
       miniOperToMakeAllEleEqual(arr, n, k);

   // This code is contributed by Potta Lokesh

   </script>
```

**Output**

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)