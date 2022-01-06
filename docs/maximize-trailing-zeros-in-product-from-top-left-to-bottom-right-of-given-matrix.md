# 从给定矩阵的左上角到右下角最大化乘积中的尾随零

> 原文:[https://www . geeksforgeeks . org/给定矩阵从左上方到右下方最大化产品中的尾随零/](https://www.geeksforgeeks.org/maximize-trailing-zeros-in-product-from-top-left-to-bottom-right-of-given-matrix/)

给定一个尺寸为 **N * M** 、
的[矩阵](https://www.geeksforgeeks.org/matrix/) **mat[][]** ，任务是打印从给定矩阵的左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的路径中矩阵元素乘积的最大尾随零数。任何单元格 **(i，j)** 唯一可能的移动是 **(i + 1，j)** 或 **(i，j + 1)。**

**示例:**

> **输入:** N = 3，M = 4，mat[][] = {{6，25，4，10}，{12，25，1，15}，{7，15，15，5}}
> **输出:** 4
> **说明:**在从左上方到右下方的所有可能路径中，路径(6，25，4，10，15，5)有最大尾随 0 个数的乘积(= 450000)。因此，零的计数是 4。
> 
> **输入:** N = 3，M = 3，mat[][] = {{2，5，2}，{10，2，40}，{5，4，8}}
> 输出: 2

**天真方法:**想法是生成从给定矩阵的左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的所有可能路径[递归](https://www.geeksforgeeks.org/recursion/)并计算每个路径中元素的乘积。打印产品中尾随零的最大数量。按照以下步骤解决问题:

*   初始化一个变量，说**乘积**存储从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**路径上所有可能元素的乘积。
*   下面的递归关系计算从左上角单元格 **(0，0)** 到右下角单元格**(N–1，M–1)**的所有可能路径的**最大零**值。

> maxZeros(i，j，ProductValue)= max(maxZeros(i–1，j，product*mat[i][j])，maxZeros(I，j–1，product*mat[i][j]))
> 其中，
> maxZeros()是返回最大尾随零个数的函数。

*   根据上述递归关系，递归生成所有可能的路径，当任何路径到达单元格**(N–1，M–1)**时，计算该路径之前乘积的尾随零的计数。
*   当每次递归调用结束时，最大化该递归调用返回的零的数量。
*   在上述步骤之后，打印最大数量的尾随零。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

#define N 3
#define M 4

// Stores the maximum count of zeros
int zeros = 0;

// Function that counts the trailing
// zeros in the given number num
int countZeros(int num)
{

    // Stores the count of zeros
    int count = 0;

    // Iterate digits of num
    while (num > 0 && num % 10 == 0)
    {
        num /= 10;
        count++;
    }

    // Return the count
    return count;
}

// Function to count maximum trailing
// zeros in product of elements in a
// path from top-left to bottom-right
void maxZeros(int mat[][M], int i,
              int j, int product)
{

    // If reached end of matrix
    if (i == N - 1 && j == M - 1)
    {

        // Count the no of zeros product
        product *= mat[i][j];
        zeros = max(zeros, countZeros(product));
        return;
    }

    // If out of bounds, return
    if (i >= N)
        return;
    if (j >= M)
        return;

    // Recurse with move (i+1, j)
    maxZeros(mat, i + 1, j,
            product * mat[i][j]);

    // Recurse with  move(i, j+1)
    maxZeros(mat, i, j + 1,
               product * mat[i][j]);
}

// Function to print the maximum
// count of trailing zeros obtained
void maxZerosUtil(int mat[][M], int i,
                  int j, int product)
{

    // Function Call
    maxZeros(mat, 0, 0, 1);

    // Print the maximum count
    cout << zeros << endl;
}

// Driver Code
int main()
{

    // Given matrix
    int mat[N][M] = { { 6, 25, 4, 10 },
                      { 12, 25, 1, 15 },
                      { 7, 15, 15, 5 } };

    // Function Call
    maxZerosUtil(mat, 0, 0, 1);
}

// This code is contributed by bolliranadheer
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
class GFG {

    // Stores the maximum count of zeros
    static int zeros = 0;

    // Function to count maximum trailing
    // zeros in product of elements in a
    // path from top-left to bottom-right
    public static void maxZeros(int[][] mat,
                                int i, int j,
                                int product)
    {
        // If reached end of matrix
        if (i == mat.length - 1
            && j == mat[0].length - 1) {

            // Count the no of zeros product
            product *= mat[i][j];
            zeros = Math.max(zeros,
                             countZeros(product));
            return;
        }

        // If out of bounds, return
        if (i >= mat.length)
            return;
        if (j >= mat[0].length)
            return;

        // Recurse with move (i+1, j)
        maxZeros(mat, i + 1, j,
                 product * mat[i][j]);

        // Recurse with  move(i, j+1)
        maxZeros(mat, i, j + 1,
                 product * mat[i][j]);
    }

    // Function that counts the trailing
    // zeros in the given number num
    public static int countZeros(int num)
    {
        // Stores the count of zeros
        int count = 0;

        // Iterate digits of num
        while (num > 0 && num % 10 == 0) {

            num /= 10;
            count++;
        }

        // Return the count
        return count;
    }

    // Function to print the maximum
    // count of trailing zeros obtained
    public static void maxZerosUtil(
        int[][] mat, int i, int j, int product)
    {

        // Function Call
        maxZeros(mat, 0, 0, 1);

        // Print the maximum count
        System.out.println(zeros);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given N & M
        int N = 3, M = 4;

        // Given matrix
        int mat[][] = { { 6, 25, 4, 10 },
                        { 12, 25, 1, 15 },
                        { 7, 15, 15, 5 } };

        // Function Call
        maxZerosUtil(mat, 0, 0, 1);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the
# above approach
N = 3
M = 4

# Stores the maximum count
# of zeros
zeros = 0

# Function that counts the
# trailing zeros in the
# given number num
def countZeros(num):

    #  Stores the count of
    #zeros
    count = 0

    # Iterate digits of
    # num
    while (num > 0 and
           num % 10 == 0):
        num //= 10
        count += 1

    # Return the count
    return count

# Function to count maximum
# trailing zeros in product
# of elements in a path from
# top-left to bottom-right
def maxZeros(mat, i,
             j, product):

    global M
    global N

    # If reached end of
    # matrix
    if (i == N - 1 and
        j == M - 1):

        # Count the no of
        # zeros product
        product *= mat[i][j]
        global zeros
        zeros = max(zeros,
                    countZeros(product))
        return

    # If out of bounds,
    # return
    if (i >= N):
        return
    if (j >= M):
        return

    # Recurse with move
    # (i+1, j)
    maxZeros(mat, i + 1, j,
             product * mat[i][j])

    # Recurse with move
    # (i, j+1)
    maxZeros(mat, i, j + 1,
             product * mat[i][j])

# Function to print the
# maximum count of trailing
# zeros obtained
def maxZerosUtil(mat, i,
                 j, product):

    # Function Call
    maxZeros(mat, 0, 0, 1)

    # Print the maximum
    # count
    print(zeros)

# Driver Code
if __name__ == "__main__":

    # Given matrix
    mat = [[6, 25, 4, 10],
           [12, 25, 1, 15],
           [7, 15, 15, 5]]

    # Function Call
    maxZerosUtil(mat, 0, 0, 1)

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Stores the maximum count of zeros
static int zeros = 0;

// Function to count maximum trailing
// zeros in product of elements in a
// path from top-left to bottom-right
public static void maxZeros(int[,] mat,
                            int i, int j,
                            int product,
                            int N, int M)
{

    // If reached end of matrix
    if (i == N - 1 && j == M - 1)
    {

        // Count the no of zeros product
        product *= mat[i, j];
        zeros = Math.Max(zeros,
                         countZeros(product));
        return;
    }

    // If out of bounds, return
    if (i >= mat.GetLength(0))
        return;
    if (j >= mat.GetLength(1))
        return;

    // Recurse with move (i+1, j)
    maxZeros(mat, i + 1, j,
             product * mat[i, j], N, M);

    // Recurse with  move(i, j+1)
    maxZeros(mat, i, j + 1,
             product * mat[i, j], N, M);
}

// Function that counts the trailing
// zeros in the given number num
public static int countZeros(int num)
{

    // Stores the count of zeros
    int count = 0;

    // Iterate digits of num
    while (num > 0 && num % 10 == 0)
    {
        num /= 10;
        count++;
    }

    // Return the count
    return count;
}

// Function to print the maximum
// count of trailing zeros obtained
public static void maxZerosUtil(int[,] mat, int i,
                                int j, int product,
                                int N, int M)
{

    // Function Call
    maxZeros(mat, 0, 0, 1, N, M);

    // Print the maximum count
    Console.WriteLine(zeros);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N & M
    int N = 3, M = 4;

    // Given matrix
    int [,]mat = { { 6, 25, 4, 10 },
                   { 12, 25, 1, 15 },
                   { 7, 15, 15, 5 } };

    // Function Call
    maxZerosUtil(mat, 0, 0, 1, N, M);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

var N = 3
var M = 4

// Stores the maximum count of zeros
var zeros = 0;

// Function that counts the trailing
// zeros in the given number num
function countZeros(num)
{

    // Stores the count of zeros
    var count = 0;

    // Iterate digits of num
    while (num > 0 && num % 10 == 0)
    {
        num /= 10;
        count++;
    }

    // Return the count
    return count;
}

// Function to count maximum trailing
// zeros in product of elements in a
// path from top-left to bottom-right
function maxZeros(mat, i, j, product)
{

    // If reached end of matrix
    if (i == N - 1 && j == M - 1)
    {

        // Count the no of zeros product
        product *= mat[i][j];
        zeros = Math.max(zeros, countZeros(product));
        return;
    }

    // If out of bounds, return
    if (i >= N)
        return;
    if (j >= M)
        return;

    // Recurse with move (i+1, j)
    maxZeros(mat, i + 1, j,
            product * mat[i][j]);

    // Recurse with  move(i, j+1)
    maxZeros(mat, i, j + 1,
               product * mat[i][j]);
}

// Function to print the maximum
// count of trailing zeros obtained
function maxZerosUtil(mat, i, j, product)
{

    // Function Call
    maxZeros(mat, 0, 0, 1);

    // Print the maximum count
    document.write( zeros + "<br>");
}

// Driver Code
// Given matrix
var mat = [ [ 6, 25, 4, 10 ],
            [ 12, 25, 1, 15 ],
            [ 7, 15, 15, 5 ]];

// Function Call

maxZerosUtil(mat, 0, 0, 1);

</script>
```

**Output**

```
4
```

***时间复杂度:**O(2<sup>N * M</sup>)*
***辅助空间:** O(1)*

[**<u>【动态规划】</u>**](https://www.geeksforgeeks.org/dynamic-programming/) **<u>使用自下而上的方法</u> :** 上述方法中的递归调用可以使用辅助数组 **dp[][]** 来减少，并计算自下而上方法中每个状态的值。请遵循以下步骤:

*   创建一个大小为 **N*M** 的辅助数组 **dp[][]** 。
*   **dp[i][j]** 表示第 i <sup>行第</sup>列和第 j <sup>列第</sup>列之前的五位数和二位数。
*   遍历矩阵，将 **dp[][]** 数组的每个状态更新为:

> dp[i][j] =最大值(DP[I–1][j]，DP[I][j–1])

*   打印上述步骤后 **(2s，5s)** 各自计数的最小值作为结果。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

// Create a class pair to store
// count of 2's and 5's
class pair {
    int x, y;

    // Parameterized Constructor
    pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    // Function to covert into Strings
    public String toString()
    {
        return "(" + this.x + ", "
            + this.y + ")";
    }
}

class GFG {

    // Function to get maximum no of
    // zeros in product of path from
    // topleft to bottom right
    public static void maxZeros(
        int[][] mat, int n, int m)
    {
        // Base Case
        if (n == 0 || m == 0)
            return;

        // Store the maximum count of
        // zeros till ith and jth index
        pair dp[][] = new pair[n + 1][m + 1];

        // Initialize the (0, 0)
        dp[0][0] = new pair(countTwos(mat[0][0]),
                            countFives(mat[0][0]));

        // Initialize the first  row
        // and column explicitly
        for (int i = 1; i < n; i++)
            dp[i][0] = add(
                dp[i - 1][0],
                new pair(
                    countTwos(mat[i][0]),
                    countFives(mat[i][0])));

        for (int i = 1; i < m; i++)
            dp[0][i] = add(
                dp[0][i - 1],
                new pair(
                    countTwos(mat[0][i]),
                    countFives(mat[0][i])));

        // Iterate through all the cells
        for (int i = 1; i < n; i++) {

            for (int j = 1; j < m; j++) {

                // Get the pair from the
                // top and from left
                pair top = dp[i - 1][j];
                pair left = dp[i][j - 1];

                pair curr = new pair(
                    countTwos(mat[i][j]),
                    countFives(mat[i][j]));
                top = add(top, curr);
                left = add(left, curr);

                // If there are more number
                // of 0s from top or left
                if (check(top, left))
                    dp[i][j] = top;
                else
                    dp[i][j] = left;
            }
        }

        // Print the no of zeros
        // min(no of 2's, no of 5's)
        System.out.println(
            Math.min(dp[n - 1][m - 1].x,
                     dp[n - 1][m - 1].y));
    }

    // Function to calculate no of zeros
    public static boolean check(
        pair one, pair two)
    {
        int top = Math.min(one.x, one.y);
        int left = Math.min(two.x, two.y);
        if (top > left)
            return true;
        else
            return false;
    }

    // Function to calculate no of 2's
    public static int countTwos(int num)
    {
        int count = 0;
        while (num != 0 && num % 2 == 0) {
            num /= 2;
            count++;
        }

        // Return the final count
        return count;
    }

    // Function to calculate no of 5's
    public static int countFives(int num)
    {
        int count = 0;
        while (num != 0 && num % 5 == 0) {
            num /= 5;
            count++;
        }

        // Return the final count
        return count;
    }

    // Function to add pairs
    public static pair add(pair one,
                           pair two)
    {
        pair np = new pair(one.x + two.x,
                           one.y + two.y);

        // Return the resultant pair
        return np;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given N & M
        int N = 3, M = 4;

        // Given matrix
        int mat[][] = { { 6, 25, 4, 10 },
                        { 12, 25, 1, 15 },
                        { 7, 15, 15, 5 } };

        // Function Call
        maxZeros(mat, N, M);
    }
}
```

## C#

```
// C# program for the above approach
using System;

// Create a class pair to store
// count of 2's and 5's
public class pair
{
    public int x, y;

    // Parameterized Constructor
    public pair(int x, int y)
    {
        this.x = x;
        this.y = y;
    }

    // Function to covert into Strings
    public String toString()
    {
        return "(" + this.x + ", " +
                     this.y + ")";
    }
}

class GFG{

// Function to get maximum no of
// zeros in product of path from
// topleft to bottom right
public static void maxZeros(int[,] mat, int n,
                                        int m)
{

    // Base Case
    if (n == 0 || m == 0)
        return;

    // Store the maximum count of
    // zeros till ith and jth index
    pair [,]dp = new pair[n + 1, m + 1];

    // Initialize the (0, 0)
    dp[0, 0] = new pair(countTwos(mat[0, 0]),
                       countFives(mat[0, 0]));

    // Initialize the first  row
    // and column explicitly
    for(int i = 1; i < n; i++)
        dp[i, 0] = add(dp[i - 1, 0],
                   new pair(
                       countTwos(mat[i, 0]),
                       countFives(mat[i, 0])));

    for(int i = 1; i < m; i++)
        dp[0, i] = add(dp[0, i - 1],
                   new pair(
                       countTwos(mat[0, i]),
                       countFives(mat[0, i])));

    // Iterate through all the cells
    for(int i = 1; i < n; i++)
    {
        for(int j = 1; j < m; j++)
        {

            // Get the pair from the
            // top and from left
            pair top = dp[i - 1, j];
            pair left = dp[i, j - 1];

            pair curr = new pair(
                countTwos(mat[i, j]),
                countFives(mat[i, j]));

            top = add(top, curr);
            left = add(left, curr);

            // If there are more number
            // of 0s from top or left
            if (check(top, left))
                dp[i, j] = top;
            else
                dp[i, j] = left;
        }
    }

    // Print the no of zeros
    // min(no of 2's, no of 5's)
    Console.WriteLine(
        Math.Min(dp[n - 1, m - 1].x,
                 dp[n - 1, m - 1].y));
}

// Function to calculate no of zeros
public static bool check(pair one, pair two)
{
    int top = Math.Min(one.x, one.y);
    int left = Math.Min(two.x, two.y);

    if (top > left)
        return true;
    else
        return false;
}

// Function to calculate no of 2's
public static int countTwos(int num)
{
    int count = 0;
    while (num != 0 && num % 2 == 0)
    {
        num /= 2;
        count++;
    }

    // Return the readonly count
    return count;
}

// Function to calculate no of 5's
public static int countFives(int num)
{
    int count = 0;
    while (num != 0 && num % 5 == 0)
    {
        num /= 5;
        count++;
    }

    // Return the readonly count
    return count;
}

// Function to add pairs
public static pair add(pair one,
                       pair two)
{
    pair np = new pair(one.x + two.x,
                       one.y + two.y);

    // Return the resultant pair
    return np;
}

// Driver Code
public static void Main(String[] args)
{

    // Given N & M
    int N = 3, M = 4;

    // Given matrix
    int [,]mat = { { 6, 25, 4, 10 },
                   { 12, 25, 1, 15 },
                   { 7, 15, 15, 5 } };

    // Function Call
    maxZeros(mat, N, M);
}
}

// This code is contributed by Amit Katiyar
```

**Output**

```
4
```

***时间复杂度:** O(N*M*log <sub>10</sub> (maxE))，其中 maxE 是给定矩阵中的最大值。*
***辅助空间:** O(N*M)*