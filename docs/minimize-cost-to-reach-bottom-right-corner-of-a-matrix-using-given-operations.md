# 使用给定的操作最小化到达矩阵右下角的成本

> 原文:[https://www . geeksforgeeks . org/使用给定操作最小化到达矩阵右下角的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reach-bottom-right-corner-of-a-matrix-using-given-operations/)

给定一个大小为 **N x N** 的[矩阵](https://www.geeksforgeeks.org/matrix/) **网格【】【】【】**，任务是找到从左上角到达矩阵右下角所需的最小成本，其中移动到新单元格的成本为**【S/2】+K**，其中 **S** 是上一个索引处的分数， **K** 是当前索引处的矩阵元素。
***注:**此处，【X】为不超过 **X** 的最大整数。*

**示例:**

> ***输入:**格[][]= {*0、3、9、6}、{1、4、4、5}、{8、2、5、4}、{1、8、5、9}}
> ***输出:*** 12
> ***解释:*** 可能的一组招式如下 0->1->4->4-
> 
> ***输入:** g* rid[][] = {{0，82，2，6，7}，{4，3，1，5，21}，{6，4，20，2，8}，{6，6，64，1，8}，{1，65，1，6，4}}
> ***输出:*** 7

**方法:**按照以下步骤解决问题:

*   使矩阵的第一个元素为零 ***。**T3】*
*   在**【0，N-1】**范围内遍历:
    *   初始化一个列表，说出**移动列表**，追加移动 **i** 和 **j** 。
    *   初始化另一个列表，说**可能的日子，**并在其中追加**移动列表**。
    *   初始化一个列表，说**可能是一个问题，**最初是一个空列表。
    *   遍历列表**可能的方式**:
        *   遍历附加的**移动列表**:
            *   检查移动是否等于 **i，**然后更新 **i = i + 1。**
            *   否则，更新 **j = j + 1** 。
            *   初始化变量，表示 **tempSum。**集**tempsum = tempsum+grid[I][j]**。
        *   在循环后的**可能的路线**列表中添加**时间总和**。
*   打印从**开始的最小成本可能值**作为输出。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

vector<vector<char> > possibleWays;

// Returns true if str[curr] does not matches with any
// of the characters after str[start]
bool shouldSwap(char str[], int start, int curr)
{
  for (int i = start; i < curr; i++) {
    if (str[i] == str[curr]) {
      return false;
    }
  }
  return true;
}

// Function for the swap
void swap(char str[], int i, int j)
{
  char c = str[i];
  str[i] = str[j];
  str[j] = c;
}

// Prints all distinct permutations in str[0..n-1]
void findPermutations(char str[], int index, int n)
{
  if (index >= n) {
    vector<char> l;
    for (int i = 0; i < n; i++)
      l.push_back(str[i]);
    possibleWays.push_back(l);
    return;
  }

  for (int i = index; i < n; i++) {

    // Proceed further for str[i] only if it
    // doesn't match with any of the characters
    // after str[index]
    bool check = shouldSwap(str, index, i);
    if (check) {
      swap(str, index, i);
      findPermutations(str, index + 1, n);
      swap(str, index, i);
    }
  }
}

// Function to print the minimum cost
void minCost(int grid[][5], int N)
{

  vector<char> moveList;

  // Making top-left value 0
  // implicitly to generate list of moves
  grid[0][0] = 0;
  vector<int> possibleWaysSum;

  for (int k = 0; k < N - 1; k++) {

    moveList.push_back('i');
    moveList.push_back('j');

    possibleWays.clear();

    // Convert into set to make only unique values
    int n = moveList.size();
    char str[n];
    for (int i = 0; i < n; i++)
      str[i] = moveList[i];

    // To store the unique permutation of moveLst
    // into the possibleWays
    findPermutations(str, 0, n);
    possibleWaysSum.clear();

    // Traverse the list
    for (vector<char> way : possibleWays) {
      int i = 0, j = 0, tempSum = 0;
      for (char move : way) {
        if (move == 'i') {
          i += 1;
        }
        else {
          j += 1;
        }

        // Stores cost according to given
        // conditions
        tempSum = (int)(floor(tempSum / 2))
          + grid[i][j];
      }
      possibleWaysSum.push_back(tempSum);
    }
  }

  // Print the minimum possible cost
  int ans = possibleWaysSum[0];
  for (int i = 1; i < possibleWaysSum.size(); i++)
    ans = min(ans, possibleWaysSum[i]);

  cout << ans;
}

// Driven Program
int main()
{

  // Size of the grid
  int N = 4;

  // Given grid[][]
  int grid[][5] = { { 0, 3, 9, 6 },
                   { 1, 4, 4, 5 },
                   { 8, 2, 5, 4 },
                   { 1, 8, 5, 9 } };

  // Function call to print the minimum
  // cost to reach bottom-right corner
  // from the top-left corner of the matrix
  minCost(grid, N);

  return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{
    static ArrayList<ArrayList<Character> > possibleWays;

    // Returns true if str[curr] does not matches with any
    // of the characters after str[start]
    static boolean shouldSwap(char str[], int start,
                              int curr)
    {
        for (int i = start; i < curr; i++)
        {
            if (str[i] == str[curr])
            {
                return false;
            }
        }
        return true;
    }

    // Prints all distinct permutations in str[0..n-1]
    static void findPermutations(char str[], int index,
                                 int n)
    {
        if (index >= n)
        {
            ArrayList<Character> l = new ArrayList<>();
            for (char ch : str)
                l.add(ch);
            possibleWays.add(l);
            return;
        }

        for (int i = index; i < n; i++) {

            // Proceed further for str[i] only if it
            // doesn't match with any of the characters
            // after str[index]
            boolean check = shouldSwap(str, index, i);
            if (check) {
                swap(str, index, i);
                findPermutations(str, index + 1, n);
                swap(str, index, i);
            }
        }
    }

    // Function for the swap
    static void swap(char[] str, int i, int j)
    {
        char c = str[i];
        str[i] = str[j];
        str[j] = c;
    }

    // Function to print the minimum cost
    static void minCost(int grid[][], int N)
    {

        ArrayList<Character> moveList = new ArrayList<>();

        // Making top-left value 0
        // implicitly to generate list of moves
        grid[0][0] = 0;
        ArrayList<Integer> possibleWaysSum
            = new ArrayList<>();

        for (int k = 0; k < N - 1; k++) {

            moveList.add('i');
            moveList.add('j');

            possibleWays = new ArrayList<>();

            // Convert into set to make only unique values
            int n = moveList.size();
            char str[] = new char[n];
            for (int i = 0; i < n; i++)
                str[i] = moveList.get(i);

            // To store the unique permutation of moveLst
            // into the possibleWays
            findPermutations(str, 0, n);
            possibleWaysSum = new ArrayList<>();

            // Traverse the list
            for (ArrayList<Character> way : possibleWays) {
                int i = 0, j = 0, tempSum = 0;
                for (char move : way) {
                    if (move == 'i') {
                        i += 1;
                    }
                    else {
                        j += 1;
                    }

                    // Stores cost according to given
                    // conditions
                    tempSum = (int)(Math.floor(tempSum / 2))
                              + grid[i][j];
                }
                possibleWaysSum.add(tempSum);
            }
        }

        // Print the minimum possible cost
        int ans = possibleWaysSum.get(0);
        for (int i = 1; i < possibleWaysSum.size(); i++)
            ans = Math.min(ans, possibleWaysSum.get(i));

        System.out.println(ans);
    }

    // Driver code
    public static void main(String[] args)
    {

        // Size of the grid
        int N = 4;

        // Given grid[][]
        int grid[][] = { { 0, 3, 9, 6 },
                         { 1, 4, 4, 5 },
                         { 8, 2, 5, 4 },
                         { 1, 8, 5, 9 } };

        // Function call to print the minimum
        // cost to reach bottom-right corner
        // from the top-left corner of the matrix
        minCost(grid, N);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

from itertools import permutations
from math import floor

# Function to print the minimum cost

def minCost(grid, N):
    moveList = []

    # Making top-left value 0
    # implicitly to generate list of moves
    grid[0][0] = 0

    for i in range(N - 1):
        moveList.append('i')
        moveList.append('j')

        # Convert into set to make only unique values
        possibleWays = list(set(permutations(moveList)))
        possibleWaysSum = []

        # Traverse the list
        for way in possibleWays:
            i, j, tempSum = 0, 0, 0
            for move in way:
                if move == 'i':
                    i += 1
                else:
                    j += 1

                # Stores cost according to given conditions
                tempSum = floor(tempSum/2) + grid[i][j]

            possibleWaysSum.append(tempSum)
        minWayIndex = possibleWaysSum.index(min(possibleWaysSum))

    # Print the minimum possible ccost
    print(min(possibleWaysSum))

# Size of the grid
N = 4

# Given grid[][]
grid = [[0, 3, 9, 6], [1, 4, 4, 5], [8, 2, 5, 4], [1, 8, 5, 9]]

# Function call to print the minimum
# cost to reach bottom-right corner
# from the top-left corner of the matrix
minCost(grid, N)
```

**Output:** 

```
12
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*