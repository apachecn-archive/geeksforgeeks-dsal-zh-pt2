# 通过在每个元素上使用天花板或地板使数组总和为 0

> 原文:[https://www . geeksforgeeks . org/通过在每个元素上使用非天花板即地板的方式制作 0 的数组和/](https://www.geeksforgeeks.org/make-the-array-sum-0-by-using-either-ceil-or-floor-on-each-element/)

给定一个由 **N** 个浮点整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是通过对每个数组元素执行 [ceil()或 floor()](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/) 来修改数组，使得数组元素的[和接近 **0** 。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {6.455，-1.24，-3.87，2.434，-4.647}
> **输出:** {6，-2，-3，3，-4}
> **解释:**
> 对索引{0，1}处的数组元素执行 floor 运算，对索引{2，3，4}处的 ceil 运算将数组修改为{6，-2，-3，3，-4}，其元素之和最接近 0
> 
> ***输入:** arr[] = {-12.42，9.264，24.24，-13.04，4.0，-9.66，-2.99}*
> ***输出:** {-13，9，24，-13，4，-9，-2}*

**方法:**给定的问题可以通过找到所有数组元素的 ceil()值的和来解决，如果[数组的和](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)为正，则找到该数量元素的 ceil，使得最接近值 0。按照以下步骤解决给定的问题:

*   初始化一个变量，比如说 **sum** 到 **0** ，存储数组元素的和。
*   初始化一个数组，比如说**一个存储更新后的数组元素的[]** 。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** ，求数组元素的 **ceil()** 之和，将 **A[i]** 的值更新为 **ceil(arr[i])** 的值。
*   如果**和**的值为正，则找到某个数组元素的楼层，将该和减少到最接近 **0** ，并且该数组元素的计数由**和**以及 **N** 的[最小值](https://www.geeksforgeeks.org/stdmin-in-cpp/)给出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to modify the array element
// such that the sum is close to 0
void setSumtoZero(double arr[], int N)
{
    // Stores the modified elements
    int A[N];

    // Stores the sum of array element
    int sum = 0;

    // Stores minimum size of the array
    int m = INT_MIN;

    // Traverse the array and find the
    // sum
    for (int i = 0; i < N; i++) {
        sum += ceil(arr[i]);
        A[i] = ceil(arr[i]);
    }

    // If sum is positive
    if (sum > 0) {

        // Find the minimum number of
        // elements that must be changed
        m = min(sum, N);

        // Iterate until M elements are
        // modified or the array end
        for (int i = 0; i < N && m > 0; i++) {

            // Update the current array
            // elements to its floor
            A[i] = floor(arr[i]);
            if (A[i] != floor(arr[i]))
                m--;
        }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        cout << A[i] << " ";
    }
}

// Driver Code
int main()
{
    double arr[] = { -2, -2, 4.5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    setSumtoZero(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to modify the array element
// such that the sum is close to 0
static void setSumtoZero(double arr[], int N)
{

    // Stores the modified elements
    int []A = new int[N];

    // Stores the sum of array element
    int sum = 0;

    // Stores minimum size of the array
    int m = Integer.MIN_VALUE;

    // Traverse the array and find the
    // sum
    for (int i = 0; i < N; i++) {
        sum += Math.ceil(arr[i]);
        A[i] = (int) Math.ceil(arr[i]);
    }

    // If sum is positive
    if (sum > 0) {

        // Find the minimum number of
        // elements that must be changed
        m = Math.min(sum, N);

        // Iterate until M elements are
        // modified or the array end
        for (int i = 0; i < N && m > 0; i++) {

            // Update the current array
            // elements to its floor
            A[i] = (int) Math.floor(arr[i]);
            if (A[i] != Math.floor(arr[i]))
                m--;
        }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        System.out.print(A[i]+ " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    double arr[] = { -2, -2, 4.5 };
    int N = arr.length;
    setSumtoZero(arr, N);

}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys
from math import ceil,floor

# Function to modify the array element
# such that the sum is close to 0
def setSumtoZero(arr, N):

    # Stores the modified elements
    A = [0 for i in range(N)]

    # Stores the sum of array element
    sum = 0

    # Stores minimum size of the array
    m = -sys.maxsize-1

    # Traverse the array and find the
    # sum
    for i in range(N):
        sum += ceil(arr[i])
        A[i] = ceil(arr[i])

    # If sum is positive
    if (sum > 0):

        # Find the minimum number of
        # elements that must be changed
        m = min(sum, N)

        # Iterate until M elements are
        # modified or the array end
        i = 0
        while(i < N and m > 0):

            # Update the current array
            # elements to its floor
            A[i] = floor(arr[i])
            if (A[i] != floor(arr[i])):
                m -= 1
            i += 1

    # Print the resultant array
    for i in range(N):
        print(A[i],end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [-2, -2, 4.5]
    N = len(arr)
    setSumtoZero(arr, N)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

public class GFG{

// Function to modify the array element
// such that the sum is close to 0
static void setSumtoZero(double []arr, int N)
{

    // Stores the modified elements
    int []A = new int[N];

    // Stores the sum of array element
    int sum = 0;

    // Stores minimum size of the array
    int m = int.MinValue;

    // Traverse the array and find the
    // sum
    for (int i = 0; i < N; i++) {
        sum += (int)Math.Ceiling(arr[i]);
        A[i] = (int) Math.Ceiling(arr[i]);
    }

    // If sum is positive
    if (sum > 0) {

        // Find the minimum number of
        // elements that must be changed
        m = Math.Min(sum, N);

        // Iterate until M elements are
        // modified or the array end
        for (int i = 0; i < N && m > 0; i++) {

            // Update the current array
            // elements to its floor
            A[i] = (int) Math.Floor(arr[i]);
            if (A[i] != Math.Floor(arr[i]))
                m--;
        }
    }

    // Print the resultant array
    for (int i = 0; i < N; i++) {
        Console.Write(A[i]+ " ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    double []arr = { -2, -2, 4.5 };
    int N = arr.Length;
    setSumtoZero(arr, N);

}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to modify the array element
        // such that the sum is close to 0
        function setSumtoZero(arr, N)
        {

            // Stores the modified elements
            let A = new Array(N);

            // Stores the sum of array element
            let sum = 0;

            // Stores minimum size of the array
            let m = Number.MIN_VALUE;

            // Traverse the array and find the
            // sum
            for (let i = 0; i < N; i++) {
                sum += Math.ceil(arr[i]);
                A[i] = Math.ceil(arr[i]);
            }

            // If sum is positive
            if (sum > 0) {

                // Find the minimum number of
                // elements that must be changed
                m = Math.min(sum, N);

                // Iterate until M elements are
                // modified or the array end
                for (let i = 0; i < N && m > 0; i++) {

                    // Update the current array
                    // elements to its floor
                    A[i] = Math.floor(arr[i]);
                    if (A[i] != Math.floor(arr[i]))
                        m--;
                }
            }

            // Print the resultant array
            for (let i = 0; i < N; i++) {
                document.write(A[i] + " ");
            }
        }

        // Driver Code
        let arr = [-2, -2, 4.5];
        let N = arr.length;
        setSumtoZero(arr, N);

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
-2 -2 4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)