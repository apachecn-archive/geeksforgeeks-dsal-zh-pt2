# 奇数乘积子阵列计数

> 原文:[https://www . geeksforgeeks . org/带奇数积的子数组计数/](https://www.geeksforgeeks.org/count-of-sub-arrays-with-odd-product/)

给定一个大小为 **N** 的整数数组 **arr[]** ，任务是计算具有奇数乘积的子数组的数量。
**例:**

> **输入:** arr[] = {5，1，2，3，4}
> **输出:** 4
> **说明:**奇数积的子阵列为-
> {5}、{1}、{3}、{5，1}。因此计数为 4。
> **输入:** arr[] = {12，15，7，3，25，6，2，1，1，7}
> **输出:** 16

**天真方法:**一个简单的解决方法是计算每个子阵列的乘积，检查它是否为奇数，并相应地计算计数。
**时间复杂度:***O(N<sup>2</sup>)*
**高效途径:**奇数的乘积只有通过奇数的乘积才有可能。因此，对于阵列中每一个 **K** 连续奇数，具有奇数乘积的子阵列的计数增加 **K*(K+1)/2** 。计算连续奇数的一种方法是计算每两个连续偶数的指数之差，并用 **1** 减去。计算时，将 **-1** 和 **N** 视为偶数的指标。
以下是上述方法的实施:

## C++

```
// C++ program to find the count of
// sub-arrays with odd product
#include <bits/stdc++.h>
using namespace std;

// Function that returns the count of
// sub-arrays with odd product
int countSubArrayWithOddProduct(int* A, int N)
{
    // Initialize the count variable
    int count = 0;

    // Initialize variable to store the
    // last index with even number
    int last = -1;

    // Initialize variable to store
    // count of continuous odd numbers
    int K = 0;

    // Loop through the array
    for (int i = 0; i < N; i++) {
        // Check if the number
        // is even or not
        if (A[i] % 2 == 0) {
            // Calculate count of continuous
            // odd numbers
            K = (i - last - 1);

            // Increase the count of sub-arrays
            // with odd product
            count += (K * (K + 1) / 2);

            // Store the index of last
            // even number
            last = i;
        }
    }

    // N considered as index of
    // even number
    K = (N - last - 1);

    count += (K * (K + 1) / 2);

    return count;
}

// Driver Code
int main()
{
    int arr[] = { 12, 15, 7, 3, 25,
                  6, 2, 1, 1, 7 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << countSubArrayWithOddProduct(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// sub-arrays with odd product
class GFG {

// Function that returns the count of
// sub-arrays with odd product
static int countSubArrayWithOddProduct(int A[],
                                       int N)
{

    // Initialize the count variable
    int count = 0;

    // Initialize variable to store the
    // last index with even number
    int last = -1;

    // Initialize variable to store
    // count of continuous odd numbers
    int K = 0;

    // Loop through the array
    for(int i = 0; i < N; i++)
    {

       // Check if the number
       // is even or not
       if (A[i] % 2 == 0)
       {

           // Calculate count of continuous
           // odd numbers
           K = (i - last - 1);

           // Increase the count of sub-arrays
           // with odd product
           count += (K * (K + 1) / 2);

           // Store the index of last
           // even number
           last = i;
       }
    }

    // N considered as index of
    // even number
    K = (N - last - 1);
    count += (K * (K + 1) / 2);

    return count;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 12, 15, 7, 3, 25, 6, 2, 1, 1, 7 };
    int n = arr.length;

    // Function call
    System.out.println(countSubArrayWithOddProduct(arr, n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program to find the count of
# sub-arrays with odd product

# Function that returns the count of
# sub-arrays with odd product
def countSubArrayWithOddProduct(A, N):

    # Initialize the count variable
    count = 0

    # Initialize variable to store the
    # last index with even number
    last = -1

    # Initialize variable to store
    # count of continuous odd numbers
    K = 0

    # Loop through the array
    for i in range(N):

        # Check if the number
        # is even or not
        if (A[i] % 2 == 0):

            # Calculate count of continuous
            # odd numbers
            K = (i - last - 1)

            # Increase the count of sub-arrays
            # with odd product
            count += (K * (K + 1) / 2)

            # Store the index of last
            # even number
            last = i

    # N considered as index of
    # even number
    K = (N - last - 1)

    count += (K * (K + 1) / 2)
    return count

# Driver Code
if __name__ == '__main__':

    arr = [ 12, 15, 7, 3, 25, 6, 2, 1, 1, 7 ]
    n = len(arr)

    # Function call
    print(int(countSubArrayWithOddProduct(arr, n)))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to find the count of
// sub-arrays with odd product
using System;
class GFG{

// Function that returns the count of
// sub-arrays with odd product    
static int countSubArrayWithOddProduct(int[] A,
                                       int N)
{

    // Initialize the count variable
    int count = 0;

    // Initialize variable to store the
    // last index with even number
    int last = -1;

    // Initialize variable to store
    // count of continuous odd numbers
    int K = 0;

    // Loop through the array
    for(int i = 0; i < N; i++)
    {

       // Check if the number
       // is even or not
       if (A[i] % 2 == 0)
       {

           // Calculate count of continuous
           // odd numbers
           K = (i - last - 1);

           // Increase the count of sub-arrays
           // with odd product
           count += (K * (K + 1) / 2);

           // Store the index of last
           // even number
           last = i;
       }
    }

    // N considered as index of
    // even number
    K = (N - last - 1);
    count += (K * (K + 1) / 2);

    return count;
}

// Driver code
static void Main()
{
    int[] arr = { 12, 15, 7, 3, 25,
                  6, 2, 1, 1, 7 };
    int n = arr.Length;

    // Function call
    Console.WriteLine(countSubArrayWithOddProduct(arr, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to find the count of
// sub-arrays with odd product

// Function that returns the count of
// sub-arrays with odd product
function countSubArrayWithOddProduct(A, N)
{

    // Initialize the count variable
    var count = 0;

    // Initialize variable to store the
    // last index with even number
    var last = -1;

    // Initialize variable to store
    // count of continuous odd numbers
    var K = 0;

    // Loop through the array
    for (var i = 0; i < N; i++)
    {

        // Check if the number
        // is even or not
        if (A[i] % 2 == 0)
        {

            // Calculate count of continuous
            // odd numbers
            K = (i - last - 1);

            // Increase the count of sub-arrays
            // with odd product
            count += (K * (K + 1) / 2);

            // Store the index of last
            // even number
            last = i;
        }
    }

    // N considered as index of
    // even number
    K = (N - last - 1);
    count += (K * (K + 1) / 2);
    return count;
}

// Driver Code
var arr = [ 12, 15, 7, 3, 25,
              6, 2, 1, 1, 7 ];
var n = arr.length;

// Function call
document.write( countSubArrayWithOddProduct(arr, n));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
16
```

**时间复杂度:***O(N)*
T5】辅助空间: *O(1)*