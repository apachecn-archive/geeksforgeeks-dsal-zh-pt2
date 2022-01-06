# 所需的最小翻转次数，以便可以从任何其他单元格到达矩阵的最后一个单元格

> 原文:[https://www . geeksforgeeks . org/需要最小翻转次数，以便可以从任何其他单元到达矩阵的最后一个单元/](https://www.geeksforgeeks.org/minimum-number-of-flips-required-such-that-the-last-cell-of-matrix-can-be-reached-from-any-other-cell/)

给定尺寸为 **N * M** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **arr[][]** ，其中除了包含**【F】**的单元格**arr【N】【M】**之外，每个单元格都由字符**【R】**或**【D】**组成。**‘R’****‘D’**表示玩家可以从当前单元格分别向右和向下移动。任务是找到从**“R”**翻转到**“D”**或**“D”**到**“R”**所需的最小字符数，以便可以从每个单元格到达完成单元格，即 **arr[N][M]** 。

**示例:**

> **输入:** N = 2，M = 3，arr[][] = {{D，D，R}，{R，R，F}}
> **输出:** 1
> **说明:**将(1，3)的方向改为‘D’后，每个单元格都能到达终点。
> 
> **输入:** N = 1，M = 3，arr[1][3] = {{D，D，F } }
> T3】输出: 2

**方法:**通过观察每个细胞在改变以下细胞后能达到终点，可以解决这个问题:

*   将最后一排的**【D】**全部改为**【R】**。
*   将最后一列的**【R】**全部改为**【D】**。

按照以下步骤解决问题:

1.  初始化一个变量，比如**和**，来存储最小的翻转次数。
2.  从 **i = 0** 遍历到**N–1**并计算包含**【R】**的单元格**arr【I】【M-1】**的数量。
3.  从 **i = 0 到 M–1**遍历并计数包含**【D】**的单元格**arr【N–1】【I】**的数量。
4.  将上述步骤中获得的两个计数的总和打印为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of flips required
int countChanges(vector<vector<char> > mat)
{
    // Dimensions of mat[][]
    int n = mat.size();
    int m = mat[0].size();

    // Initialize answer
    int ans = 0;

    // Count all 'D's in the last row
    for (int j = 0; j < m - 1; j++) {
        if (mat[n - 1][j] != 'R')
            ans++;
    }

    // Count all 'R's in the last column
    for (int i = 0; i < n - 1; i++) {
        if (mat[i][m - 1] != 'D')
            ans++;
    }

    // Print answer
    return ans;
}

// Driver Code
int main()
{
    // Given matrix
    vector<vector<char> > arr = { { 'R', 'R', 'R', 'D' },
                                  { 'D', 'D', 'D', 'R' },
                                  { 'R', 'D', 'R', 'F' } };

    // Function call
    int cnt = countChanges(arr);

    // Print answer
    cout << cnt << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to calculate the minimum
// number of flips required    
public static int countChanges(char mat[][])
{

    // Dimensions of mat[][]
    int n = mat.length;
    int m = mat[0].length;

    // Initialize answer
    int ans = 0;

    // Count all 'D's in the last row
    for(int j = 0; j < m - 1; j++)
    {
        if (mat[n - 1][j] != 'R')
            ans++;
    }

    // Count all 'R's in the last column
    for(int i = 0; i < n - 1; i++)
    {
        if (mat[i][m - 1] != 'D')
            ans++;
    }

    // Print answer
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    char arr[][] = { { 'R', 'R', 'R', 'D' },
                     { 'D', 'D', 'D', 'R' },
                     { 'R', 'D', 'R', 'F' } };

    // Function call
    int cnt = countChanges(arr);

    // Print answer
    System.out.println(cnt);
}
}

// This code is contributed by Manu Pathria
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to calculate the minimum
# number of flips required
def countChanges(mat):

    # Dimensions of mat[][]
    n = len(mat)
    m = len(mat[0])

    # Initialize answer
    ans = 0

    # Count all 'D's in the last row
    for j in range(m - 1):
        if (mat[n - 1][j] != 'R'):
            ans += 1

    # Count all 'R's in the last column
    for i in range(n - 1):
        if (mat[i][m - 1] != 'D'):
            ans += 1

    # Print answer
    return ans

# Driver Code

# Given matrix
arr = [ [ 'R', 'R', 'R', 'D' ] ,
        [ 'D', 'D', 'D', 'R' ],
        [ 'R', 'D', 'R', 'F' ] ]

# Function call
cnt = countChanges(arr)

# Print answer   
print(cnt)

# This code is contributed by susmitakundugoaldanga
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to calculate the minimum
// number of flips required    
public static int countChanges(char [,]mat)
{

    // Dimensions of [,]mat
    int n = mat.GetLength(0);
    int m = mat.GetLength(1);

    // Initialize answer
    int ans = 0;

    // Count all 'D's in the last row
    for(int j = 0; j < m - 1; j++)
    {
        if (mat[n - 1,j] != 'R')
            ans++;
    }

    // Count all 'R's in the last column
    for(int i = 0; i < n - 1; i++)
    {
        if (mat[i,m - 1] != 'D')
            ans++;
    }

    // Print answer
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    char [,]arr = { { 'R', 'R', 'R', 'D' },
                    { 'D', 'D', 'D', 'R' },
                    { 'R', 'D', 'R', 'F' } };

    // Function call
    int cnt = countChanges(arr);

    // Print answer
    Console.WriteLine(cnt);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the minimum
// number of flips required   
function countChanges(mat)
{

    // Dimensions of mat[][]
    let n = mat.length;
    let m = mat[0].length;

    // Initialize answer
    let ans = 0;

    // Count all 'D's in the last row
    for(let j = 0; j < m - 1; j++)
    {
        if (mat[n - 1][j] != 'R')
            ans++;
    }

    // Count all 'R's in the last column
    for(let i = 0; i < n - 1; i++)
    {
        if (mat[i][m - 1] != 'D')
            ans++;
    }

    // Print let answer
    return ans;
}

// Driver code
let arr = [ [ 'R', 'R', 'R', 'D' ],
            [ 'D', 'D', 'D', 'R' ],
            [ 'R', 'D', 'R', 'F' ] ];

// Function call
let cnt = countChanges(arr);

// Print let answer
document.write(cnt);

// This code is contributed by code_hunt

</script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*M)*
***辅助空间** : O(N*M)*