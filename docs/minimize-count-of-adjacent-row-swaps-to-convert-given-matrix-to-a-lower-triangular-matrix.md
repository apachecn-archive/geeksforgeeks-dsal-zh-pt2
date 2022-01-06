# 最小化相邻行交换的次数，将给定矩阵转换为下三角矩阵

> 原文:[https://www . geesforgeks . org/minimum-相邻行计数-交换-转换-给定矩阵-下三角矩阵/](https://www.geeksforgeeks.org/minimize-count-of-adjacent-row-swaps-to-convert-given-matrix-to-a-lower-triangular-matrix/)

给定大小为 **N × N** 的[矩阵](https://www.geeksforgeeks.org/matrix-introduction/)、 **mat[][]** ，任务是最小化相邻行交换的数量，以将给定矩阵转换为[下三角矩阵](https://www.geeksforgeeks.org/program-print-lower-triangular-upper-triangular-matrix-array/)。如果无法将给定矩阵转换为下三角矩阵，则打印-1。
***注:**下三角矩阵在主对角线以上的所有索引处都包含 0。*

**示例:**

> **输入:** mat[][] = {{0，0，2}，{3，1，0}，{4，0，0}}
> **输出:** 3
> **解释:**
> 交换第一行和第二行{{3，1，0}，{0，0，2}，{4，0，0}}
> 交换第二行和第三行{{3，1，0}，{4，0，0}
> 
> **输入:** mat[][] = {{0，2，3，0}，{0，2，4，0}，{0，5，1，0}，{0，1，1，0}}
> **输出:** -1

**方法:**这个问题可以用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。首先找出每行中出现的零的数量，并将其存储在一个整数数组中。然后，[根据按降序排列的 **0** 的数量，计算排列](https://www.geeksforgeeks.org/number-swaps-sort-adjacent-swapping-allowed/)所需的相邻交换的最小数量。按照以下步骤解决问题:

1.  初始化一个数组，说 **cntZero[]** 来存储每行中出现的 **0** 的计数。
2.  对于 **i <sup>第</sup>T3】行，从 **(i + 1) <sup>第</sup>** 索引遍历**cntZero【】**数组，找到第一个索引，说 **First** 其中**ctnZero【First】>=(N–I-1)**。**
3.  将所有相邻元素从**I<sup>th</sup>T3】索引交换到**cntZero【】T7】数组的 **First** 索引，并增加计数。****
4.  最后，返回将给定矩阵转换为下三角矩阵所需的相邻交换的计数。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of  adjacent swaps
int minAdjSwaps(vector<vector<int> >& mat)
{
    // Stores the size of
    // the given matrix
    int N = mat.size();

    // Stores the count of zero
    // at the end of each row
    vector<int> cntZero(N, 0);

    // Traverse the given matrix
    for (int i = 0; i < N; i++) {

        // Count of 0s at the end
        // of the ith row
        for (int j = N - 1;
             j >= 0 && mat[i][j] == 0;
             j--) {
            cntZero[i]++;
        }
    }

    // Stores the count of swaps
    int cntSwaps = 0;

    // Traverse the cntZero array
    for (int i = 0; i < N; i++) {

        // If count of zero in the
        // i-th row < (N - i - 1)
        if (cntZero[i]
            < (N - i - 1)) {

            // Stores the index of the row
            // where count of zero > (N-i-1)
            int First = i;
            while (First < N
                   && cntZero[First]
                          < (N - i - 1)) {
                First++;
            }

            // If no row found that
            // satisfy the condition
            if (First == N) {
                return -1;
            }

            // Swap the adjacent row
            while (First > i) {
                swap(cntZero[First],
                     cntZero[First - 1]);
                First--;
                cntSwaps++;
            }
        }
    }
    return cntSwaps;
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 0, 0, 2 },
            { 3, 1, 0 },
            { 4, 0, 0 } };
    cout << minAdjSwaps(mat);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count the minimum
// number of  adjacent swaps
static int minAdjSwaps(int [][]mat)
{

    // Stores the size of
    // the given matrix
    int N = mat.length;

    // Stores the count of zero
    // at the end of each row
    int []cntZero = new int[N];

    // Traverse the given matrix
    for(int i = 0; i < N; i++)
    {

        // Count of 0s at the end
        // of the ith row
        for(int j = N - 1;
                j >= 0 && mat[i][j] == 0;
                j--)
        {
            cntZero[i]++;
        }
    }

    // Stores the count of swaps
    int cntSwaps = 0;

    // Traverse the cntZero array
    for(int i = 0; i < N; i++)
    {

        // If count of zero in the
        // i-th row < (N - i - 1)
        if (cntZero[i] < (N - i - 1))
        {

            // Stores the index of the row
            // where count of zero > (N-i-1)
            int First = i;
            while (First < N && cntZero[First] <
                  (N - i - 1))
            {
                First++;
            }

            // If no row found that
            // satisfy the condition
            if (First == N)
            {
                return -1;
            }

            // Swap the adjacent row
            while (First > i)
            {
                cntZero = swap(cntZero, First,
                               First - 1);
                First--;
                cntSwaps++;
            }
        }
    }
    return cntSwaps;
}

static int[] swap(int []arr, int i, int j)
{
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    return arr;
}

// Driver Code
public static void main(String[] args)
{
    int [][]mat = { { 0, 0, 2 },
                    { 3, 1, 0 },
                    { 4, 0, 0 } };

    System.out.print(minAdjSwaps(mat));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the minimum
# number of  adjacent swaps
def minAdjSwaps(mat):

    # Stores the size of
    # the given matrix
    N = len(mat)

    # Stores the count of zero
    # at the end of each row
    cntZero = [0] * (N)

    # Traverse the given matrix
    for i in range(N):

        # Count of 0s at the end
        # of the ith row
        for j in range(N - 1, -1, -1):
            if mat[i][j] != 0:
                break

            cntZero[i] += 1

    # Stores the count of swaps
    cntSwaps = 0

    # Traverse the cntZero array
    for i in range(N):

        # If count of zero in the
        # i-th row < (N - i - 1)
        if (cntZero[i] < (N - i - 1)):

            # Stores the index of the row
            # where count of zero > (N-i-1)
            First = i

            while (First < N and
           cntZero[First] < (N - i - 1)):
                First += 1

            # If no row found that
            # satisfy the condition
            if (First == N):
                return -1

            # Swap the adjacent row
            while (First > i):
                cntZero[First] = cntZero[First - 1]
                cntZero[First - 1] = cntZero[First]

                First -= 1
                cntSwaps += 1

    return cntSwaps

# Driver Code
if __name__ == '__main__':

    mat = [ [ 0, 0, 2 ],
            [ 3, 1, 0 ],
            [ 4, 0, 0 ] ]

    print(minAdjSwaps(mat))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to count the minimum
// number of  adjacent swaps
static int minAdjSwaps(int [,]mat)
{
  // Stores the size of
  // the given matrix
  int N = mat.GetLength(0);

  // Stores the count of zero
  // at the end of each row
  int []cntZero = new int[N];

  // Traverse the given matrix
  for(int i = 0; i < N; i++)
  {
    // Count of 0s at the end
    // of the ith row
    for(int j = N - 1;
            j >= 0 && mat[i, j] == 0;
            j--)
    {
      cntZero[i]++;
    }
  }

  // Stores the count of swaps
  int cntSwaps = 0;

  // Traverse the cntZero array
  for(int i = 0; i < N; i++)
  {
    // If count of zero in the
    // i-th row < (N - i - 1)
    if (cntZero[i] < (N - i - 1))
    {
      // Stores the index of the row
      // where count of zero > (N-i-1)
      int First = i;

      while (First < N &&
             cntZero[First] < (N - i - 1))
      {
        First++;
      }

      // If no row found that
      // satisfy the condition
      if (First == N)
      {
        return -1;
      }

      // Swap the adjacent row
      while (First > i)
      {
        cntZero = swap(cntZero,
                       First, First - 1);
        First--;
        cntSwaps++;
      }
    }
  }
  return cntSwaps;
}

static int[] swap(int []arr,
                  int i, int j)
{
  int temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
  return arr;
}

// Driver Code
public static void Main(String[] args)
{
  int [,]mat = {{0, 0, 2},
                {3, 1, 0},
                {4, 0, 0}};
  Console.Write(minAdjSwaps(mat));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to count the minimum
    // number of adjacent swaps
    function minAdjSwaps(mat) {

        // Stores the size of
        // the given matrix
        var N = mat.length;

        // Stores the count of zero
        // at the end of each row
        var cntZero = Array(N).fill(0);

        // Traverse the given matrix
        for (i = 0; i < N; i++) {

            // Count of 0s at the end
            // of the ith row
            for (j = N - 1; j >= 0 &&
            mat[i][j] == 0; j--)
            {
                cntZero[i]++;
            }
        }

        // Stores the count of swaps
        var cntSwaps = 0;

        // Traverse the cntZero array
        for (i = 0; i < N; i++) {

            // If count of zero in the
            // i-th row < (N - i - 1)
            if (cntZero[i] < (N - i - 1)) {

                // Stores the index of the row
                // where count of zero > (N-i-1)
                var First = i;
                while (First < N && cntZero[First] <
                (N - i - 1))
                {
                    First++;
                }

                // If no row found that
                // satisfy the condition
                if (First == N) {
                    return -1;
                }

                // Swap the adjacent row
                while (First > i) {
                    cntZero = swap(cntZero, First,
                    First - 1);
                    First--;
                    cntSwaps++;
                }
            }
        }
        return cntSwaps;
    }

    function swap(arr , i , j) {
        var temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
        return arr;
    }

    // Driver Code

        var mat = [ [ 0, 0, 2 ],
        [ 3, 1, 0 ],
        [ 4, 0, 0 ] ];

        document.write(minAdjSwaps(mat));

// This code contributed by gauravrajput1

</script>
```

**Output**

```
3
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)