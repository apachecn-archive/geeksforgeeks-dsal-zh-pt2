# 最大化减少除 1 到 0 之外的所有数组元素所需的对减量

> 原文:[https://www . geeksforgeeks . org/maximum-pair-reducts-需要减少所有数组元素-除了一对 0/](https://www.geeksforgeeks.org/maximize-pair-decrements-required-to-reduce-all-array-elements-except-one-to-0/)

给定一个由 **N** 个不同元素组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出每一步中需要减少 **1** 的最大对数，使得**N–1**个数组元素减少为 0，剩余的数组元素为非负整数。

**示例:**

> **输入:** arr[] = {1，2，3}
> **输出:** 3
> **解释:**
> 将 arr[1]和 arr[2]减少 1 会修改 arr[] = {1，1，2}
> 将 arr[1]和 arr[2]减少 1 会修改 arr[] = {1，0，1}
> 将 arr[0]和 arr[2]减少 1 会修改 arr[] = {0，0，0}
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 7

**进场:**问题可以解决[贪婪地](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   初始化一个变量，比如 **cntOp** ，以存储使数组的**(N–1)**元素等于 **0** 所需的最大步数。
*   创建一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)，比如说 **PQ** ，来存储数组元素。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)[将](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)数组元素插入 **PQ** 。
*   现在重复[从优先级队列中提取顶部](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/) **2** 元素，将这两个元素的值减少 **1** ，再次将这两个元素插入优先级队列，并将 **cntOp** 增加 **1** 。当 **PQ** 的**(N–1)**元素变为等于 **0** 时，此过程继续。
*   最后，打印 **cntOp** 的值

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number of steps
// to make (N - 1) array elements to 0
int cntMaxOperationToMakeN_1_0(int arr[], int N)
{

    // Stores maximum count of steps to make
    // (N - 1) elements equal to 0
    int cntOp = 0;

    // Stores array elements
    priority_queue<int> PQ;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Insert arr[i] into PQ
        PQ.push(arr[i]);
    }

    // Extract top 2 elements from the array
    // while (N - 1) array elements become 0
    while (PQ.size() > 1) {

        // Stores top element
        // of PQ
        int X = PQ.top();

        // Pop the top element
        // of PQ.
        PQ.pop();

        // Stores top element
        // of PQ
        int Y = PQ.top();

        // Pop the top element
        // of PQ.
        PQ.pop();

        // Update X
        X--;

        // Update Y
        Y--;

        // If X is not equal to 0
        if (X != 0) {

            // Insert X into PQ
            PQ.push(X);
        }

        // if Y is not equal
        // to 0
        if (Y != 0) {

            // Insert Y
            // into PQ
            PQ.push(Y);
        }

        // Update cntOp
        cntOp += 1;
    }

    return cntOp;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << cntMaxOperationToMakeN_1_0(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count maximum number of steps
// to make (N - 1) array elements to 0
static int cntMaxOperationToMakeN_1_0(int[] arr, int N)
{

    // Stores maximum count of steps to make
    // (N - 1) elements equal to 0
    int cntOp = 0;

    // Stores array elements
    PriorityQueue<Integer> PQ = new PriorityQueue<Integer>((a, b) -> b - a);

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Insert arr[i] into PQ
        PQ.add(arr[i]);
    }

    // Extract top 2 elements from the array
    // while (N - 1) array elements become 0
    while (PQ.size() > 1)
    {

        // Stores top element
        // of PQ
        int X = PQ.peek();

        // Pop the top element
        // of PQ.
        PQ.remove();

        // Stores top element
        // of PQ
        int Y = PQ.peek();

        // Pop the top element
        // of PQ.
        PQ.remove();

        // Update X
        X--;

        // Update Y
        Y--;

        // If X is not equal to 0
        if (X != 0)
        {

            // Insert X into PQ
            PQ.add(X);
        }

        // if Y is not equal
        // to 0
        if (Y != 0)
        {

            // Insert Y
            // into PQ
            PQ.add(Y);
        }

        // Update cntOp
        cntOp += 1;
    }
    return cntOp;
}

// Driver code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    System.out.print(cntMaxOperationToMakeN_1_0(arr, N));
}
}

