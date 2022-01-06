# 通过给定操作

最小化数组中的非零元素

> 原文:[https://www . geeksforgeeks . org/按给定操作最小化数组中的非零元素/](https://www.geeksforgeeks.org/minimize-the-non-zero-elements-in-the-array-by-given-operation/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是通过将当前元素的值与其任何相邻元素相加并最多从当前元素中减去一次来最小化非零元素的数量。
**例:**

> **输入:** arr[] = { 1，0，1，0，0，1 }
> **输出:** 2
> **解释:**
> **操作 1:** arr[0] - > arr[1]，arr[] = {0，1，1，0，0，1}
> **操作 2:** arr[2] - > arr[1]，arr[] = {0，2，0，0，0，0 1 }
> **输出:** 3
> **说明:**
> **操作 1:** arr[2] - > arr[3]，arr[] = {1，0，3，0，2，1，0，1}
> **操作 2:** arr[4] - > arr[3]，arr[] = {1，0，3，0，0，1}
> 非零计数

**方法:**思路是用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)在每一步贪婪地选择。问题中的关键观察是，三个连续的指数 I、j 和 k 只能有三种可能性，即

*   结束索引都有非零元素。
*   任何一个索引都有非零元素。

在以上两种情况下，我们总是可以将值加到中间的元素上，然后减去相邻的元素。同样，我们可以贪婪地选择操作并更新数组的元素，以最小化非零元素。
以下是上述方法的实现:

## C++

```
// C++ implementation to minimize the
// non-zero elements in the array

#include <bits/stdc++.h>
using namespace std;

// Function to minimize the non-zero
// elements in the given array
int minOccupiedPosition(int A[], int n)
{

    // To store the min pos needed
    int minPos = 0;

    // Loop to iterate over the elements
    // of the given array
    for (int i = 0; i < n; ++i) {

        // If current position A[i] is occupied
        // the we can place A[i], A[i+1] and A[i+2]
        // elements together at A[i+1] if exists.
        if (A[i] > 0) {
            ++minPos;
            i += 2;
        }
    }

    return minPos;
}

// Driver Code
int main()
{
    int A[] = { 8, 0, 7, 0, 0, 6 };
    int n = sizeof(A) / sizeof(A[0]);

    // Function Call
    cout << minOccupiedPosition(A, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to minimize the
// non-zero elements in the array

class GFG{

// Function to minimize the non-zero
// elements in the given array
static int minOccupiedPosition(int A[], int n)
{

    // To store the min pos needed
    int minPos = 0;

    // Loop to iterate over the elements
    // of the given array
    for (int i = 0; i < n; ++i)
    {

        // If current position A[i] is occupied
        // the we can place A[i], A[i+1] and A[i+2]
        // elements together at A[i+1] if exists.
        if (A[i] > 0) {
            ++minPos;
            i += 2;
        }
    }
    return minPos;
}

// Driver Code
public static void main(String[] args)
{
    int A[] = { 8, 0, 7, 0, 0, 6 };
    int n = A.length;

    // Function Call
    System.out.print(minOccupiedPosition(A, n));
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 implementation to minimize the
# non-zero elements in the array

# Function to minimize the non-zero
# elements in the given array
def minOccupiedPosition(A, n):

    # To store the min pos needed
    minPos = 0

    # Loop to iterate over the elements
    # of the given array
    i = 0
    while i < n:

        # If current position A[i] is
        # occupied the we can place A[i],
        # A[i+1] and A[i+2] elements
        # together at A[i+1] if exists.
        if(A[i] > 0):

            minPos += 1
            i += 2
        i += 1

    return minPos

# Driver Code
if __name__ == '__main__':

    A = [ 8, 0, 7, 0, 0, 6 ]
    n = len(A)

    # Function Call
    print(minOccupiedPosition(A, n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation to minimize the
// non-zero elements in the array
using System;

class GFG {

// Function to minimize the non-zero
// elements in the given array
static int minOccupiedPosition(int[] A, int n)
{

    // To store the min pos needed
    int minPos = 0;

    // Loop to iterate over the elements
    // of the given array
    for(int i = 0; i < n; ++i)
    {

       // If current position A[i] is occupied
       // the we can place A[i], A[i+1] and A[i+2]
       // elements together at A[i+1] if exists.
       if (A[i] > 0)
       {
           ++minPos;
           i += 2;
       }
    }
    return minPos;
}

// Driver code   
static void Main()
{
    int[] A = { 8, 0, 7, 0, 0, 6 };
    int n = A.Length;

    // Function Call
    Console.WriteLine(minOccupiedPosition(A, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript implementation to minimize the
// non-zero elements in the array

// Function to minimize the non-zero
// elements in the given array
function minOccupiedPosition( A, n)
{

    // To store the min pos needed
    var minPos = 0;

    // Loop to iterate over the elements
    // of the given array
    for (var i = 0; i < n; ++i) {

        // If current position A[i] is occupied
        // the we can place A[i], A[i+1] and A[i+2]
        // elements together at A[i+1] if exists.
        if (A[i] > 0) {
            ++minPos;
            i += 2;
        }
    }

    return minPos;
}

 var A = [ 8, 0, 7, 0, 0, 6 ];
 var n = A.length;

    // Function Call
    document.write(minOccupiedPosition(A, n));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N)* 。

***辅助空间:**O(1)*T4】