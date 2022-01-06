# 计算在棋盘中放置 L 形移动骑士的方式

> 原文:[https://www . geesforgeks . org/count-way-to-place-knights-移动中的 l 形棋盘/](https://www.geeksforgeeks.org/count-ways-to-place-knights-moving-in-l-shape-in-chessboard/)

给定两个整数， **N** 和 **M** ，表示棋盘的尺寸。任务是计算在 N * M 棋盘上放置一个*黑骑士和一个白骑士*的方法，这样他们就不会互相攻击了？骑士们必须被安置在不同的广场上。骑士可以水平移动两个方块，垂直移动一个方块(L 形)，或者垂直移动两个方块，水平移动一个方块(L 形)。如果一个人能一步到位，骑士们就会互相攻击。

**示例:**

```
Input: N=2, M=2
Output: 12
Explanation: 
We can place a black and a white knight in 12 possible 
ways such that none of them attracts each other.

Input: N=2, M=3
Output: 26
```

**天真方法:**

*   天真的方法是为每个细胞计数的方式骑士可以放置，这样两者都可以互相攻击，然后从总排列中减去计数。
*   总排列可以计算为:

```
Total arrangements = M * N * (M * N - 1)
```

*   因为对于每个单元，我们可以在(M * N–1)个单元中放置其他骑士，并且总的 M * N 个单元将在那里。

## C++

```
// C++ program to count arrangements
// of two knight so that they do not
// attack each other.
#include <iostream>
using namespace std;

// Function returns the count
// of arrangements
long long Solve(int n, int m)
{
    int X_axis[]{ -2, -1, 1, 2};
    int Y_axis[]{ 1, 2, 2, 1 };

    long long ret = 0;

    for (int i = 0; i < m; ++i)
    {
        for (int j = 0; j < n; ++j)
        {
            for (int k = 0; k < 4; ++k)
            {
                int x = i + X_axis[k],
                    y = j + Y_axis[k];

                if (x >= 0 && x < m
                    && y >= 0 && y < n)
                    ++ret;
            }
        }
    }

    long long Total = m * n;
    Total = Total * (Total - 1) / 2;

    return 2 * (Total - ret);
}
// Driver code
int main()
{

    int N = 2, M = 3;

    cout << Solve(N, M) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count arrangements
// of two knight so that they do not
// attack each other.
import java.io.*;
import java.util.*;

class GFG {

// Function returns the count
// of arrangements
static long Solve(int n, int m)
{
    int X_axis[] = { -2, -1, 1, 2};
    int Y_axis[] = { 1, 2, 2, 1 };

    long ret = 0;

    for(int i = 0; i < m; ++i)
    {
       for(int j = 0; j < n; ++j)
       {
          for(int k = 0; k < 4; ++k)
          {
             int x = i + X_axis[k];
             int y = j + Y_axis[k];

             if (x >= 0 && x < m &&
                 y >= 0 && y < n)
                 ++ret;
          }
       }
    }

    long Total = m * n;
    Total = Total * (Total - 1) / 2;
    return 2 * (Total - ret);
}

// Driver code
public static void main(String[] args)
{
    int N = 2, M = 3;
    System.out.println(Solve(N, M));
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to count arrangements
# of two knight so that they do not
# attack each other

# Function returns the count
# of arrangements
def Solve(n, m):

    X_axis = []
    X_axis = [ -2, -1, 1, 2 ]
    Y_axis = []
    Y_axis = [ 1, 2, 2, 1 ]

    ret = 0

    for i in range(m):
        for j in range(n):
            for k in range(4):

                x = i + X_axis[k]
                y = j + Y_axis[k]

                if (x >= 0 and x < m and
                    y >= 0 and y < n):
                    ret += 1

    Total = m * n
    Total = Total * (Total - 1) // 2

    return 2 * (Total - ret)

# Driver code
N = 2
M = 3

print(Solve(N, M))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program to count arrangements
// of two knight so that they do not
// attack each other.
using System;
class GFG{

// Function returns the count
// of arrangements
static long Solve(int n, int m)
{
    int []X_axis = { -2, -1, 1, 2};
    int []Y_axis = { 1, 2, 2, 1 };

    long ret = 0;

    for(int i = 0; i < m; ++i)
    {
        for(int j = 0; j < n; ++j)
        {
            for(int k = 0; k < 4; ++k)
            {
                int x = i + X_axis[k];
                int y = j + Y_axis[k];

                if (x >= 0 && x < m &&
                    y >= 0 && y < n)
                    ++ret;
            }
        }
    }

    long Total = m * n;
    Total = Total * (Total - 1) / 2;
    return 2 * (Total - ret);
}

// Driver code
public static void Main(String[] args)
{
    int N = 2, M = 3;
    Console.Write(Solve(N, M));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

    // Javascript program to count arrangements
    // of two knight so that they do not
    // attack each other.

    // Function returns the count
    // of arrangements
    function Solve(n, m)
    {
        let X_axis = [ -2, -1, 1, 2];
        let Y_axis = [ 1, 2, 2, 1 ];

        let ret = 0;

        for (let i = 0; i < m; ++i)
        {
            for (let j = 0; j < n; ++j)
            {
                for (let k = 0; k < 4; ++k)
                {
                    let x = i + X_axis[k],
                        y = j + Y_axis[k];

                    if (x >= 0 && x < m
                        && y >= 0 && y < n)
                        ++ret;
                }
            }
        }

        let Total = m * n;
        Total = Total * (Total - 1) / 2;

        return 2 * (Total - ret);
    }

    let N = 2, M = 3;

    document.write(Solve(N, M));

</script>
```

**Output:** 

```
26
```