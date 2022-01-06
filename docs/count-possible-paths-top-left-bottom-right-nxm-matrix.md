# 计算从 mXn 矩阵的左上角到右下角的所有可能路径

> 原文:[https://www . geesforgeks . org/count-可能路径-左上角-右下角-nxm-matrix/](https://www.geeksforgeeks.org/count-possible-paths-top-left-bottom-right-nxm-matrix/)

问题是计算从 mXn 矩阵的左上方到右下方的所有可能路径，限制条件是从每个单元格 ***只能向右或向下移动***
**示例:**

```
Input :  m = 2, n = 2;
Output : 2
There are two paths
(0, 0) -> (0, 1) -> (1, 1)
(0, 0) -> (1, 0) -> (1, 1)

Input :  m = 2, n = 3;
Output : 3
There are three paths
(0, 0) -> (0, 1) -> (0, 2) -> (1, 2)
(0, 0) -> (0, 1) -> (1, 1) -> (1, 2)
(0, 0) -> (1, 0) -> (1, 1) -> (1, 2)
```

我们已经讨论了一个[解决方案来打印所有可能的路径](https://www.geeksforgeeks.org/print-all-possible-paths-from-top-left-to-bottom-right-of-a-mxn-matrix/)，计算所有路径更容易。设 NumberOfPaths(m，n)为到达矩阵中行号 m 和列号 n 的路径数，NumberOfPaths(m，n)可递归写成如下。

## C++

```
// A C++  program to count all possible paths
// from top left to bottom right

#include <iostream>
using namespace std;

// Returns count of possible paths to reach cell at row
// number m and column number n from the topmost leftmost
// cell (cell at 1, 1)
int numberOfPaths(int m, int n)
{
    // If either given row number is first or given column
    // number is first
    if (m == 1 || n == 1)
        return 1;

    // If diagonal movements are allowed then the last
    // addition is required.
    return numberOfPaths(m - 1, n) + numberOfPaths(m, n - 1);
    // + numberOfPaths(m-1, n-1);
}

int main()
{
    cout << numberOfPaths(3, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to count all possible paths
// from top left to bottom right

class GFG {

    // Returns count of possible paths to reach
    // cell at row number m and column number n
    // from the topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // If either given row number is first or
        // given column number is first
        if (m == 1 || n == 1)
            return 1;

        // If diagonal movements are allowed then
        // the last addition is required.
        return numberOfPaths(m - 1, n) + numberOfPaths(m, n - 1);
        // + numberOfPaths(m-1, n-1);
    }

    public static void main(String args[])
    {
        System.out.println(numberOfPaths(3, 3));
    }
}

// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to count all possible paths
# from top left to bottom right

# function to return count of possible paths
# to reach cell at row number m and column
# number n from the topmost leftmost
# cell (cell at 1, 1)
def numberOfPaths(m, n):
# If either given row number is first
# or given column number is first
    if(m == 1 or n == 1):
        return 1

# If diagonal movements are allowed
# then the last addition
# is required.
    return numberOfPaths(m-1, n) + numberOfPaths(m, n-1)

# Driver program to test above function
m = 3
n = 3
print(numberOfPaths(m, n))

# This code is contributed by Aditi Sharma
```

## C#

```
// A C# program to count all possible paths
// from top left to bottom right

using System;

public class GFG {
    // Returns count of possible paths to reach
    // cell at row number m and column number n
    // from the topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // If either given row number is first or
        // given column number is first
        if (m == 1 || n == 1)
            return 1;

        // If diagonal movements are allowed then
        // the last addition is required.
        return numberOfPaths(m - 1, n) + numberOfPaths(m, n - 1);
        // + numberOfPaths(m-1, n-1);
    }

    static public void Main()
    {
        Console.WriteLine(numberOfPaths(3, 3));
    }
}

// This code is contributed by ajit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

// Returns count of possible paths
// to reach cell at row number m
// and column number n from the
// topmost leftmost cell (cell at 1, 1)
function numberOfPaths($m, $n)
{

    // If either given row number
    // is first or given column
    // number is first
    if ($m == 1 || $n == 1)
            return 1;

    // If diagonal movements
    // are allowed then the last
    // addition is required.
    return numberOfPaths($m - 1, $n) +
           numberOfPaths($m, $n - 1);
}

// Driver Code
echo numberOfPaths(3, 3);

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
// A Javascript program to count all possible paths
// from top left to bottom right

    // Returns count of possible paths to reach
    // cell at row number m and column number n
    // from the topmost leftmost cell (cell at 1, 1)
    function numberOfPaths(m, n)
    {

        // If either given row number is first or
        // given column number is first
        if (m == 1 || n == 1)
            return 1;

        // If diagonal movements are allowed then
        // the last addition is required.
        return numberOfPaths(m - 1, n) + numberOfPaths(m, n - 1);

       // + numberOfPaths(m - 1, n - 1);
    }

    document.write(numberOfPaths(3, 3)+"<br>");

    // This code is contributed by rag2127
</script>
```

**输出:**

```
6
```

上述递归解的时间复杂度是指数的。有许多重叠的子问题。我们可以为 numberOfPaths，3)绘制一个递归树，并看到许多重叠的子问题。递归树类似于最长公共子序列问题的[递归树](https://www.geeksforgeeks.org/dynamic-programming-set-4-longest-common-subsequence/)。
所以这个问题既有动态规划问题的属性(见[这个](https://www.geeksforgeeks.org/dynamic-programming-set-1/)又有[这个](https://www.geeksforgeeks.org/dynamic-programming-set-2-optimal-substructure-property/))。像其他典型的[动态规划(DP)问题](https://www.geeksforgeeks.org/archives/tag/dynamic-programming)一样，通过使用上述递归公式以自下而上的方式构造临时数组计数[][]，可以避免相同子问题的重新计算。

## C++

```
// A C++ program to count all possible paths
// from top left to bottom right
#include <iostream>
using namespace std;

// Returns count of possible paths to reach cell at
// row number m and column  number n from the topmost
// leftmost cell (cell at 1, 1)
int numberOfPaths(int m, int n)
{
    // Create a 2D table to store results of subproblems
    int count[m][n];

    // Count of paths to reach any cell in first column is 1
    for (int i = 0; i < m; i++)
        count[i][0] = 1;

    // Count of paths to reach any cell in first row is 1
    for (int j = 0; j < n; j++)
        count[0][j] = 1;

    // Calculate count of paths for other cells in
    // bottom-up manner using the recursive solution
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++)

            // By uncommenting the last part the code calculates the total
            // possible paths if the diagonal Movements are allowed
            count[i][j] = count[i - 1][j] + count[i][j - 1]; //+ count[i-1][j-1];
    }
    return count[m - 1][n - 1];
}

// Driver program to test above functions
int main()
{
    cout << numberOfPaths(3, 3);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java program to count all possible paths
// from top left to bottom right
class GFG {
    // Returns count of possible paths to reach
    // cell at row number m and column number n from
    // the topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // Create a 2D table to store results
        // of subproblems
        int count[][] = new int[m][n];

        // Count of paths to reach any cell in
        // first column is 1
        for (int i = 0; i < m; i++)
            count[i][0] = 1;

        // Count of paths to reach any cell in
        // first column is 1
        for (int j = 0; j < n; j++)
            count[0][j] = 1;

        // Calculate count of paths for other
        // cells in bottom-up manner using
        // the recursive solution
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++)

                // By uncommenting the last part the
                // code calculates the total possible paths
                // if the diagonal Movements are allowed
                count[i][j] = count[i - 1][j] + count[i][j - 1]; //+ count[i-1][j-1];
        }
        return count[m - 1][n - 1];
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        System.out.println(numberOfPaths(3, 3));
    }
}

// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to count all possible paths
# from top left to bottom right

# Returns count of possible paths to reach cell
# at row number m and column number n from the
# topmost leftmost cell (cell at 1, 1)
def numberOfPaths(m, n):
    # Create a 2D table to store
    # results of subproblems
    # one-liner logic to take input for rows and columns
    # mat = [[int(input()) for x in range (C)] for y in range(R)]

    count = [[0 for x in range(n)] for y in range(m)]

    # Count of paths to reach any
    # cell in first column is 1
    for i in range(m):
        count[i][0] = 1;

    # Count of paths to reach any
    # cell in first column is 1
    for j in range(n):
        count[0][j] = 1;

    # Calculate count of paths for other
    # cells in bottom-up
    # manner using the recursive solution
    for i in range(1, m):
        for j in range(1, n):            
            count[i][j] = count[i-1][j] + count[i][j-1]
    return count[m-1][n-1]

# Driver program to test above function
m = 3
n = 3
print( numberOfPaths(m, n))

# This code is contributed by Aditi Sharma
```

## C#

```
// A C#  program to count all possible paths
// from top left to bottom right
using System;

public class GFG {

    // Returns count of possible paths to reach
    // cell at row number m and column number n from
    // the topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // Create a 2D table to store results
        // of subproblems
        int[, ] count = new int[m, n];

        // Count of paths to reach any cell in
        // first column is 1
        for (int i = 0; i < m; i++)
            count[i, 0] = 1;

        // Count of paths to reach any cell in
        // first column is 1
        for (int j = 0; j < n; j++)
            count[0, j] = 1;

        // Calculate count of paths for other
        // cells in bottom-up manner using
        // the recursive solution
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++)

                // By uncommenting the last part the
                // code calculates the total possible paths
                // if the diagonal Movements are allowed
                count[i, j] = count[i - 1, j] + count[i, j - 1]; //+ count[i-1][j-1];
        }
        return count[m - 1, n - 1];
    }

    // Driver program to test above function
    static public void Main()
    {
        Console.WriteLine(numberOfPaths(3, 3));
    }
}

// This code is contributed by akt_mit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A PHP program to count all possible
// paths from top left to bottom right

// Returns count of possible paths to
// reach cell at row number m and column
// number n from the topmost leftmost
// cell (cell at 1, 1)
function numberOfPaths($m, $n)
{
    // Create a 2D table to store
    // results of subproblems
    $count = array();

    // Count of paths to reach any cell
    // in first column is 1
    for ($i = 0; $i < $m; $i++)
        $count[$i][0] = 1;

    // Count of paths to reach any cell
    // in first column is 1
    for ($j = 0; $j < $n; $j++)
        $count[0][$j] = 1;

    // Calculate count of paths for other
    // cells in bottom-up manner using the
    // recursive solution
    for ($i = 1; $i < $m; $i++)
    {
        for ($j = 1; $j < $n; $j++)

            // By uncommenting the last part the
            // code calculated the total possible
            // paths if the diagonal Movements are allowed
            $count[$i][$j] = $count[$i - 1][$j] +
                             $count[$i][$j - 1]; //+ count[i-1][j-1];
    }
    return $count[$m - 1][$n - 1];
}

// Driver Code
echo numberOfPaths(3, 3);

// This code is contributed
// by Mukul Singh
?>
```

## java 描述语言

```
<script>

// A javascript program to count all possible paths
// from top left to bottom right

// Returns count of possible paths to reach
// cell at row number m and column number n from
// the topmost leftmost cell (cell at 1, 1)
function numberOfPaths(m , n)
{
    // Create a 2D table to store results
    // of subproblems
    var count = Array(m).fill(0).map(x => Array(n).fill(0));

    // Count of paths to reach any cell in
    // first column is 1
    for (i = 0; i < m; i++)
        count[i][0] = 1;

    // Count of paths to reach any cell in
    // first column is 1
    for (j = 0; j < n; j++)
        count[0][j] = 1;

    // Calculate count of paths for other
    // cells in bottom-up manner using
    // the recursive solution
    for (i = 1; i < m; i++) {
        for (j = 1; j < n; j++)

            // By uncommenting the last part the
            // code calculates the total possible paths
            // if the diagonal Movements are allowed

            //+ count[i-1][j-1];
            count[i][j] = count[i - 1][j] + count[i][j - 1];
    }
    return count[m - 1][n - 1];
}

// Driver program to test above function
document.write(numberOfPaths(3, 3));

// This code is contributed by 29AjayKumar

</script>
```

**输出:**

```
6
```

**递归动态规划解。**以下实施基于自上而下的方法。

## C++

```
// A C++ program to count all possible paths from
// top left to top bottom right using
// Recursive Dynamic Programming
#include <iostream>
#include <cstring>
using namespace std;

// Returns count of possible paths to reach
// cell at row number m and column number n from
// the topmost leftmost cell (cell at 1, 1)
int numberOfPaths(int n,int m,int DP[4][4]){

    if(n == 1 || m == 1)
        return DP[n][m] = 1;

    // Add the element in the DP table
    // If it is was not computed before
    if(DP[n][m] == 0)
        DP[n][m] = numberOfPaths(n - 1, m,DP) + numberOfPaths(n, m - 1,DP);

    return DP[n][m];
}

// Driver code
int main()
{
    // Create an empty 2D table
    int DP[4][4] = {0};
    memset(DP, 0, sizeof(DP));

    cout << numberOfPaths(3, 3,DP);

    return 0;
}
  // This code is contributed
  // by Gatea David
```

以上 2 个动态规划解的时间复杂度为 O(mn)。
以上 2 个解的空间复杂度为 O(mn)。
**动力定位解的空间优化。**
上面的解法比较直观但是我们也可以把空间缩小 O(n)；其中 n 是列大小。

## C++

```
#include <bits/stdc++.h>

using namespace std;

// Returns count of possible paths to reach
// cell at row number m and column number n from
// the topmost leftmost cell (cell at 1, 1)
int numberOfPaths(int m, int n)
{
    // Create a 1D array to store results of subproblems
    int dp[n] = { 1 };
    dp[0] = 1;

    for (int i = 0; i < m; i++) {
        for (int j = 1; j < n; j++) {
            dp[j] += dp[j - 1];
        }
    }

    return dp[n - 1];
}

// Driver code
int main()
{
    cout << numberOfPaths(3, 3);
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
class GFG {
    // Returns count of possible paths to reach
    // cell at row number m and column number n from
    // the topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // Create a 1D array to store results of subproblems
        int[] dp = new int[n];
        dp[0] = 1;

        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] += dp[j - 1];
            }
        }

        return dp[n - 1];
    }

    // Driver program to test above function
    public static void main(String args[])
    {
        System.out.println(numberOfPaths(3, 3));
    }
}
```

## 蟒蛇 3

```
# Returns count of possible paths
# to reach cell at row number m and
# column number n from the topmost
# leftmost cell (cell at 1, 1)
def numberOfPaths(p, q):

    # Create a 1D array to store
    # results of subproblems
    dp = [1 for i in range(q)]
    for i in range(p - 1):
        for j in range(1, q):
            dp[j] += dp[j - 1]
    return dp[q - 1]

# Driver Code
print(numberOfPaths(3, 3))

# This code is contributed
# by Ankit Yadav
```

## C#

```
using System;

class GFG {
    // Returns count of possible paths
    // to reach cell at row number m
    // and column number n from the
    // topmost leftmost cell (cell at 1, 1)
    static int numberOfPaths(int m, int n)
    {
        // Create a 1D array to store
        // results of subproblems
        int[] dp = new int[n];
        dp[0] = 1;

        for (int i = 0; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[j] += dp[j - 1];
            }
        }

        return dp[n - 1];
    }

    // Driver Code
    public static void Main()
    {
        Console.Write(numberOfPaths(3, 3));
    }
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Returns count of possible paths to
// reach cell at row number m and
// column number n from the topmost
// leftmost cell (cell at 1, 1)
function numberOfPaths($m, $n)
{
    // Create a 1D array to store
    // results of subproblems
    $dp = array();
    $dp[0] = 1;

    for ($i = 0; $i < $m; $i++)
    {
    for ($j = 1; $j < $n; $j++)
    {
        $dp[$j] += $dp[$j - 1];
    }
    }

    return $dp[$n - 1];
}

// Driver Code
echo numberOfPaths(3, 3);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Returns count of possible paths to reach
// cell at row number m and column number n from
// the topmost leftmost cell (cell at 1, 1)
function numberOfPaths(m , n)
{
    // Create a 1D array to store results of subproblems
    dp = Array.from({length: n}, (_, i) => 0);
    dp[0] = 1;

    for (i = 0; i < m; i++) {
        for (j = 1; j < n; j++) {
            dp[j] += dp[j - 1];
        }
    }

    return dp[n - 1];
}

// Driver program to test above function
document.write(numberOfPaths(3, 3));

// This code contributed by Princi Singh

</script>
```

**输出:**

```
6
```

此代码由 [**Vivek Singh**](https://www.facebook.com/vvkvivek.singh)
贡献注意计数也可以用公式(m-1 + n-1)计算！/(m-1)！(n-1)！。
**另一种方法:**(使用组合学)在这种方法中，我们必须计算 m+n-2 C n-1，这里是(m+n-2)！/ (n-1)！(m-1)！

现在，让我们看看这个公式是如何给出正确答案的[(参考文献 1)](https://towardsdatascience.com/understanding-combinatorics-number-of-paths-on-a-grid-bddf08e28384) [(参考文献 2)](https://math.stackexchange.com/a/541080) **阅读参考文献 1 和参考文献 2，更好地理解**

**m =行数**

**n =列数**

**我们必须向下移动才能到达最后一行的移动总数= m–1(m 行，因为我们从不包括的(1，1)开始)**

**我们必须向右移动才能到达最后一列的移动总数= n–1(n 列，因为我们是从不包括的(1，1)开始)**

****向下移动=(m–1)****

****右移=(n–1)****

****总移动=向下移动+向右移动=(m–1)+(n–1)****

****现在把移动看作一串“R”和“D”字符，其中任何一个索引处的“R”会告诉我们“向右”移动，“D”会告诉我们“向下”移动****

****现在想一想，在总共应该有(n–1+m–1)个字符和应该有(m–1)‘D’个字符和(n–1)‘R’个字符的地方，我们能做出多少个唯一的字符串(移动)？****

**选择(n–1)‘R’字符的位置会导致自动选择(m–1)‘D’字符位置**

**[计算<sup>n</sup>C<sub>R</sub>T5
选择位置的方式数量为(n–1)【R】字符= <sup>总位置</sup>C<sub>n–1</sub>=<sup>总位置</sup>C<sub>m–1</sub>=(n–1+m–1)！= ![\frac {(n - 1 + m - 1)!} {(n - 1) ! (m - 1)!}  ](img/a0ce2529d72414e64b879ff7cb29bc04.png "Rendered by QuickLaTeX.com")](https://www.geeksforgeeks.org/program-to-calculate-the-value-of-ncr-efficiently/)** 

*****思考这个问题的另一种方式:*** 数一数用**【X】0**和**【Y】1**组成一个 **N 位二进制串**(只包含 0 和 1 的串)(这里我们把‘R’分别替换为‘0’或‘1’，把‘D’替换为‘1’或‘0’，哪个更适合你)** 

## **C++**

```
// A C++ program to count all possible paths from
// top left to top bottom using combinatorics

#include <iostream>
using namespace std;

int numberOfPaths(int m, int n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    int path = 1;
    for (int i = n; i < (m + n - 1); i++) {
        path *= i;
        path /= (i - n + 1);
    }
    return path;
}

// Driver code
int main()
{
    cout << numberOfPaths(3, 3);
    return 0;
}

// This code is suggested by Kartik Sapra
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to count all possible paths from
// top left to top bottom using combinatorics
class GFG {

    static int numberOfPaths(int m, int n)
    {
        // We have to calculate m+n-2 C n-1 here
        // which will be (m+n-2)! / (n-1)! (m-1)!
        int path = 1;
        for (int i = n; i < (m + n - 1); i++) {
            path *= i;
            path /= (i - n + 1);
        }
        return path;
    }

    // Driver code
    public static void main(String[] args)
    {
        System.out.println(numberOfPaths(3, 3));
    }
}

// This code is contributed by Code_Mech.
```

## **蟒蛇 3**

```
# Python3 program to count all possible
# paths from top left to top bottom
# using combinatorics
def numberOfPaths(m, n) :

    # We have to calculate m + n-2 C n-1 here
    # which will be (m + n-2)! / (n-1)! (m-1)! path = 1;
    for i in range(n, (m + n - 1)):
        path *= i;
        path //= (i - n + 1);

    return path;

# Driver code
print(numberOfPaths(3, 3));

# This code is contributed
# by Akanksha Rai
```

## **C#**

```
// C# program to count all possible paths from
// top left to top bottom using combinatorics
using System;

class GFG {

    static int numberOfPaths(int m, int n)
    {
        // We have to calculate m+n-2 C n-1 here
        // which will be (m+n-2)! / (n-1)! (m-1)!
        int path = 1;
        for (int i = n; i < (m + n - 1); i++) {
            path *= i;
            path /= (i - n + 1);
        }
        return path;
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(numberOfPaths(3, 3));
    }
}

// This code is contributed by Code_Mech.
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php

// PHP program to count all possible paths from
// top left to top bottom using combinatorics
function numberOfPaths($m, $n)
{
    // We have to calculate m+n-2 C n-1 here
    // which will be (m+n-2)! / (n-1)! (m-1)!
    $path = 1;
    for ($i = $n; $i < ($m + $n - 1); $i++)
    {
        $path *= $i;
        $path /= ($i - $n + 1);
    }
    return $path;
}

// Driver code
{
    echo(numberOfPaths(3, 3));
}

// This code is contributed by Code_Mech.
```

## **java 描述语言**

```
<script>

// javascript program to count all possible paths from
// top left to top bottom using combinatorics  
function numberOfPaths(m , n)
    {
        // We have to calculate m+n-2 C n-1 here
        // which will be (m+n-2)! / (n-1)! (m-1)!
        var path = 1;
        for (i = n; i < (m + n - 1); i++) {
            path *= i;
            path = parseInt(path/(i - n + 1));
        }
        return path;
    }

// Driver code
document.write(numberOfPaths(3, 3));

// This code contributed by Princi Singh
</script>
```

****输出:****

```
6
```

**本文由 **Hariprasad NG** 供稿。如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。**