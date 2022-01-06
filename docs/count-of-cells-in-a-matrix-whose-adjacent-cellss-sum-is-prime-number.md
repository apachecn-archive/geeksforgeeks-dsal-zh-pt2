# 相邻细胞之和为素数的矩阵中细胞的计数

> 原文:[https://www . geeksforgeeks . org/矩阵中相邻单元的个数是素数/](https://www.geeksforgeeks.org/count-of-cells-in-a-matrix-whose-adjacent-cellss-sum-is-prime-number/)

给定一个 **M x N** 矩阵 **mat[][]** ，任务是计算其相邻单元之和等于一个**素数**的单元数。对于单元格 **x[i][j]** ，只有 **x[i+1][j]、x[i-1][j]、x[i][j+1]** 和 **x[i][j-1]** 是相邻单元格。
**示例:**

> **输入:** mat[][] = {{1，3}，{2，5}}
> **输出:** 2
> **说明:**只有细胞 mat[0][0]和 mat[1][1]满足条件。
> 即 mat[0][0]:(3+2) = 5，mat[1][1]: (3+2) = 5
> **输入:** mat[][] = {{1，2，3，4}，{5，6，7，8}，{9，10，11，12}}
> **输出:** 6
> **解释:**细胞 mat[0][0]，mat[0]

**先决条件:**T2【厄拉多塞之筛】T4**进场:**

*   使用筛预计算并存储质数。
*   迭代整个矩阵，对于每个单元格，求所有相邻单元格的和。
*   如果相邻单元格的总和等于一个素数，则递增计数。
*   返回计数的值。

下面是上述方法的实现。

## C++

```
// CPP program to find the cells whose
// adjacent cells's sum is prime Number
#include <bits/stdc++.h>
using namespace std;
#define MAX 100005

bool prime[MAX];

void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..MAX-1]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    memset(prime, true, sizeof(prime));

    prime[0] = prime[1] = false;

    for (int p = 2; p * p < MAX; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to count the cells having
// adjacent cell's sum
// is equal to prime
int PrimeSumCells(vector<vector<int> >& mat)
{
    int count = 0;

    int N = mat.size();
    int M = mat[0].size();

    // Traverse for all the cells
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {

            int sum = 0;

            // i-1, j
            if (i - 1 >= 0)
                sum += mat[i - 1][j];

            // i+1, j
            if (i + 1 < N)
                sum += mat[i + 1][j];

            // i, j-1
            if (j - 1 >= 0)
                sum += mat[i][j - 1];

            // i, j+1
            if (j + 1 < M)
                sum += mat[i][j + 1];

            // If the sum is a prime number
            if (prime[sum])
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver Program
int main()
{
    SieveOfEratosthenes();

    vector<vector<int> > mat = { { 1, 2, 3, 4 },
                                 { 5, 6, 7, 8 },
                                 { 9, 10, 11, 12 } };

    // Function call
    cout << PrimeSumCells(mat) << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the cells whose
// adjacent cells's sum is prime Number
class GFG{
static final int MAX = 100005;

static boolean []prime = new boolean[MAX];

static void SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..MAX-1]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    for (int i = 0; i < prime.length; i++)
    prime[i] = true;

    prime[0] = prime[1] = false;

    for (int p = 2; p * p < MAX; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to count the cells having
// adjacent cell's sum
// is equal to prime
static int PrimeSumCells(int [][]mat)
{
    int count = 0;

    int N = mat.length;
    int M = mat[0].length;

    // Traverse for all the cells
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            int sum = 0;

            // i-1, j
            if (i - 1 >= 0)
                sum += mat[i - 1][j];

            // i+1, j
            if (i + 1 < N)
                sum += mat[i + 1][j];

            // i, j-1
            if (j - 1 >= 0)
                sum += mat[i][j - 1];

            // i, j+1
            if (j + 1 < M)
                sum += mat[i][j + 1];

            // If the sum is a prime number
            if (prime[sum])
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void main(String[] args)
{
    SieveOfEratosthenes();

    int [][]mat = { { 1, 2, 3, 4 },
                    { 5, 6, 7, 8 },
                    { 9, 10, 11, 12 } };

    // Function call
    System.out.print(PrimeSumCells(mat) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to
# find the cells whose
# adjacent cells's
# sum is prime Number
MAX = 100005
prime = [True] * MAX

def SieveOfEratosthenes():

    # Create a boolean array "prime[0..MAX-1]"
    # and initialize all entries it as true.
    # A value in prime[i] will finally
    # be false if i is Not a prime, else true.
    global prime

    prime[0] = prime[1] = False

    p = 2
    while p * p < MAX:

        # If prime[p] is not changed,
        # then it is a prime
        if (prime[p] == True):

            # Update all multiples of p
            # greater than or
            # equal to the square of it
            # numbers which are multiple of
            # p and are less than p^2 are
            # already been marked.
            for i in range (p * p, MAX, p):
                prime[i] = False               
        p += 1

# Function to count the
# cells having adjacent
# cell's sum is equal to prime
def PrimeSumCells(mat):

    count = 0
    N = len(mat)
    M = len(mat[0])

    # Traverse for all the cells
    for i in range (N):
        for j in range (M):

            sum = 0

            # i - 1, j
            if (i - 1 >= 0):
                sum += mat[i - 1][j]

            # i + 1, j
            if (i + 1 < N):
                sum += mat[i + 1][j]

            # i, j - 1
            if (j - 1 >= 0):
                sum += mat[i][j - 1]

            # i, j + 1
            if (j + 1 < M):
                sum += mat[i][j + 1]

            # If the sum is a prime number
            if (prime[sum]):
                count += 1

    # Return the count
    return count

# Driver code
if __name__ =="__main__":

    SieveOfEratosthenes()
    mat = [[1, 2, 3, 4],
           [5, 6, 7, 8],
           [9, 10, 11, 12]]

    # Function call
    print (PrimeSumCells(mat))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the cells whose
// adjacent cells's sum is prime Number
using System;
class GFG{

static readonly int MAX = 100005;
static bool []prime = new bool[MAX];

static void SieveOfEratosthenes()
{
    // Create a bool array "prime[0..MAX-1]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    for (int i = 0; i < prime.Length; i++)
    prime[i] = true;

    prime[0] = prime[1] = false;

    for (int p = 2; p * p < MAX; p++)
    {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true)
        {
            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (int i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to count the cells having
// adjacent cell's sum
// is equal to prime
static int PrimeSumCells(int [,]mat)
{
    int count = 0;

    int N = mat.GetLength(0);
    int M = mat.GetLength(1);

    // Traverse for all the cells
    for (int i = 0; i < N; i++)
    {
        for (int j = 0; j < M; j++)
        {
            int sum = 0;

            // i-1, j
            if (i - 1 >= 0)
                sum += mat[i - 1, j];

            // i+1, j
            if (i + 1 < N)
                sum += mat[i + 1, j];

            // i, j-1
            if (j - 1 >= 0)
                sum += mat[i, j - 1];

            // i, j+1
            if (j + 1 < M)
                sum += mat[i, j + 1];

            // If the sum is a prime number
            if (prime[sum])
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver Code
public static void Main(String[] args)
{
    SieveOfEratosthenes();

    int [,]mat = { { 1, 2, 3, 4 },
                   { 5, 6, 7, 8 },
                   { 9, 10, 11, 12 } };

    // Function call
    Console.Write(PrimeSumCells(mat) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript program to find the cells whose
// adjacent cells's sum is prime Number

let MAX = 100005

let prime = new Array(MAX);

function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..MAX-1]"
    // and initialize all entries it as true.
    // A value in prime[i] will finally
    // be false if i is Not a prime, else true.
    prime.fill(true)

    prime[0] = prime[1] = false;

    for (let p = 2; p * p < MAX; p++) {
        // If prime[p] is not changed,
        // then it is a prime
        if (prime[p] == true) {
            // Update all multiples of p
            // greater than or
            // equal to the square of it
            // numbers which are multiple of p and are
            // less than p^2 are already been marked.
            for (let i = p * p; i < MAX; i += p)
                prime[i] = false;
        }
    }
}

// Function to count the cells having
// adjacent cell's sum
// is equal to prime
function PrimeSumCells(mat)
{
    let count = 0;

    let N = mat.length;
    let M = mat[0].length;

    // Traverse for all the cells
    for (let i = 0; i < N; i++) {
        for (let j = 0; j < M; j++) {

            let sum = 0;

            // i-1, j
            if (i - 1 >= 0)
                sum += mat[i - 1][j];

            // i+1, j
            if (i + 1 < N)
                sum += mat[i + 1][j];

            // i, j-1
            if (j - 1 >= 0)
                sum += mat[i][j - 1];

            // i, j+1
            if (j + 1 < M)
                sum += mat[i][j + 1];

            // If the sum is a prime number
            if (prime[sum])
                count++;
        }
    }

    // Return the count
    return count;
}

// Driver Program
    SieveOfEratosthenes();

    let mat = [ [ 1, 2, 3, 4 ],
                                [ 5, 6, 7, 8 ],
                                [ 9, 10, 11, 12 ] ];

    // Function call
    document.write(PrimeSumCells(mat) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
6
```