# 形成给定阵列所需的 K 尺寸子阵列增量的最小计数

> 原文:[https://www . geeksforgeeks . org/k 尺寸子阵列增量最小计数-形成给定阵列所需/](https://www.geeksforgeeks.org/minimum-count-of-increment-of-k-size-subarrays-required-to-form-a-given-array/)

给定一个数组 **arr[]** 和一个整数 **K** ，任务是找到改变大小为 **N** 的数组 **B** 所需的最小操作数，该数组包含全零，使得 B 的每个元素都大于或等于 arr。即 arr[i] > = B[i]。在任何操作中，您都可以选择大小为 K 的 B 的子阵列，并将子阵列的所有元素增加 1。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，K = 2
> **输出:** 9
> **解释:**
> 起初 B[] = {0，0，0，0，0}运算= 0
> 将子阵列 a[1:2]增加 1 = > B = {1，1，0，0，0}，运算= 1
> 将子阵列 a[2:3]增加 1 = > operations = 2
> 将子数组 a[3:4]增加 2 = > B = {1，2，3，2，0}，operations = 4
> 将子数组 a[4:5]增加 5 = > B = {1，2，3，7，5}，operations = 9
> 因此，此类操作所需的计数为 9。
> 
> **输入:** arr[] = {2，3，1}，K = 3
> **输出:** 3
> **解释:**
> 将整个数组递增 3

**方法:**想法是每当 B[i]小于 arr[i]时递增大小为 K 的子阵列，并且还在每一步将这种操作的计数递增 1。要增加大小为 K 的子阵列，请在 O(1) 中使用[差异数组进行范围查询更新。](https://www.geeksforgeeks.org/difference-array-range-update-query-o1/)

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// minimum number of operations
// required to change an array of
// all zeros such that every element
// is greater than the given array
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// number of operations required
// to change all the array of zeros
// such that every element is greater
// than the given array
int find_minimum_operations(int n, int b[],
                            int k)
{

    // Declaring the difference
    // array of size N
    int d[n + 1] = {0};

    // Number of operations
    int operations = 0, need;

    for(int i = 0; i < n; i++)
    {

        // First update the D[i] value
        // with the previous value
        if (i > 0)
        {
            d[i] += d[i - 1];
        }

        // The index i has to be incremented
        if (b[i] > d[i])
        {

            // We have to perform
            // (b[i]-d[i]) operations more
            operations += b[i] - d[i];

            need = b[i] - d[i];

            // Increment the range
            // i to i + k by need
            d[i] += need;

            // Check if i + k is valid index
            if(i + k <= n)
            {
                d[i + k]-= need;
            }
        }
    }
    cout << operations << endl;
}

// Driver Code
int main()
{
    int n = 5;
    int b[] = { 1, 2, 3, 4, 5 };
    int k = 2;

    // Function Call
    find_minimum_operations(n, b, k);

    return 0;
}

// This code is contributed by shubhamsingh10
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of operations
// required to change an array of
// all zeros such that every element
// is greater than the given array
class GFG{

// Function to find the minimum
// number of operations required
// to change all the array of zeros
// such that every element is greater
// than the given array
static void find_minimum_operations(int n, int b[],
                                    int k)
{

    // Declaring the difference
    // array of size N
    int d[] = new int[n + 1];

    // Number of operations
    int i, operations = 0, need;

    for(i = 0; i < n; i++)
    {

        // First update the D[i] value
        // with the previous value
        if (i > 0)
        {
            d[i] += d[i - 1];
        }

        // The index i has to be incremented
        if (b[i] > d[i])
        {

            // We have to perform
            // (b[i]-d[i]) operations more
            operations += b[i] - d[i];

            need = b[i] - d[i];

            // Increment the range
            // i to i + k by need
            d[i] += need;

            // Check if i + k is valid index
            if(i + k <= n)
            {
                d[i + k]-= need;
            }
        }
    }
    System.out.println(operations);
}

// Driver Code
public static void main (String []args)
{
    int n = 5;
    int b[] = { 1, 2, 3, 4, 5 };
    int k = 2;

    // Function Call
    find_minimum_operations(n, b, k);
}
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 implementation to find the
# minimum number of operations required
# to change an array of all zeros
# such that every element is greater than
# the given array

# Function to find the minimum
# number of operations required
# to change all the array of zeros
# such that every element is greater
# than the given array
def find_minimum_operations(n, b, k):

    # Declaring the difference
    # array of size N
    d =[0 for i in range(n + 1)]

    # Number of operations
    operations = 0

    for i in range(n):

        # First update the D[i] value with
        # the previous value
        d[i]+= d[i-1]

        # The index i has to be incremented
        if b[i]>d[i]:

            # We have to perform
            # (b[i]-d[i]) operations more
            operations+=(b[i]-d[i])

            need =(b[i]-d[i])

            # Increment the range
            # i to i + k by need
            d[i]+= need

            # Check if i + k is valid index
            if i + k<= n:
                d[i + k]-= need

    return operations

# Driver Code
if __name__ == "__main__":
    n = 5
    b =[1, 2, 3, 4, 5]
    k = 2

    # Function Call
    print(find_minimum_operations(n, b, k))
```

## C#

```
// C# implementation to find the
// minimum number of operations
// required to change an array of
// all zeros such that every element
// is greater than the given array
using System;
class GFG{

// Function to find the minimum
// number of operations required
// to change all the array of zeros
// such that every element is greater
// than the given array
static void find_minimum_operations(int n, int[] b,
                                    int k)
{

    // Declaring the difference
    // array of size N
    int[] d = new int[n + 1];

    // Number of operations
    int i, operations = 0, need;

    for(i = 0; i < n; i++)
    {

        // First update the D[i] value
        // with the previous value
        if (i > 0)
        {
            d[i] += d[i - 1];
        }

        // The index i has to be incremented
        if (b[i] > d[i])
        {

            // We have to perform
            // (b[i]-d[i]) operations more
            operations += b[i] - d[i];

            need = b[i] - d[i];

            // Increment the range
            // i to i + k by need
            d[i] += need;

            // Check if i + k is valid index
            if(i + k <= n)
            {
                d[i + k]-= need;
            }
        }
    }
    Console.Write(operations);
}

// Driver Code
public static void Main (string []args)
{
    int n = 5;
    int[] b = { 1, 2, 3, 4, 5 };
    int k = 2;

    // Function Call
    find_minimum_operations(n, b, k);
}
}

// This code is contributed by rock_cool
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum number of operations
// required to change an array of
// all zeros such that every element
// is greater than the given array

// Function to find the minimum
// number of operations required
// to change all the array of zeros
// such that every element is greater
// than the given array
function find_minimum_operations(n, b, k)
{

    // Declaring the difference
    // array of size N
    let d = new Array(n + 1);
    d.fill(0);

    // Number of operations
    let i, operations = 0, need;

    for(i = 0; i < n; i++)
    {

        // First update the D[i] value
        // with the previous value
        if (i > 0)
        {
            d[i] += d[i - 1];
        }

        // The index i has to be incremented
        if (b[i] > d[i])
        {

            // We have to perform
            // (b[i]-d[i]) operations more
            operations += b[i] - d[i];

            need = b[i] - d[i];

            // Increment the range
            // i to i + k by need
            d[i] += need;

            // Check if i + k is valid index
            if (i + k <= n)
            {
                d[i + k]-= need;
            }
        }
    }
    document.write(operations);
}

// Driver code
let n = 5;
let b = [ 1, 2, 3, 4, 5 ];
let k = 2;

// Function Call
find_minimum_operations(n, b, k);

// This code is contributed by divyesh072019

</script>
```

**Output:** 

```
9
```

***时间复杂度:** O(N)*
***辅助空间** : O(N)*