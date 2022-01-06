# 在一个周围有最多星星的矩阵中找到字母表

> 原文:[https://www . geeksforgeeks . org/find-矩阵中的字母-它周围的星星数最多/](https://www.geeksforgeeks.org/find-alphabet-in-a-matrix-which-has-maximum-number-of-stars-around-it/)

给定一个由 ***** 和小写英文字母组成的矩阵 **mat** ，任务是找到其周围有最大数量 ***** 的字符(也包括对角线元素)。如果两个字符具有相同的最大计数，则按字典顺序打印最小字符。
**来源:**[D-E 肖面试经验](https://www.geeksforgeeks.org/de-shaw-interview-experience-set-23-full-time/)
**举例:**

```
Input: 
mat[][] = {{'b', '*', '*', '*'}, 
           {'*', '*', 'c', '*'}, 
           {'*', 'a', '*', '*'}, 
           {'*', '*', '*', 'd'}}
Output: a
'a', 'b', 'c' and 'd' are surrounded by 
'7', '3', '7' and '3' stars respectively.
'a' and 'c' are surrounded by maximum stars 
but 'a' is lexicographically smaller than 'c'.

Input: 
mat[][] = {{'*', 'r', '*', '*'}, 
           {'m', 'a', 'z', '*'}, 
           {'l', '*', 'f', 'k'}, 
           {'*', '*', '*', 'd'} }
Output: f
```

**方法:**想法是遍历矩阵，如果找到一个字符，那么计算它周围的星星数。检查它周围的所有 8 个位置，并计算开始的次数。
使用[地图](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/)来记录人物及其周围的星星数量。然后遍历地图，找到被最大星星包围的、字典上最小的字符。
以下是上述方法的实施:

## C++

```
// C++ program to find alphabet in a Matrix
// which has maximum number of stars
// surrounding it
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of stars
// around a particular index
int countStars(int mat[][4], int i, int j, int n)
{
    int count = 0;

    int rowNum[] = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int colNum[] = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // consider all 8 neighbours
    for (int k = 0; k < 8; k++) {
        int x = i + rowNum[k];
        int y = j + colNum[k];
        if (x >= 0 && x < n && y >= 0 && y < n
            && mat[x][y] == '*')
            count++;
    }

    return count;
}

// Function to return the character in a Matrix
// which has maximum number of stars around it
char alphabetWithMaxStars(int mat[][4], int n)
{
    unordered_map<char, int> umap;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {

            // If current element is a character
            if ((mat[i][j] - 97) >= 0
                && (mat[i][j] - 97) < 26) {
                // Count of start surrounding it
                int stars = countStars(mat, i, j, n);
                umap[mat[i][j]] = stars;
            }
        }
    }

    int max = -1;
    char result = 'z' + 1;

    // Traverse the map
    for (auto x : umap) {
        if (x.second > max || (x.second == max
                               && x.first < result)) {
            max = x.second;
            result = x.first;
        }
    }

    return result;
}

// Driver code
int main()
{
    int mat[][4] = { { 'b', '*', '*', '*' },
                     { '*', '*', 'c', '*' },
                     { '*', 'a', '*', '*' },
                     { '*', '*', '*', 'd' } };

    int n = 4;

    cout << alphabetWithMaxStars(mat, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find alphabet in a Matrix
// which has maximum number of stars
// surrounding it
import java.util.*;

class GFG
{

// Function to return the count of stars
// around a particular index
static int countStars(int mat[][], int i, int j, int n)
{
    int count = 0;

    int rowNum[] = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int colNum[] = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // consider all 8 neighbours
    for (int k = 0; k < 8; k++)
    {
        int x = i + rowNum[k];
        int y = j + colNum[k];
        if (x >= 0 && x < n && y >= 0 && y < n
            && mat[x][y] == '*')
            count++;
    }

    return count;
}

// Function to return the character in a Matrix
// which has maximum number of stars around it
static char alphabetWithMaxStars(int mat[][], int n)
{
    HashMap<Character,Integer> umap =
        new HashMap<Character,Integer>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // If current element is a character
            if ((mat[i][j] - 97) >= 0
                && (mat[i][j] - 97) < 26)
            {

                // Count of start surrounding it
                int stars = countStars(mat, i, j, n);
                umap.put((char)mat[i][j], stars);
            }
        }
    }

    int max = -1;
    char result = 'z' + 1;

    // Traverse the map
    for (Map.Entry<Character,Integer> x : umap.entrySet())
    {
        if (x.getValue() > max || (x.getValue() == max
            && x.getKey() < result))
        {
            max = x.getValue();
            result = x.getKey();
        }
    }

    return result;
}

// Driver code
public static void main(String[] args)
{
    int mat[][] = { { 'b', '*', '*', '*' },
                    { '*', '*', 'c', '*' },
                    { '*', 'a', '*', '*' },
                    { '*', '*', '*', 'd' } };

    int n = 4;

    System.out.print(alphabetWithMaxStars(mat, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find alphabet in a
# Matrix which has maximum number of stars
# surrounding it
import math as mt

# Function to return the count of stars
# around a particular index
def countStars(mat, i, j, n):

    count = 0

    rowNum = [-1, -1, -1, 0, 0, 1, 1, 1 ]
    colNum = [-1, 0, 1, -1, 1, -1, 0, 1 ]

    # consider all 8 neighbours
    for k in range(8):
        x = i + rowNum[k]
        y = j + colNum[k]
        if (x >= 0 and x < n and y >= 0 and
            y < n and mat[x][y] == '*'):
            count += 1

    return count

# Function to return the character in a Matrix
# which has maximum number of stars around it
def alphabetWithMaxStars(mat, n):

    umap = dict()

    for i in range(n):
        for j in range(n):

            # If current element is a character
            if ((ord(mat[i][j]) - 97) >= 0 and
                (ord(mat[i][j]) - 97) < 26):
                # Count of start surrounding it
                stars = countStars(mat, i, j, n)
                umap[mat[i][j]] = stars

    Max = -1
    result = chr(ord('z') + 1)

    # Traverse the map
    for x in umap:
        if (umap[x] > Max or
           (umap[x] == Max and x < result)):
            Max = umap[x]
            result = x

    return result

# Driver code
mat = [[ 'b', '*', '*', '*' ],
       [ '*', '*', 'c', '*' ],
       [ '*', 'a', '*', '*' ],
       [ '*', '*', '*', 'd' ]]

n = 4

print(alphabetWithMaxStars(mat, n))

# This code is contributed by
# Mohit kumar 29
```

## C#

```
// C# program to find alphabet in a Matrix
// which has maximum number of stars
// surrounding it
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the count of stars
// around a particular index
static int countStars(int [,]mat, int i, int j, int n)
{
    int count = 0;

    int []rowNum = { -1, -1, -1, 0, 0, 1, 1, 1 };
    int []colNum = { -1, 0, 1, -1, 1, -1, 0, 1 };

    // consider all 8 neighbours
    for (int k = 0; k < 8; k++)
    {
        int x = i + rowNum[k];
        int y = j + colNum[k];
        if (x >= 0 && x < n && y >= 0 && y < n
            && mat[x, y] == '*')
            count++;
    }

    return count;
}

// Function to return the character in a Matrix
// which has maximum number of stars around it
static char alphabetWithMaxStars(int [,]mat, int n)
{
    Dictionary<char,int> umap =
        new Dictionary<char,int>();

    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {

            // If current element is a character
            if ((mat[i, j] - 97) >= 0
                && (mat[i, j] - 97) < 26)
            {

                // Count of start surrounding it
                int stars = countStars(mat, i, j, n);
                if(umap.ContainsKey((char)mat[i,j]))
                    umap[(char)mat[i,j]] = stars;
                else
                    umap.Add((char)mat[i,j], stars);
            }
        }
    }

    int max = -1;
    char result = (char)('z' + 1);

    // Traverse the map
    foreach(KeyValuePair<char, int> x in umap)
    {
        if (x.Value > max || (x.Value == max
            && x.Key < result))
        {
            max = x.Value;
            result = x.Key;
        }
    }

    return result;
}

// Driver code
public static void Main(String[] args)
{
    int [,]mat = { { 'b', '*', '*', '*' },
                    { '*', '*', 'c', '*' },
                    { '*', 'a', '*', '*' },
                    { '*', '*', '*', 'd' } };

    int n = 4;

    Console.Write(alphabetWithMaxStars(mat, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find alphabet in a Matrix
// which has maximum number of stars
// surrounding it

// Function to return the count of stars
// around a particular index
function countStars(mat,i,j,n)
{
    let count = 0;

    let rowNum = [-1, -1, -1, 0, 0, 1, 1, 1];
    let colNum = [-1, 0, 1, -1, 1, -1, 0, 1];

    // consider all 8 neighbours
    for (let k = 0; k < 8; k++)
    {
        let x = i + rowNum[k];
        let y = j + colNum[k];
        if (x >= 0 && x < n && y >= 0 && y < n
            && mat[x][y] == '*')
            count++;
    }

    return count;
}

// Function to return the character in a Matrix
// which has maximum number of stars around it
function alphabetWithMaxStars(mat,n)
{
    let umap = new Map();

    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
        {

            // If current element is a character
            if ((mat[i][j].charCodeAt(0) - 97) >= 0
                && (mat[i][j].charCodeAt(0) - 97) < 26)
            {

                // Count of start surrounding it
                let stars = countStars(mat, i, j, n);
                umap.set((mat[i][j]), stars);
            }
        }
    }

    let max = -1;
    let result = String.fromCharCode('z'.charCodeAt(0) + 1);

    // Traverse the map
    for (let [key, value] of umap.entries())
    {
        if (value > max || (value == max
            && key < result))
        {
            max = value;
            result = key;
        }
    }

    return result;
}

// Driver code
let mat = [[ 'b', '*', '*', '*' ],
       [ '*', '*', 'c', '*' ],
       [ '*', 'a', '*', '*' ],
       [ '*', '*', '*', 'd' ]];

let n = 4;
document.write(alphabetWithMaxStars(mat, n));

// This code is contributed by unknown2108.
</script>
```

**Output:** 

```
a
```