# 可以放置在 N*N 棋盘上的最大非攻击车

> 原文:[https://www . geeksforgeeks . org/最大-非攻击-可以放置在 nn 棋盘上的车/](https://www.geeksforgeeks.org/maximum-non-attacking-rooks-that-can-be-placed-on-an-nn-chessboard/)

给定一个整数 **N** ，使得存在一个大小为 **N*N** 的棋盘和一个由 **K** 对整数组成的数组**pos【】【】【】**,这些整数代表在给定棋盘中被开叉放置的位置。任务是找到最大数量的车，它们的位置可以放在给定的棋盘上，这样就不会有车攻击其他车。按字典顺序打印位置。

**示例:**

> **输入:** N = 4，K = 2，pos[][] = {{1，4}，{2，2}}
> **输出:**
> 2
> 3 1
> 4 3
> **说明:**
> 给定棋盘上只能再放 2 个车，它们的位置是(3，1)和(4，3)。
> **输入:** N = 5，K = 0，pos[][] = {}
> **输出:**
> 5
> 1 1
> 2 2
> 3 3
> 4 4
> 5
> **解释:**
> 由于棋盘是空的，我们可以在给定的棋盘上放置 5 个车，它们的位置是(1，1)、(2，2)、(3)、(4，4)和(5)

**天真方法:**最简单的方法是尝试在棋盘的每个空位置放置一个车，并检查它是否攻击已经放置的车。以下是步骤:

1.  初始化一个大小为 N*N 的 2D 矩阵 **M[][]** 来表示棋盘，并将已经给定的车放入其中。
2.  横向移动整个矩阵 **M[][]** ，检查第 I 行和第 jth 列是否包含任何车
3.  如果第 I 行和第 jth 列都不包含任何车，则将车放在那里，并将该单元格添加到结果中。
4.  否则，移动到棋盘上的下一个空单元格。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(N <sup>2</sup> )*

**高效进场:**该进场基于根据[鸽笼原则](https://www.geeksforgeeks.org/discrete-mathematics-the-pigeonhole-principle/)最多可在棋盘上放置**(N–K)**车的思路。以下是步骤:

1.  因为没有两个给定的车互相攻击，所以输入中给定的所有行必须是唯一的。同样，输入中给出的所有列必须是唯一的。
2.  因此，只将车放在**N–K**未使用的行和**N–K**未使用的列中。
3.  因此，通过将最小的未使用行与最小的未使用列配对，将第二小的未使用行与第二小的未使用列配对，等等，可以实现字典式的最小配置。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the maximum rooks
// and their positions
void countRooks(int n, int k,
                int pos[2][2])
 {
     int row[n] = {0};
     int col[n] = {0};

     // Initialize row and col array
     for (int i = 0; i < n; i++)
     {
         row[i] = 0;
         col[i] = 0;
     }

     // Marking the location of
     // already placed rooks
     for (int i = 0; i < k; i++)
     {
         row[pos[i][0] - 1] = 1;
         col[pos[i][1] - 1] = 1;
     }

     int res = n - k;

     // Print number of non-attacking
     // rooks that can be placed
     cout << res << " " << endl;

     // To store the placed rook
     // location
     int ri = 0, ci = 0;
     while (res-- > 0)
     {
         // Print lexographically
         // smallest order
         while (row[ri] == 1)
         {
             ri++;
         }
         while (col[ci] == 1)
         {
             ci++;
         }
         cout << (ri + 1) << " " <<
                 (ci + 1) << " " <<endl;
         ri++;
         ci++;
     }
 }

// Driver Code
int main()
{
 // Size of board
    int N = 4;

    // Number of rooks already placed
    int K = 2;

    // Position of rooks
    int pos[2][2] = {{1, 4}, {2, 2}};

    // Function call
    countRooks(N, K, pos);
}
// This code is contributed by shikhasingrajput
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG {

    // Function to print the maximum rooks
    // and their positions
    private static void countRooks(int n, int k,
                                   int pos[][])
    {
        int row[] = new int[n];
        int col[] = new int[n];

        // Initialize row and col array
        for (int i = 0; i < n; i++) {
            row[i] = 0;
            col[i] = 0;
        }

        // Marking the location of
        // already placed rooks
        for (int i = 0; i < k; i++) {
            row[pos[i][0] - 1] = 1;
            col[pos[i][1] - 1] = 1;
        }

        int res = n - k;

        // Print number of non-attacking
        // rooks that can be placed
        System.out.println(res + " ");

        // To store the placed rook
        // location
        int ri = 0, ci = 0;
        while (res-- > 0) {

            // Print lexographically
            // smallest order
            while (row[ri] == 1) {
                ri++;
            }
            while (col[ci] == 1) {
                ci++;
            }
            System.out.println(
                (ri + 1)
                + " " + (ci + 1)
                + " ");
            ri++;
            ci++;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Size of board
        int N = 4;

        // Number of rooks already placed
        int K = 2;

        // Position of rooks
        int pos[][] = { { 1, 4 }, { 2, 2 } };

        // Function call
        countRooks(N, K, pos);
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach
# Function to print maximum rooks
# and their positions
def countRooks(n, k, pos):

    row = [0 for i in range(n)]
    col = [0 for i in range(n)]

    # Marking the location of
    # already placed rooks
    for i in range(k):
        row[pos[i][0] - 1] = 1
        col[pos[i][1] - 1] = 1

    res = n - k

    # Print number of non-attacking
    # rooks that can be placed
    print(res)

    # To store the placed rook
    # location
    ri = 0
    ci = 0

    while (res > 0):

        # Print lexographically
        # smallest order
        while (row[ri] == 1):
            ri += 1

        while (col[ci] == 1):
            ci += 1

        print((ri + 1), (ci + 1))

        ri += 1
        ci += 1
        res -= 1

# Driver Code
if __name__ == '__main__':

    # Size of board
    N = 4

    # Number of rooks already placed
    K = 2

    # Position of rooks
    pos= [ [ 1, 4 ], [ 2, 2 ] ]

    # Function call
    countRooks(N, K, pos)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG{

    // Function to print the maximum rooks
    // and their positions
    private static void countRooks(int n, int k,
                                   int [, ]pos)
    {
        int []row = new int[n];
        int []col = new int[n];

        // Initialize row and col array
        for (int i = 0; i < n; i++)
        {
            row[i] = 0;
            col[i] = 0;
        }

        // Marking the location of
        // already placed rooks
        for (int i = 0; i < k; i++)
        {
            row[pos[i, 0] - 1] = 1;
            col[pos[i, 1] - 1] = 1;
        }

        int res = n - k;

        // Print number of non-attacking
        // rooks that can be placed
        Console.WriteLine(res + " ");

        // To store the placed rook
        // location
        int ri = 0, ci = 0;
        while (res -- > 0)
        {
            // Print lexographically
            // smallest order
            while (row[ri] == 1)
            {
                ri++;
            }
            while (col[ci] == 1)
            {
                ci++;
            }
            Console.WriteLine((ri + 1) + " " +
                              (ci + 1) + " ");
            ri++;
            ci++;
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Size of board
        int N = 4;

        // Number of rooks already placed
        int K = 2;

        // Position of rooks
        int [, ]pos = {{1, 4}, {2, 2}};

        // Function call
        countRooks(N, K, pos);
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

    // Function to print the maximum rooks
    // and their positions
    function countRooks(n, k, pos)
    {
        let row = new Array(n).fill(0);
        let col = new Array(n).fill(0);

        // Initialize row and col array
        for (let i = 0; i < n; i++) {
            row[i] = 0;
            col[i] = 0;
        }

        // Marking the location of
        // already placed rooks
        for (let i = 0; i < k; i++) {
            row[pos[i][0] - 1] = 1;
            col[pos[i][1] - 1] = 1;
        }

        let res = n - k;

        // Print number of non-attacking
        // rooks that can be placed
        document.write(res + " " + "<br/>");

        // To store the placed rook
        // location
        let ri = 0, ci = 0;
        while (res-- > 0) {

            // Print lexographically
            // smallest order
            while (row[ri] == 1) {
                ri++;
            }
            while (col[ci] == 1) {
                ci++;
            }
            document.write(
                (ri + 1)
                + " " + (ci + 1)
                + " " + "<br/>");
            ri++;
            ci++;
        }
    }

// Driver Code

        // Size of board
        let N = 4;

        // Number of rooks already placed
        let K = 2;

        // Position of rooks
        let pos = [[ 1, 4 ], [ 2, 2 ]];

        // Function call
        countRooks(N, K, pos);

</script>
```

**Output:** 

```
2 
3 1 
4 3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N <sup>2</sup> )*