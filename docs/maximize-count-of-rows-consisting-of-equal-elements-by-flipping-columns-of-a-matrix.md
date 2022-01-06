# 通过翻转矩阵的列来最大化由相等元素组成的行数

> 原文:[https://www . geeksforgeeks . org/通过翻转矩阵的列来最大化由相等元素组成的行数/](https://www.geeksforgeeks.org/maximize-count-of-rows-consisting-of-equal-elements-by-flipping-columns-of-a-matrix/)

给定尺寸为 **N * M** 的二元[矩阵](https://www.geeksforgeeks.org/matrix/)、 **mat[][]** ，任务是通过选择矩阵的任意一列并在每次操作中翻转该列的所有元素来最大化仅由相等元素组成的行数。打印可形成相等元素的最大行数。

**示例:**

> **输入:** mat[][] = { { 0，1，0，0，1 }，{ 1，1，0，1，1 }，{ 1，0，1，1，0 } }
> **输出:** 2
> **解释:**
> 选择 2 <sup>nd</sup> 列，翻转该列的所有元素，将 mat[][]修改为{ { 0，0，0，0，1 }，{ 1，0，1，1，1 } 0 } }
> 选择第 5 个<sup>列，翻转该列的所有元素，将 mat[][]修改为{ { 0，0，0，0，0 }，{ 1，0，0，1，0 }，{ 1，1，1，1，1 } }
> 因为矩阵的第 1 个<sup>行和第 3 个<sup>行</sup>的所有元素都是相等的，也是可以包含相等元素的最大行数
> **输入:** mat[][] = { {0，0}，{0，1} }
> **输出:** 1</sup></sup>

**天真方法:**解决这个问题最简单的方法是计算只包含相等元素的行数，这是选择列组合并翻转其元素的每种可能方式。最后，打印上述任意组合获得的最大计数。
***时间复杂度:**O(N * M * 2<sup>M</sup>)*
***辅助空间:** O(N * M)*

**高效方法:**为了优化上述方法，该思想基于这样一个事实，即如果一行是另一行的 **1** 的补码或者两行是相同的，那么只有通过执行给定的操作，这两行才会包含相等的元素。

> **图解:**
> 让我们考虑以下矩阵:
> 
> <figure class="table">
> 
> | **1** | **0** | **1** | **0** | **1** | **1** | **0** | **0** |
> | **0** | **1** | **0** | **1** | **0** | **0** | **1** | **1** |
> | Zero | one | one | one | Zero | Zero | Zero | Zero |
> | **0** | **1** | **0** | **1** | **0** | **0** | **1** | **1** |
> | **1** | **0** | **1** | **0** | **1** | **1** | **0** | **0** |
> 
> 在上面的矩阵中，第 1 行和第 2 行是 1 的补码，第 5<sup>行和第 4<sup>行是 1 的补码。</sup></sup> 
> 
> </figure>

按照以下步骤解决问题:

*   初始化一个变量，比如 **cntMaxRows** ，以存储仅由相等元素组成的最大行数。
*   初始化一个[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **mp** ，来存储矩阵的所有可能的行。
*   [遍历矩阵的每一行](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)并存储在**地图**中。
*   [使用变量**行**遍历矩阵的每一行](https://www.geeksforgeeks.org/row-wise-vs-column-wise-traversal-matrix/)。计算 **1** 对**行**的补码并更新 **cntMaxRows = max(cntMaxRows，mp[row] + mp[1 的 s_comp_row])**

*   最后，打印 **cntMaxRows** 的值。

以下是我们方法的实施情况:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of rows containing all equal elements
int maxEqrows(vector<vector<int> >& mat,
              int N, int M)
{

    // Store each row of the matrix
    map<vector<int>, int> mp;

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++) {

        // Update frequency of
        // current row
        mp[mat[i]]++;
    }

    // Stores maximum count of rows
    // containing all equal elements
    int cntMaxRows = 0;

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++) {

        // Stores 1's complement
        // of the current row
        vector<int> onesCompRow(M, 0);

        // Traverse current row
        // of the given matrix
        for (int j = 0; j < M; j++) {

            // Stores 1s complement of
            // mat[i][j]
            onesCompRow[j]
                = (mat[i][j] ^ 1);
        }

        // Update cntMaxRows
        cntMaxRows = max(cntMaxRows,
                         mp[mat[i]] + mp[onesCompRow]);
    }

    return cntMaxRows;
}

// Driver Code
int main()
{
    vector<vector<int> > mat
        = { { 0, 1, 0, 0, 1 },
            { 1, 1, 0, 1, 1 },
            { 1, 0, 1, 1, 0 } };

    // Stores count of rows
    int N = mat.size();

    // Stores count of columns
    int M = mat[0].size();

    cout << maxEqrows(mat, N, M);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
import java.util.*;
class GFG
{
  // Function to find the maximum number
  // of rows containing all equal elements
  static int maxEqrows(Vector<Vector<Integer>> mat,
                       int N, int M)
  {

    // Store each row of the matrix
    HashMap<Vector<Integer>, Integer> mp = new HashMap<>();

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++)
    {

      // Update frequency of
      // current row
      if(mp.containsKey(mat.get(i)))
      {
        mp.put(mat.get(i), mp.get(mat.get(i)) + 1);
      }
      else
      {
        mp.put(mat.get(i), 1);
      }
    }

    // Stores maximum count of rows
    // containing all equal elements
    int cntMaxRows = 0;

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++)
    {

      // Stores 1's complement
      // of the current row
      Vector<Integer> onesCompRow = new Vector<Integer>();
      for(int j = 0; j < M; j++)
      {
        onesCompRow.add(0);
      }

      // Traverse current row
      // of the given matrix
      for (int j = 0; j < M; j++)
      {

        // Stores 1s complement of
        // mat[i][j]
        onesCompRow.set(j, mat.get(i).get(j) ^ 1);
      }

      // Update cntMaxRows
      if(!mp.containsKey(mat.get(i)))
      {
        cntMaxRows = Math.max(cntMaxRows, mp.get(onesCompRow));
      }
      else if(!mp.containsKey(onesCompRow))
      {
        cntMaxRows = Math.max(cntMaxRows, mp.get(mat.get(i)));
      }
      else
      {
        cntMaxRows = Math.max(cntMaxRows, mp.get(mat.get(i)) +
                              mp.get(onesCompRow));
      }
    }
    return cntMaxRows;
  }

  // Driver code
  public static void main(String[] args)
  {
    Vector<Vector<Integer>> mat = new Vector<Vector<Integer>>();
    mat.add(new Vector<Integer>());
    mat.add(new Vector<Integer>());
    mat.add(new Vector<Integer>());
    mat.get(0).add(0);
    mat.get(0).add(1);
    mat.get(0).add(0);
    mat.get(0).add(0);
    mat.get(0).add(1);       
    mat.get(1).add(1);
    mat.get(1).add(1);
    mat.get(1).add(0);
    mat.get(1).add(1);
    mat.get(1).add(1);
    mat.get(2).add(1);
    mat.get(2).add(0);
    mat.get(2).add(1);
    mat.get(2).add(1);
    mat.get(2).add(0);

    // Stores count of rows
    int N = mat.size();

    // Stores count of columns
    int M = mat.get(0).size();    
    System.out.println(maxEqrows(mat, N, M));
  }
}

