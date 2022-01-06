# 找到初始序列，该序列通过循环增量产生给定的数组，直到索引 P

> 原文:[https://www . geesforgeks . org/find-initial-sequence-产生给定数组的循环增量-up-index-p/](https://www.geeksforgeeks.org/find-initial-sequence-that-produces-a-given-array-by-cyclic-increments-upto-index-p/)

给定一个由 **N** 元素和一个整数 **P** 组成的数组 **arr[]** ，任务是通过以下操作找到产生给定 arr[]的初始数组:

*   从初始阵列中选择一个元素**arr【I】**。 **i <sup>第</sup>指数**为*降为 0* 。
*   **arr[i]** 指数以*循环方式*增加 1，使得最后增加的指数是 **P** 。

**示例:**

> **输入:** arr[] = {4，3，1，6}，P = 4
> **输出:** 3 2 5 4
> **解释:**
> 元素 arr[2]是从初始数组中选择的。以下 arr[i]操作按以下顺序修改给定数组:
> {3，2，0，4} - > {3，2，0，5} - > {4，2，0，5} - > {4，3，0，5} - > {4，3，1，5} - > {4，3，1，6}
> **输入:** arr[] = {3，2，0，2，7}，

**方法:**上述问题可以通过以下步骤解决:

1.  找到数组中的最小元素，从每个索引中减去**min–1**。
2.  现在开始从第**(P–1)**指数中减去 1，并以循环方式对左侧的所有指数重复，直到一个指数变为 0。
3.  将操作数添加到该索引中。
4.  arr[]的当前状态给出了所需的初始状态。打印数组。

下面是上述方法的实现:

## C++

```
// C++ program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to generate and return the
// required initial arrangement
void findArray(int* a,
               int n,
               int P)
{
    // Store the minimum element
    // in the array
    int mi = *min_element(a, a + n);

    // Store the number of increments
    int ctr = 0;
    mi = max(0, mi - 1);

    // Subtract mi - 1 from every index
    for (int i = 0; i < n; i++) {

        a[i] -= mi;

        ctr += mi;
    }

    // Start from the last index which
    // had been incremented
    int i = P - 1;

    // Stores the index chosen to
    // distribute its element
    int start = -1;

    // Traverse the array cyclically and
    // find the index whose element was
    // distributed
    while (1) {

        // If any index has its
        // value reduced to 0
        if (a[i] == 0) {

            // Index whose element was
            // distributed
            start = i;

            break;
        }

        a[i] -= 1;
        ctr += 1;
        i = (i - 1 + n) % n;
    }

    // Store the number of increments
    // at the starting index
    a[start] = ctr;

    // Print the original array
    for (int i = 0; i < n; i++) {
        cout << a[i] << ", ";
    }
}

// Driver Code
int main()
{
    int N = 5;
    int P = 2;

    int arr[] = { 3, 2, 0, 2, 7 };

    findArray(arr, N, P);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{

// Function to generate and return the
// required initial arrangement
static void findArray(int []a, int n,
                               int P)
{

    // Store the minimum element
    // in the array
    int mi = Arrays.stream(a).min().getAsInt();

    // Store the number of increments
    int ctr = 0;
    mi = Math.max(0, mi - 1);

    // Subtract mi - 1 from every index
    for(int i = 0; i < n; i++)
    {
        a[i] -= mi;
        ctr += mi;
    }

    // Start from the last index which
    // had been incremented
    int i = P - 1;

    // Stores the index chosen to
    // distribute its element
    int start = -1;

    // Traverse the array cyclically and
    // find the index whose element was
    // distributed
    while (true)
    {

        // If any index has its
        // value reduced to 0
        if (a[i] == 0)
        {

            // Index whose element was
            // distributed
            start = i;
            break;
        }
        a[i] -= 1;
        ctr += 1;
        i = (i - 1 + n) % n;
    }

    // Store the number of increments
    // at the starting index
    a[start] = ctr;

    // Print the original array
    for(i = 0; i < n; i++)
    {
        System.out.print(a[i] + ", ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int N = 5;
    int P = 2;
    int arr[] = { 3, 2, 0, 2, 7 };

    findArray(arr, N, P);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to generate and return the
# required initial arrangement
def findArray(a, n, P):

    # Store the minimum element
    # in the array
    mi = min(a)

    # Store the number of increments
    ctr = 0
    mi = max(0, mi - 1)

    # Subtract mi - 1 from every index
    for i in range(n):
        a[i] -= mi
        ctr += mi

    # Start from the last index which
    # had been incremented
    i = P - 1

    # Stores the index chosen to
    # distribute its element
    start = -1

    # Traverse the array cyclically and
    # find the index whose element was
    # distributed
    while (1):

        # If any index has its
        # value reduced to 0
        if (a[i] == 0):

            # Index whose element was
            # distributed
            start = i
            break

        a[i] -= 1
        ctr += 1
        i = (i - 1 + n) % n

    # Store the number of increments
    # at the starting index
    a[start] = ctr

    # Print the original array
    print(*a, sep = ', ')

# Driver Code
if __name__ == '__main__':

    N = 5
    P = 2

    arr = [ 3, 2, 0, 2, 7 ]

    findArray(arr, N, P)

# This code is contributed by himanshu77
```

## C#

```
// C# program to implement the
// above approach
using System;
using System.Linq;
class GFG{

// Function to generate and return the
// required initial arrangement
static void findArray(int []a, int n,
                               int P)
{

    // Store the minimum element
    // in the array
    int mi = a.Min();

    // Store the number of increments
    int ctr = 0;
    mi = Math.Max(0, mi - 1);

    // Subtract mi - 1 from every index
    int i;
    for(i = 0; i < n; i++)
    {
        a[i] -= mi;
        ctr += mi;
    }

    // Start from the last index which
    // had been incremented
     i = P - 1;

    // Stores the index chosen to
    // distribute its element
    int start = -1;

    // Traverse the array cyclically and
    // find the index whose element was
    // distributed
    while (true)
    {

        // If any index has its
        // value reduced to 0
        if (a[i] == 0)
        {

            // Index whose element was
            // distributed
            start = i;
            break;
        }
        a[i] -= 1;
        ctr += 1;
        i = (i - 1 + n) % n;
    }

    // Store the number of increments
    // at the starting index
    a[start] = ctr;

    // Print the original array
    for(i = 0; i < n; i++)
    {
        Console.Write(a[i] + ", ");
    }
}

// Driver Code
public static void Main(String[] args)
{
    int N = 5;
    int P = 2;
    int []arr = { 3, 2, 0, 2, 7 };

    findArray(arr, N, P);
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>
// Javascript implementation for the above approach

// Function to generate and return the
// required initial arrangement
function findArray(a, n, P)
{

    // Store the minimum element
    // in the array
    let mi = Math.min(...a);

    // Store the number of increments
    let ctr = 0;
    mi = Math.max(0, mi - 1);

    // Subtract mi - 1 from every index
    for(let i = 0; i < n; i++)
    {
        a[i] -= mi;
        ctr += mi;
    }

    // Start from the last index which
    // had been incremented
    let i = P - 1;

    // Stores the index chosen to
    // distribute its element
    let start = -1;

    // Traverse the array cyclically and
    // find the index whose element was
    // distributed
    while (true)
    {

        // If any index has its
        // value reduced to 0
        if (a[i] == 0)
        {

            // Index whose element was
            // distributed
            start = i;
            break;
        }
        a[i] -= 1;
        ctr += 1;
        i = (i - 1 + n) % n;
    }

    // Store the number of increments
    // at the starting index
    a[start] = ctr;

    // Print the original array
    for(i = 0; i < n; i++)
    {
        document.write(a[i] + ", ");
    }
}

    // Driver Code

    let N = 5;
    let P = 2;
    let arr = [ 3, 2, 0, 2, 7 ];

    findArray(arr, N, P);

</script>
```

**Output:** 

```
2, 1, 4, 1, 6,
```

***时间复杂度:** O(N)*
***辅助空间:** O(1)*