# 矩阵回文中每条路径所需的最小变化

> 原文:[https://www . geeksforgeeks . org/minimum-changes-required-make-in-matrix-回文中的每条路径/](https://www.geeksforgeeks.org/minimum-changes-required-to-make-each-path-in-a-matrix-palindrome/)

给定一个具有 **N** 行和 **M** 列的矩阵，任务是通过单元格值的最小变化，使从单元格 **(N，M)** 到 **(1，1)** 的所有可能路径成为回文。

> 任何单元格 **(x，y)** 的可能移动是向左移动**(x–1，y)** 或向下移动 **(x，y–1)**。

**例:**

> **输入:** mat[ ][ ] = { { 1，2，2 }，{ 1，0，0 } }
> **输出:** 3
> **解释:**
> 对于待回文的矩阵中的每个路径，可能的矩阵(更改后)为
> { { 0，2，2 }，{ 2，2，0 } }或{ { 1，2，2 }，{ 2，2，1 } }。
> **输入:** mat[ ][ ] = { { 5，3 }，{ 0，5 } }
> **输出:** 0
> **说明:**
> 以上矩阵不需要改动。从(N，M)到(1，1)的每个路径都已经是回文

**进场:**

*   如果最后一个单元格的值等于第一个单元格的值，第二个最后一个单元格的值等于第二个单元格的值，依此类推，则路径称为回文。

*   因此我们可以得出结论，要使路径回文，距离([曼哈滕距离](https://en.wiktionary.org/wiki/Manhattan_distance))**×距离 **(N，M)** 的细胞必须等于距离**×距离**×距离 **(1，1)** 的细胞。** 
*   为了最大限度地减少更改次数，请将距离为 **x** 的每个单元格从 **(1，1)** 和 **(N，M)** 转换为这些单元格中所有值中最频繁出现的**。** 

**下面是上述方法的实现。** 

## **C++**

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

#define N 7

// Function for counting changes
int countChanges(int matrix[][N],
                 int n, int m)
{
    // Maximum distance possible
    // is (n - 1 + m - 1)
    int dist = n + m - 1;

    // Stores the maximum element
    int Max_element = 0;
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            // Update the maximum
            Max_element = max(Max_element,
                              matrix[i][j]);
        }
    }

    // Stores frequencies of
    // values for respective
    // distances
    int freq[dist][Max_element + 1];

    // Initialize frequencies of
    // cells as 0
    for (int i = 0; i < dist; i++) {
        for (int j = 0; j < Max_element + 1;
             j++)
            freq[i][j] = 0;
    }

    // Count frequencies of cell
    // values in the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // Increment frequency of
            // value at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    int min_changes_sum = 0;
    for (int i = 0; i < dist / 2; i++) {

        // Store the most frequent
        // value at i-th distance
        // from (0, 0) and (N - 1, M - 1)
        int maximum = 0;
        int total_values = 0;

        // Calculate max frequency
        // and total cells at distance i
        for (int j = 0; j < Max_element + 1;
             j++) {

            maximum
                = max(maximum,
                      freq[i][j]
                          + freq[n + m - 2
                                 - i][j]);

            total_values
                += freq[i][j]
                   + freq[n + m - 2 - i][j];
        }

        // Count changes required
        // to convert all cells
        // at i-th distance to
        // most frequent value
        min_changes_sum
            += total_values - maximum;
    }

    return min_changes_sum;
}

// Driver Code
int main()
{
    int mat[][N] = { { 7, 0, 3, 1, 8, 1, 3 },
                     { 0, 4, 0, 1, 0, 4, 0 },
                     { 3, 1, 8, 3, 1, 0, 7 } };

    int minChanges = countChanges(mat, 3, 7);

    cout << minChanges;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement the
// above approach
import java.util.*;

class GFG{
static int N = 7;

// Function for counting changes
static int countChanges(int matrix[][],
                        int n, int m)
{

    // Maximum distance possible
    // is (n - 1 + m - 1)
    int i, j, dist = n + m - 1;

    // Stores the maximum element
    int Max_element = 0;
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Update the maximum
            Max_element = Math.max(Max_element,
                                   matrix[i][j]);
        }
    }

    // Stores frequencies of
    // values for respective
    // distances
    int freq[][] = new int[dist][Max_element + 1];

    // Initialize frequencies of
    // cells as 0
    for(i = 0; i < dist; i++)
    {
        for(j = 0; j < Max_element + 1;
            j++)
            freq[i][j] = 0;
    }

    // Count frequencies of cell
    // values in the matrix
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Increment frequency of
            // value at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    int min_changes_sum = 0;
    for(i = 0; i < dist / 2; i++)
    {

        // Store the most frequent
        // value at i-th distance
        // from (0, 0) and (N - 1, M - 1)
        int maximum = 0;
        int total_values = 0;

        // Calculate max frequency
        // and total cells at distance i
        for(j = 0; j < Max_element + 1; j++)
        {
            maximum = Math.max(maximum,
                               freq[i][j] +
                               freq[n + m -
                                    2 - i][j]);
            total_values += freq[i][j] +
                            freq[n + m -
                                 2 - i][j];
        }

        // Count changes required
        // to convert all cells
        // at i-th distance to
        // most frequent value
        min_changes_sum += total_values -
                           maximum;
    }
    return min_changes_sum;
}

// Driver Code
public static void main (String []args)
{
    int mat[][] = { { 7, 0, 3, 1, 8, 1, 3 },
                    { 0, 4, 0, 1, 0, 4, 0 },
                    { 3, 1, 8, 3, 1, 0, 7 } };

    int minChanges = countChanges(mat, 3, 7);

    System.out.print(minChanges);
}
}

