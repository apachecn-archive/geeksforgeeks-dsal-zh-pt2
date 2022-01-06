# 创建每个子矩阵中对角线之和为偶数的矩阵

> 原文:[https://www . geesforgeks . org/create-matrix-其每个子矩阵中的对角线之和为偶数/](https://www.geeksforgeeks.org/create-matrix-whose-sum-of-diagonals-in-each-sub-matrix-is-even/)

给定一个数字 **N** ，任务是创建一个大小为 **N*N** 的正方形矩阵，其值在范围【1，N*N】内，这样一个偶数子正方形矩阵的每个对角线之和为偶数。

**示例:**

> **输入:** N = 3
> **输出:**
> 1 2 3
> 4 5 6
> 7 8 9
> **说明:**对于每个偶数子方阵，每个对角线之和为偶数。
> 1 2
> 4 5
> 每条对角线的和为 6 和 6，即偶数。
> 
> **输入:** N = 4
> **输出:**
> 1 2 3 4
> 6 5 8 7
> 9 10 11 12
> 14 13 16 15
> **说明:**
> 对于每个偶数子方阵，每个对角线之和为偶数。
> 1 2
> 6 5
> 每条对角线之和为 6 和 8，即偶数。

**方法:**思路是从 **1 到 N*N** 按照以下给定方式排列元素:

1.  分别用 1 和 2 个元素初始化奇数和偶数。
2.  迭代范围**【0，N】**内的两个嵌套循环。
3.  如果两个嵌套循环中的索引之和为偶数，则打印**奇数**的值，并将**奇数**增加 **2** ，如果和为奇数，则打印**偶数**的值，并将**偶数**增加 **2** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Function to print N*N order matrix
// with all sub-matrix of even order
// is sum of its diagonal also even
void evenSubMatrix(int N)
{
    // Even index
    int even = 1;

    // Odd index
    int odd = 2;

    // Iterate two nested loop
    for (int i = 0; i < N; i++) {

        for (int j = 0; j < N; j++) {

            // For even index the element
            // should be consecutive odd
            if ((i + j) % 2 == 0) {
                cout << even << " ";
                even += 2;
            }

            // for odd index the element
            // should be consecutive even
            else {
                cout << odd << " ";
                odd += 2;
            }
        }
        cout << "\n";
    }
}

// Driver Code
int main()
{
    // Given order of matrix
    int N = 4;

    // Function call
    evenSubMatrix(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print N*N order matrix
// with all sub-matrix of even order
// is sum of its diagonal also even
static void evenSubMatrix(int N)
{

    // Even index
    int even = 1;

    // Odd index
    int odd = 2;

    // Iterate two nested loop
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // For even index the element
            // should be consecutive odd
            if ((i + j) % 2 == 0)
            {
                System.out.print(even + " ");
                even += 2;
            }

            // For odd index the element
            // should be consecutive even
            else
            {
                System.out.print(odd + " ");
                odd += 2;
            }
        }
        System.out.println();
    }
}

// Driver code
public static void main(String[] args)
{

    // Given order of matrix
    int N = 4;

    // Function call
    evenSubMatrix(N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to prN*N order matrix
# with all sub-matrix of even order
# is sum of its diagonal also even
def evenSubMatrix(N):

    # Even index
    even = 1

    # Odd index
    odd = 2

    # Iterate two nested loop
    for i in range(N):
        for j in range(N):

            # For even index the element
            # should be consecutive odd
            if ((i + j) % 2 == 0):
                print(even, end = " ")
                even += 2

            # For odd index the element
            # should be consecutive even
            else:
                print(odd, end = " ")
                odd += 2

        print()

# Driver Code

# Given order of matrix
N = 4

# Function call
evenSubMatrix(N)

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print N*N order matrix
// with all sub-matrix of even order
// is sum of its diagonal also even
static void evenSubMatrix(int N)
{

    // Even index
    int even = 1;

    // Odd index
    int odd = 2;

    // Iterate two nested loop
    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < N; j++)
        {

            // For even index the element
            // should be consecutive odd
            if ((i + j) % 2 == 0)
            {
                Console.Write(even + " ");
                even += 2;
            }

            // For odd index the element
            // should be consecutive even
            else
            {
                Console.Write(odd + " ");
                odd += 2;
            }
        }
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String[] args)
{

    // Given order of matrix
    int N = 4;

    // Function call
    evenSubMatrix(N);
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>
// Java script program for the above approach

// Function to print N*N order matrix
// with all sub-matrix of even order
// is sum of its diagonal also even
function evenSubMatrix( N)
{

    // Even index
    let even = 1;

    // Odd index
    let odd = 2;

    // Iterate two nested loop
    for(let i = 0; i < N; i++)
    {
        for(let j = 0; j < N; j++)
        {

            // For even index the element
            // should be consecutive odd
            if ((i + j) % 2 == 0)
            {
                document.write(even + " ");
                even += 2;
            }

            // For odd index the element
            // should be consecutive even
            else
            {
                document.write(odd + " ");
                odd += 2;
            }
        }
        document.write("<br>");
    }
}

// Driver code

    // Given order of matrix
    let N = 4;

    // Function call
    evenSubMatrix(N);

// This code is contributed by manoj
</script>
```

**Output:** 

```
1 2 3 4 
6 5 8 7 
9 10 11 12 
14 13 16 15
```

**时间复杂度:***O(N * N)*
T5】辅助空间: *O(1)*