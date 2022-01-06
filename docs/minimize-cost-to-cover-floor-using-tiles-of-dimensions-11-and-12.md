# 使用尺寸为 1*1 和 1*2 的瓷砖覆盖地板的成本最小化

> 原文:[https://www . geeksforgeeks . org/最小化使用尺寸为 11 和 12 的瓷砖覆盖地板的成本/](https://www.geeksforgeeks.org/minimize-cost-to-cover-floor-using-tiles-of-dimensions-11-and-12/)

给定一个由**' '组成的 **N*M** 大小的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** '**和**' ***字符分别代表一个楼层和两个正整数 **A** 和 **B** 分别代表一个 **1*1** 和 **1*2** 瓷砖的成本，任务是填充所有有**的字符。'**在地板上铺上尺寸为 **1*1** 或 **1*2** 的瓷砖，以使填充地板的成本最小化，并且瓷砖不允许旋转。

**示例:**

> **输入:** A = 2，B = 10，arr[][] = {{ ' . ', '.', '*'}, {'.'、“*”、“*”}
> **输出:** 6
> **解释:**
> 用 1*1 平铺覆盖 arr[0][0]，用 1*1 平铺覆盖 arr[0][1]，用 1*1 平铺覆盖 arr[1][0]。
> 因此，最小成本为 2 + 2 +2 = 6。
> 
> **输入:** A = 2，B = 6，arr[][] = {{ ' . ', '.', '.'}, {'*', '*', '.'}, {'.', '.'，' * }
> T3】输出: 12

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思路是[逐行遍历给定的 2D 阵](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)，如果连续两个**' '遇到**时，则选择放置两个 **1 * 1 瓷砖**或一个 **1 * 2 瓷砖**成本最低的瓷砖。按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 为 **0** 存储最小总成本。
*   使用用于行索引的 **i** 和用于列索引的 **j** 逐行遍历给定的 2D 数组**arr[][]**，并执行以下步骤:
    *   如果 **arr[i][j]** 的值等于**' ***，则[继续迭代](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   否则，检查以下情况:
        *   如果 **j** 的值为**M(M–1)**，则将 **A** 添加到变量 **ans** 中。
        *   否则，如果 **(arr[i][j + 1])** 的值为**' . '**，然后将值 **2*A** 和 **B** 的最小值添加到变量**和**中。
        *   在所有其他情况下，将 **A** 的值添加到变量 **ans** 中。
*   完成上述步骤后，打印**和**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum cost
// of flooring with the given tiles
void minCost(vector<vector<char> > arr,
             int A, int B)
{
    // Store the size of the 2d array
    int n = arr.size();
    int m = arr[0].size();

    // Stores the minimum cost of
    // flooring
    int ans = 0;

    // Traverse the 2d array row-wise
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If the current character
            // is '*', then skip it
            if (arr[i][j] == '*')
                continue;

            // Choose the 1*1 tile if
            // j is m-1
            if (j == m - 1)
                ans += A;

            // If consecutive '.' are
            // present, the greedily
            // choose tile with the
            // minimum cost
            else {
                if (arr[i][j + 1] == '.') {
                    ans += min(2 * A, B);
                    j++;
                }

                // Otherwise choose
                // the 1*1 tile
                else
                    ans += A;
            }
        }
    }

    // Print the minimum cost
    cout << ans;
}

// Driver Code
int main()
{
    vector<vector<char> > arr = { { '.', '.', '*' },
                                  { '.', '*', '*' } };
    int A = 2, B = 10;
    minCost(arr, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class MyClass
{

// Function to find the minimum cost
// of flooring with the given tiles
static void minCost(char arr[][], int A, int B)
{

    // Store the size of the 2d array
    int n = arr.length;
    int m = arr[0].length;

    // Stores the minimum cost of
    // flooring
    int ans = 0;

    // Traverse the 2d array row-wise
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If the current character
            // is '*', then skip it
            if (arr[i][j] == '*')
                continue;

            // Choose the 1*1 tile if
            // j is m-1
            if (j == m - 1)
                ans += A;

            // If consecutive '.' are
            // present, the greedily
            // choose tile with the
            // minimum cost
            else {
                if (arr[i][j + 1] == '.') {
                    ans += Math.min(2 * A, B);
                    j++;
                }

                // Otherwise choose
                // the 1*1 tile
                else
                    ans += A;
            }
        }
    }

    // Print the minimum cost
    System.out.println(ans);
}

// Driver Code
public static void main(String args[])
{
    char [][]arr = { { '.', '.', '*' },
                                  { '.', '*', '*' } };
    int A = 2, B = 10;
    minCost(arr, A, B);
}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the minimum cost
# of flooring with the given tiles
def minCost(arr, A, B):

    # Store the size of the 2d array
    n = len(arr)
    m = len(arr[0])

    # Stores the minimum cost of
    # flooring
    ans = 0

    # Traverse the 2d array row-wise
    for i in range(n):
        j = 0

        while j < m:

            # If the current character
            # is '*', then skip it
            if (arr[i][j] == '*'):
                j += 1
                continue

            # Choose the 1*1 tile if
            # j is m-1
            if (j == m - 1):
                ans += A

            # If consecutive '.' are
            # present, the greedily
            # choose tile with the
            # minimum cost
            else:
                if (arr[i][j + 1] == '.'):
                    ans += min(2 * A, B)
                    j += 1

                # Otherwise choose
                # the 1*1 tile
                else:
                    ans += A

            j += 1

    # Print the minimum cost
    print (ans)

# Driver Code
if __name__ == '__main__':

    arr = [ [ '.', '.', '*' ],
            [ '.', '*', '*' ] ]
    A, B = 2, 10

    minCost(arr, A, B)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
public class GFG{

    // Function to find the minimum cost
// of flooring with the given tiles
static void minCost(char[,] arr, int A, int B)
{

    // Store the size of the 2d array
    int n = arr.GetLength(0);
    int m = arr.GetLength(1);

    // Stores the minimum cost of
    // flooring
    int ans = 0;

    // Traverse the 2d array row-wise
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If the current character
            // is '*', then skip it
            if (arr[i,j] == '*')
                continue;

            // Choose the 1*1 tile if
            // j is m-1
            if (j == m - 1)
                ans += A;

            // If consecutive '.' are
            // present, the greedily
            // choose tile with the
            // minimum cost
            else {
                if (arr[i,j + 1] == '.') {
                    ans += Math.Min(2 * A, B);
                    j++;
                }

                // Otherwise choose
                // the 1*1 tile
                else
                    ans += A;
            }
        }
    }

    // Print the minimum cost
    Console.WriteLine(ans);
}

// Driver Code
    static public void Main ()
    {

        char[,] arr = { { '.', '.', '*' },
                                  { '.', '*', '*' } };
    int A = 2, B = 10;
    minCost(arr, A, B);

    }
}

// This code is contributed by patel2127.
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

        // Function to find the minimum cost
        // of flooring with the given tiles
        function minCost(arr, A, B)
        {

            // Store the size of the 2d array
            let n = arr.length;
            let m = arr[0].length;

            // Stores the minimum cost of
            // flooring
            let ans = 0;

            // Traverse the 2d array row-wise
            for (let i = 0; i < n; i++) {
                for (let j = 0; j < m; j++) {

                    // If the current character
                    // is '*', then skip it
                    if (arr[i][j] == '*')
                        continue;

                    // Choose the 1*1 tile if
                    // j is m-1
                    if (j == m - 1)
                        ans += A;

                    // If consecutive '.' are
                    // present, the greedily
                    // choose tile with the
                    // minimum cost
                    else {
                        if (arr[i][j + 1] == '.') {
                            ans += Math.min(2 * A, B);
                            j++;
                        }

                        // Otherwise choose
                        // the 1*1 tile
                        else
                            ans += A;
                    }
                }
            }

            //Print the minimum cost
            document.write(ans);
        }

        // Driver Code
        var arr = [['.', '.', '*'],
        ['.', '*', '*']];
        let A = 2, B = 10;
        minCost(arr, A, B);

  // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*