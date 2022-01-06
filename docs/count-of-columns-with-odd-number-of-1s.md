# 奇数为 1 的列数

> 原文:[https://www . geesforgeks . org/带奇数个 1 的列数/](https://www.geeksforgeeks.org/count-of-columns-with-odd-number-of-1s/)

给定一个 **N * M** 2D 二进制矩阵，任务是找出奇数个 **1s** 的列数。
**例:**

> **输入:** mat[][] = {
> {0，0，1，0}，
> {1，0，0，1}，
> {1，1，1，0}}
> **输出:** 2
> 列 2 和 4 是仅有的奇数为 1 的列
> 。
> **输入:** mat[][] = {
> {1，1，0，0，1，1}，

**逼近:**分别求矩阵所有列的和。具有奇数和的列是具有奇数个 1 的列。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

const int col = 4;
const int row = 3;

// Function to return the count of
// columns having odd number of 1s
int countOddColumn(int arr[row][col])
{

    // To store the sum of every column
    int sum[col] = { 0 };

    // For every column
    for (int i = 0; i < col; i++) {

        // Sum of all the element
        // of the current column
        for (int j = 0; j < row; j++) {
            sum[i] += arr[j][i];
        }
    }

    // To store the required count
    int count = 0;

    for (int i = 0; i < col; i++) {

        // If the sum of the current
        // column is odd
        if (sum[i] % 2 == 1) {
            count++;
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[row][col] = { { 0, 0, 1, 0 },
                          { 1, 0, 0, 1 },
                          { 1, 1, 1, 0 } };

    cout << countOddColumn((arr));

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int col = 4;
static int row = 3;

// Function to return the count of
// columns having odd number of 1s
static int countOddColumn(int arr[][])
{

    // To store the sum of every column
    int []sum = new int[col];

    // For every column
    for (int i = 0; i < col; i++)
    {

        // Sum of all the element
        // of the current column
        for (int j = 0; j < row; j++)
        {
            sum[i] += arr[j][i];
        }
    }

    // To store the required count
    int count = 0;

    for (int i = 0; i < col; i++)
    {

        // If the sum of the current
        // column is odd
        if (sum[i] % 2 == 1)
        {
            count++;
        }
    }
    return count;
}

// Driver code
public static void main(String []args)
{
    int arr[][] = {{ 0, 0, 1, 0 },
                   { 1, 0, 0, 1 },
                   { 1, 1, 1, 0 }};

    System.out.println(countOddColumn((arr)));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
col = 4
row = 3

# Function to return the count of
# columns having odd number of 1s
def countOddColumn(arr):

    # To store the sum of every column
    sum = [0 for i in range(col)]

    # For every column
    for i in range(col):

        # Sum of all the element
        # of the current column
        for j in range(row):
            sum[i] += arr[j][i]

    # To store the required count
    count = 0

    for i in range(col):

        # If the sum of the current
        # column is odd
        if (sum[i] % 2 == 1):
            count += 1

    return count

# Driver code
arr = [[0, 0, 1, 0],
       [1, 0, 0, 1],
       [1, 1, 1, 0]]

print(countOddColumn((arr)))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    static int col = 4;
    static int row = 3;

    // Function to return the count of
    // columns having odd number of 1s
    static int countOddColumn(int [,]arr)
    {

        // To store the sum of every column
        int []sum = new int[col];

        // For every column
        for (int i = 0; i < col; i++)
        {

            // Sum of all the element
            // of the current column
            for (int j = 0; j < row; j++)
            {
                sum[i] += arr[j, i];
            }
        }

        // To store the required count
        int count = 0;

        for (int i = 0; i < col; i++)
        {

            // If the sum of the current
            // column is odd
            if (sum[i] % 2 == 1)
            {
                count++;
            }
        }
        return count;
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = {{ 0, 0, 1, 0 },
                      { 1, 0, 0, 1 },
                      { 1, 1, 1, 0 }};

        Console.WriteLine(countOddColumn((arr)));
    }
}

// This code is contributed by kanugargng
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

const col = 4;
const row = 3;

// Function to return the count of
// columns having odd number of 1s
function countOddColumn(arr) {

    // To store the sum of every column
    let sum = new Array(col).fill(0);

    // For every column
    for (let i = 0; i < col; i++) {

        // Sum of all the element
        // of the current column
        for (let j = 0; j < row; j++) {
            sum[i] += arr[j][i];
        }
    }

    // To store the required count
    let count = 0;

    for (let i = 0; i < col; i++) {

        // If the sum of the current
        // column is odd
        if (sum[i] % 2 == 1) {
            count++;
        }
    }

    return count;
}

// Driver code

let arr = [[0, 0, 1, 0],
[1, 0, 0, 1],
[1, 1, 1, 0]];

document.write(countOddColumn((arr)))

</script>
```

**Output:** 

```
2
```

**时间复杂度** : O(行*列)。
**辅助空间** : O(col)。