# 根据值与位置的比率选择访问整个数组的起始元素的最小数量

> 原文:[https://www . geesforgeks . org/起始元素最小计数-选择访问-整个数组-取决于值与位置的比率/](https://www.geeksforgeeks.org/minimum-count-of-starting-elements-chosen-to-visit-whole-array-depending-on-ratio-of-values-to-positions/)

给定一个[数组](https://www.geeksforgeeks.org/array-class-c/) **arr[]，**，任务是计算可供选择的起始元素的最小数量，以便可以访问该数组的所有其他元素。只有当一个元素的值的[比率](https://www.geeksforgeeks.org/ratio-proportion-and-partnership/)与数组中这些元素的位置不成反比时，另一个元素才能访问该元素。数组中元素的位置定义为其索引+ 1
**示例:**

> **输入:**arr =【1，2，3，4】
> **输出:** 1
> **说明:**可以选择任意元素开始访问其他元素。对于前两个元素，(1/2)不等于(2/1)。同样，对于第二个和第三个元素，(2/3)不等于(3/2)。其他对也是如此。
> 
> **输入:**arr =【6，3，2】
> **输出:** 3
> **说明:**这里对于每一对，元素的比值等于它们位置的反比:
> 
> *   (6/3)等于(2/1)
> *   (3/2)等于(3/2)
> *   (6/2)等于(3/1)
>     没有元素可以被另一个元素访问

**方法:**给定的问题可以通过观察元素可以互相访问来解决，如果**arr[I/arr[j]！= j/i** ，其中 **j** 和 **i** 是元素的位置。公式可以改写为 **arr[i]*i！= arr[j]*j** 。可以遵循以下步骤:

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并将每个元素相乘到它的位置(索引+ 1)
*   [再次从索引 1 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查公式是否适用于每个元素及其前一个元素
*   如果公式满足任何元素，则返回 1，因为所有元素都将被访问
*   否则，返回 **N** ，因为没有元素可以相互访问，并且需要首先访问所有元素

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <iostream>
using namespace std;

// Function to calculate minimum number
// of elements to visit initially
int minimumStudentsToInform(int A[], int N)
{
    // Multiply array elements
    // with their indices
    for (int i = 0; i < N; i++) {
        A[i] = A[i] * (i + 1);
    }
    for (int i = 1; i < N; i++) {

        // If any two elements can visit
        // each other then all elements
        // in the array can be visited
        if (A[i] != A[i - 1]) {

            return 1;
        }
    }

    // All elements should be
    // visited initially
    return N;
}

int main()
{
    int A[] = { 6, 3, 2 };
    int N = sizeof(A) / sizeof(int);
    cout << minimumStudentsToInform(A, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

public class GFG {

    // Function to calculate minimum number
    // of elements to visit initially
    static int minimumStudentsToInform(int A[], int N)
    {
        // Multiply array elements
        // with their indices
        for (int i = 0; i < N; i++) {
            A[i] = A[i] * (i + 1);
        }
        for (int i = 1; i < N; i++) {

            // If any two elements can visit
            // each other then all elements
            // in the array can be visited
            if (A[i] != A[i - 1]) {

                return 1;
            }
        }

        // All elements should be
        // visited initially
        return N;
    }

    public static void main(String[] args)
    {
        int A[] = { 6, 3, 2 };
        int N = A.length;
        System.out.println(minimumStudentsToInform(A, N));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python implementation for the above approach

# Function to calculate minimum number
# of elements to visit initially
def minimumStudentsToInform( A, N):

  # Multiply array elements
  # with their indices
  for i in range(N):
    A[i] = A[i] * (i + 1)

  for i in range(1, N):

    # If any two elements can visit
    # each other then all elements
    # in the array can be visited
    if (A[i] != A[i - 1]):
      return 1

  # All elements should be
  # visited initially
  return N

A = [ 6, 3, 2 ]
N = len(A)
print(minimumStudentsToInform(A, N))
# This code is contributed by rohitsingh07052
```

## C#

```
// C# implementation for the above approach
using System;

public class GFG
{

    // Function to calculate minimum number
    // of elements to visit initially
    static int minimumStudentsToInform(int []A, int N)
    {

        // Multiply array elements
        // with their indices
        for (int i = 0; i < N; i++) {
            A[i] = A[i] * (i + 1);
        }
        for (int i = 1; i < N; i++) {

            // If any two elements can visit
            // each other then all elements
            // in the array can be visited
            if (A[i] != A[i - 1]) {

                return 1;
            }
        }

        // All elements should be
        // visited initially
        return N;
    }

  // Driver code
    public static void Main(string[] args)
    {
        int []A = { 6, 3, 2 };
        int N = A.Length;
        Console.WriteLine(minimumStudentsToInform(A, N));
    }
}

// This code is contributed by AnkThon
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to calculate minimum number
// of elements to visit initially
function minimumStudentsToInform(A, N)
{

  // Multiply array elements
  // with their indices
  for (let i = 0; i < N; i++) {
    A[i] = A[i] * (i + 1);
  }
  for (let i = 1; i < N; i++)
  {

    // If any two elements can visit
    // each other then all elements
    // in the array can be visited
    if (A[i] != A[i - 1]) {
      return 1;
    }
  }

  // All elements should be
  // visited initially
  return N;
}

let A = [6, 3, 2];
let N = A.length;
document.write(minimumStudentsToInform(A, N));

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
3
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)