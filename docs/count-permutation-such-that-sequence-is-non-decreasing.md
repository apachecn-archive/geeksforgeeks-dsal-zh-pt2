# 对排列进行计数，使序列不递减

> 原文:[https://www . geeksforgeeks . org/count-arrangement-so-sequence-is-non-reducing/](https://www.geeksforgeeks.org/count-permutation-such-that-sequence-is-non-decreasing/)

给定整数数组 **arr[]** ，任务是找到数组的置换计数，使得置换按递增顺序排列，即**arr[0]≤arr[1]≤arr[2]≤…≤arr[n–1]**。
**例:**

> **输入:** arr[] = {1，2，1}
> **输出:** 2
> 1，1，2 和 1，1，2 是唯一有效的排列。
> **输入:** arr[] = {5，4，4，5}
> **输出:** 4

**方法:**序列应是非递减的，即**arr[0]≤arr[1]≤arr[2]≤…≤arr[n–1]**。
首先，对数组进行排序，然后将焦点放在所有元素都相等的块上，因为这些元素可以在 **P 中重新排列！**方式，其中 **P** 是该块的大小。
置换该块不会违反给定条件。现在，找到所有元素都相等的所有块，将单个块的答案乘以最终答案，得到可能排列的总数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

#define N 20

// To store the factorials
int fact[N];

// Function to update fact[] array
// such that fact[i] = i!
void pre()
{

    // 0! = 1
    fact[0] = 1;
    for (int i = 1; i < N; i++) {

        // i! = i * (i - 1)!
        fact[i] = i * fact[i - 1];
    }
}

// Function to return the count
// of possible permutations
int CountPermutation(int a[], int n)
{

    // To store the result
    int ways = 1;

    // Sort the array
    sort(a, a + n);

    // Initial size of the block
    int size = 1;
    for (int i = 1; i < n; i++) {

        // Increase the size of block
        if (a[i] == a[i - 1]) {
            size++;
        }
        else {

            // Update the result for
            // the previous block
            ways *= fact[size];

            // Reset the size to 1
            size = 1;
        }
    }

    // Update the result for
    // the last block
    ways *= fact[size];

    return ways;
}

// Driver code
int main()
{

    int a[] = { 1, 2, 4, 4, 2, 4 };
    int n = sizeof(a) / sizeof(a[0]);

    // Pre-calculating factorials
    pre();

    cout << CountPermutation(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.util.Arrays;
import java.io.*;

class GFG
{
static int N = 20;

// To store the factorials
static int []fact=new int[N];

// Function to update fact[] array
// such that fact[i] = i!
static void pre()
{

    // 0! = 1
    fact[0] = 1;
    for (int i = 1; i < N; i++)
    {

        // i! = i * (i - 1)!
        fact[i] = i * fact[i - 1];
    }
}

// Function to return the count
// of possible permutations
static int CountPermutation(int a[], int n)
{

    // To store the result
    int ways = 1;

    // Sort the array
    Arrays.sort(a);

    // Initial size of the block
    int size = 1;
    for (int i = 1; i < n; i++)
    {

        // Increase the size of block
        if (a[i] == a[i - 1])
        {
            size++;
        }
        else
        {

            // Update the result for
            // the previous block
            ways *= fact[size];

            // Reset the size to 1
            size = 1;
        }
    }

    // Update the result for
    // the last block
    ways *= fact[size];

    return ways;
}

// Driver Code
public static void main (String[] args)
{
    int a[] = { 1, 2, 4, 4, 2, 4 };
    int n = a.length;

    // Pre-calculating factorials
    pre();

    System.out.println (CountPermutation(a, n));
}
}

// This code is contributed by Sachin
```

## 蟒蛇 3

```
# Python3 implementation of the approach
N = 20

# To store the factorials
fact = [0] * N;

# Function to update fact[] array
# such that fact[i] = i!
def pre() :

    # 0! = 1
    fact[0] = 1;
    for i in range(1, N):

        # i! = i * (i - 1)!
        fact[i] = i * fact[i - 1];

# Function to return the count
# of possible permutations
def CountPermutation(a, n):

    # To store the result
    ways = 1;

    # Sort the array
    a.sort();

    # Initial size of the block
    size = 1;
    for i in range(1, n):

        # Increase the size of block
        if (a[i] == a[i - 1]):
            size += 1;

        else :

            # Update the result for
            # the previous block
            ways *= fact[size];

            # Reset the size to 1
            size = 1;

    # Update the result for
    # the last block
    ways *= fact[size];

    return ways;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 4, 4, 2, 4 ];
    n = len(a);

    # Pre-calculating factorials
    pre();

    print(CountPermutation(a, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 20;

// To store the factorials
static int []fact = new int[N];

// Function to update fact[] array
// such that fact[i] = i!
static void pre()
{

    // 0! = 1
    fact[0] = 1;
    for (int i = 1; i < N; i++)
    {

        // i! = i * (i - 1)!
        fact[i] = i * fact[i - 1];
    }
}

// Function to return the count
// of possible permutations
static int CountPermutation(int []a, int n)
{

    // To store the result
    int ways = 1;

    // Sort the array
    Array.Sort(a);

    // Initial size of the block
    int size = 1;
    for (int i = 1; i < n; i++)
    {

        // Increase the size of block
        if (a[i] == a[i - 1])
        {
            size++;
        }
        else
        {

            // Update the result for
            // the previous block
            ways *= fact[size];

            // Reset the size to 1
            size = 1;
        }
    }

    // Update the result for
    // the last block
    ways *= fact[size];

    return ways;
}

// Driver Code
static public void Main ()
{
    int []a = { 1, 2, 4, 4, 2, 4 };
    int n = a.Length;

    // Pre-calculating factorials
    pre();

    Console.Write(CountPermutation(a, n));
}
}

// This code is contributed by Sachin.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const N = 20;

// To store the factorials
let fact = new Array(N);

// Function to update fact[] array
// such that fact[i] = i!
function pre()
{

    // 0! = 1
    fact[0] = 1;
    for (let i = 1; i < N; i++) {

        // i! = i * (i - 1)!
        fact[i] = i * fact[i - 1];
    }
}

// Function to return the count
// of possible permutations
function CountPermutation(a, n)
{

    // To store the result
    let ways = 1;

    // Sort the array
    a.sort();

    // Initial size of the block
    let size = 1;
    for (let i = 1; i < n; i++) {

        // Increase the size of block
        if (a[i] == a[i - 1]) {
            size++;
        }
        else {

            // Update the result for
            // the previous block
            ways *= fact[size];

            // Reset the size to 1
            size = 1;
        }
    }

    // Update the result for
    // the last block
    ways *= fact[size];

    return ways;
}

// Driver code

    let a = [ 1, 2, 4, 4, 2, 4 ];
    let n = a.length;

    // Pre-calculating factorials
    pre();

    document.write(CountPermutation(a, n));

</script>
```

**Output:** 

```
12
```

**时间复杂度:** O(N * logN)