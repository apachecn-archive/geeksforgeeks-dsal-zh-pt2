# 给定矩阵回文所需的最小增量

> 原文:[https://www . geeksforgeeks . org/最小增量-制造给定矩阵所需-回文/](https://www.geeksforgeeks.org/minimum-increments-required-to-make-given-matrix-palindromic/)

给定维度为 **N * M** 的矩阵 M[][]，任务是找到将矩阵转换为回文矩阵所需的矩阵元素增量为 1 的最小数量。

> 回文矩阵是每一行每一列都是[回文](https://www.geeksforgeeks.org/tag/palindrome/)的矩阵。

**示例:**

> **输入:** N = 4，M = 2，arr[][]={{5，3}，{3，5}，{5，3}，{3，5}}
> **输出:** 8
> **解释:**回文矩阵将为 arr[][] = {{5，5}，{5，5}，{5，5}，{5，5}
> 
> **输入:** N = 3，M = 3，arr[][]={{1，2，1}，{3，4，1}，{1，2，1}}
> **输出:** 2
> **解释:**
> 回文矩阵将为 arr[][] = {{1，2，1}，{3，4，3}，{1，2，1}

**方法:**如果 **arr[0][0]** 的值等于 X，那么 **arr[M-1][0]** 、 **arr[0][M-1]** 和 **arr[N-1][M-1]** 的值也必须通过回文属性等于 **X** 。所有元素 **arr[i][j]，arr[N–I–1][j]，arr[N–I–1][M–j–1]，arr[I][M–j–1]**也有类似的性质。因此，这个问题简化为寻找以最小增量从相关的四倍中可以得到的数。按照以下步骤解决问题:

1.  将矩阵分成 4 个象限。[遍历矩阵](https://www.geeksforgeeks.org/traverse-a-given-matrix-using-recursion/)从(0，0)索引到((N + 1) / 2)-1、((M + 1) / 2)-1)(仅在第一象限)。
2.  对于每个索引 **(i，j)** 存储( **i，j)，(N–I–1，j)，(N–I–1，M–j–1)，(I，M–j–1)**集合中的索引，以便集合中只存在唯一的索引。
3.  然后将这些唯一索引中的元素存储在向量**值**中，并计算该向量中的最大值。
4.  现在将最大值与**值**向量的其余元素之差相加，并更新 **ans。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to evaluate minimum number
// of operation required to convert
// the matrix to a palindrome matrix
int palindromeMatrix(int N, int M, vector<vector<int> > arr)
{
    // Variable to store number
    // of operations required
    int ans = 0;

    // Iterate over the first
    // quadrant of the matrix
    for (int i = 0; i < (N + 1) / 2; i++) {

        for (int j = 0; j < (M + 1) / 2; j++) {

            // Store positions of all four
            // values from four quadrants
            set<pair<int, int> > s;
            s.insert({ i, j });
            s.insert({ i, M - j - 1 });
            s.insert({ N - i - 1, j });
            s.insert({ N - i - 1, M - j - 1 });

            // Store the values having
            // unique indexes
            vector<int> values;
            for (pair<int, int> p : s) {

                values.push_back(
                    arr[p.first][p.second]);
            }

            // Largest value in the values vector
            int max = *max_element(
                values.begin(),
                values.end());

            // Evaluate minimum increments
            // required to make all vector
            // elements equal
            for (int k = 0; k < values.size(); k++) {

                ans += max - values[k];
            }
        }
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    int N = 3, M = 3;
    vector<vector<int> > arr
        = { { 1, 2, 1 },
            { 3, 4, 1 },
            { 1, 2, 1 } };

    // Function Call
    palindromeMatrix(N, M, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG{

static class pair
{
  int first, second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Function to evaluate minimum number
// of operation required to convert
// the matrix to a palindrome matrix
static void palindromeMatrix(int N, int M,
                             int[][] arr)
{
  // Variable to store number
  // of operations required
  int ans = 0;

  // Iterate over the first
  // quadrant of the matrix
  for (int i = 0;
           i < (N + 1) / 2; i++)
  {
    for (int j = 0;
             j < (M + 1) / 2; j++)
    {
      // Store positions of all four
      // values from four quadrants
      HashSet<pair> s =
              new HashSet<>();
      s.add(new pair(i, j));
      s.add(new pair(i, M - j - 1));
      s.add(new pair(N - i - 1, j));
      s.add(new pair(N - i - 1,
                     M - j - 1));

      // Store the values having
      // unique indexes
      Vector<Integer> values =
             new Vector<>();
      for (pair p : s)
      {
        values.add(
        arr[p.first][p.second]);
      }

      // Largest value in the
      // values vector
      int max =
          Collections.max(values);

      // Evaluate minimum increments
      // required to make all vector
      // elements equal
      for (int k = 1;
               k < values.size(); k++)
      {
        ans += max - values.get(k);
      }
    }
  }

  // Print the answer
  System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{
  int N = 3, M = 3;
  int[][] arr = {{1, 2, 1},
                 {3, 4, 1},
                 {1, 2, 1}};

  // Function Call
  palindromeMatrix(N, M, arr);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to evaluate minimum number
# of operation required to convert
# the matrix to a palindrome matrix
def palindromeMatrix(N, M, arr):

    # Variable to store number
    # of operations required
    ans = 0

    # Iterate over the first
    # quadrant of the matrix
    for i in range((N + 1) // 2):
        for j in range((M + 1) // 2):

            # Store positions of all four
            # values from four quadrants
            s = {}
            s[(i, j)] = 1
            s[(i, M - j - 1)] = 1
            s[(N - i - 1, j)] = 1
            s[(N - i - 1, M - j - 1)] = 1

            # Store the values having
            # unique indexes
            values = []

            for p, q in s:
                values.append(arr[p][q])

            # Largest value in the values vector
            maxm = max(values)

            # Evaluate minimum increments
            # required to make all vector
            # elements equal
            for k in range(len(values)):
                ans += maxm - values[k]

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    N, M = 3, 3

    arr = [ [ 1, 2, 1 ],
            [ 3, 4, 1 ],
            [ 1, 2, 1 ] ]

    # Function Call
    palindromeMatrix(N, M, arr)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;

class GFG{

public class pair
{
  public int first, second;
  public pair(int first,
              int second) 
  {
    this.first = first;
    this.second = second;
  }   
}

// Function to evaluate minimum number
// of operation required to convert
// the matrix to a palindrome matrix
static void palindromeMatrix(int N, int M,
                             int[,] arr)
{

  // Variable to store number
  // of operations required
  int ans = 0;

  // Iterate over the first
  // quadrant of the matrix
  for(int i = 0;
          i < (N + 1) / 2; i++)
  {
    for(int j = 0;
            j < (M + 1) / 2; j++)
    {

      // Store positions of all four
      // values from four quadrants
      HashSet<pair> s = new HashSet<pair>();
      s.Add(new pair(i, j));
      s.Add(new pair(i, M - j - 1));
      s.Add(new pair(N - i - 1, j));
      s.Add(new pair(N - i - 1,
                     M - j - 1));

      // Store the values having
      // unique indexes
      List<int> values = new List<int>();

      foreach (pair p in s)
      {
        values.Add(arr[p.first, p.second]);
      }

      // Largest value in the
      // values vector
      values.Sort();
      int max = values[values.Count - 1];

      // Evaluate minimum increments
      // required to make all vector
      // elements equal
      for(int k = 1;
              k < values.Count; k++)
      {
        ans += max - values[k];
      }
    }
  }

  // Print the answer
  Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{
  int N = 3, M = 3;
  int[,] arr = { { 1, 2, 1 },
                 { 3, 4, 1 },
                 { 1, 2, 1 } };

  // Function Call
  palindromeMatrix(N, M, arr);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>
// Javascript program for the
// above approach

class pair
{
    constructor(first, second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to evaluate minimum number
// of operation required to convert
// the matrix to a palindrome matrix
function palindromeMatrix(N, M, arr)
{

    // Variable to store number
  // of operations required
  let ans = 0;

  // Iterate over the first
  // quadrant of the matrix
  for (let i = 0;
           i < Math.floor((N + 1) / 2); i++)
  {
    for (let j = 0;
             j < Math.floor((M + 1) / 2); j++)
    {

      // Store positions of all four
      // values from four quadrants
      let s = new Set();
      s.add(new pair(i, j));
      s.add(new pair(i, M - j - 1));
      s.add(new pair(N - i - 1, j));
      s.add(new pair(N - i - 1,
                     M - j - 1));

      // Store the values having
      // unique indexes
      let values = [];
      for (let p of s.values())
      {
        values.push(
        arr[p.first][p.second]);

      }
         values.sort(function(a,b){return a-b;});

      // Largest value in the
      // values vector
      let max =Math.max(...values);

      // Evaluate minimum increments
      // required to make all vector
      // elements equal
      for (let k = 1;
               k < values.length; k++)
      {
        ans += max - values[k];
      }
    }
  }

  // Print the answer
  document.write(ans);
}

// Driver Code
let N = 3, M = 3;
let arr=[[1, 2, 1],
                 [3, 4, 1],
                 [1, 2, 1]];
// Function Call
palindromeMatrix(N, M, arr);

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(1)*