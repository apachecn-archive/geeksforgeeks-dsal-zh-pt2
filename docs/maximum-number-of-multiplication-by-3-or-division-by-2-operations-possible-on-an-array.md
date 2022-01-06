# 一个数组中可能的最大 3 乘或 2 除运算次数

> 原文:[https://www . geeksforgeeks . org/数组上最大可能的 3 乘 3 或 2 除运算数/](https://www.geeksforgeeks.org/maximum-number-of-multiplication-by-3-or-division-by-2-operations-possible-on-an-array/)

给定一个由 **N** 正整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是找出每个数组元素可以乘以 **M** 或除以 **K** 的最大次数。
***注:**每次操作至少需要用 **M** 和 **K** 分别划分一个元素。*

**示例:**

> **输入:** arr[] = {5，2，4}，M = 3，K = 2
> **输出:** 3
> **解释:**
> 执行操作的一种可能方式是:
> 
> 1.  将 arr[1]和 arr[2]乘以 3，将 arr[3]除以 2。数组修改为{15，6，2}。
> 2.  将 arr[1]和 arr[3]乘以 3，将 arr[2]除以 2。数组修改为{45，3，6}。
> 3.  将 arr[1]乘以 3，将 arr[2]乘以 3，将 arr[3]除以 2。数组修改为{135，9，3}。
> 4.  因为没有一个元素能被 2 整除，所以不可能有进一步的运算。
> 
> 因此，可能的最大操作数是 3。
> 
> **输入:** arr[] = {3，5，7 }
> T3】输出: 0

**方法:**这个问题可以通过观察到，将一个数组元素依次除以 **2** ，偶数元素的计数在某个恒定的步数后会减少来解决。所以，为了最大化匝数，只需用 **2** 除一个偶素，其他所有偶素用 **3** 一步相乘即可。按照以下步骤解决问题:

*   初始化一个变量，比如说**计数**为 0，这将在数组的每个元素中存储 **2** 的幂的计数。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N-1】**中迭代，并执行以下步骤:
    *   [迭代直到](https://www.geeksforgeeks.org/java-while-loop-with-examples/)****arr[I]**被 **2、**整除，然后将**计数**增加 **1** ，将 **arr[i]** 除以 **2** 。**
*   **执行上述步骤后，打印**计数**的值作为答案。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count maximum number
// of multiplication by 3 or division
// by 2 operations that can be performed
int maximumTurns(int arr[], int N)
{

    // Stores the maximum number
    // of operations possible
    int Count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Iterate until arr[i] is even
        while (arr[i] % 2 == 0) {

            // Increment count by 1
            Count++;

            // Update arr[i]
            arr[i] = arr[i] / 2;
        }
    }

    // Return the value of
    // Count as the answer
    return Count;
}

// Driver Code
int main()
{

    // Given Input
    int arr[] = { 5, 2, 4 };
    int M = 3, K = 2;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << maximumTurns(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG
{

    // Function to count maximum number
    // of multiplication by 3 or division
    // by 2 operations that can be performed
    static int maximumTurns(int arr[], int N)
    {

        // Stores the maximum number
        // of operations possible
        int Count = 0;

        // Traverse the array arr[]
        for (int i = 0; i < N; i++) {

            // Iterate until arr[i] is even
            while (arr[i] % 2 == 0) {

                // Increment count by 1
                Count++;

                // Update arr[i]
                arr[i] = arr[i] / 2;
            }
        }

        // Return the value of
        // Count as the answer
        return Count;
    }

    // Driver code
    public static void main(String[] args)
    {

        // Given Input
        // Given Input
        int arr[] = { 5, 2, 4 };
        int M = 3, K = 2;
        int N = arr.length;

        // Function Call
        System.out.println(maximumTurns(arr, N));
    }
}

// This code is contributed by abhinavjain194
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count maximum number
# of multiplication by 3 or division
# by 2 operations that can be performed
def maximumTurns(arr, N):

    # Stores the maximum number
    # of operations possible
    Count = 0

    # Traverse the array arr[]
    for i in range(0, N):

        # Iterate until arr[i] is even
        while (arr[i] % 2 == 0):

            # Increment count by 1
            Count += 1

            # Update arr[i]
            arr[i] = arr[i] // 2

    # Return the value of
    # Count as the answer
    return Count

# Driver code

# Given Input
arr = [ 5, 2, 4 ]
M = 3
K = 2
N = len(arr)

# Function Call
print(maximumTurns(arr, N))

# This code is contributed by amreshkumar3
```

## **C#**

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to count maximum number
// of multiplication by 3 or division
// by 2 operations that can be performed
static int maximumTurns(int []arr, int N)
{

    // Stores the maximum number
    // of operations possible
    int Count = 0;

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {

        // Iterate until arr[i] is even
        while (arr[i] % 2 == 0) {

            // Increment count by 1
            Count++;

            // Update arr[i]
            arr[i] = arr[i] / 2;
        }
    }

    // Return the value of
    // Count as the answer
    return Count;
}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = { 5, 2, 4 };
    int N = arr.Length;

    // Function Call
    Console.Write(maximumTurns(arr, N));
}
}

// This code is contributed by ipg2016107.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to count maximum number
// of multiplication by 3 or division
// by 2 operations that can be performed
function maximumTurns(arr, N) {

    // Stores the maximum number
    // of operations possible
    let Count = 0;

    // Traverse the array arr[]
    for (let i = 0; i < N; i++) {

        // Iterate until arr[i] is even
        while (arr[i] % 2 == 0) {

            // Increment count by 1
            Count++;

            // Update arr[i]
            arr[i] = Math.floor(arr[i] / 2);
        }
    }

    // Return the value of
    // Count as the answer
    return Count;
}

// Driver Code

// Given Input
let arr = [5, 2, 4];
let M = 3, K = 2;
let N = arr.length;

// Function Call
document.write(maximumTurns(arr, N));

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:** O(N*log(M))其中 M 是数组的最大值。*
***辅助空间:** O(1)***