# 找到满足给定条件的大小为 N 的数组

> 原文:[https://www . geesforgeks . org/find-一个满足给定条件的 n 大小数组/](https://www.geeksforgeeks.org/find-an-array-of-size-n-that-satisfies-the-given-conditions/)

给定三个整数 **N** 、 **S** 和 **K** ，任务是创建一个由 **N** 个正整数组成的数组，使得该数组中任意两个连续元素的按位“或”为奇数，并且正好有总和等于 **S** 的 **K** 个子数组，其中 **1 ≤ K ≤ N / 2** 。

**示例:**

> **输入:** N = 4，K = 2，S = 6
> **输出:** 6 7 6 7
> 这里正好有 2 个子阵列{6}和{6}
> ，其和为 6，
> 任意相邻元素的按位 OR 为奇数。
> **输入:** N = 8，K = 3，S = 12
> **输出:**12 13 12 13 12 13 13 13 13

**进场:**

*   在这里观察一个模式 **{S，P，S，P，S，P，…，P，P，P，P}** 。
*   这里 **P** 是奇数 **> S** ，在每一个 **S** 之后都有一个 **P** 的出现。已知奇数位的按位 OR 总是奇数，因此确认每个相邻元素的按位 OR 都是奇数。
*   现在，将 **S** 的 **K** 号准确地放入阵列的上述图案中。
*   除了 **S** 之外，所有元素(P)都大于 S，所以除了那些 K 个子阵之外，不可能有任何子阵的和正好是 **S** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to generate and print
// the required array
void findArray(int n, int k, int s)
{

    // Initially all the positions are empty
    int vis[n] = { 0 };

    // To store the count of positions
    // i such that arr[i] = s
    int cnt = 0;

    // To store the final array elements
    int arr[n];

    for (int i = 0; i < n && cnt < k; i += 2) {

        // Set arr[i] = s and the gap between
        // them is exactly 2 so in for loop
        // we use i += 2
        arr[i] = s;

        // Mark the i'th position as visited
        // as we put arr[i] = s
        vis[i] = 1;

        // Increment the count
        cnt++;
    }
    int val = s;

    // Finding the next odd number after s
    if (s % 2 == 0)
        val++;
    else
        val = val + 2;

    for (int i = 0; i < n; i++) {
        if (vis[i] == 0) {

            // If the i'th position is not visited
            // it means we did not put any value
            // at position i so we put 1 now
            arr[i] = val;
        }
    }

    // Print the final array
    printArr(arr, n);
}

// Driver code
int main()
{
    int n = 8, k = 3, s = 12;

    findArray(n, k, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Utility function to print the
    // contents of an array
    static void printArr(int arr[], int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to generate and print
    // the required array
    static void findArray(int n, int k, int s)
    {

        // Initially all the positions are empty
        int vis[] = new int[n] ;

        // To store the count of positions
        // i such that arr[i] = s
        int cnt = 0;

        // To store the final array elements
        int arr[] = new int[n];

        for (int i = 0; i < n && cnt < k; i += 2)
        {

            // Set arr[i] = s and the gap between
            // them is exactly 2 so in for loop
            // we use i += 2
            arr[i] = s;

            // Mark the i'th position as visited
            // as we put arr[i] = s
            vis[i] = 1;

            // Increment the count
            cnt++;
        }
        int val = s;

        // Finding the next odd number after s
        if (s % 2 == 0)
            val++;
        else
            val = val + 2;

        for (int i = 0; i < n; i++)
        {
            if (vis[i] == 0)
            {

                // If the i'th position is not visited
                // it means we did not put any value
                // at position i so we put 1 now
                arr[i] = val;
            }
        }

        // Print the final array
        printArr(arr, n);
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 8, k = 3, s = 12;

        findArray(n, k, s);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print the
# contents of an array
def printArr(arr, n) :

    for i in range(n) :
        print(arr[i], end= " ");

# Function to generate and print
# the required array
def findArray(n, k, s) :

    # Initially all the positions are empty
    vis = [0] * n;

    # To store the count of positions
    # i such that arr[i] = s
    cnt = 0;

    # To store the final array elements
    arr = [0] * n;
    i = 0;

    while (i < n and cnt < k) :

        # Set arr[i] = s and the gap between
        # them is exactly 2 so in for loop
        # we use i += 2
        arr[i] = s;

        # Mark the i'th position as visited
        # as we put arr[i] = s
        vis[i] = 1;

        # Increment the count
        cnt += 1;
        i += 2;
    val = s;

    # Finding the next odd number after s
    if (s % 2 == 0) :
        val += 1;
    else :
        val = val + 2;

    for i in range(n) :
        if (vis[i] == 0) :

            # If the i'th position is not visited
            # it means we did not put any value
            # at position i so we put 1 now
            arr[i] = val;

    # Print the final array
    printArr(arr, n);

# Driver code
if __name__ == "__main__" :

    n = 8; k = 3; s = 12;

    findArray(n, k, s);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Utility function to print the
    // contents of an array
    static void printArr(int []arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to generate and print
    // the required array
    static void findArray(int n, int k, int s)
    {

        // Initially all the positions are empty
        int []vis = new int[n] ;

        // To store the count of positions
        // i such that arr[i] = s
        int cnt = 0;

        // To store the final array elements
        int []arr = new int[n];

        for (int i = 0; i < n && cnt < k; i += 2)
        {

            // Set arr[i] = s and the gap between
            // them is exactly 2 so in for loop
            // we use i += 2
            arr[i] = s;

            // Mark the i'th position as visited
            // as we put arr[i] = s
            vis[i] = 1;

            // Increment the count
            cnt++;
        }
        int val = s;

        // Finding the next odd number after s
        if (s % 2 == 0)
            val++;
        else
            val = val + 2;

        for (int i = 0; i < n; i++)
        {
            if (vis[i] == 0)
            {

                // If the i'th position is not visited
                // it means we did not put any value
                // at position i so we put 1 now
                arr[i] = val;
            }
        }

        // Print the final array
        printArr(arr, n);
    }

    // Driver code
    public static void Main()
    {
        int n = 8, k = 3, s = 12;

        findArray(n, k, s);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach    
// Utility function to print the
    // contents of an array
    function printArr(arr , n) {
        for (i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Function to generate and print
    // the required array
    function findArray(n , k , s) {

        // Initially all the positions are empty
        var vis = Array(n).fill(0);

        // To store the count of positions
        // i such that arr[i] = s
        var cnt = 0;

        // To store the final array elements
        var arr = Array(n).fill(0);

        for (i = 0; i < n && cnt < k; i += 2) {

            // Set arr[i] = s and the gap between
            // them is exactly 2 so in for loop
            // we use i += 2
            arr[i] = s;

            // Mark the i'th position as visited
            // as we put arr[i] = s
            vis[i] = 1;

            // Increment the count
            cnt++;
        }
        var val = s;

        // Finding the next odd number after s
        if (s % 2 == 0)
            val++;
        else
            val = val + 2;

        for (i = 0; i < n; i++) {
            if (vis[i] == 0) {

                // If the i'th position is not visited
                // it means we did not put any value
                // at position i so we put 1 now
                arr[i] = val;
            }
        }

        // Print the final array
        printArr(arr, n);
    }

    // Driver code

        var n = 8, k = 3, s = 12;

        findArray(n, k, s);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
12 13 12 13 12 13 13 13
```

**时间复杂度:** O(N)