# 最大化移除至少两种不同类型的球

> 原文:[https://www . geeksforgeeks . org/最大化移除至少两种不同类型的球/](https://www.geeksforgeeks.org/maximize-removals-of-balls-of-at-least-two-different-types/)

给定一个大小为 **3** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，分别表示类型为 **1、2** 和 **3** 的球的数量，任务是找出如果在一次移动中移除三个球，其中至少有两个不同类型的球，可以执行的最大移动数量。

**示例:**

> **输入:** arr[] = {2，3，3}
> **输出:** 2
> **说明:**
> 移动 1:每种类型移除 1 个球。因此，arr[]变成了{1，2，2}。
> 移动 2:每种类型取出 1 个球。因此，arr[]变成{0，1，1}。
> 不能进行进一步的移动。
> 
> **输入:** arr[] = {100，1，2}
> **输出:** 3
> **说明:**
> 移动 1:移除 1 个 2 型球和 2 个 1 型球。因此，arr[]变为{98，0，2}。
> 移动 2:取出 1 个 3 型球和 2 个 1 型球。因此，arr[]变为{96，0，1}。
> 移动 3:取出 1 个 3 型球和 2 个 1 型球。因此，arr[]变为{94，0，0}。
> 不能进行进一步的移动。

**方法:**按照递增的顺序对数组进行排序的想法然后出现了两种情况:

*   如果 **arr[2]** 小于 **2 * (arr[0] + arr[1])** ，则答案为 **(arr[0] + arr[1] + arr[2]) / 3** 。
*   如果 **arr[2]** 大于 **2 * (arr[0] + arr[1])** ，则答案为 **arr[0] + arr[1]** 。

按照以下步骤解决问题:

*   [按递增顺序排列数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   打印**的[最小值](https://www.geeksforgeeks.org/stdmin-in-cpp/)(arr[0]+arr[1]+arr[2])/3**和 **arr[0]+arr[1]** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum moves that
// can be performed if in each move 3
// balls of different types are removed
void findMoves(int arr[])
{
    // Sort the array in increasing order
    sort(arr, arr + 3);

    // Print the answer
    cout << (min(arr[0] + arr[1],
                 (arr[0] + arr[1] + arr[2]) / 3));
}

// Driver Code
int main()
{
    // Given Input
    int arr[3] = { 2, 3, 3 };

    // Function Call
    findMoves(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;  

class GFG{

// Function to find maximum moves that
// can be performed if in each move 3
// balls of different types are removed
static void findMoves(int arr[])
{

    // Sort the array in increasing order
    Arrays.sort(arr);

    // Print the answer
    System.out.println(Math.min(arr[0] + arr[1],
                               (arr[0] + arr[1] +
                                arr[2]) / 3));
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 2, 3, 3 };

    // Function Call
    findMoves(arr);
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find maximum moves that
# can be performed if in each move 3
# balls of different types are removed
def findMoves(arr):

    # Sort the array in increasing order
    arr = sorted(arr)

    # Print the answer
    print (min(arr[0] + arr[1],
              (arr[0] + arr[1] +
               arr[2]) // 3))

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 2, 3, 3 ]

    # Function Call
    findMoves(arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// Java program for the above approach
using System;  
class GFG
{

// Function to find maximum moves that
// can be performed if in each move 3
// balls of different types are removed
static void findMoves(int []arr)
{

    // Sort the array in increasing order
    Array.Sort(arr);

    // Print the answer
    Console.Write(Math.Min(arr[0] + arr[1],
                               (arr[0] + arr[1] +
                                arr[2]) / 3));
}

// Driver Code
public static void Main(String[] args)
{

    // Given Input
    int []arr = { 2, 3, 3 };

    // Function Call
    findMoves(arr);
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

      // Function to find maximum moves that
      // can be performed if in each move 3
      // balls of different types are removed
      function findMoves(arr) {
          // Sort the array in increasing order
          arr.sort(function (a, b) { return a - b; })

          // Print the answer
          document.write(Math.min(arr[0] + arr[1],
              parseInt((arr[0] + arr[1] + arr[2]) / 3)));
      }

      // Driver Code

      // Given Input
      let arr = [2, 3, 3];

      // Function Call
      findMoves(arr);

      // This code is contributed by Potta Lokesh

 </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)