// This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic; 
class GFG {

  // Function to find the maximum number
  // of rows containing all equal elements
  static int maxEqrows(List<List<int>> mat, int N, int M)
  {

    // Store each row of the matrix
    Dictionary<List<int>, int> mp = new Dictionary<List<int>, int>();

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++) {

      // Update frequency of
      // current row
      if(mp.ContainsKey(mat[i]))
      {
        mp[mat[i]]++;
      }
      else{
        mp[mat[i]] = 1;
      }
    }

    // Stores maximum count of rows
    // containing all equal elements
    int cntMaxRows = 0;

    // Traverse each row of the matrix
    for (int i = 0; i < N; i++) {

      // Stores 1's complement
      // of the current row
      List<int> onesCompRow = new List<int>();
      for(int j = 0; j < M; j++)
      {
        onesCompRow.Add(0);
      }

      // Traverse current row
      // of the given matrix
      for (int j = 0; j < M; j++) {

        // Stores 1s complement of
        // mat[i][j]
        onesCompRow[j] = (mat[i][j] ^ 1);
      }

      // Update cntMaxRows
      if(!mp.ContainsKey(mat[i]))
      {
        cntMaxRows = Math.Max(cntMaxRows, mp[onesCompRow] + 1);
      }
      else if(!mp.ContainsKey(onesCompRow))
      {
        cntMaxRows = Math.Max(cntMaxRows, mp[mat[i]] + 1);
      }
      else{
        cntMaxRows = Math.Max(cntMaxRows, mp[mat[i]] + mp[onesCompRow] + 1);
      }
    }

    return cntMaxRows;
  }

  // Driver code
  static void Main() {
    List<List<int>> mat = new List<List<int>>();
    mat.Add(new List<int> { 0, 1, 0, 0, 1 });
    mat.Add(new List<int> { 1, 1, 0, 1, 1 });
    mat.Add(new List<int> { 1, 0, 1, 1, 0 });

    // Stores count of rows
    int N = mat.Count;

    // Stores count of columns
    int M = mat[0].Count;

    Console.WriteLine(maxEqrows(mat, N, M));
  }
}

// This code is contributed by divyeshrabadiya07
```

**Output:** 

```
2
```

***时间复杂度:** O(N * M)*
***辅助空间:** O(M)*