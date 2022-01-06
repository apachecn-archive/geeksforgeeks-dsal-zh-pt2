# 左侧可被当前元素整除的元素数|集合 2

> 原文:[https://www . geeksforgeeks . org/左侧可被当前元素集 2 整除的元素计数/](https://www.geeksforgeeks.org/count-of-elements-on-the-left-which-are-divisible-by-current-element-set-2/)

给定一个 **N** 整数的数组 **A[]** ，任务是生成一个数组 **B[]** ，使得 **B[i]** 包含 **A[]** 中的索引 **j** 的计数，使得 **j < i** 和 **A[j] % A[i] = 0**
**示例:**

> **输入:** arr[] = {3，5，1}
> **输出:** 0 0 2
> **解释:**
> 3 和 5 不除其左边的任何元素
> 而是 1 除 3 和 5。
> **输入:** arr[] = {8，1，28，4，2，6，7}
> **输出:** 0 1 0 2 3 0 1

**天真方法:**这个方法已经在[这里](https://www.geeksforgeeks.org/count-of-elements-on-the-left-which-are-divisible-by-current-element/)讨论过了。但是这种方法的复杂性是 O(N <sup>2</sup> )。
**高效方法:**

*   我们可以说，如果一个数 A 除以一个数 B，那么 A 就是 B 的一个因子。所以，我们需要找到因子是当前元素的先前元素的数量。

*   我们将维护一个计数数组，其中包含每个元素的因子的计数。

*   现在，迭代数组，对于每个元素
    1.  使当前元素的答案等于计数[ arr[i] ]和

    2.  增加计数数组中每个 arr[i]因子的频率。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to print the
// elements of the array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Function to increment the count
// for each factor of given val
void IncrementFactors(int count[],
                      int val)
{

    for (int i = 1; i * i <= val; i++) {
        if (val % i == 0) {
            if (i == val / i) {
                count[i]++;
            }
            else {
                count[i]++;
                count[val / i]++;
            }
        }
    }
}

// Function to generate and print
// the required array
void generateArr(int A[], int n)
{
    int B[n];

    // Find max element of array
    int maxi = *max_element(A, A + n);

    // Create count array of maxi size
    int count[maxi + 1] = { 0 };

    // For every element of the array
    for (int i = 0; i < n; i++) {

        // Count[ A[i] ] denotes how many
        // previous elements are there whose
        // factor is the current element.
        B[i] = count[A[i]];

        // Increment in count array for
        // factors of A[i]
        IncrementFactors(count, A[i]);
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
int main()
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    generateArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

// Utility function to print the
// elements of the array
static void printArr(int arr[], int n)
{
    for(int i = 0; i < n; i++)
       System.out.print(arr[i] + " ");
}

// Function to increment the count
// for each factor of given val
static void IncrementFactors(int count[],
                             int val)
{
    for(int i = 1; i * i <= val; i++)
    {
       if (val % i == 0)
       {
           if (i == val / i)
           {
               count[i]++;
           }
           else
           {
               count[i]++;
               count[val / i]++;
           }
       }
    }
}

// Function to generate and print
// the required array
static void generateArr(int A[], int n)
{
    int []B = new int[n];

    // Find max element of array
    int maxi = Arrays.stream(A).max().getAsInt();

    // Create count array of maxi size
    int count[] = new int[maxi + 1];

    // For every element of the array
    for(int i = 0; i < n; i++)
    {

       // Count[ A[i] ] denotes how many
       // previous elements are there whose
       // factor is the current element.
       B[i] = count[A[i]];

       // Increment in count array for
       // factors of A[i]
       IncrementFactors(count, A[i]);
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.length;

    generateArr(arr, n);
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Utility function to print
# elements of the array
def printArr(arr, n):

    for i in range(n):
        print(arr[i], end = " ")

# Function to increment the count
# for each factor of given val
def IncrementFactors(count, val):

    i = 1
    while(i * i <= val):
        if (val % i == 0):
            if (i == val // i):
                count[i] += 1

            else:
                count[i] += 1
                count[val // i] += 1

        i += 1

# Function to generate and print
# the required array
def generateArr(A, n):

    B = [0] * n

    # Find max element of arr
    maxi = max(A)

    # Create count array of maxi size
    count = [0] * (maxi + 1)

    # For every element of the array
    for i in range(n):

        # Count[ A[i] ] denotes how many
        # previous elements are there whose
        # factor is the current element.
        B[i] = count[A[i]]

        # Increment in count array for
        # factors of A[i]
        IncrementFactors(count, A[i])

    # Print the generated array
    printArr(B, n)

# Driver code
arr = [ 8, 1, 28, 4, 2, 6, 7 ]
n = len(arr)

generateArr(arr, n)

# This code is contributed by code_hunt
```

## C#

```
// C# implementation of the approach
using System;
using System.Linq;

class GFG{

// Utility function to print the
// elements of the array
static void printArr(int []arr, int n)
{
    for(int i = 0; i < n; i++)
       Console.Write(arr[i] + " ");
}

// Function to increment the count
// for each factor of given val
static void IncrementFactors(int []count,
                             int val)
{
    for(int i = 1; i * i <= val; i++)
    {
       if (val % i == 0)
       {
           if (i == val / i)
           {
               count[i]++;
           }
           else
           {
               count[i]++;
               count[val / i]++;
           }
       }
    }
}

// Function to generate and print
// the required array
static void generateArr(int []A, int n)
{
    int []B = new int[n];

    // Find max element of array
    int maxi = A.Max();

    // Create count array of maxi size
    int []count = new int[maxi + 1];

    // For every element of the array
    for(int i = 0; i < n; i++)
    {

       // Count[ A[i] ] denotes how many
       // previous elements are there whose
       // factor is the current element.
       B[i] = count[A[i]];

       // Increment in count array for
       // factors of A[i]
       IncrementFactors(count, A[i]);
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 8, 1, 28, 4, 2, 6, 7 };
    int n = arr.Length;

    generateArr(arr, n);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Utility function to print the
// elements of the array
function printArr(arr, n)
{
    for (let i = 0; i < n; i++)
        document.write(arr[i] + " ");
}

// Function to increment the count
// for each factor of given val
function IncrementFactors(count, val)
{

    for (let i = 1; i * i <= val; i++) {
        if (val % i == 0) {
            if (i == parseInt(val / i)) {
                count[i]++;
            }
            else {
                count[i]++;
                count[parseInt(val / i)]++;
            }
        }
    }
}

// Function to generate and print
// the required array
function generateArr(A, n)
{
    let B = new Array(n);

    // Find max element of array
    let maxi = Math.max(...A);

    // Create count array of maxi size
    let count = new Array(maxi + 1).fill(0);

    // For every element of the array
    for (let i = 0; i < n; i++) {

        // Count[ A[i] ] denotes how many
        // previous elements are there whose
        // factor is the current element.
        B[i] = count[A[i]];

        // Increment in count array for
        // factors of A[i]
        IncrementFactors(count, A[i]);
    }

    // Print the generated array
    printArr(B, n);
}

// Driver code
    let arr = [ 8, 1, 28, 4, 2, 6, 7 ];
    let n = arr.length;

    generateArr(arr, n);

</script>
```

**Output:** 

```
0 1 0 2 3 0 1
```

***时间复杂度:** O(N *根(MaxElement))*