// This code is contributed by chitranayal
```

## **蟒蛇 3**

```
# Python3 program to implement the
# above approach

# Function for counting changes
def countChanges(matrix, n, m):

    # Maximum distance possible
    # is (n - 1 + m - 1)
    dist = n + m - 1

    # Stores the maximum element
    Max_element = 0
    for i in range(n):
        for j in range(m):

            # Update the maximum
            Max_element = max(Max_element,
                              matrix[i][j])

    # Stores frequencies of
    # values for respective
    # distances
    freq = [[0 for i in range(Max_element + 1)]
               for j in range(dist)]

    # Initialize frequencies of
    # cells as 0
    for i in range(dist):
        for j in range(Max_element + 1):
            freq[i][j] = 0

    # Count frequencies of cell
    # values in the matrix
    for i in range(n):
        for j in range(m):

            # Increment frequency of
            # value at distance i+j
            freq[i + j][matrix[i][j]] += 1

    min_changes_sum = 0
    for i in range(dist // 2):

        # Store the most frequent
        # value at i-th distance
        # from (0, 0) and (N - 1, M - 1)
        maximum = 0
        total_values = 0

        # Calculate max frequency
        # and total cells at distance i
        for j in range(Max_element + 1):
            maximum = max(maximum,
                          freq[i][j] +
                          freq[n + m - 2 - i][j])

            total_values += (freq[i][j] +
                             freq[n + m - 2 - i][j])

        # Count changes required
        # to convert all cells
        # at i-th distance to
        # most frequent value
        min_changes_sum += total_values - maximum

    return min_changes_sum

# Driver code
if __name__ == '__main__':

    mat = [ [ 7, 0, 3, 1, 8, 1, 3 ],
            [ 0, 4, 0, 1, 0, 4, 0 ],
            [ 3, 1, 8, 3, 1, 0, 7 ] ]

    minChanges = countChanges(mat, 3, 7)

    print(minChanges)

# This code is contributed by Shivam Singh
```

## **C#**

```
// C# program to implement the
// above approach
using System;
class GFG{

//static int N = 7;

// Function for counting changes
static int countChanges(int [,]matrix,
                        int n, int m)
{

    // Maximum distance possible
    // is (n - 1 + m - 1)
    int i, j, dist = n + m - 1;

    // Stores the maximum element
    int Max_element = 0;
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Update the maximum
            Max_element = Math.Max(Max_element,
                                   matrix[i, j]);
        }
    }

    // Stores frequencies of
    // values for respective
    // distances
    int [,]freq = new int[dist, Max_element + 1];

    // Initialize frequencies of
    // cells as 0
    for(i = 0; i < dist; i++)
    {
        for(j = 0; j < Max_element + 1;
            j++)
            freq[i, j] = 0;
    }

    // Count frequencies of cell
    // values in the matrix
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Increment frequency of
            // value at distance i+j
            freq[i + j, matrix[i, j]]++;
        }
    }

    int min_changes_sum = 0;
    for(i = 0; i < dist / 2; i++)
    {

        // Store the most frequent
        // value at i-th distance
        // from (0, 0) and (N - 1, M - 1)
        int maximum = 0;
        int total_values = 0;

        // Calculate max frequency
        // and total cells at distance i
        for(j = 0; j < Max_element + 1; j++)
        {
            maximum = Math.Max(maximum,
                               freq[i, j] +
                               freq[n + m -
                                    2 - i, j]);
            total_values += freq[i, j] +
                            freq[n + m -
                                 2 - i, j];
        }

        // Count changes required
        // to convert all cells
        // at i-th distance to
        // most frequent value
        min_changes_sum += total_values -
                           maximum;
    }
    return min_changes_sum;
}

