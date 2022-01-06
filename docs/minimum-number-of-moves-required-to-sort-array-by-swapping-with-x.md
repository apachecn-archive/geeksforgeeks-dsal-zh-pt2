# 通过交换 X 对数组进行排序所需的最小移动次数

> 原文:[https://www . geeksforgeeks . org/最小移动次数-需要通过交换 x 对数组进行排序/](https://www.geeksforgeeks.org/minimum-number-of-moves-required-to-sort-array-by-swapping-with-x/)

给定一个整数[数组](https://www.geeksforgeeks.org/array-data-structure/)， **arr[]** 大小为 **N** 和一个整数 **X** 。任务是通过将大于 **X** 的任何数组元素与 **X** 交换任意次数，以最小移动次数将数组按递增顺序排序。如果无法打印 **-1** 。

**示例:**

> **输入:** arr[] = {1，3，4，6，5}，X = 2
> **输出:** 3
> **解释:**用 X = 2 交换 arr[1] = 3，arr[]变成{1，2，4，6，5}，X = 3。
> 用 X = 3 交换 arr[2] = 4，arr[]变成{1，2，3，6，5}，X = 4。
> 用 X = 4 交换 arr[3] = 6，arr[]变成{1，2，3，4，5}。
> 
> **输入:** arr[] = {7，5}，X = 6
> **输出:** -1
> **说明:**无法使用给定条件对数组进行排序。

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。按照以下步骤解决问题:

*   将变量**和**初始化为 0，以存储所需的结果。
*   [使用变量 **i** 在范围**【0，N-1】**内遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]**
    *   如果 **arr[i] > arr[i+1]** ，[的值使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，I】**中迭代，并用 **X** 交换 **arr[j]** ，如果 **arr[j] > X** 的值，同时将 **ans** 的值递增 1。
*   [检查数组是否排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)。如果没有，则更新 **ans** 为-1。
*   打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// moves required to sort the array
void minSwaps(int a[], int n, int x)
{
    int c = 0;

    // Store the required number of moves
    int ans = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < n - 1; i++) {

        // If mismatch found
        if (a[i] > a[i + 1]) {

            // Start from first index to
            // maintain the increasing order
            // of array
            for (int k = 0; k <= i; k++) {

                // If true, swap a[k] and x
                // and increment ans by 1
                if (a[k] > x) {
                    int tt = a[k];
                    a[k] = x;
                    x = tt;
                    ans++;
                }
            }
        }
    }

    // Check if now the array is sorted,
    // if not, set c=1
    for (int i = 0; i < n - 1; i++) {
        if (a[i] > a[i + 1]) {
            c = 1;
            break;
        }
    }

    // Print the result
    if (c == 1) {
        cout << "-1";
    }
    else {
        cout << ans;
    }
}

// Driver Code
int main()
{
    // Given Input
    int n = 5;
    int x = 2;
    int a[] = { 1, 3, 4, 6, 5 };

    // Function Call
    minSwaps(a, n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find the minimum number of
  // moves required to sort the array
  static void minSwaps(int a[], int n, int x)
  {
    int c = 0;

    // Store the required number of moves
    int ans = 0;

    // Traverse the array, arr[]
    for (int i = 0; i < n - 1; i++) {

      // If mismatch found
      if (a[i] > a[i + 1]) {

        // Start from first index to
        // maintain the increasing order
        // of array
        for (int k = 0; k <= i; k++) {

          // If true, swap a[k] and x
          // and increment ans by 1
          if (a[k] > x) {
            int tt = a[k];
            a[k] = x;
            x = tt;
            ans++;
          }
        }
      }
    }

    // Check if now the array is sorted,
    // if not, set c=1
    for (int i = 0; i < n - 1; i++) {
      if (a[i] > a[i + 1]) {
        c = 1;
        break;
      }
    }

    // Print the result
    if (c == 1) {
      System.out.println("-1");
    }
    else {
      System.out.println(ans);
    }
  }

  // Driver Code
  public static void main (String[] args)
  {

    // Given Input
    int n = 5;
    int x = 2;
    int a[] = { 1, 3, 4, 6, 5 };

    // Function Call
    minSwaps(a, n, x);
  }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum number of
# moves required to sort the array
def minSwaps(a, n, x):

    c = 0

    # Store the required number of moves
    ans = 0

    # Traverse the array, arr[]
    for i in range(n - 1):

        # If mismatch found
        if (a[i] > a[i + 1]):

            # Start from first index to
            # maintain the increasing order
            # of array
            for k in range(i + 1):

                # If true, swap a[k] and x
                # and increment ans by 1
                if (a[k] > x):
                    tt = a[k]
                    a[k] = x
                    x = tt
                    ans += 1

    # Check if now the array is sorted,
    # if not, set c=1
    for i in range(n - 1):
        if (a[i] > a[i + 1]):
            c = 1
            break

    # Print the result
    if (c == 1):
        print("-1")
    else:
        print(ans)

# Driver Code
if __name__ == '__main__':

    # Given Input
    n = 5
    x = 2
    a = [ 1, 3, 4, 6, 5 ]

    # Function Call
    minSwaps(a, n, x)

# This code is contributed by ipg2016107
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum number of
// moves required to sort the array
static void minSwaps(int[] a, int n, int x)
{
    int c = 0;

    // Store the required number of moves
    int ans = 0;

    // Traverse the array, arr[]
    for(int i = 0; i < n - 1; i++)
    {

        // If mismatch found
        if (a[i] > a[i + 1])
        {

            // Start from first index to
            // maintain the increasing order
            // of array
            for(int k = 0; k <= i; k++)
            {

                // If true, swap a[k] and x
                // and increment ans by 1
                if (a[k] > x)
                {
                    int tt = a[k];
                    a[k] = x;
                    x = tt;
                    ans++;
                }
            }
        }
    }

    // Check if now the array is sorted,
    // if not, set c=1
    for(int i = 0; i < n - 1; i++)
    {
        if (a[i] > a[i + 1])
        {
            c = 1;
            break;
        }
    }

    // Print the result
    if (c == 1)
    {
        Console.Write("-1");
    }
    else
    {
        Console.Write(ans);
    }
}

// Driver Code
static public void Main()
{

    // Given Input
    int n = 5;
    int x = 2;
    int[] a = { 1, 3, 4, 6, 5 };

    // Function Call
    minSwaps(a, n, x);
}
}

// This code is contributed by avijitmondal1998
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the minimum number of
// moves required to sort the array
function minSwaps(a, n, x) {
    let c = 0;

    // Store the required number of moves
    let ans = 0;

    // Traverse the array, arr[]
    for (let i = 0; i < n - 1; i++) {

        // If mismatch found
        if (a[i] > a[i + 1]) {

            // Start from first index to
            // maintain the increasing order
            // of array
            for (let k = 0; k <= i; k++) {

                // If true, swap a[k] and x
                // and increment ans by 1
                if (a[k] > x) {
                    let tt = a[k];
                    a[k] = x;
                    x = tt;
                    ans++;
                }
            }
        }
    }

    // Check if now the array is sorted,
    // if not, set c=1
    for (let i = 0; i < n - 1; i++) {
        if (a[i] > a[i + 1]) {
            c = 1;
            break;
        }
    }

    // Print the result
    if (c == 1) {
        document.write("-1");
    }
    else {
        document.write(ans);
    }
}

// Driver Code

// Given Input
let n = 5;
let x = 2;
let a = [1, 3, 4, 6, 5];

// Function Call
minSwaps(a, n, x);

// This code is contributed by gfgking.
</script>
```

**Output**

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*