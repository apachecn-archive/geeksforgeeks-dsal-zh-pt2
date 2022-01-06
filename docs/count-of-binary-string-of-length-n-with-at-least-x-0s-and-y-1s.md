# 长度为 N 且至少有 X 0 和 Y 1 的二进制字符串的计数

> 原文:[https://www . geesforgeks . org/count-of-binary-string-length-n-with-x-0s-and-y-1s/](https://www.geeksforgeeks.org/count-of-binary-string-of-length-n-with-at-least-x-0s-and-y-1s/)

给定三个数字 **N、X** 和 **Y** ，求长度为 **N** 的唯一二进制字符串的计数，这些字符串至少有**X**T8】0s 和**Y**T12】1s。

**示例**:

> **输入:** N=5，X=1，Y = 2
> T3】输出: 25
> 
> **输入:** N=3，X=1，Y=1
> **输出:** 6
> **说明:**有 3 个长度为 3 的二进制字符串，至少有 1 个 0 和 1 个 1，如:001，010，100，011，101，110

**天真的做法:**生成所有长度为 **N** 的二进制字符串，然后用至少 **X** **0s** 和 **Y** **1s** 来统计字符串的数量。
***时间复杂度:** O(2^N)*
***辅助空间:** O(1)*

**更好的做法:**这个问题也可以用[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)解决。如果长度是 **N** ，给定的是 **X 0s** ，那么就会有 **Y (=N-X) 1s** 。所以我们需要为此找到唯一组合的个数，可以得到为 **(N)C(X)** 或 **(N)C(Y)。**现在对于所有唯一的二进制字符串，我们需要在**【X，N-Y】**范围内找到 **i** 值的 **nCi** 并将其添加到变量中。在所有迭代之后，这个和的值将是所需的计数。

**高效方法:**上述方法可以借助[帕斯卡三角形](https://www.geeksforgeeks.org/pascal-triangle/)进一步优化计算 **nCr** 。按照以下步骤解决问题:

*   [初始化二维数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **p[][]** 使用帕斯卡三角形进行计算。
*   将变量**和**初始化为 **0** 存储答案。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【x，n-y】**，并执行以下任务:
    *   将值 **p[n][i]** 加到变量**和**上。
*   执行上述步骤后，打印**和**的值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

long long int p[31][31];

// Function to use pascal triangle
void pascalTriangle()
{
    p[0][0] = 1;
    p[1][0] = 1;
    p[1][1] = 1;
    for (int i = 2; i < 31; i++) {
        p[i][0] = 1;
        for (int j = 1; j < i; j++)
            p[i][j] = p[i - 1][j]
                      + p[i - 1][j - 1];
        p[i][i] = 1;
    }
}

// Function to count the total number of ways
long long int countWays(int n, int x, int y)
{

    // Store the answer
    long long int sum = 0;

    // Traverse
    for (long long int i = x; i <= n - y; i++) {
        sum += p[n][i];
    }
    return sum;
}

// Driver Code
int main()
{
    pascalTriangle();

    int N = 5, X = 1, Y = 2;
    cout << countWays(N, X, Y) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.io.*;
class GFG {

    static int[][] p = new int[31][31];

    // Function to use pascal triangle
    static void pascalTriangle()
    {
        p[0][0] = 1;
        p[1][0] = 1;
        p[1][1] = 1;
        for (int i = 2; i < 31; i++) {
            p[i][0] = 1;
            for (int j = 1; j < i; j++)
                p[i][j] = p[i - 1][j] + p[i - 1][j - 1];
            p[i][i] = 1;
        }
    }

    // Function to count the total number of ways
    static long countWays(int n, int x, int y)
    {

        // Store the answer
        long sum = 0;

        // Traverse
        for (int i = x; i <= n - y; i++) {
            sum += p[n][i];
        }
        return sum;
    }

    // Driver Code
    public static void main(String[] args)
    {
        pascalTriangle();

        int N = 5;
        int X = 1;
        int Y = 2;

        System.out.println(countWays(N, X, Y));
    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python program for the above approach
p = [[0 for i in range(31)] for i in range(31)]

# Function to use pascal triangle
def pascalTriangle():
    p[0][0] = 1
    p[1][0] = 1
    p[1][1] = 1
    for i in range(2, 31):
        p[i][0] = 1
        for j in range(1, i):
            p[i][j] = p[i - 1][j] + p[i - 1][j - 1]
        p[i][i] = 1

# Function to count the total number of ways
def countWays(n, x, y):

    # Store the answer
    sum = 0

    # Traverse
    for i in range(x, n - y + 1):
        sum += p[n][i]
    return sum

# Driver Code
pascalTriangle()

N = 5
X = 1
Y = 2
print(countWays(N, X, Y))

# This code is contributed by gfgking
```

## C#

```
// C# code for the above approach
using System;

public class GFG {

    static int[,] p = new int[31,31];

    // Function to use pascal triangle
    static void pascalTriangle()
    {
        p[0,0] = 1;
        p[1,0] = 1;
        p[1,1] = 1;
        for (int i = 2; i < 31; i++) {
            p[i,0] = 1;
            for (int j = 1; j < i; j++)
                p[i,j] = p[i - 1,j] + p[i - 1,j - 1];
            p[i,i] = 1;
        }
    }

    // Function to count the total number of ways
    static long countWays(int n, int x, int y)
    {

        // Store the answer
        long sum = 0;

        // Traverse
        for (int i = x; i <= n - y; i++) {
            sum += p[n,i];
        }
        return sum;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        pascalTriangle();

        int N = 5;
        int X = 1;
        int Y = 2;

        Console.WriteLine(countWays(N, X, Y));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    let p = new Array(31).fill(0).map(() => new Array(31).fill(0));

    // Function to use pascal triangle
    const pascalTriangle = () => {
        p[0][0] = 1;
        p[1][0] = 1;
        p[1][1] = 1;
        for (let i = 2; i < 31; i++) {
            p[i][0] = 1;
            for (let j = 1; j < i; j++)
                p[i][j] = p[i - 1][j]
                    + p[i - 1][j - 1];
            p[i][i] = 1;
        }
    }

    // Function to count the total number of ways
    const countWays = (n, x, y) => {

        // Store the answer
        let sum = 0;

        // Traverse
        for (let i = x; i <= n - y; i++) {
            sum += p[n][i];
        }
        return sum;
    }

    // Driver Code

    pascalTriangle();

    let N = 5, X = 1, Y = 2;
    document.write(countWays(N, X, Y));

// This code is contributed by rakeshsahni

</script>
```

**Output**

```
25
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)