// Driver Code
public static void Main(String []args)
{
    int [,]mat = { { 7, 0, 3, 1, 8, 1, 3 },
                    { 0, 4, 0, 1, 0, 4, 0 },
                    { 3, 1, 8, 3, 1, 0, 7 } };

    int minChanges = countChanges(mat, 3, 7);

    Console.Write(minChanges);
}
}

// This code is contributed by sapnasingh4991
```

## **java 描述语言**

```
<script>
// javascript program to implement
// the above approach

// Function for counting changes
function countChanges(matrix,
                        n, m)
{

    // Maximum distance possible
    // is (n - 1 + m - 1)
    let i, j, dist = n + m - 1;

    // Stores the maximum element
    let Max_element = 0;
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Update the maximum
            Max_element = Math.max(Max_element,
                                   matrix[i][j]);
        }
    }

    // Stores frequencies of
    // values for respective
    // distances
    let freq = new Array(dist);
    for (i = 0; i < freq.length; i++) {
        freq[i] = new Array(2);
    }

    // Initialize frequencies of
    // cells as 0
    for(i = 0; i < dist; i++)
    {
        for(j = 0; j < Max_element + 1;
            j++)
            freq[i][j] = 0;
    }

    // Count frequencies of cell
    // values in the matrix
    for(i = 0; i < n; i++)
    {
        for(j = 0; j < m; j++)
        {

            // Increment frequency of
            // value at distance i+j
            freq[i + j][matrix[i][j]]++;
        }
    }

    let min_changes_sum = 0;
    for(i = 0; i <Math.floor(dist / 2); i++)
    {

        // Store the most frequent
        // value at i-th distance
        // from (0, 0) and (N - 1, M - 1)
        let maximum = 0;
        let total_values = 0;

        // Calculate max frequency
        // and total cells at distance i
        for(j = 0; j < Max_element + 1; j++)
        {
            maximum = Math.max(maximum,
                               freq[i][j] +
                               freq[n + m -
                                    2 - i][j]);
            total_values += freq[i][j] +
                            freq[n + m -
                                 2 - i][j];
        }

        // Count changes required
        // to convert all cells
        // at i-th distance to
        // most frequent value
        min_changes_sum += total_values -
                           maximum;
    }
    return min_changes_sum;
}

    // Driver Code

        let mat = [[ 7, 0, 3, 1, 8, 1, 3 ],
                    [ 0, 4, 0, 1, 0, 4, 0 ],
                    [ 3, 1, 8, 3, 1, 0, 7 ]];

    let minChanges = countChanges(mat, 3, 7);

   document.write(minChanges);

   // This code is contributed by avijitmondal1998.
</script>
```

****Output:**

```
6
```** 

*****时间复杂度:** O(N * M)*
***辅助空间:** O((N + M)*maxm)，其中 maxm 是矩阵中存在的最大元素。***