// This code is contributed by susmitakundugoaldanga
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count maximum number of steps
# to make (N - 1) array elements to 0
def cntMaxOperationToMakeN_1_0(arr, N):

    # Stores maximum count of steps to make
    # (N - 1) elements equal to 0
    cntOp = 0

    # Stores array elements
    PQ = []

    # Traverse the array
    for i in range(N):

        # Insert arr[i] into PQ
        PQ.append(arr[i])
    PQ = sorted(PQ)

    # Extract top 2 elements from the array
    # while (N - 1) array elements become 0
    while (len(PQ) > 1):

        # Stores top element
        # of PQ
        X = PQ[-1]

        # Pop the top element
        # of PQ.
        del PQ[-1]

        # Stores top element
        # of PQ
        Y = PQ[-1]

        # Pop the top element
        # of PQ.
        del PQ[-1]

        # Update X
        X -= 1

        # Update Y
        Y -= 1

        # If X is not equal to 0
        if (X != 0):

            # Insert X into PQ
            PQ.append(X)

        # if Y is not equal
        # to 0
        if (Y != 0):

            # Insert Y
            # into PQ
            PQ.append(Y)

        # Update cntOp
        cntOp += 1
        PQ = sorted(PQ)
    return cntOp

# Driver Code
if __name__ == '__main__':

    arr = [1, 2, 3, 4, 5]
    N = len(arr)
    print (cntMaxOperationToMakeN_1_0(arr, N))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to count maximum number of steps
  // to make (N - 1) array elements to 0
  static int cntMaxOperationToMakeN_1_0(int[] arr, int N)
  {

    // Stores maximum count of steps to make
    // (N - 1) elements equal to 0
    int cntOp = 0;

    // Stores array elements
    List<int> PQ = new List<int>();

    // Traverse the array
    for (int i = 0; i < N; i++) {

      // Insert arr[i] into PQ
      PQ.Add(arr[i]);
    }

    PQ.Sort();
    PQ.Reverse();

    // Extract top 2 elements from the array
    // while (N - 1) array elements become 0
    while (PQ.Count > 1) {

      // Stores top element
      // of PQ
      int X = PQ[0];

      // Pop the top element
      // of PQ.
      PQ.RemoveAt(0);

      // Stores top element
      // of PQ
      int Y = PQ[0];

      // Pop the top element
      // of PQ.
      PQ.RemoveAt(0);

      // Update X
      X--;

      // Update Y
      Y--;

      // If X is not equal to 0
      if (X != 0) {

        // Insert X into PQ
        PQ.Add(X);
        PQ.Sort();
        PQ.Reverse();
      }

      // if Y is not equal
      // to 0
      if (Y != 0) {

        // Insert Y
        // into PQ
        PQ.Add(Y);
        PQ.Sort();
        PQ.Reverse();
      }

      // Update cntOp
      cntOp += 1;
    }

    return cntOp;
  }

  // Driver code
  static void Main() {
    int[] arr = { 1, 2, 3, 4, 5 };

    int N = arr.Length;

    Console.WriteLine(cntMaxOperationToMakeN_1_0(arr, N));
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to implement the above approach

    // Function to count maximum number of steps
    // to make (N - 1) array elements to 0
    function cntMaxOperationToMakeN_1_0(arr, N)
    {

      // Stores maximum count of steps to make
      // (N - 1) elements equal to 0
      let cntOp = 0;

      // Stores array elements
      let PQ = [];

      // Traverse the array
      for (let i = 0; i < N; i++) {

        // Insert arr[i] into PQ
        PQ.push(arr[i]);
      }

      PQ.sort(function(a, b){return a - b});
      PQ.reverse();

      // Extract top 2 elements from the array
      // while (N - 1) array elements become 0
      while (PQ.length > 1) {

        // Stores top element
        // of PQ
        let X = PQ[0];

        // Pop the top element
        // of PQ.
        PQ.shift();

        // Stores top element
        // of PQ
        let Y = PQ[0];

        // Pop the top element
        // of PQ.
        PQ.shift();

        // Update X
        X--;

        // Update Y
        Y--;

        // If X is not equal to 0
        if (X != 0) {

          // Insert X into PQ
          PQ.push(X);
          PQ.sort(function(a, b){return a - b});
          PQ.reverse();
        }

        // if Y is not equal
        // to 0
        if (Y != 0) {

          // Insert Y
          // into PQ
          PQ.push(Y);
          PQ.sort(function(a, b){return a - b});
          PQ.reverse();
        }

        // Update cntOp
        cntOp += 1;
      }

      return cntOp;
    }

    let arr = [ 1, 2, 3, 4, 5 ];
    let N = arr.length;
    document.write(cntMaxOperationToMakeN_1_0(arr, N));

    // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*