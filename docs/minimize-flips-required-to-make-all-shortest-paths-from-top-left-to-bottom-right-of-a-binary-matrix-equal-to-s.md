# 最小化使二进制矩阵从左上角到右下角的所有最短路径等于 S 所需的翻转

> 原文:[https://www . geeksforgeeks . org/minimum-flips-required-to-make-all-最短路径-从二进制矩阵的左上角到右下角-等于-s/](https://www.geeksforgeeks.org/minimize-flips-required-to-make-all-shortest-paths-from-top-left-to-bottom-right-of-a-binary-matrix-equal-to-s/)

给定具有尺寸 **N * M** 的二进制矩阵 **mat[][]** 和长度**N+M–1**的二进制字符串 **S** ，任务是找到使从**左上角单元格**到**右下角单元格**的所有最短路径等于给定字符串 **S** 所需的最小翻转次数。

**示例:**

> **输入:** mat[][] = [[1，0，1，1，1]，[1，1，0]]，S = "10010"
> **输出:** 3
> **解释:**
> 第 1 步:[[1，0，1，1]，[ **1** ，1，1，0]] - > [[1，0，1，1]，[ **0** ，1 0]]
> 步骤 3: [[1，0，0，1]，[0， **1** ，1，0]] - > [[1，0，0，1]，[0， **0** ，1，0]]
> 一旦执行了上述步骤，从左上角到右下角的每个最短路径都等于 S.
> 因此，所需的计数为 3。
> 
> **输入:** mat[][] = [[1，0，0，1，0]]，S = "01101"
> **输出:** 5

**天真方法:**最简单的方法是递归地在给定矩阵的每个单元中生成所有可能的翻转并检查最小翻转的哪个组合生成满足所需条件的矩阵。
***时间复杂度:**O(2<sup>N * M</sup>)*
***辅助空间:** O(N * M)*

**高效方法:**优化上述方法，思路是遍历矩阵，观察如果 **(i，j)** 是给定矩阵的当前索引，那么这个位置将在索引 **(i + j)** 处的最短路径串中，其中，**I∈0，N-1】**和**j∈0，M-1】**。
按照以下步骤解决问题:

1.  将计数器初始化为 **0** 。
2.  遍历矩阵的每个位置 **arr[][]** 。
3.  如果给定矩阵中的当前位置为 **(i，j)** ，则该位置位于**(I+j)**索引处的最短路径串中。
4.  在每个位置，比较 **arr[i][j]** 和 **S[i + j]** 。如果发现相等，继续到下一个位置。否则，将**计数**增加 **1** 。
5.  对整个矩阵执行上述步骤后，打印**计数**的值作为所需的最小翻转。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the minimum
// number of flips required
int minFlips(vector<vector<int> >& mat,
             string s)
{
    // Dimensions of matrix
    int N = mat.size();
    int M = mat[0].size();

    // Stores the count the flips
    int count = 0;

    for (int i = 0; i < N; i++) {

        for (int j = 0; j < M; j++) {

            // Check if element is same
            // or not
            if (mat[i][j]
                != s[i + j] - '0') {
                count++;
            }
        }
    }

    // Return the final count
    return count;
}

// Driver Code
int main()
{
    // Given Matrix
    vector<vector<int> > mat
        = { { 1, 0, 1 },
            { 0, 1, 1 },
            { 0, 0, 0 } };

    // Given path as a string
    string s = "10001";

    // Function Call
    cout << minFlips(mat, s);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to count the minimum
    // number of flips required
    static int minFlips(int mat[][],
                        String s)
    {
        // Dimensions of matrix
        int N = mat.length;
        int M = mat[0].length;

        // Stores the count the flips
        int count = 0;

        for (int i = 0; i < N; i++)
        {
            for (int j = 0; j < M; j++)
            {
                // Check if element is same
                // or not
                if (mat[i][j] !=
                    s.charAt(i + j) - '0')
                {
                    count++;
                }
            }
        }

        // Return the final count
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Matrix
        int mat[][] = {{1, 0, 1},
                       {0, 1, 1}, {0, 0, 0}};

        // Given path as a string
        String s = "10001";

        // Function Call
        System.out.print(minFlips(mat, s));
    }
}

// This code is contributed by Chitranayal
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the minimum
# number of flips required
def minFlips(mat, s):

    # Dimensions of matrix
    N = len(mat)
    M = len(mat[0])

    # Stores the count the flips
    count = 0

    for i in range(N):
        for j in range(M):

            # Check if element is same
            # or not
            if(mat[i][j] != ord(s[i + j]) -
                            ord('0')):
                count += 1

    # Return the final count
    return count

# Driver Code

# Given Matrix
mat = [ [ 1, 0, 1 ],
        [ 0, 1, 1 ],
        [ 0, 0, 0 ] ]

# Given path as a string
s = "10001"

# Function call
print(minFlips(mat, s))

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the minimum
// number of flips required
static int minFlips(int [,]mat,
                    String s)
{

    // Dimensions of matrix
    int N = mat.GetLength(0);
    int M = mat.GetLength(1);

    // Stores the count the flips
    int count = 0;

    for(int i = 0; i < N; i++)
    {
        for(int j = 0; j < M; j++)
        {

            // Check if element is same
            // or not
            if (mat[i, j] !=
                  s[i + j] - '0')
            {
                count++;
            }
        }
    }

    // Return the readonly count
    return count;
}

// Driver Code
public static void Main(String[] args)
{

    // Given Matrix
    int [,]mat = { { 1, 0, 1 },
                   { 0, 1, 1 },
                   { 0, 0, 0 } };

    // Given path as a string
    String s = "10001";

    // Function call
    Console.Write(minFlips(mat, s));
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// javascript program for the
// above approach

    // Function to count the minimum
    // number of flips required
    function minFlips(mat, s)
    {
        // Dimensions of matrix
        let N = mat.length;
        let M = mat[0].length;

        // Stores the count the flips
        let count = 0;

        for (let i = 0; i < N; i++)
        {
            for (let j = 0; j < M; j++)
            {
                // Check if element is same
                // or not
                if (mat[i][j] !=
                    s[(i + j)] - '0')
                {
                    count++;
                }
            }
        }

        // Return the final count
        return count;
    }

// Driver Code

     // Given Matrix
        let mat = [[ 1, 0, 1],
                       [0, 1, 1], [0, 0, 0]];

        // Given path as a string
        let s = "10001";

        // Function Call
        document.write(minFlips(mat, s));

// This code is contributed by trget_2.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(N * M)*