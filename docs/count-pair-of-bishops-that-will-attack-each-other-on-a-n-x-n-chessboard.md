# 在 N×N 棋盘上数一对会互相攻击的主教

> 原文:[https://www . geesforgeks . org/count-pair-of-bishops-the-on-a-n-x-n-棋盘上互相攻击/](https://www.geeksforgeeks.org/count-pair-of-bishops-that-will-attack-each-other-on-a-n-x-n-chessboard/)

给定一个 **N x N** [棋盘](https://www.geeksforgeeks.org/tag/chessboard-problems/)和上面 **X** 主教的位置，任务是计算成对主教的数量，使它们互相攻击。请注意，在考虑一对主教时，所有其他主教都不被视为董事会成员。

**示例:**

> **输入:** N = 5，主教[][] = {{2，1}，{3，2}，{2，3}}
> **输出:** 2
> **解释:**位置{2，1}和{3，2}上的主教和位置{3，2}和{2，3}上的主教相互攻击。
> 
> **输入:** N = 10，主教[][] = {{1，1}，{1，5}，{3，3}，{5，1}，{5，5}}
> 输出: 6

**方法:**给定的问题可以用基本的[组合数学](https://www.geeksforgeeks.org/combinatorics-gq/)来解决。因为所有位于同一对角线上的主教都会互相攻击，所以所有可能形成的位于同一对角线上的主教对都会互相攻击。因此，[在左右两个方向上遍历所有对角线](https://www.geeksforgeeks.org/zigzag-or-diagonal-traversal-of-matrix/)的矩阵，并在变量 **cnt** 中计算当前对角线上的主教数量。现在对于每条对角线，攻击的主教数量将为**<sup>CNT</sup>C<sub>2</sub>**。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

int board[20][20];

int countPairs(int N, vector<pair<int, int> > bishops)
{
    // Set all bits to 0
    memset(board, 0, sizeof(board));

    // Set all the bits
    // having bishop to 1
    for (int i = 0; i < bishops.size(); i++) {
        board[bishops[i].first][bishops[i].second] = 1;
    }

    // Stores the final answer
    int ans = 0;

    // Loop to traverse the matrix
    // diagonally in left direction
    for (int s = 2; s <= 2 * N; s++) {

        // Stores count of bishop
        // in the current diagonal
        int cnt = 0;

        for (int i = 1, j = s - i;
             max(i, j) <= min(N, s - 1); i++, j--) {
            if (board[j][i - j] == 1)

                // Update cnt
                cnt++;
        }

        // Update the answer
        if (cnt > 1)
            ans += ((cnt + 1) * cnt) / 2;
    }

    // Loop to traverse the matrix
    // diagonally in right direction
    for (int s = 2; s <= 2 * N; s++) {

        // Stores count of bishop
        // in the current diagonal
        int cnt = 0;

        for (int i = 1, j = s - i;
             max(i, j) <= min(N, s - 1); i++, j--) {
            if (board[i][N - j + 1] == 1)

                // Update cnt
                cnt++;
        }

        // Update the answer
        if (cnt > 1)
            ans += ((cnt + 1) * cnt) / 2;
    }

    // Return answer
    return ans;
}

// Driver code
int main()
{
    int N = 10;
    vector<pair<int, int> > bishops = {
        { 1, 1 }, { 1, 5 }, { 3, 3 }, { 5, 1 }, { 5, 5 }
    };

    cout << countPairs(N, bishops);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;
class GFG
{
  static int [][]board = new int[20][20];

  static int countPairs(int N, int[][] bishops)
  {

    // Set all the bits
    // having bishop to 1
    for (int i = 0; i < bishops.length; i++) {
      board[bishops[i][0]][bishops[i][1]] = 1;
    }

    // Stores the final answer
    int ans = 0;

    // Loop to traverse the matrix
    // diagonally in left direction
    for (int s = 2; s <= 2 * N; s++) {

      // Stores count of bishop
      // in the current diagonal
      int cnt = 0;

      for (int i = 1, j = s - i;
           Math.max(i, j) <= Math.min(N, s - 1)&&i-j>0; i++, j--) {
        if (board[j][i - j] == 1)

          // Update cnt
          cnt++;
      }

      // Update the answer
      if (cnt > 1)
        ans += ((cnt + 1) * cnt) / 2;
    }

    // Loop to traverse the matrix
    // diagonally in right direction
    for (int s = 2; s <= 2 * N; s++) {

      // Stores count of bishop
      // in the current diagonal
      int cnt = 0;

      for (int i = 1, j = s - i;
           Math.max(i, j) <= Math.min(N, s - 1); i++, j--) {
        if (board[i][N - j + 1] == 1)

          // Update cnt
          cnt++;
      }

      // Update the answer
      if (cnt > 1)
        ans += ((cnt + 1) * cnt) / 2;
    }

    // Return answer
    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int N = 10;
    int[][] bishops = {
      { 1, 1 }, { 1, 5 }, { 3, 3 }, { 5, 1 }, { 5, 5 }
    };

    System.out.print(countPairs(N, bishops));

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program for above approach
board = [[0 for i in range(20)] for j in range(20)]

def countPairs(N, bishops):

    # Set all the bits
    # having bishop to 1
    for i in range(len(bishops)):
        board[bishops[i][0]][bishops[i][1]] = 1

    # Stores the final answer
    ans = 0

    # Loop to traverse the matrix
    # diagonally in left direction
    for s in range(2, (2 * N) + 1):

        # Stores count of bishop
        # in the current diagonal
        cnt = 0

        i = 1
        j = s - i
        while(max(i, j) <= min(N, s - 1)):
            if (board[j][i - j] == 1):
                # Update cnt
                cnt += 1
            i += 1
            j -= 1

        # Update the answer
        if (cnt > 1):
            ans += ((cnt + 1) * cnt) // 2

    # Loop to traverse the matrix
    # diagonally in right direction
    for s in range(2, (2 * N) + 1):

        # Stores count of bishop
        # in the current diagonal
        cnt = 0

        i = 1
        j = s - i
        while(max(i, j) <= min(N, s - 1)):

            if (board[i][N - j + 1] == 1):
                # Update cnt
                cnt += 1
            i += 1
            j -= 1

        # Update the answer
        if (cnt > 1):
            ans += ((cnt + 1) * cnt) // 2

    # Return answer
    return ans

# Driver code
N = 10
bishops = [[1, 1], [1, 5], [3, 3], [5, 1], [5, 5]]
print(countPairs(N, bishops))

# This code is contributed by gfgking
```

## C#

```
using System;
class GFG
{
    static int[,] board = new int[20,20];
    static int countPairs(int N, int[,] bishops)
    {

        // Set all the bits
        // having bishop to 1
        for (int i = 0; i < bishops.GetLength(0); i++)
        {
            board[bishops[i,0], bishops[i,1]] = 1;
        }

        // Stores the final answer
        int ans = 0;

        // Loop to traverse the matrix
        // diagonally in left direction
        for (int s = 2; s <= 2 * N; s++)
        {

            // Stores count of bishop
            // in the current diagonal
            int cnt = 0;

            for (int i = 1, j = s - i;
                 Math.Max(i, j) <= Math.Min(N, s - 1) && i - j > 0; i++, j--)
            {
                if (board[j,i - j] == 1)

                    // Update cnt
                    cnt++;
            }

            // Update the answer
            if (cnt > 1)
                ans += ((cnt + 1) * cnt) / 2;
        }

        // Loop to traverse the matrix
        // diagonally in right direction
        for (int s = 2; s <= 2 * N; s++)
        {

            // Stores count of bishop
            // in the current diagonal
            int cnt = 0;

            for (int i = 1, j = s - i;
                 Math.Max(i, j) <= Math.Min(N, s - 1); i++, j--)
            {
                if (board[i,N - j + 1] == 1)

                    // Update cnt
                    cnt++;
            }

            // Update the answer
            if (cnt > 1)
                ans += ((cnt + 1) * cnt) / 2;
        }

        // Return answer
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int N = 10;
        int[,] bishops = new int[5, 2]{{ 1, 1 }, { 1, 5 }, { 3, 3 }, { 5, 1 }, { 5, 5 }};

        Console.Write(countPairs(N, bishops));

    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>

    // JavaScript program for above approach
    let board = new Array(20).fill(0).map(() => new Array(20).fill(0));

    const countPairs = (N, bishops) => {

        // Set all the bits
        // having bishop to 1
        for (let i = 0; i < bishops.length; i++) {
            board[bishops[i][0]][bishops[i][1]] = 1;
        }

        // Stores the final answer
        let ans = 0;

        // Loop to traverse the matrix
        // diagonally in left direction
        for (let s = 2; s <= 2 * N; s++) {

            // Stores count of bishop
            // in the current diagonal
            let cnt = 0;

            for (let i = 1, j = s - i;
                Math.max(i, j) <= Math.min(N, s - 1); i++, j--) {
                if (board[j][i - j] == 1)

                    // Update cnt
                    cnt++;
            }

            // Update the answer
            if (cnt > 1)
                ans += ((cnt + 1) * cnt) / 2;
        }

        // Loop to traverse the matrix
        // diagonally in right direction
        for (let s = 2; s <= 2 * N; s++) {

            // Stores count of bishop
            // in the current diagonal
            let cnt = 0;

            for (let i = 1, j = s - i;
                Math.max(i, j) <= Math.min(N, s - 1); i++, j--) {
                if (board[i][N - j + 1] == 1)

                    // Update cnt
                    cnt++;
            }

            // Update the answer
            if (cnt > 1)
                ans += ((cnt + 1) * cnt) / 2;
        }

        // Return answer
        return ans;
    }

    // Driver code
    let N = 10;
    let bishops = [
        [1, 1], [1, 5], [3, 3], [5, 1], [5, 5]
    ];

    document.write(countPairs(N, bishops));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
6
```

***时间复杂度:**O(N * N)*
T5**辅助空间:** O(N * N)