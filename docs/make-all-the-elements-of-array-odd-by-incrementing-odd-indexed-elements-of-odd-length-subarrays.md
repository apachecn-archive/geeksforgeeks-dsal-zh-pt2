# 通过增加奇数长度子阵列的奇数索引元素使阵列的所有元素为奇数

> 原文:[https://www . geeksforgeeks . org/将数组的所有元素都变成奇数乘奇数索引长度的元素子数组/](https://www.geeksforgeeks.org/make-all-the-elements-of-array-odd-by-incrementing-odd-indexed-elements-of-odd-length-subarrays/)

给定一个大小为 **N** 的[阵列](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过选择 **arr[]** 的奇数长度[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)使所有阵列元素为奇数，并在该子阵列中将所有奇数位置的元素增加 **1** 。打印此类所需操作的计数。

**示例:**

> **输入:** arr[] = {2，3，4，3，5，3，2}
> **输出:** 2
> **解释:**
> 在第一次操作中，选择子阵列{2，3，4}并在奇数位置增加其所有元素，即该子阵列的 1 和 3。更新后的数组是{3，3，5，3，5，3，2}。
> 在第二次操作中，选择最后一个索引，即长度为 1 的子阵列，并增加其值。更新后的数组是{3，3，5，3，5，3，3}
> 
> **输入:** arr[] = {1，5，7}
> **输出:** 0
> **说明:**由于所有数组元素都是奇数，所以不需要修改。

**方法:**这个想法是基于这样的观察:每当选择一个子阵列时，要么改变原始阵列中奇数位置的值，要么改变偶数位置的值。每次操作都贪婪地选择子阵就能解决问题。首先，遍历所有奇数索引，一旦找到偶数，就标记子阵列的开始，找到奇数，就结束子阵列，同时更新运算次数。对偶数索引重复相同的过程。按照以下步骤解决问题:

1.  初始化一个变量，比如说**翻转**，以存储所需的最小操作次数。
2.  [遍历数组的偶数索引](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 执行以下步骤:
    *   如果[当前元素为奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)迭代。
    *   否则，从该索引开始每第二个元素迭代一次，直到遇到偶数元素。在完成数组遍历之后，或者如果遇到偶数元素，递增**将**翻转 **1** 。
3.  对于奇数索引，也重复第 2 步**。**
4.  **完成上述步骤后，打印**的值，根据需要翻转**作为最小操作次数。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum subarrays
// whose odd-indexed elements need to
// be incremented to make array odd
void minOperations(int arr[], int n)
{
    // Stores the minimum number of
    // operations required
    int flips = 0;

    // Iterate over even-indices
    for (int i = 0; i < n; i += 2) {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1) {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0) {
            i += 2;
        }

        // Increment number of operations
        flips++;
    }

    // Iterate over odd indexed
    // positions of arr[]
    for (int i = 1; i < n; i += 2) {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1) {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0) {
            i += 2;
        }

        // Increment the number
        // of operations
        flips++;
    }

    // Print the number of operations
    cout << flips;
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 4, 3, 5, 3, 2 };
    int N = sizeof(arr) / sizeof(int);

    // Function Call
    minOperations(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to count minimum subarrays
// whose odd-indexed elements need to
// be incremented to make array odd
static void minOperations(int arr[], int n)
{

    // Stores the minimum number of
    // operations required
    int flips = 0;

    // Iterate over even-indices
    for(int i = 0; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment number of operations
        flips++;
    }

    // Iterate over odd indexed
    // positions of arr[]
    for(int i = 1; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment the number
        // of operations
        flips++;
    }

    // Print the number of operations
    System.out.println(flips);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 3, 5, 3, 2 };
    int N = arr.length;

    // Function Call
    minOperations(arr, N);
}
}

// This code is contributed by jana_sayantan
```

## **C#**

```
// C# program for the above approach
using System;
class GFG
{

// Function to count minimum subarrays
// whose odd-indexed elements need to
// be incremented to make array odd
static void minOperations(int []arr, int n)
{

    // Stores the minimum number of
    // operations required
    int flips = 0;

    // Iterate over even-indices
    for(int i = 0; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment number of operations
        flips++;
    }

    // Iterate over odd indexed
    // positions of []arr
    for(int i = 1; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment the number
        // of operations
        flips++;
    }

    // Print the number of operations
    Console.WriteLine(flips);
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 2, 3, 4, 3, 5, 3, 2 };
    int N = arr.Length;

    // Function Call
    minOperations(arr, N);
}
}

// This code is contributed by Princi Singh
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to count minimum subarrays
# whose odd-indexed elements need to
# be incremented to make array odd
def minOperations(arr, n) :

    # Stores the minimum number of
    # operations required
    flips = 0;
    i = 0;

    # Iterate over even-indices
    while i < n :

        # Check if the current
        # element is odd
        if (arr[i] % 2 == 1) :           
            i += 2;

            # If true, continue
            continue;

        # Otherwise, mark the starting
        # of the subarray and iterate
        # until i < n and arr[i] is even
        while (i < n and arr[i] % 2 == 0) :
            i += 2;

        # Increment number of operations
        flips += 1;       
        i += 2;

    # Iterate over odd indexed
    # positions of arr[]
    i = 1
    while i < n :

        # Check if the current
        # element is odd
        if (arr[i] % 2 == 1) :
            i += 2;

            # If true, continue
            continue;

        # Otherwise, mark the starting
        # of the subarray and iterate
        # until i < n and arr[i] is even
        while (i < n and arr[i] % 2 == 0) :
            i += 2;

        # Increment the number
        # of operations
        flips += 1;       
        i += 2;

    # Print the number of operations
    print(flips);

# Driver Code
if __name__ == "__main__" :

    arr = [ 2, 3, 4, 3, 5, 3, 2 ];
    N = len(arr);

    # Function Call
    minOperations(arr, N);

    # This code is contributed by AnkThon
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to count minimum subarrays
// whose odd-indexed elements need to
// be incremented to make array odd
function minOperations(arr, n)
{

    // Stores the minimum number of
    // operations required
    let flips = 0;

    // Iterate over even-indices
    for(let i = 0; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment number of operations
        flips++;
    }

    // Iterate over odd indexed
    // positions of arr[]
    for(let i = 1; i < n; i += 2)
    {

        // Check if the current
        // element is odd
        if (arr[i] % 2 == 1)
        {

            // If true, continue
            continue;
        }

        // Otherwise, mark the starting
        // of the subarray and iterate
        // until i < n and arr[i] is even
        while (i < n && arr[i] % 2 == 0)
        {
            i += 2;
        }

        // Increment the number
        // of operations
        flips++;
    }

    // Print the number of operations
    document.write(flips);
}

    // Driver Code

    let arr = [ 2, 3, 4, 3, 5, 3, 2 ];
    let N = arr.length;

    // Function Call
    minOperations(arr, N);

// This code is contributed by souravghosh0416.
</script>
```

****Output:** 

```
2
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**