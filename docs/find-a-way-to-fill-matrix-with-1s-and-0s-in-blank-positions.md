# 想办法在空白位置用 1 和 0 填充矩阵

> 原文:[https://www . geesforgeks . org/find-a-way-fill-matrix-with-1s-0s-in-blank-position/](https://www.geeksforgeeks.org/find-a-way-to-fill-matrix-with-1s-and-0s-in-blank-positions/)

给定一个 **N * M** 矩阵**mat【】【】**由两种类型的字符**' '组成****' _ '**。任务是在矩阵包含**的位置填充矩阵。**用 **1** 和 **0** 填充矩阵，使相邻的两个单元格不包含相同的数字，并打印修改后的矩阵。
**举例:**

> **输入:** mat[][] = {{ ' . ', '_'}, {'_', '.'}}
> **输出:**
> 1 _
> _ 1
> **输入:** mat[][] = {{'_ '，' _'}，{'_ '，' _ ' }
> **输出:**
> _ _
> _ _
> 无处填写数字。

**方法:**一种有效的方法是按照以下模式填充矩阵:

> 10101010…
> 01010101…
> 10101010…

遇到时跳过“_”字符。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define N 2
#define M 2

// Function to generate and
// print the required matrix
void Matrix(char a[N][M])
{
    char ch = '1';

    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            // Replace the '.'
            if (a[i][j] == '.')
                a[i][j] = ch;

            // Toggle number
            ch = (ch == '1') ? '0' : '1';

            cout << a[i][j] << " ";
        }
        cout << endl;

        // For each row, change
        // the starting number
        if (i % 2 == 0)
            ch = '0';
        else
            ch = '1';
    }
}

// Driver code
int main()
{
    char a[N][M] = { { '.', '_' },
                     { '_', '.' } };

    Matrix(a);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

static int N = 2;
static int M = 2;

// Function to generate and
// print the required matrix
static void Matrix(char a[][])
{
    char ch = '1';

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            // Replace the '.'
            if (a[i][j] == '.')
                a[i][j] = ch;

            // Toggle number
            ch = (ch == '1') ? '0' : '1';

            System.out.print( a[i][j] + " ");
        }
        System.out.println();

        // For each row, change
        // the starting number
        if (i % 2 == 0)
            ch = '0';
        else
            ch = '1';
    }
}

    // Driver code
    public static void main (String[] args)
    {
        char a[][] = { { '.', '_' },
                    { '_', '.' } };

        Matrix(a);
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

N = 2
M = 2

# Function to generate and
# print the required matrix
def Matrix(a) :
    ch = '1';

    for i in range(N) :
        for j in range(M) :

            # Replace the '.'
            if (a[i][j] == '.') :
                a[i][j] = ch;

            # Toggle number
            if (ch == '1') :
                ch == '0'
            else :
                ch = '1'

            print(a[i][j],end = " ");

        print()

        # For each row, change
        # the starting number
        if (i % 2 == 0) :
            ch = '0';
        else :
            ch = '1';

# Driver code
if __name__ == "__main__" :

    a = [
            [ '.', '_' ],
            [ '_', '.' ],
        ]

    Matrix(a);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

static int N = 2;
static int M = 2;

// Function to generate and
// print the required matrix
static void Matrix(char [,]a)
{
    char ch = '1';

    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {

            // Replace the '.'
            if (a[i,j] == '.')
                a[i,j] = ch;

            // Toggle number
            ch = (ch == '1') ? '0' : '1';

            Console.Write( a[i,j] + " ");
        }
        Console.WriteLine();

        // For each row, change
        // the starting number
        if (i % 2 == 0)
            ch = '0';
        else
            ch = '1';
    }
}

// Driver code
public static void Main (String[] args)
{
    char [,]a = { { '.', '_' },
                { '_', '.' } };

    Matrix(a);
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

const N = 2;
const M = 2;

// Function to generate and
// print the required matrix
function Matrix(a)
{
    let ch = '1';

    for (let i = 0; i < N; i++) {
        for (let j = 0; j < M; j++) {

            // Replace the '.'
            if (a[i][j] == '.')
                a[i][j] = ch;

            // Toggle number
            ch = (ch == '1') ? '0' : '1';

            document.write(a[i][j] + " ");
        }
        document.write("<br>");

        // For each row, change
        // the starting number
        if (i % 2 == 0)
            ch = '0';
        else
            ch = '1';
    }
}

// Driver code
    let a = [ [ '.', '_' ],
                     [ '_', '.' ] ];

    Matrix(a);

</script>
```

**Output:** 

```
1 _ 
_ 1
```