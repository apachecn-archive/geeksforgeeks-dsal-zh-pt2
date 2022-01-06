# 将 3×3 矩阵转化为幻方的最小成本

> 原文:[https://www . geesforgeks . org/mini-cost-convert-3-x-3-matrix-magic-square/](https://www.geeksforgeeks.org/minimum-cost-convert-3-x-3-matrix-magic-square/)

A [幻方](https://en.wikipedia.org/wiki/Magic_square)是一个从 1 到 n2 的 n×n 不同元素的矩阵，其中任何行、列或对角线的和总是等于同一个数。
考虑一个 3 X 3 矩阵， **s** ，包含范围为[1，9]的整数。我们可以将范围[1，9]内的任意数字 **a** 转换为任意其他数字 **b** ，费用为**| a–b |**。
给定 **s** ，通过改变其零个或多个位数，以最小的代价将其转换为幻方。任务是找到最小成本。

**注意:**生成的矩阵必须包含包含在[1，9]范围内的不同整数。

示例:

```
Input : mat[][] = { { 4, 9, 2 },
                    { 3, 5, 7 },
                    { 8, 1, 5 }};
Output : 1
Given matrix s is not a magic square. To convert
it into magic square we change the bottom right 
value, s[2][2], from 5 to 6 at a cost of | 5 - 6 |
= 1.

Input : mat[][] = { { 4, 8, 2 },
                    { 4, 5, 7 },
                    { 6, 1, 6 }};
Output : 4
```

这个想法是找到所有 3×3 的魔方，并为每个魔方计算将**垫**变成已知魔方的成本。结果是这些成本中最小的。
我们知道 **s** 永远是 3 X 3。3 X 3 矩阵有 8 种可能的幻方。
有两种方法可以解决这个问题:
那么，通过检查整数 1，2，3，…的所有排列来计算所有 8 个幻方..对于每一个，检查它是否形成一个幻方，如果排列是从左上角开始插入的。

下面是这种方法的 C++实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Return if given vector denote the magic square or not.
bool is_magic_square(vector<int> v)
{
    int a[3][3];

    // Convert vector into 3 X 3 matrix
    for (int i = 0; i < 3; ++i)
        for (int j = 0; j < 3; ++j)
            a[i][j] = v[3 * i + j];      

    int s = 0;
    for (int j = 0; j < 3; ++j)
        s += a[0][j];

    // Checking if each row sum is same
    for (int i = 1; i <= 2; ++i) {
        int tmp = 0;
        for (int j = 0; j < 3; ++j)
            tmp += a[i][j];
        if (tmp != s)
            return 0;
    }

    // Checking if each column sum is same
    for (int j = 0; j < 3; ++j) {
        int tmp = 0;
        for (int i = 0; i < 3; ++i)
            tmp += a[i][j];
        if (tmp != s)
            return 0;
    }   

    // Checking if diagonal 1 sum is same
    int tmp = 0;
    for (int i = 0; i < 3; ++i)
        tmp += a[i][i];
    if (tmp != s)
        return 0;   

    // Checking if diagonal 2 sum is same
    tmp = 0;
    for (int i = 0; i < 3; ++i)
        tmp += a[2 - i][i];
    if (tmp != s)
        return 0;
    return 1;
}

// Generating all magic square
void find_magic_squares(vector<vector<int> >& magic_squares)
{
    vector<int> v(9);

    // Initialing the vector
    for (int i = 0; i < 9; ++i)
        v[i] = i + 1;

    // Producing all permutation of vector
    // and checking if it denote the magic square or not.
    do {
        if (is_magic_square(v)) {
            magic_squares.push_back(v);
        }
    } while (next_permutation(v.begin(), v.end()));
}

// Return sum of difference between each element of two vector
int diff(vector<int> a, vector<int> b)
{
    int res = 0;

    for (int i = 0; i < 9; ++i)
        res += abs(a[i] - b[i]);

    return res;
}

// Wrapper function
int wrapper(vector<int> v)
{
    int res = INT_MAX;
    vector<vector<int> > magic_squares;

    // generating all magic square
    find_magic_squares(magic_squares);

    for (int i = 0; i < magic_squares.size(); ++i) {

        // Finding the difference with each magic square
        // and assigning the minimum value.
        res = min(res, diff(v, magic_squares[i]));
    }
    return res;
}

// Driven Program
int main()
{
    // Taking matrix in vector in rowise to make
    // calculation easy
    vector<int> v;
    v.push_back(4);
    v.push_back(9);
    v.push_back(2);

    v.push_back(3);
    v.push_back(5);
    v.push_back(7);

    v.push_back(8);
    v.push_back(1);
    v.push_back(5);

    cout << wrapper(v) << endl;

    return 0;
}
```

输出:

```
1
```

本文由 **Anuj Chauhan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。