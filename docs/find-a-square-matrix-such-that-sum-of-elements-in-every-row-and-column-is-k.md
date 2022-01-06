# 找到一个正方形矩阵，使得每行每列的元素之和为 K

> 原文:[https://www . geeksforgeeks . org/find-a-square-matrix-so-每行每列元素之和为-k/](https://www.geeksforgeeks.org/find-a-square-matrix-such-that-sum-of-elements-in-every-row-and-column-is-k/)

给定两个整数 **N** 和 **K** ，任务是找到一个 **N** x **N** 的正方形矩阵，这样每一行和每一列的和应该等于 **K** 。**注意**可以有多个这样的矩阵。打印其中任何一个。
**示例:**

> **输入:** N = 3，K = 15
> **输出:**
> 2 7 6
> 9 5 1
> 4 3 8
> **输入:** N = 3，K = 7
> **输出:**
> 7 0 0
> 0 7 0
> 0 7

**方法:**一个 **N x N** 矩阵，使得每个左对角线元素等于 **K** ，其余元素为 **0** 将满足给定条件。这样，每行每列的元素之和就等于 **K** 。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// required matrix
void printMatrix(int n, int k)
{
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // Print k for the left
            // diagonal elements
            if (i == j)
                cout << k << " ";

            // Print 0 for the rest
            else
                cout << "0 ";
        }
        cout << "\n";
    }
}

// Driver code
int main()
{
    int n = 3, k = 7;

    printMatrix(n, k);

    return (0);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to print the required matrix
static void printMatrix(int n, int k)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // Print k for the left
            // diagonal elements
            if (i == j)
                System.out.print(k + " ");

            // Print 0 for the rest
            else
                System.out.print("0 ");
        }
        System.out.print("\n");
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 3, k = 7;

    printMatrix(n, k);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the
# required matrix
def printMatrix(n, k) :

    for i in range(n) :
        for j in range(n) :

            # Print k for the left
            # diagonal elements
            if (i == j) :
                print(k, end = " ");

            # Print 0 for the rest
            else:
                print("0", end = " ");

        print();

# Driver code
if __name__ == "__main__" :

    n = 3; k = 7;

    printMatrix(n, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the required matrix
static void printMatrix(int n, int k)
{
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // Print k for the left
            // diagonal elements
            if (i == j)
                Console.Write(k + " ");

            // Print 0 for the rest
            else
                Console.Write("0 ");
        }
        Console.Write("\n");
    }
}

// Driver code
public static void Main(String[] args)
{
    int n = 3, k = 7;

    printMatrix(n, k);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// javascript implementation of the approach

// Function to print the required matrix
function printMatrix(n , k)
{
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
        {

            // Print k for the left
            // diagonal elements
            if (i == j)
                document.write(k + " ");

            // Prvar 0 for the rest
            else
                document.write("0 ");
        }
        document.write("</br>");
    }
}

// Driver code
var n = 3, k = 7;

printMatrix(n, k);

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
7 0 0 
0 7 0 
0 0 7
```