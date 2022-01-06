# 按降序对前 K 个自然数组成的子阵进行计数

> 原文:[https://www . geesforgeks . org/count-subarrays-由-first-k-自然数组成-降序/](https://www.geeksforgeeks.org/count-subarrays-consisting-of-first-k-natural-numbers-in-descending-order/)

给定一个大小的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr[]****N**和一个整数 **K** ，任务是按降序计算由第一个 **K** 个自然数组成的子数组的数量。

**示例:**

> **输入:** arr[] = {1，2，3，7，9，3，2，1，8，3，2，1}，K = 3
> **输出:** 2
> **说明:**子阵列{3，2，1}在阵列中出现两次。
> 
> **输入:** arr = {100，7，6，5，4，3，2，1，100}，K = 6
> **输出:** 1

**方法:**思路是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查从当前索引开始所需的递减顺序是否存在。按照以下步骤解决问题:

*   初始化两个变量， **temp** 到 **K** ，检查模式，**用 **0** 计数**，存储匹配的子阵列总数。
*   使用变量 **i** 遍历数组**arr【】**，并执行以下操作:
    *   如果**arr【I】**等于**温度**，**温度**的值为 **1** ，则将**计数**增加 **1** ，并将**温度**更新为 **K** 。否则将**温度**降低 **1** 。
    *   否则，将**温度**更新为**温度= K** ，如果**arr【I】**等于 **K** ，则将 **i** 递减 **1** 。
*   完成上述步骤后，打印**的值并计算**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count subarray having
// the decreasing sequence K to 1
int CountSubarray(int arr[], int n,
                  int k)
{
    int temp = k, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

        // Check if required sequence
        // is present or not
        if (arr[i] == temp) {
            if (temp == 1) {
                count++;
                temp = k;
            }
            else
                temp--;
        }

        // Reset temp to k
        else {
            temp = k;
            if (arr[i] == k)
                i--;
        }
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 7, 9, 3,
                  2, 1, 8, 3, 2, 1 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 3;

    // Function Call
    cout << CountSubarray(arr, N, K);

    return 0;
}

// This code is contributed by Dharanendra L V
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to count subarray having
  // the decreasing sequence K to 1
  static int CountSubarray(int arr[], int n,
                           int k)
  {
    int temp = k, count = 0;

    // Traverse the array
    for (int i = 0; i < n; i++) {

      // Check if required sequence
      // is present or not
      if (arr[i] == temp) {
        if (temp == 1) {
          count++;
          temp = k;
        }
        else
          temp--;
      }

      // Reset temp to k
      else {
        temp = k;
        if (arr[i] == k)
          i--;
      }
    }

    // Return the count
    return count;
  }

  // Driver code
  public static void main(String[] args)
  {
    int arr[] = { 1, 2, 3, 7, 9, 3,
                 2, 1, 8, 3, 2, 1 };
    int N = arr.length;
    int K = 3;

    // Function Call
    System.out.println(CountSubarray(arr, N, K));
  }
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count subarray having
# the decreasing sequence K to 1
def CountSubarray(arr, n, k):

    temp = k
    count = 0

    # Traverse the array
    for i in range(n):

        # Check if required sequence
        # is present or not
        if (arr[i] == temp):
            if (temp == 1):
                count += 1
                temp = k
            else:
                   temp -= 1

        # Reset temp to k
        else:
            temp = k

            if (arr[i] == k):
                i -= 1

    # Return the count
    return count

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 7, 9, 3,
            2, 1, 8, 3, 2, 1 ]
    N = len(arr)
    K = 3

    # Function Call
    print(CountSubarray(arr, N, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count subarray having
// the decreasing sequence K to 1
static int CountSubarray(int[] arr,
                         int n, int k)
{
    int temp = k, count = 0;

    // Traverse the array
    for(int i = 0; i < n; i++)
    {

        // Check if required sequence
        // is present or not
        if (arr[i] == temp)
        {
            if (temp == 1)
            {
                count++;
                temp = k;
            }
            else
                temp--;
        }

        // Reset temp to k
        else
        {
            temp = k;

            if (arr[i] == k)
                i--;
        }
    }

    // Return the count
    return count;
}

// Driver code
static public void Main()
{
    int[] arr = { 1, 2, 3, 7, 9, 3,
                  2, 1, 8, 3, 2, 1 };
    int N = arr.Length;
    int K = 3;

    // Function Call
    Console.Write(CountSubarray(arr, N, K));
}
}

// This code is contributed by Dharanendra L V
```

## java 描述语言

```
<script>

      // JavaScript program for the above approach

      // Function to count subarray having
      // the decreasing sequence K to 1
      function CountSubarray(arr, n, k) {
        var temp = k,
          count = 0;

        // Traverse the array
        for (var i = 0; i < n; i++)
        {
          // Check if required sequence
          // is present or not
          if (arr[i] == temp)
          {
            if (temp == 1) {
              count++;
              temp = k;
            } else temp--;
          }

          // Reset temp to k
          else {
            temp = k;
            if (arr[i] == k) i--;
          }
        }

        // Return the count
        return count;
      }

      // Driver Code

      var arr = [1, 2, 3, 7, 9, 3, 2, 1, 8, 3, 2, 1];
      var N = arr.length;
      var K = 3;

      // Function Call
      document.write(CountSubarray(arr, N, K));

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)