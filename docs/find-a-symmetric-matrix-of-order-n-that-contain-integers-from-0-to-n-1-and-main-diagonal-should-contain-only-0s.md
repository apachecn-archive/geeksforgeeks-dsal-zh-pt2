# 求一个 N 阶对称矩阵，它包含 0 到 N-1 的整数，主对角线应该只包含 0

> 原文:[https://www . geesforgeks . org/find-a-对称 n 阶矩阵-包含从 0 到 n-1 的整数-主对角线-应该只包含-0s/](https://www.geeksforgeeks.org/find-a-symmetric-matrix-of-order-n-that-contain-integers-from-0-to-n-1-and-main-diagonal-should-contain-only-0s/)

给定一个整数 **N** 。任务是生成一个具有以下属性的[对称矩阵](https://www.geeksforgeeks.org/program-to-check-if-a-matrix-is-symmetric/)**N * N**。

1.  主对角线应该只包含 0
2.  矩阵应该只包含从 0 到 N-1 的元素。

**例:**

> **输入:** N = 4
> **输出:**
> 0 2 3 1
> 2 0 1 3
> 3 1 0 2
> 1 3 2 0
> T10】输入: N = 5
> **输出:**
> 0 2 3 4 1
> 2 0 4 1 3
> 3 4 0 2 1
> 4 1 2 0 3
> 1 3 1 3 3 0

**方法:**由于所需矩阵必须是正方形矩阵，我们可以生成一个包含 1 到 n-1 元素的对称矩阵，不包括 0。稍后我们将处理 0 的情况。
**以 N = 4 时为例:**
我们首先生成一个对称矩阵，按照循环顺序从 1 到 n-1 填充每一行，也就是将第一行填充 1 ^ 2 ^ 3，对后续所有行按照循环顺序这样做，就很容易做到。

> 所以，最终的矩阵将是，
> 1 2 3
> 2 3 1
> 3 1 2

现在，我们已经生成了一个包含从 1 到 n 的元素的对称矩阵。让我们讨论一下情况 0。我们将利用上述矩阵对称的优势，我们将像这样添加一列 0 和多行 0，

> 1 2 3 0
> 2 3 1 0
> 3 1 2 0
> 0 0 0

现在，我们必须把所有的 0 放在对角线上。为此，我们将从第一行开始，直到最后一行-1，用每行中的数字交换所有的 0，并且还将在最后一行中进行如下更改:

> 对于第 1 行，我们交换 0 和 1，并将最后一行的第 1 个元素放入我们交换的数字，即 1。
> 0 2 3 1
> 2 3 1 0
> 3 1 2 0
> 1 0 0 0
> 对于第 2 行，我们交换 0 和 3，并使最后一行的第二个元素也为 3。
> 0 2 3 1
> 2 0 1 3
> 3 1 2 0
> 1 3 0 0
> 以此类推……
> 生成的最终矩阵将是所需的矩阵。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate the required matrix
void solve(long long n)
{
    long long initial_array[n - 1][n - 1], final_array[n][n];

    for (long long i = 0; i < n - 1; ++i)
        initial_array[0][i] = i + 1;

    // Form cyclic array of elements 1 to n-1
    for (long long i = 1; i < n - 1; ++i)
        for (long long j = 0; j < n - 1; ++j)
            initial_array[i][j]
                = initial_array[i - 1][(j + 1) % (n - 1)];

    // Store initial array into final array
    for (long long i = 0; i < n - 1; ++i)
        for (long long j = 0; j < n - 1; ++j)
            final_array[i][j] = initial_array[i][j];

    // Fill the last row and column with 0's
    for (long long i = 0; i < n; ++i)
        final_array[i][n - 1] = final_array[n - 1][i] = 0;

    for (long long i = 0; i < n; ++i) {
        long long t0 = final_array[i][i];
        long long t1 = final_array[i][n - 1];

        // Swap 0 and the number present
        // at the current indexed row
        swap(final_array[i][i], final_array[i][n - 1]);

        // Also make changes in the last row
        // with the number we swapped
        final_array[n - 1][i] = t0;
    }

    // Print the final array
    for (long long i = 0; i < n; ++i) {
        for (long long j = 0; j < n; ++j)
            cout << final_array[i][j] << " ";
        cout << endl;
    }
}

// Driver code
int main()
{
    long long n = 5;
    solve(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to generate the required matrix
static void solve(long n)
{
    long initial_array[][]= new long[(int)n - 1][(int)n - 1],
                    final_array[][]= new long[(int)n][(int)n];

    for (long i = 0; i < n - 1; ++i)
        initial_array[0][(int)i] = i + 1;

    // Form cyclic array of elements 1 to n-1
    for (long i = 1; i < n - 1; ++i)
        for (long j = 0; j < n - 1; ++j)
            initial_array[(int)i][(int)j]
                = initial_array[(int)i - 1][(int)((int)j + 1) % ((int)n - 1)];

    // Store initial array into final array
    for (long i = 0; i < n - 1; ++i)
        for (long j = 0; j < n - 1; ++j)
            final_array[(int)i][(int)j] = initial_array[(int)i][(int)j];

    // Fill the last row and column with 0's
    for (long i = 0; i < n; ++i)
        final_array[(int)i][(int)n - 1] = final_array[(int)n - 1][(int)i] = 0;

    for (long i = 0; i < n; ++i)
    {
        long t0 = final_array[(int)i][(int)i];
        long t1 = final_array[(int)i][(int)n - 1];

        // Swap 0 and the number present
        // at the current indexed row
        long s = final_array[(int)i][(int)i];
        final_array[(int)i][(int)i]=final_array[(int)i][(int)n - 1];
        final_array[(int)i][(int)n - 1]=s;

        // Also make changes in the last row
        // with the number we swapped
        final_array[(int)n - 1][(int)i] = t0;
    }

    // Print the final array
    for (long i = 0; i < n; ++i)
    {
        for (long j = 0; j < n; ++j)
            System.out.print( final_array[(int)i][(int)j] + " ");
        System.out.println();
    }
}

// Driver code
public static void main(String args[])
{
    long n = 5;
    solve(n);
}
}

// This code is contributed by Arnab Kundu

```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to generate the required matrix
def solve(n):
    initial_array = [[0 for i in range(n-1)] for j in range(n-1)]
    final_array = [[0 for i in range(n)]for j in range(n)]

    for i in range(n - 1):
        initial_array[0][i] = i + 1

    # Form cyclic array of elements 1 to n-1
    for i in range(1, n - 1):
        for j in range(n - 1):
            initial_array[i][j] = initial_array[i - 1][(j + 1) % (n - 1)]

    # Store initial array into final array
    for i in range(n-1):
        for j in range(n-1):
            final_array[i][j] = initial_array[i][j]

    # Fill the last row and column with 0's
    for i in range(n):
        final_array[i][n - 1] = final_array[n - 1][i] = 0

    for i in range(n):
        t0 = final_array[i][i]
        t1 = final_array[i][n - 1]

        # Swap 0 and the number present
        # at the current indexed row
        temp = final_array[i][i]
        final_array[i][i] = final_array[i][n - 1]
        final_array[i][n - 1] = temp

        # Also make changes in the last row
        # with the number we swapped
        final_array[n - 1][i] = t0

    # Print the final array
    for i in range(n):
        for j in range(n):
            print(final_array[i][j],end = " ")
        print("\n",end = "")

# Driver code
if __name__ == '__main__':
    n = 5
    solve(n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to generate the required matrix
static void solve(long n)
{
    long [,]initial_array = new long[(int)n - 1,(int)n - 1];
    long [,]final_array = new long[(int)n,(int)n];

    for (long i = 0; i < n - 1; ++i)
        initial_array[0,(int)i] = i + 1;

    // Form cyclic array of elements 1 to n-1
    for (long i = 1; i < n - 1; ++i)
        for (long j = 0; j < n - 1; ++j)
            initial_array[(int)i,(int)j]
                = initial_array[(int)i - 1,(int)((int)j + 1) % ((int)n - 1)];

    // Store initial array into final array
    for (long i = 0; i < n - 1; ++i)
        for (long j = 0; j < n - 1; ++j)
            final_array[(int)i,(int)j] = initial_array[(int)i,(int)j];

    // Fill the last row and column with 0's
    for (long i = 0; i < n; ++i)
        final_array[(int)i,(int)n - 1] = final_array[(int)n - 1,(int)i] = 0;

    for (long i = 0; i < n; ++i)
    {
        long t0 = final_array[(int)i, (int)i];
        long t1 = final_array[(int)i, (int)n - 1];

        // Swap 0 and the number present
        // at the current indexed row
        long s = final_array[(int)i,(int)i];
        final_array[(int)i,(int)i] = final_array[(int)i, (int)n - 1];
        final_array[(int)i,(int)n - 1] = s;

        // Also make changes in the last row
        // with the number we swapped
        final_array[(int)n - 1,(int)i] = t0;
    }

    // Print the final array
    for (long i = 0; i < n; ++i)
    {
        for (long j = 0; j < n; ++j)
            Console.Write( final_array[(int)i,(int)j] + " ");
        Console.WriteLine();
    }
}

// Driver code
public static void Main(String []args)
{
    long n = 5;
    solve(n);
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to generate the required matrix
function solve($n)
{
    $initial_array = array(array()) ;
    $final_array = array(array()) ;

    for ($i = 0; $i < $n - 1; ++$i)
        $initial_array[0][$i] = $i + 1;

    // Form cyclic array of elements 1 to n-1
    for ($i = 1; $i < $n - 1; ++$i)
        for ($j = 0; $j < $n - 1; ++$j)
            $initial_array[$i][$j] =
                $initial_array[$i - 1][($j + 1) % ($n - 1)];

    // Store initial array into final array
    for ($i = 0; $i < $n - 1; ++$i)
        for ($j = 0; $j < $n - 1; ++$j)
            $final_array[$i][$j] = $initial_array[$i][$j];

    // Fill the last row and column with 0's
    for ($i = 0; $i < $n; ++$i)
        $final_array[$i][$n - 1] = $final_array[$n - 1][$i] = 0;

    for ($i = 0; $i < $n; ++$i)
    {
        $t0 = $final_array[$i][$i];
        $t1 = $final_array[$i][$n - 1];

        // Swap 0 and the number present
        // at the current indexed row
        $temp = $final_array[$i][$i] ;
        $final_array[$i][$i] = $final_array[$i][$n - 1] ;
        $final_array[$i][$n - 1] = $temp ;

        // Also make changes in the last row
        // with the number we swapped
        $final_array[$n - 1][$i] = $t0;
    }

    // Print the final array
    for ($i = 0; $i < $n; ++$i)
    {
        for ($j = 0; $j < $n; ++$j)
            echo $final_array[$i][$j]," ";
        echo "\n";
    }
}

    // Driver code
    $n = 5;
    solve($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to generate the required matrix
function solve(n)
{
    let initial_array = new Array(n-1);
    for (var i = 0; i < initial_array.length; i++) {
    initial_array[i] = new Array(2);
    }

    let final_array = new Array(n);
    for (var i = 0; i < final_array.length; i++) {
    final_array[i] = new Array(2);
    }

    for (let i = 0; i < n - 1; ++i)
        initial_array[0][i] = i + 1;

    // Form cyclic array of elements 1 to n-1
    for (let i = 1; i < n - 1; ++i)
        for (let j = 0; j < n - 1; ++j)
            initial_array[i][j]
                = initial_array[i - 1][(j + 1) % (n - 1)];

    // Store initial array into final array
    for (let i = 0; i < n - 1; ++i)
        for (let j = 0; j < n - 1; ++j)
            final_array[i][j] = initial_array[i][j];

    // Fill the last row and column with 0's
    for (let i = 0; i < n; ++i)
        final_array[i][n - 1] = final_array[n - 1][i] = 0;

    for (let i = 0; i < n; ++i)
    {
        let t0 = final_array[i][i];
        let t1 = final_array[i][n - 1];

        // Swap 0 and the number present
        // at the current indexed row
        let s = final_array[i][i];
        final_array[i][i]=final_array[i][n - 1];
        final_array[i][n - 1]=s;

        // Also make changes in the last row
        // with the number we swapped
        final_array[n - 1][i] = t0;
    }

    // Print the final array
    for (let i = 0; i < n; ++i)
    {
        for (let j = 0; j < n; ++j)
            document.write( final_array[i][j] + " ");
        document.write("<br/>");
    }
}  

// Driver Code
    let n = 5;
    solve(n);

  // This code is contributed by target_2.
</script>
```

**Output**

```
0 2 3 4 1 
2 0 4 1 3 
3 4 0 2 1 
4 1 2 0 3 
1 3 1 3 0 
```

**时间复杂度:** O(N <sup>2</sup> )

**辅助空间:** O(N <sup>2</sup> )