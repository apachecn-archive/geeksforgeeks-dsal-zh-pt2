# 最小化偶数和奇数阵列元素计数相等所需的增量

> 原文:[https://www . geeksforgeeks . org/最小化增量-要求使偶数和奇数数组元素的计数相等/](https://www.geeksforgeeks.org/minimize-increments-required-to-make-count-of-even-and-odd-array-elements-equal/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到需要对数组元素执行的最小增量 **1** ，使得给定数组中偶数和奇数的[计数相等。如果不可能，则打印【T10 "-" 1 "。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

**示例:**

> **输入:** arr[] = {1，3，4，9}
> **输出:** 1
> **说明:**
> 数组中偶数和奇数的个数分别为 1 和 3。
> 将 arr[3] ( = 9)加 1，使其为 10(偶数)。
> 所以，由于偶数和奇数的计数在上述步骤后是相同的。因此，最小增量操作是 1。
> 
> **输入:** arr[] = {2，2，2，2 }
> T3】输出: 2

**方法:**解决给定问题的思路如下:

*   如果 **N** 为**偶数**，则[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并统计**奇数**和**偶数**整数。偶数和奇数的计数除以 2 的绝对差给出了使偶数和奇数相等所需的最小增量操作。
*   如果 **N** 为**奇数**，则不可能使偶数和奇数相等，因此打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find min operations
// to make even and odd count equal
int minimumIncrement(int arr[], int N)
{
    // Odd size will never make odd
    // and even counts equal
    if (N % 2 != 0) {
        cout << "-1";
        exit(0);
    }

    // Stores the count of even
    // numbers in the array arr[]
    int cntEven = 0;

    // Stores count of odd numbers
    // in the array arr[]
    int cntOdd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // If arr[i] is an
        // even number
        if (arr[i] % 2 == 0) {

            // Update cntEven
            cntEven += 1;
        }
    }

    // Odd numbers in arr[]
    cntOdd = N - cntEven;

    // Return absolute difference
    // divided by 2
    return abs(cntEven - cntOdd) / 2;
}

// Driver Code
int main()
{
    int arr[] = { 1, 3, 4, 9 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << minimumIncrement(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;
class GFG
{

// Function to find min operations
// to make even and odd count equal
static int minimumIncrement(int arr[], int N)
{

    // Odd size will never make odd
    // and even counts equal
    if (N % 2 != 0)
    {
        System.out.println( "-1");
        System.exit(0);
    }

    // Stores the count of even
    // numbers in the array arr[]
    int cntEven = 0;

    // Stores count of odd numbers
    // in the array arr[]
    int cntOdd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // If arr[i] is an
        // even number
        if (arr[i] % 2 == 0)
        {

            // Update cntEven
            cntEven += 1;
        }
    }

    // Odd numbers in arr[]
    cntOdd = N - cntEven;

    // Return absolute difference
    // divided by 2
    return Math.abs(cntEven - cntOdd) / 2;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 3, 4, 9 };
    int N = arr.length;

    // Function call
    System.out.println(minimumIncrement(arr, N));
}
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find min operations
# to make even and odd count equal
def minimumIncrement(arr, N):

    # Odd size will never make odd
    # and even counts equal
    if (N % 2 != 0):
        print("-1")
        return

    # Stores the count of even
    # numbers in the array arr[]
    cntEven = 0

    # Stores count of odd numbers
    # in the array arr[]
    cntOdd = 0

    # Traverse the array arr[]
    for i in range(N):

        # If arr[i] is an
        # even number
        if (arr[i] % 2 == 0):

            # Update cntEven
            cntEven += 1

    # Odd numbers in arr[]
    cntOdd = N - cntEven

    # Return absolute difference
    # divided by 2
    return abs(cntEven - cntOdd) // 2

# Driver Code
if __name__ == '__main__':
    arr = [1, 3, 4, 9]
    N = len(arr)

    # Function call
    print (minimumIncrement(arr, N))

    # Thiss code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to find min operations
// to make even and odd count equal
static int minimumIncrement(int[] arr, int N)
{

    // Odd size will never make odd
    // and even counts equal
    if (N % 2 != 0)
    {
        Console.WriteLine( "-1");
        Environment.Exit(0);
    }

    // Stores the count of even
    // numbers in the array arr[]
    int cntEven = 0;

    // Stores count of odd numbers
    // in the array arr[]
    int cntOdd = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++)
    {

        // If arr[i] is an
        // even number
        if (arr[i] % 2 == 0)
        {

            // Update cntEven
            cntEven += 1;
        }
    }

    // Odd numbers in arr[]
    cntOdd = N - cntEven;

    // Return absolute difference
    // divided by 2
    return Math.Abs(cntEven - cntOdd) / 2;
}

  // Driver Code
  public static void  Main()
  {
    int[] arr = { 1, 3, 4, 9 };
    int N = arr.Length;

    // Function call
    Console.WriteLine(minimumIncrement(arr, N));
  }
}

// This code is contributed by susmitakundugoaldanga.
```

## java 描述语言

```
<script>

// Javascript program for the above approach   

    // Function to find min operations
    // to make even and odd count equal
    function minimumIncrement(arr , N) {

        // Odd size will never make odd
        // and even counts equal
        if (N % 2 != 0) {
            document.write("-1");
            System.exit(0);
        }

        // Stores the count of even
        // numbers in the array arr
        var cntEven = 0;

        // Stores count of odd numbers
        // in the array arr
        var cntOdd = 0;

        // Traverse the array arr
        for (i = 0; i < N; i++) {

            // If arr[i] is an
            // even number
            if (arr[i] % 2 == 0) {

                // Update cntEven
                cntEven += 1;
            }
        }

        // Odd numbers in arr
        cntOdd = N - cntEven;

        // Return absolute difference
        // divided by 2
        return Math.abs(cntEven - cntOdd) / 2;
    }

    // Driver code

        var arr = [ 1, 3, 4, 9 ];
        var N = arr.length;

        // Function call
        document.write(minimumIncrement(arr, N));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)