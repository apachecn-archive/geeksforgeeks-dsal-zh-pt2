# 最小化给定矩阵中所有对按位“与”的数组的和

> 原文:[https://www . geeksforgeeks . org/最小化给定矩阵中存在的所有对的按位和数组总和/](https://www.geeksforgeeks.org/minimize-sum-of-an-array-having-bitwise-and-of-all-its-pairs-present-in-a-given-matrix/)

给定一个大小为 **N** 的[正方形对称矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-symmetric/)**mat【】【】**，任务是找到大小为 **N** 的数组**arr【】**的最小可能和，这样对于 **i！= j** ，**arr【I】**和**arr【j】**的 [**按位 AND**](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 的值为**mat【I】【j】**。

**示例:**

> **输入:** mat[][] = {{-1，0，1，1，1}，{0，-1，2，0，2}，{1，2，-1，1，3}，{1，0，1，-1}，{1，2，3，1，-1}}
> **输出:** 10
> **解释:**
> 满足上述条件的数组为{1，2，3，1，3}。
> 数组元素之和为 1 + 2 + 3 + 1 + 3 = 10，最小。
> 
> **输入:** mat[][] = {{-1，2，3}，{2，-1，7}，{3，7，-1 } }
> T3】输出: 17

**方法:**给定的问题可以基于以下观察来解决:

*   两个数字的[位与](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)只有在两个数字中设置的那些位组。
*   因此从[按位“与”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的属性可以看出，结果数组中的一个数必须具有设置在 **i <sup>第</sup>T5】行的至少一个矩阵元素中的所有位集。**
*   因此，结果数组中第**I**位置的数字是第**I**行矩阵所有元素的[位“或”](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

按照以下步骤解决问题:

*   初始化一个变量，比如说**和**到 **0** ，它存储数组的最小可能[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)
*   迭代范围**【0，N–1】**并将除**mat【I】**外的**I<sup>th</sup>T7】行处矩阵所有元素的[位“或”值加到变量 **sum** 上。](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)**
*   完成上述步骤后，打印**总和**的值作为可能的结果**总和**。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum sum
// of the array such that Bitwise
// AND of arr[i] ana arr[j] is mat[i][j]
int findMinSum(vector<vector<int> > mat,
               int N)
{
    // Stores the minimum possible sum
    int sum = 0;

    // Traverse the range [0, N - 1]
    for (int i = 0; i < N; i++) {

        // Stores the Bitwise OR of
        // all the element of a row
        int res = 0;

        // Traverse the range [0, N - 1]
        for (int j = 0; j < N; j++) {

            // If i not equal to j
            if (i != j) {

                // Update the value of
                // res
                res |= mat[i][j];
            }
        }

        // Increment the sum by res
        sum += res;
    }

    // Return minimum possible sum
    return sum;
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { -1, 2, 3 }, { 9, -1, 7 }, { 4, 5, -1 } };
    int N = mat.size();
    cout << findMinSum(mat, N);

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

// Function to find the minimum sum
// of the array such that Bitwise
// AND of arr[i] ana arr[j] is mat[i][j]
static int findMinSum(int mat[][], int N)
{

    // Stores the minimum possible sum
    int sum = 0;

    // Traverse the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores the Bitwise OR of
        // all the element of a row
        int res = 0;

        // Traverse the range [0, N - 1]
        for(int j = 0; j < N; j++)
        {

            // If i not equal to j
            if (i != j)
            {

                // Update the value of
                // res
                res |= mat[i][j];
            }
        }

        // Increment the sum by res
        sum += res;
    }

    // Return minimum possible sum
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int mat[][] = { { -1, 2, 3 },
                    { 9, -1, 7 },
                    { 4, 5, -1 } };
    int N = mat.length;

    System.out.println(findMinSum(mat, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to find the minimum sum
# of the array such that Bitwise
# AND of arr[i] ana arr[j] is mat[i][j]
def findMinSum(mat, N):

    # Stores the minimum possible sum
    sum1 = 0

    # Traverse the range [0, N - 1]
    for i in range(N):

        # Stores the Bitwise OR of
        # all the element of a row
        res = 0

        # Traverse the range [0, N - 1]
        for j in range(N):

            # If i not equal to j
            if (i != j):

                # Update the value of
                # res
                res |= mat[i][j]

        # Increment the sum by res
        sum1 += res

    # Return minimum possible sum
    return sum1

  # Driver code
if __name__ == '__main__':
    mat = [[-1, 2, 3], [9, -1, 7], [4, 5,-1]]
    N = 3
    print(findMinSum(mat, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the minimum sum
// of the array such that Bitwise
// AND of arr[i] ana arr[j] is mat[i][j]
static int findMinSum(int[,] mat, int N)
{

    // Stores the minimum possible sum
    int sum = 0;

    // Traverse the range [0, N - 1]
    for(int i = 0; i < N; i++)
    {

        // Stores the Bitwise OR of
        // all the element of a row
        int res = 0;

        // Traverse the range [0, N - 1]
        for(int j = 0; j < N; j++)
        {

            // If i not equal to j
            if (i != j)
            {

                // Update the value of
                // res
                res |= mat[i, j];
            }
        }

        // Increment the sum by res
        sum += res;
    }

    // Return minimum possible sum
    return sum;
}

// Driver Code
public static void Main(string[] args)
{
    int[,] mat = { { -1, 2, 3 },
                   { 9, -1, 7 },
                   { 4, 5, -1 } };
    int N = mat.GetLength(0);

    Console.WriteLine(findMinSum(mat, N));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript program for the above approach 

// Function to find the minimum sum
// of the array such that Bitwise
// AND of arr[i] ana arr[j] is mat[i][j]
function findMinSum(mat, N)
{

    // Stores the minimum possible sum
    var sum = 0;

    // Traverse the range [0, N - 1]
    for(var i = 0; i < N; i++)
    {

        // Stores the Bitwise OR of
        // all the element of a row
        var res = 0;

        // Traverse the range [0, N - 1]
        for(var j = 0; j < N; j++)
        {

            // If i not equal to j
            if (i != j)
            {

                // Update the value of
                // res
                res |= mat[i][j];
            }
        }

        // Increment the sum by res
        sum += res;
    }

    // Return minimum possible sum
    return sum;
}

// Driver Code
var mat = [ [ -1, 2, 3 ],
            [ 9, -1, 7 ],
            [ 4, 5, -1 ] ];
var N = mat.length;

document.write(findMinSum(mat, N));

// This code is contributed by Ankita saini

</script>
```

**Output:** 

```
23
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*