# 初始放置在给定 NxM 棋盘左上方的主教可到达的方块数

> 原文:[https://www . geeksforgeeks . org/squares-count-by-bishop-初始放置在给定棋盘的左上角-nxm-棋盘/](https://www.geeksforgeeks.org/count-of-squares-reachable-by-a-bishop-initially-placed-at-top-left-on-a-given-nxm-chessboard/)

给定两个整数 **N** 和 **M** 代表一个 **N x M** 棋盘，任务是找到主教使用任意移动次数可以到达的最大方块数，如果它最初放在棋盘的左上角。

**示例:**

> **输入:** N = 8，M = 8
> **输出:** 32
> **解释:**主教最初站在(1，1)上，这是一个白色或黑色的瓷砖。因此，根据(1，1)图块的颜色，可以使用一系列移动从(1，1)中访问所有黑色或白色图块。
> 
> **输入:** N = 7，M = 3
> T3】输出: 11

**方法:**通过观察 **(1，1)** 的可达瓦片数是与 **(1，1)** 颜色相同的瓦片，可以解决给定的问题。这种瓷砖的数量可以通过公式 **ceil((N*M)/2)** 来计算。上述说法证明错误的情况是 **N = 1** 或 **M = 1** 的情况。在这种情况下，从 **(1，1)** 无法到达任何细胞，因此需要的答案是 **1** 。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// reachable squares by a bishop in an
// N x M chessboard
int maximumSquares(int N, int M)
{
    // If either of N or M is equal to 1
    if (N == 1 || M == 1) {
        return 1;
    }

    // Otherwise the required
    // answer is Ceil(N*M/2)
    // Return Answer
    return (N * M + 1) / 2;
}

// Driver Code
int main()
{
    int N = 7;
    int M = 3;

    cout << maximumSquares(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

// Function to find the maximum number of
// reachable squares by a bishop in an
// N x M chessboard
static int maximumSquares(int N, int M)
{

    // If either of N or M is equal to 1
    if (N == 1 || M == 1) {
        return 1;
    }

    // Otherwise the required
    // answer is Ceil(N*M/2)
    // Return Answer
    return (N * M + 1) / 2;
}

// Driver Code
public static void main (String[] args) {

    int N = 7;
    int M = 3;

    System.out.println(maximumSquares(N, M));
}
}

// This code is contributed by target_2.
```

## 计算机编程语言

```
# Python program of the above approach

# Function to find the maximum number of
# reachable squares by a bishop in an
# N x M chessboard
def maximumSquares(N, M) :

    # If either of N or M is equal to 1
    if (N == 1 or M == 1) :
        return 1

    # Otherwise the required
    # answer is Ceil(N*M/2)
    # Return Answer
    return (N * M + 1) // 2

# Driver Code
if __name__ == "__main__" :
    N = 7
    M = 3

    print(maximumSquares(N, M))

    # This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;

class GFG {

// Function to find the maximum number of
// reachable squares by a bishop in an
// N x M chessboard
static int maximumSquares(int N, int M)
{

    // If either of N or M is equal to 1
    if (N == 1 || M == 1) {
        return 1;
    }

    // Otherwise the required
    // answer is Ceil(N*M/2)
    // Return Answer
    return (N * M + 1) / 2;
}

// Driver Code
public static void Main () {

    int N = 7;
    int M = 3;

    Console.Write(maximumSquares(N, M));
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program of the above approach

// Function to find the maximum number of
// reachable squares by a bishop in an
// N x M chessboard
function maximumSquares(N, M)
{
    // If either of N or M is equal to 1
    if (N == 1 || M == 1) {
        return 1;
    }

    // Otherwise the required
    // answer is Ceil(N*M/2)
    // Return Answer
    return (N * M + 1) / 2;
}

// Driver Code
let N = 7;
let M = 3;

document.write(maximumSquares(N, M));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
11
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)