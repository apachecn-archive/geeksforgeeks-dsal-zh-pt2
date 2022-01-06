# 最小化使数组的每个元素等于其索引值所需的操作

> 原文:[https://www . geesforgeks . org/minimum-operations-要求使数组的每个元素等于其索引值/](https://www.geeksforgeeks.org/minimize-operations-required-to-make-each-element-of-array-equal-to-its-index-value/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是修改该数组，使得 **arr[index] = index** 使用以下类型的最小操作数:

1.  选择任意索引 **i** 和任意整数 **X** ，将 **X** 添加到**【0，I】**范围内的所有元素。
2.  选择任意指标 **i** 和任意整数 **X** ，将**arr【j】**改为**arr【j】% X**，其中 **0 ≤ j ≤ i** 。

对于执行的每个操作，打印以下内容:

*   第一次操作:打印 **1 i X**
*   第二次操作:打印 **2 i X**

**注意:**最大 **N + 1** 操作均可。

**示例:**

> **输入:** arr[] = {7，6，3}，N = 3
> **输出:**
> 1 2 5
> 1 1 2
> 1 0 1
> 2 2 3
> **解释:【T1 1】
> 第一个操作:将所有元素加 5，直到索引 2 将数组修改为{12，11，8}。
> 第二个操作:将 2 加到所有元素上，直到索引 1 将数组修改为{14，13，8}。
> 第三个操作:将所有元素加 1，直到索引 0 将数组修改为{15，13，8}。
> 第四个操作:将所有元素加 3，直到索引 2 将数组修改为{0，1，2}。
> 这样经过 4 次运算，就得到需要的数组。
> **输入:** arr[] = {3，4，5，6}，N = 4
> **输出:**
> 1 3 5
> 1 2 4
> 1 1 4
> 1 0 4
> 2 3 4**

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  应用**类型 1** 的 **N** 操作，其中 **i <sup>第</sup>** 操作是通过以相反顺序遍历数组将**X =*****(N+I –( arr[I]% N))***添加到索引 **i** 。每进行一次操作，打印**“1i X”**。
2.  在上述 **N** 操作之后，数组将为 **0 ≤ i < N** 的 **arr[i] % N = i** 形式。
3.  还需要执行一个操作，即使用 **N** 对每个数组元素进行模运算，即操作**“2(N-1)N”**。
4.  执行上述操作后，对于每个索引 **i** ， **arr[i] = i** 。

下面是上述方法的实现:

## C++

```
// CPP program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function which makes the given
// array increasing using given
// operations
void makeIncreasing(int arr[], int N)
{
    // The ith operation will be
    // 1 i N + i - arr[i] % N
    for (int x = N - 1; x >= 0; x--)
    {
        int val = arr[x];

        // Find the value to be added
        // in each operation
        int add = N - val % N + x;

        // Print the operation
        cout << "1 " << x << " " << add << endl;

        // Performing the operation
        for (int y = x; y >= 0; y--) {
            arr[y] += add;
        }
    }

    // Last modulo with N operation
    int mod = N;
    cout << "2 " << N - 1 << " " << mod << endl;
    for (int x = N - 1; x >= 0; x--) {
        arr[x] %= mod;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 7, 6, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    makeIncreasing(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.util.*;

class GFG
{
    // Function which makes the given
    // array increasing using given
    // operations
    static void makeIncreasing(int arr[], int N)
    {

        // The ith operation will be
        // 1 i N + i - arr[i] % N
        for (int x = N - 1; x >= 0; x--)
        {
            int val = arr[x];

            // Find the value to be added
            // in each operation
            int add = N - val % N + x;

            // Print the operation
            System.out.println("1"
                               + " " + x + " " + add);

            // Performing the operation
            for (int y = x; y >= 0; y--)
            {
                arr[y] += add;
            }
        }

        // Last modulo with N operation
        int mod = N;

        System.out.println("2"
                           + " " + (N - 1) + " " + mod);

        for (int x = N - 1; x >= 0; x--)
        {
            arr[x] %= mod;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        // Given array arr[]
        int arr[] = { 7, 6, 3 };
        int N = arr.length;
        // Function Call
        makeIncreasing(arr, N);
    }
}
```

## 蟒蛇 3

```
# python Program for the above problem
# Function which makes the given
# array increasing using given
# operations
def makeIncreasing(arr, N):

    # The ith operation will be
    # 1 i N + i - arr[i] % N
    for x in range( N - 1 ,  -1, -1):
        val = arr[x]

        # Find the value to be added
        # in each operation
        add = N - val % N + x

        # Print the operation
        print("1" + " " + str(x) + " " + str(add))

        # Performing the operation
        for y in range(x, -1, -1):
            arr[y] += add

    # Last modulo with N operation
    mod = N;
    print("2" + " " + str(N - 1) + " " + str(mod))
    for i in range( N - 1, -1, -1):
        arr[i] = arr[i] % mod

# Driver code

# Given array arr
arr = [ 7, 6, 3 ]

N = len(arr)

# Function Call
makeIncreasing(arr, N)
```

## C#

```
// C# Program for the above approach
using System;

class GFG
{
    // Function which makes the given
    // array increasing using given
    // operations
    static void makeIncreasing(int[] arr, int N)
    {

        // The ith operation will be
        // 1 i N + i - arr[i] % N
        for (int x = N - 1; x >= 0; x--)
        {
            int val = arr[x];

            // Find the value to be added
            // in each operation
            int add = N - val % N + x;

            // Print the operation
            Console.WriteLine("1"
                              + " " + x + " " + add);

            // Performing the operation
            for (int y = x; y >= 0; y--)
            {
                arr[y] += add;
            }
        }

        // Last modulo with N operation
        int mod = N;

        Console.WriteLine("2"
                          + " " + (N - 1) + " " + mod);

        for (int x = N - 1; x >= 0; x--) {
            arr[x] %= mod;
        }
    }

    // Driver code
    public static void Main()
    {
        // Given array arr[]
        int[] arr = new int[] { 7, 6, 3 };

        int N = arr.Length;

        // Function Call
        makeIncreasing(arr, N);
    }
}
```

## java 描述语言

```
<script>

      // JavaScript Program for the above approach

      // Function which makes the given
      // array increasing using given
      // operations
      function makeIncreasing(arr, N)
      {
        // The ith operation will be
        // 1 i N + i - arr[i] % N
        for (var x = N - 1; x >= 0; x--) {
          var val = arr[x];

          // Find the value to be added
          // in each operation
          var add = N - (val % N) + x;

          // Print the operation
          document.write("1" + " " + x + " "
          + add + "<br>");

          // Performing the operation
          for (var y = x; y >= 0; y--) {
            arr[y] += add;
          }
        }

        // Last modulo with N operation
        var mod = N;

        document.write("2" + " " + (N - 1) + " "
        + mod + "<br>");

        for (var x = N - 1; x >= 0; x--) {
          arr[x] %= mod;
        }
      }

      // Driver code

      // Given array arr[]
      var arr = [7, 6, 3];
      var N = arr.length;

      // Function Call
      makeIncreasing(arr, N);

</script>
```

**Output**

```
1 2 5
1 1 2
1 0 1
2 2 3
```

**时间复杂度:***O(N<sup>2</sup>)*
T7】辅助空间: *O(1)*