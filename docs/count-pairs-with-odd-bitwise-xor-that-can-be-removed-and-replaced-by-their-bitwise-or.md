# 对奇数位异或的对进行计数，这些对可以被移除并由它们的按位“或”替换

> 原文:[https://www . geeksforgeeks . org/count-pairs-with-odd-bitwise-xor-the-and-replaced-with-bitwise-or/](https://www.geeksforgeeks.org/count-pairs-with-odd-bitwise-xor-that-can-be-removed-and-replaced-by-their-bitwise-or/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是计算[位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)为奇数的对的数量，这些对可以被移除并替换为它们的[位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)值，直到数组中不存在这样的对。

**示例:**

> **输入:** arr[] = {5，4，7，2}
> **输出:** 2
> **解释:**
> **对(5，4):**5 和 4 的按位异或为 1。移除这一对，并将它们的按位或(= 5)添加到数组中。因此，修改后的数组是{5，7，2}。
> **对(5，2):**5 和 2 的按位异或是 7。移除这一对，并将它们的按位或(= 7)添加到数组中。因此，修改后的数组是{7，7}。
> 
> 因此，可以移除的这种对的数量是 2。
> 
> **输入:** arr[] = {2，4，6 }
> T3】输出: 0

**方法:**给定的问题可以基于以下观察来解决:

*   [一对的逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)只有一个元素为**奇数**另一个为**偶数**时为**奇数**。
*   因此，从数组中移除这样一对并将其[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)添加到数组中不会影响数组中奇数元素的[总数。但是偶数组元素的数量减少了 **1** 。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

因此，想法是找到给定数组中偶数元素的[计数。如果偶数元素](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)的[计数为 **N** ，则需要 **0** 移动。否则，打印**计数**的值作为需要移除的对的合成计数。](https://www.geeksforgeeks.org/count-number-even-odd-elements-array/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the number of pairs
// required to be removed from the array
// and replaced by their Bitwise OR values
void countPairs(int arr[], int N)
{
    // Stores the count of
    // even array elements
    int even = 0;

    // Traverse the given array
    for (int i = 0; i < N; i++) {

        // Increment the count
        // of even array elements
        if (arr[i] % 2 == 0)
            even++;
    }

    // If the array contains at
    // least one odd array element
    if (N - even >= 1) {
        cout << even;
        return;
    }

    // Otherwise, print 0
    cout << 0;
}

// Driver Code
int main()
{
    int arr[] = { 5, 4, 7, 2 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to count the number of pairs
// required to be removed from the array
// and replaced by their Bitwise OR values
static void countPairs(int arr[], int N)
{

    // Stores the count of
    // even array elements
    int even = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Increment the count
        // of even array elements
        if (arr[i] % 2 == 0)
            even++;
    }

    // If the array contains at
    // least one odd array element
    if (N - even >= 1)
    {
        System.out.println(even);
        return;
    }

    // Otherwise, print 0
    System.out.println(0);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 5, 4, 7, 2 };
    int N = arr.length;

    countPairs(arr, N);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of pairs
# required to be removed from the array
# and replaced by their Bitwise OR values
def countPairs(arr, N):

    # Stores the count of
    # even array elements
    even = 0

    # Traverse the given array
    for i in range(N):

        # Increment the count
        # of even array elements
        if (arr[i] % 2 == 0):
            even += 1

    # If the array contains at
    # least one odd array element
    if (N - even >= 1):
        print(even)
        return

    # Otherwise, print 0
    print(0)

# Driver Code
if __name__ == "__main__":

    arr = [ 5, 4, 7, 2 ]
    N = len(arr)

    countPairs(arr, N)

# This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of pairs
// required to be removed from the array
// and replaced by their Bitwise OR values
static void countPairs(int[] arr, int N)
{

    // Stores the count of
    // even array elements
    int even = 0;

    // Traverse the given array
    for(int i = 0; i < N; i++)
    {

        // Increment the count
        // of even array elements
        if (arr[i] % 2 == 0)
            even++;
    }

    // If the array contains at
    // least one odd array element
    if (N - even >= 1)
    {
        Console.WriteLine(even);
        return;
    }

    // Otherwise, print 0
    Console.WriteLine(0);
}

// Driver code
static void Main()
{
    int[] arr = { 5, 4, 7, 2 };
    int N = arr.Length;

    countPairs(arr, N);
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to count the number of pairs
// required to be removed from the array
// and replaced by their Bitwise OR values
function countPairs(arr, N)
{
    // Stores the count of
    // even array elements
    let even = 0;

    // Traverse the given array
    for (let i = 0; i < N; i++) {

        // Increment the count
        // of even array elements
        if (arr[i] % 2 == 0)
            even++;
    }

    // If the array contains at
    // least one odd array element
    if (N - even >= 1) {
        document.write(even);
        return;
    }

    // Otherwise, print 0
    document.write(0);
}

// Driver Code
let arr = [ 5, 4, 7, 2 ];
let N = arr.length;
countPairs(arr, N);

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)