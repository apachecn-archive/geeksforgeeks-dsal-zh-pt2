# Q 查询与 K 异或后的奇偶位数组元素计数

> 原文:[https://www . geeksforgeeks . org/q 查询用 k 异或后的奇偶位数组元素计数/](https://www.geeksforgeeks.org/count-of-even-and-odd-set-bit-array-elements-after-xor-with-k-for-q-queries/)

给定一个包含 **N** 元素的数组 **arr** 和另一个包含 **K** 值的数组 **Q** ，任务是在与数组 **Q** 中的每个元素 **K** 异或后，用奇数和偶数设置位打印数组 **arr** 中的元素计数。

**示例:**

> **输入:** arr[] = { 2，7，4，5，3 }，Q[] = { 3，4，12，6 }
> T3】输出: 2 3
> 3 2
> 2 3
> 2 3
> 
> **输入:** arr[] = { 7，1，6，5，11 }，Q[] = { 2，10，3，6 }
> **输出:** 3 2
> 2 3
> 2 3
> 2 3

**进场:**

*   两个元素的异或都有奇数或偶数设置位，结果是偶数设置位。
*   对两个元素进行异或运算，一个元素具有奇数位，另一个元素具有偶数位，反之亦然，得到奇数位。
*   使用布莱恩·克尼根算法预计算所有数组元素的偶数和奇数位的元素计数。
*   对于 Q 的所有元素，计算设置位数。如果设置位的计数是偶数，则偶数和奇数设置位元素的计数保持不变。否则反转计数和显示。

下面是上述方法的实现:

## C++

```
// C++ Program to count number
// of even and odd set bits
// elements after XOR with a
// given element

#include <bits/stdc++.h>
using namespace std;

void keep_count(int arr[], int& even,
                int& odd, int N)
{
    // Store the count of set bits
    int count;
    for (int i = 0; i < N; i++) {
        count = 0;

        // Brian Kernighan's algorithm
        while (arr[i] != 0) {
            arr[i] = (arr[i] - 1) & arr[i];
            count++;
        }

        if (count % 2 == 0)
            even++;
        else
            odd++;
    }

    return;
}

// Function to solve Q queries
void solveQueries(
    int arr[], int n,
    int q[], int m)
{

    int even_count = 0, odd_count = 0;

    keep_count(arr, even_count,
               odd_count, n);

    for (int i = 0; i < m; i++) {

        int X = q[i];

        // Store set bits in X
        int count = 0;

        // Count set bits of X
        while (X != 0) {
            X = (X - 1) & X;
            count++;
        }

        if (count % 2 == 0) {
            cout << even_count << " "
                 << odd_count << "\n";
        }
        else {
            cout << odd_count << " "
                 << even_count
                 << "\n";
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 2, 7, 4, 5, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);

    int q[] = { 3, 4, 12, 6 };
    int m = sizeof(q) / sizeof(q[0]);

    solveQueries(arr, n, q, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number
// of even and odd set bits
// elements after XOR with a
// given element
class GFG{

static int even, odd;

static void keep_count(int arr[], int N)
{

    // Store the count of set bits
    int count;

    for(int i = 0; i < N; i++)
    {
       count = 0;

       // Brian Kernighan's algorithm
       while (arr[i] != 0)
       {
           arr[i] = (arr[i] - 1) & arr[i];
           count++;
       }
       if (count % 2 == 0)
           even++;
       else
           odd++;
    }
    return;
}

// Function to solve Q queries
static void solveQueries(int arr[], int n,
                         int q[], int m)
{
    even = 0;
    odd = 0;
    keep_count(arr, n);

    for(int i = 0; i < m; i++)
    {
       int X = q[i];

       // Store set bits in X
       int count = 0;

       // Count set bits of X
       while (X != 0)
       {
           X = (X - 1) & X;
           count++;
       }
       if (count % 2 == 0)
       {
           System.out.print(even + " " +
                             odd + "\n");
       }
       else
       {
           System.out.print(odd + " " +
                           even + "\n");
       }
    }
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 7, 4, 5, 3 };
    int n = arr.length;

    int q[] = { 3, 4, 12, 6 };
    int m = q.length;

    solveQueries(arr, n, q, m);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 program to count number
# of even and odd set bits
# elements after XOR with a
# given element

even = 0
odd = 0

def keep_count(arr, N):

    global even
    global odd

    # Store the count of set bits
    for i in range(N):
        count = 0

        # Brian Kernighan's algorithm
        while (arr[i] != 0):
            arr[i] = (arr[i] - 1) & arr[i]
            count += 1

        if (count % 2 == 0):
            even += 1
        else:
            odd += 1

    return

# Function to solve Q queries
def solveQueries(arr, n, q, m):

    global even
    global odd

    keep_count(arr, n)

    for i in range(m):
        X = q[i]

        # Store set bits in X
        count = 0

        # Count set bits of X
        while (X != 0):
            X = (X - 1) & X
            count += 1

        if (count % 2 == 0):
            print(even, odd)
        else:
            print(odd, even)

# Driver code
if __name__ == '__main__':

    arr = [ 2, 7, 4, 5, 3 ]
    n = len(arr)

    q = [ 3, 4, 12, 6 ]
    m = len(q)

    solveQueries(arr, n, q, m)

# This code is contributed by samarth
```

## C#

```
// C# program to count number
// of even and odd set bits
// elements after XOR with a
// given element
using System;
class GFG{

static int even, odd;

static void keep_count(int []arr, int N)
{

    // Store the count of set bits
    int count;

    for(int i = 0; i < N; i++)
    {
        count = 0;

        // Brian Kernighan's algorithm
        while (arr[i] != 0)
        {
            arr[i] = (arr[i] - 1) & arr[i];
            count++;
        }
        if (count % 2 == 0)
            even++;
        else
            odd++;
    }
    return;
}

// Function to solve Q queries
static void solveQueries(int []arr, int n,
                         int []q, int m)
{
    even = 0;
    odd = 0;
    keep_count(arr, n);

    for(int i = 0; i < m; i++)
    {
        int X = q[i];

        // Store set bits in X
        int count = 0;

        // Count set bits of X
        while (X != 0)
        {
            X = (X - 1) & X;
            count++;
        }
        if (count % 2 == 0)
        {
            Console.Write(even + " " +
                           odd + "\n");
        }
        else
        {
            Console.Write(odd + " " +
                         even + "\n");
        }
    }
}

// Driver code
public static void Main()
{
    int []arr = { 2, 7, 4, 5, 3 };
    int n = arr.Length;

    int []q = { 3, 4, 12, 6 };
    int m = q.Length;

    solveQueries(arr, n, q, m);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count number
// of even and odd set bits
// elements after XOR with a
// given element function even, odd;
function keep_count(arr, N)
{

    // Store the count of set bits
    var count;

    for(i = 0; i < N; i++)
    {
        count = 0;

        // Brian Kernighan's algorithm
        while (arr[i] != 0)
        {
            arr[i] = (arr[i] - 1) & arr[i];
            count++;
        }
        if (count % 2 == 0)
            even++;
        else
            odd++;
    }
    return;
}

// Function to solve Q queries
function solveQueries(arr, n, q, m)
{
    even = 0;
    odd = 0;
    keep_count(arr, n);

    for(i = 0; i < m; i++)
    {
        var X = q[i];

        // Store set bits in X
        var count = 0;

        // Count set bits of X
        while (X != 0)
        {
            X = (X - 1) & X;
            count++;
        }
        if (count % 2 == 0)
        {
            document.write(even + " " +
                            odd + "<br/>");
        }
        else
        {
            document.write(odd + " " +
                          even + "<br/>");
        }
    }
}

// Driver code
var arr = [ 2, 7, 4, 5, 3 ];
var n = arr.length;

var q = [ 3, 4, 12, 6 ];
var m = q.length;

solveQueries(arr, n, q, m);

// This code is contributed by aashish1995

</script>
```

**Output:** 

```
2 3
3 2
2 3
2 3
```

**时间复杂度:**T2【O(N * log N)T4】