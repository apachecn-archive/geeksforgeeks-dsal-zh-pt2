# 每个数组元素在其排序位置的右移计数

> 原文:[https://www . geeksforgeeks . org/待排序位置的每个数组元素的右移计数/](https://www.geeksforgeeks.org/count-of-right-shifts-for-each-array-element-to-be-in-its-sorted-position/)

给定一个大小为 **N** 的数组 **arr[]** ，该数组包含范围为**【1，N】**的元素，任务是计算如果对数组进行排序，每个元素到达其各自位置所需的右移次数。
**举例:**

> **输入:** arr[] = {1，4，3，2，5}，N = 5
> **输出:** 0 2 0 3 0
> **解释:**
> 排序后的数组为{1，2，3，4，5}。
> 4 在指标 1，右移 2 次到达指标 3。(1- > 2- > 3)
> 2 在指标 3，所以右移 3 次到达指标 1。(3- > 4- > 0- > 1)
> 所有其他元素都在排序数组中各自的位置。
> **输入:** arr[]={2，4，3，1，5}，N = 5
> **输出:** 2 1 0 2 0

**方法:**
想法是计算数组中每个元素的实际位置和排序位置之差。由于元素从 *1* 到 ***N、*** 可以确定每个元素的排序位置，而无需对数组进行排序。每个元素的排序位置由 ***(arr[i]-1)给出。*** 因此，右移次数由***(arr[I]–1–I+N)% N .***给出

以下是上述方法的实现:

## C++

```
// C++ Program to implement
// the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the right
// shifts required for each
// element to reach its sorted
// array position in A[]
void findShifts(int A[], int N)
{
    // Stores required number of
    // shifts for each element
    int shift[N];

    for (int i = 0; i < N; i++) {

        // If the element is
        // at sorted position
        if (i == A[i] - 1)
            shift[i] = 0;

        // Otherwise
        else

            // Calculate right shift
            shift[i]
                = (A[i] - 1 - i + N)
                  % N;
    }

    // Print the respective shifts
    for (int i = 0; i < N; i++)
        cout << shift[i] << " ";
}

// Driver Code
int main()
{
    int arr[] = { 1, 4, 3, 2, 5 };

    int N = sizeof(arr) / sizeof(arr[0]);

    findShifts(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the approach
class GFG{

// Function to find the right
// shifts required for each
// element to reach its sorted
// array position in A[]
public static void findShifts(int[] A, int N)
{

    // Stores required number of
    // shifts for each element
    int[] shift = new int[N];

    for(int i = 0; i < N; i++)
    {

        // If the element is
        // at sorted position
        if (i == A[i] - 1)
            shift[i] = 0;

        // Otherwise
        else

            // Calculate right shift
            shift[i] = (A[i] - 1 - i + N) % N;
    }

    // Print the respective shifts
    for(int i = 0; i < N; i++)
        System.out.print(shift[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 4, 3, 2, 5 };
    int N = arr.length;

    findShifts(arr, N);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 Program to implement
# the approach

# Function to find the right
# shifts required for each
# element to reach its sorted
# array position in A[]
def findShifts(A, N):

    # Stores required number of
    # shifts for each element
    shift = [0 for i in range(N)]

    for i in range(N):

        # If the element is
        # at sorted position
        if (i == A[i] - 1):
            shift[i] = 0

        # Otherwise
        else:

            # Calculate right shift
            shift[i] = (A[i] - 1 - i + N) % N

    # Print the respective shifts
    for i in range(N):
        print(shift[i], end = " ")

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 4, 3, 2, 5 ]
    N = len(arr)

    findShifts(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the approach
using System;

class GFG{

// Function to find the right
// shifts required for each
// element to reach its sorted
// array position in []A
public static void findShifts(int[] A, int N)
{

    // Stores required number of
    // shifts for each element
    int[] shift = new int[N];

    for(int i = 0; i < N; i++)
    {

        // If the element is
        // at sorted position
        if (i == A[i] - 1)
            shift[i] = 0;

        // Otherwise
        else

            // Calculate right shift
            shift[i] = (A[i] - 1 - i + N) % N;
    }

    // Print the respective shifts
    for(int i = 0; i < N; i++)
        Console.Write(shift[i] + " ");
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 4, 3, 2, 5 };
    int N = arr.Length;

    findShifts(arr, N);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// JavaScript program to implement
// the approach

// Function to find the right
// shifts required for each
// element to reach its sorted
// array position in A[]
function findShifts(A, N)
{

    // Stores required number of
    // shifts for each element
    let shift = Array.from({length: N}, (_, i) => 0);

    for(let i = 0; i < N; i++)
    {

        // If the element is
        // at sorted position
        if (i == A[i] - 1)
            shift[i] = 0;

        // Otherwise
        else

            // Calculate right shift
            shift[i] = (A[i] - 1 - i + N) % N;
    }

    // Prlet the respective shifts
    for(let i = 0; i < N; i++)
        document.write(shift[i] + " ");
}

// Driver Code   

    let arr = [ 1, 4, 3, 2, 5 ];
    let N = arr.length;

    findShifts(arr, N);

</script>
```

**Output:** 

```
0 2 0 3 0
```

***时间复杂度:** O(N)*
***辅助空间:** O(N)*