# 对给定数组中的位或等于 K 的对进行计数

> 原文:[https://www . geeksforgeeks . org/count-pairs-from-给定-array-with-bitwise-or-equal-k/](https://www.geeksforgeeks.org/count-pairs-from-given-array-with-bitwise-or-equal-to-k/)

给定一个由 **N** 正整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是[计算给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中所有可能的对，其中[按位 OR](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 等于 **K** 。

**示例:**

> **输入:** arr[] = {2，38，44，29，62}，K = 46
> **输出:** 2
> **解释:**位或为 46 的数组中只有以下两对:
> 
> *   2 或 44 = 46
> *   38 或 44 = 46
> 
> **输入:** arr[] = {1，5，20，15，14}，K = 20
> **输出:** 5
> **说明:**
> 只有 5 对位或为 20:
> 
> *   1 或 15 = 15
> *   1 或 14 = 15
> *   5 或 15 = 15
> *   5 或 14 = 15
> *   15 或 14 = 15

**方法:**解决问题的思路是[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并对那些[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K** 的对进行计数。检查所有配对后，打印存储的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function that counts the pairs from
// the array whose Bitwise OR is K
void countPairs(int arr[], int k, int size)
{
    // Stores the required
    // count of pairs
    int count = 0, x;

    // Generate all possible pairs
    for (int i = 0; i < size - 1; i++) {

        for (int j = i + 1; j < size; j++) {

            // Perform OR operation
            x = arr[i] | arr[j];

            // If Bitwise OR is equal
            // to K, increment count
            if (x == k)
                count++;
        }
    }

    // Print the total count
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 2, 38, 44, 29, 62 };
    int K = 46;
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    countPairs(arr, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

// Function that counts the pairs from
// the array whose Bitwise OR is K
static void countPairs(int[] arr, int k,
                       int size)
{

    // Stores the required
    // count of pairs
    int count = 0, x;

    // Generate all possible pairs
    for(int i = 0; i < size - 1; i++)
    {
        for(int j = i + 1; j < size; j++)
        {

            // Perform OR operation
            x = arr[i] | arr[j];

            // If Bitwise OR is equal
            // to K, increment count
            if (x == k)
                count++;
        }
    }

    // Print the total count
    System.out.println(count);
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 2, 38, 44, 29, 62 };
    int K = 46;
    int N = arr.length;

    // Function Call
    countPairs(arr, K, N);
}
}

// This code is contributed by code_hunt
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that counts the pairs from
# the array whose Bitwise OR is K
def countPairs(arr, k, size):

    # Stores the required
    # count of pairs
    count = 0

    # Generate all possible pairs
    for i in range(size - 1):
        for j in range(i + 1, size):

            # Perform OR operation
            x = arr[i] | arr[j]

            # If Bitwise OR is equal
            # to K, increment count
            if (x == k):
                count += 1

    # Print the total count
    print(count)

# Driver Code
arr = [ 2, 38, 44, 29, 62 ]
K = 46
N = len(arr)

# Function Call
countPairs(arr, K, N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function that counts the pairs from
// the array whose Bitwise OR is K
static void countPairs(int[] arr, int k,
                       int size)
{

    // Stores the required
    // count of pairs
    int count = 0, x;

    // Generate all possible pairs
    for(int i = 0; i < size - 1; i++)
    {
        for(int j = i + 1; j < size; j++)
        {

            // Perform OR operation
            x = arr[i] | arr[j];

            // If Bitwise OR is equal
            // to K, increment count
            if (x == k)
                count++;
        }
    }

    // Print the total count
    Console.WriteLine(count);
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 38, 44, 29, 62 };
    int K = 46;
    int N = arr.Length;

    // Function Call
    countPairs(arr, K, N);
}
}

// This code is contributed by susmitakundugoaldanga
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function that counts the pairs from
// the array whose Bitwise OR is K
function countPairs(arr, k, size)
{

    // Stores the required
    // count of pairs
    let count = 0, x;

    // Generate all possible pairs
    for(let i = 0; i < size - 1; i++)
    {
        for(let j = i + 1; j < size; j++)
        {

            // Perform OR operation
            x = arr[i] | arr[j];

            // If Bitwise OR is equal
            // to K, increment count
            if (x == k)
                count++;
        }
    }

    // Prlet the total count
    document.write(count);
}

// Driver Code
       let arr = [ 2, 38, 44, 29, 62 ];
    let K = 46;
    let N = arr.length;

    // Function Call
    countPairs(arr, K, N);

   // This code is contributed by avijitmondal998.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*