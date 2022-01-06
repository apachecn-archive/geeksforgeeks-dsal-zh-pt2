# 计算将一个数表示为完美平方之和的方法

> 原文:[https://www . geeksforgeeks . org/count-way-to-to-presentation-a-number-as-sum-of-perfect-squares/](https://www.geeksforgeeks.org/count-ways-to-represent-a-number-as-sum-of-perfect-squares/)

给定一个整数 **N** ，任务是找到将数字 **N** 表示为[完美平方](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)之和的方法数。

**示例:**

> **输入:** N = 9
> **输出:** 4
> **解释:**
> 将 9 表示为完美平方之和有四种方式:
> 1+1+1+1+1+1+1+1 = 9
> 1+1+1+1+1+4 = 9
> 1+4+4 = 9
> 9 = 9
> 
> **输入:**N =**T3】8
> T5】输出:** 3

**天真方法:**想法是将所有小于或等于 **N** 的完美方块存储在[数组](https://www.geeksforgeeks.org/array-data-structure/)中。现在问题简化为找到[方法，使用允许重复的数组元素](https://www.geeksforgeeks.org/ways-sum-n-using-array-elements-repetition-allowed/)求和到 **N** ，这可以使用[递归](https://www.geeksforgeeks.org/recursion/)解决。按照以下步骤解决问题:

*   将所有小于或等于 **N** 的[完美方块](https://www.geeksforgeeks.org/check-if-given-number-is-perfect-square-in-cpp/)存储在[数组](https://www.geeksforgeeks.org/array-data-structure/) **方块【】**中。
*   创建一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/)**count way(索引，目标)**，该函数采用两个参数 **index** 、(初始 N-1) 和 **target** (初始 N):
    *   处理基本案例:
        *   如果****目标**为 0，返回 1。**
        *   **如果**指数**或**目标**小于 0，返回 0。**
    *   **否则，通过从**目标**中减去元素**并递归调用**目标**的剩余值，将元素**psquare【index】**包含在总和中。****
    *   **通过移动到下一个索引并递归调用**目标**的相同值，从总和中排除元素**psquare【index】**。**
    *   **返回包含和不包含元素的总和。**
*   **打印**count way(N-1，N)** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Store perfect squares
// less than or equal to N
vector<int> psquare;

// Utility function to calculate perfect
// squares less than or equal to N
void calcPsquare(int N)
{
    for (int i = 1; i * i <= N; i++)
        psquare.push_back(i * i);
}

// Function to find the number
// of ways to represent a number
// as sum of perfect squares
int countWays(int index, int target)
{
    // Handle the base cases
    if (target == 0)
        return 1;

    if (index < 0 || target < 0)
        return 0;

    // Include the i-th index element
    int inc = countWays(
        index, target - psquare[index]);

    // Exclude the i-th index element
    int exc = countWays(index - 1, target);

    // Return the result
    return inc + exc;
}

// Driver Code
int main()
{
    // Given Input
    int N = 9;

    // Precalculate perfect
    // squares <= N
    calcPsquare(N);

    // Function Call
    cout << countWays(psquare.size() - 1, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Store perfect squares
    // less than or equal to N
    static ArrayList<Integer> psquare = new ArrayList<>();

    // Utility function to calculate perfect
    // squares less than or equal to N
    static void calcPsquare(int N)
    {
        for (int i = 1; i * i <= N; i++)
            psquare.add(i * i);
    }

    // Function to find the number
    // of ways to represent a number
    // as sum of perfect squares
    static int countWays(int index, int target)
    {
        // Handle the base cases
        if (target == 0)
            return 1;

        if (index < 0 || target < 0)
            return 0;

        // Include the i-th index element
        int inc
            = countWays(index, target - psquare.get(index));

        // Exclude the i-th index element
        int exc = countWays(index - 1, target);

        // Return the result
        return inc + exc;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int N = 9;

        // Precalculate perfect
        // squares <= N
        calcPsquare(N);

        // Function Call
        System.out.print(countWays(psquare.size() - 1, N));
    }
}

// This code is contributed by Kingash.
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Store perfect squares
# less than or equal to N
psquare = []

# Utility function to calculate perfect
# squares less than or equal to N
def calcPsquare(N):

    for i in range(1, N):
        if i * i > N:
            break

        psquare.append(i * i)

# Function to find the number
# of ways to represent a number
# as sum of perfect squares
def countWays(index, target):

    # Handle the base cases
    if (target == 0):
        return 1

    if (index < 0 or target < 0):
        return 0

    # Include the i-th index element
    inc = countWays(index, target - psquare[index])

    # Exclude the i-th index element
    exc = countWays(index - 1, target)

    # Return the result
    return inc + exc

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 9

    # Precalculate perfect
    # squares <= N
    calcPsquare(N)

    # Function Call
    print (countWays(len(psquare) - 1, N))

# This code is contributed by mohit kumar 29
```

## **C#**

```
using System.IO;
using System;
using System.Collections;

class GFG {
    // Store perfect squares
    // less than or equal to N
    static ArrayList psquare = new ArrayList();

    // Utility function to calculate perfect
    // squares less than or equal to N
    static void calcPsquare(int N)
    {
        for (int i = 1; i * i <= N; i++)
            psquare.Add(i * i);
    }

    // Function to find the number
    // of ways to represent a number
    // as sum of perfect squares
    static int countWays(int index, int target)
    {
        // Handle the base cases
        if (target == 0)
            return 1;

        if (index < 0 || target < 0)
            return 0;

        // Include the i-th index element
        int inc = countWays(index,
                            target - (int)psquare[index]);

        // Exclude the i-th index element
        int exc = countWays(index - 1, target);

        // Return the result
        return inc + exc;
    }

    static void Main()
    {

        // Given Input
        int N = 9;

        // Precalculate perfect
        // squares <= N
        calcPsquare(N);

        // Function Call
        Console.WriteLine(countWays(psquare.Count - 1, N));
    }
}

// This code is contributed by abhinavjain194.
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Store perfect squares
// less than or equal to N
var psquare = []

// Utility function to calculate perfect
// squares less than or equal to N
function calcPsquare(N)
{
    var i;
    for (i = 1; i * i <= N; i++)
        psquare.push(i * i);
}

// Function to find the number
// of ways to represent a number
// as sum of perfect squares
function countWays(index, target)
{
    // Handle the base cases
    if (target == 0)
        return 1;

    if (index < 0 || target < 0)
        return 0;

    // Include the i-th index element
    var inc = countWays(
        index, target - psquare[index]);

    // Exclude the i-th index element
    var exc = countWays(index - 1, target);

    // Return the result
    return inc + exc;
}

// Driver Code
    // Given Input
    var N = 9;

    // Precalculate perfect
    // squares <= N
    calcPsquare(N);

    // Function Call
    document.write(countWays(psquare.length - 1, N));

</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:** O(2 <sup>K</sup> ，其中 K 为小于等于 N 的完美方块数*
***辅助空间:** O(1)***

****有效途径:**这个问题有[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)和[最优子结构性质](https://www.geeksforgeeks.org/optimal-substructure-property-in-dynamic-programming-dp-2/)。为了优化上述方法，想法是使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)，通过使用大小为 **K*N** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)来记忆上述递归调用，其中 **K** 是小于或等于 **N** 的完美正方形的数量。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Store perfect squares
// less than or equal to N
vector<int> psquare;

// Utility function to calculate
// perfect squares <= N
void calcPsquare(int N)
{
    for (int i = 1; i * i <= N; i++)
        psquare.push_back(i * i);
}

// DP array for memoization
vector<vector<int> > dp;

// Recursive function to count
// number of ways to represent
// a number as a sum of perfect squares
int countWaysUtil(int index, int target)
{
    // Handle base cases
    if (target == 0)
        return 1;
    if (index < 0 || target < 0)
        return 0;

    // If already computed, return the result
    if (dp[index][target] != -1)
        return dp[index][target];

    // Else, compute the result
    return dp[index][target]
           = countWaysUtil(
                 index, target - psquare[index])

             + countWaysUtil(
                   index - 1, target);
}

// Function to find the number of ways to
// represent a number as a sum of perfect squares
int countWays(int N)
{
    // Precalculate perfect squares less
    // than or equal to N
    calcPsquare(N);

    // Create dp array to memoize
    dp.resize(psquare.size() + 1,
              vector<int>(N + 1, -1));

    // Function call to fill dp array
    return countWaysUtil(psquare.size() - 1, N);
}

// Driver Code
int main()
{
    // Given Input
    int N = 9;

    // Function Call
    cout << countWays(N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG {

    // Store perfect squares
    // less than or equal to N
    private static ArrayList<Integer> psquare;

    // Utility function to calculate
    // perfect squares <= N
    private static void calcPsquare(int n) {

        for (int i = 1; i * i <= n; i++)
            psquare.add(i * i);

    }

    // DP array for memoization
    private static int[][] dp;

    // Recursive function to count
    // number of ways to represent
    // a number as a sum of perfect squares
    private static int countWaysUtil(int index, int target) {
        // Handle base cases
        if (target == 0)
            return 1;
        if (index < 0 || target < 0)
            return 0;

        // If already computed, return the result
        if (dp[index][target] != -1)
            return dp[index][target];

        // Else, compute the result
        return dp[index][target]
               = countWaysUtil(
                     index, target - psquare.get(index))

                 + countWaysUtil(
                       index - 1, target);
    }

    // Function to find the number of ways to
    // represent a number as a sum of perfect squares
    private static int countWays(int n) {
        // Precalculate perfect squares less
        // than or equal to N
        psquare = new ArrayList<Integer>();
        calcPsquare(n);

        // Create dp array to memoize
        dp = new int[psquare.size()+1][n+1];
        for(int i = 0; i<=psquare.size(); i++)Arrays.fill(dp[i], -1);

        // Function call to fill dp array
        return countWaysUtil(psquare.size() - 1, n);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Input
        int N = 9;

        // Function Call
        System.out.print(countWays(N));
    }

}

// This code is contributed by Dheeraj Bhagchandani.
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from math import sqrt

# Store perfect squares
# less than or equal to N
psquare = []

# DP array for memoization
dp = []

# Utility function to calculate
# perfect squares <= N
def calcPsquare(N):

    global psquare
    for i in range(1, int(sqrt(N)) + 1, 1):
        psquare.append(i * i)

# Recursive function to count
# number of ways to represent
# a number as a sum of perfect squares
def countWaysUtil(index, target):

    global dp

    # Handle base cases
    if (target == 0):
        return 1
    if (index < 0 or target < 0):
        return 0

    # If already computed, return the result
    if (dp[index][target] != -1):
        return dp[index][target]

    dp[index][target] = (countWaysUtil(
                               index, target - psquare[index]) +
                         countWaysUtil(index - 1, target))

    # Else, compute the result
    return dp[index][target]

# Function to find the number of ways to
# represent a number as a sum of perfect squares
def countWays(N):

    global dp
    global psquare

    # Precalculate perfect squares less
    # than or equal to N
    calcPsquare(N)
    temp = [-1 for i in range(N + 1)]

    # Create dp array to memoize
    dp = [temp for i in range(len(psquare) + 1)]

    # Function call to fill dp array
    return countWaysUtil(len(psquare) - 1, N) - 1

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 9

    # Function Call
    print(countWays(N))

# This code is contributed by ipg2016107
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Store perfect squares
// less than or equal to N
static List<int> psquare;

// Utility function to calculate
// perfect squares <= N
private static void calcPsquare(int n)
{
    for(int i = 1; i * i <= n; i++)
        psquare.Add(i * i);
}

// DP array for memoization
private static int[,]dp;

// Recursive function to count
// number of ways to represent
// a number as a sum of perfect squares
private static int countWaysUtil(int index,
                                 int target)
{

    // Handle base cases
    if (target == 0)
        return 1;
    if (index < 0 || target < 0)
        return 0;

    // If already computed, return the result
    if (dp[index, target] != -1)
        return dp[index, target];

    // Else, compute the result
    return dp[index, target] = countWaysUtil(index,
                                             target - psquare[index]) +
                               countWaysUtil(index - 1, target);
}

// Function to find the number of ways to
// represent a number as a sum of perfect squares
private static int countWays(int n)
{

    // Precalculate perfect squares less
    // than or equal to N
    psquare = new List<int>();
    calcPsquare(n);

    // Create dp array to memoize
    dp = new int[psquare.Count + 1, n + 1];
    for(int i = 0; i <= psquare.Count; i++)
    {
        for(int j = 0; j <= n; j++)
        {
            dp[i, j] = -1;
        }

        //Array.Fill(dp[i], -1);
    }

    // Function call to fill dp array
    return countWaysUtil(psquare.Count - 1, n);
}

// Driver Code
static void Main()
{

    // Given Input
    int N = 9;

    // Function Call
   Console.Write(countWays(N));
}
}

// This code is contributed by SoumikMondal
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

let psquare;

function calcPsquare(n)
{
     for (let i = 1; i * i <= n; i++)
            psquare.push(i * i);
}

 // DP array for memoization
let dp;

// Recursive function to count
    // number of ways to represent
    // a number as a sum of perfect squares
function countWaysUtil(index,target)
{
    // Handle base cases
        if (target == 0)
            return 1;
        if (index < 0 || target < 0)
            return 0;

        // If already computed, return the result
        if (dp[index][target] != -1)
            return dp[index][target];

        // Else, compute the result
        return dp[index][target]
               = countWaysUtil(
                     index, target - psquare[index])

                 + countWaysUtil(
                       index - 1, target);
}

// Function to find the number of ways to
    // represent a number as a sum of perfect squares
function countWays(n)
{
    // Precalculate perfect squares less
        // than or equal to N
        psquare = [];
        calcPsquare(n);

        // Create dp array to memoize
        dp = new Array(psquare.length+1);
        for(let i=0;i<psquare.length+1;i++)
        {
            dp[i]=new Array(n+1);
            for(let j=0;j<n+1;j++)
            {
                dp[i][j]=-1;
            }
        }

        // Function call to fill dp array
        return countWaysUtil(psquare.length - 1, n);
}

// Driver Code
// Given Input
let N = 9;

// Function Call
document.write(countWays(N));

// This code is contributed by patel2127

</script>
```

****Output**

```
4
```** 

*****时间复杂度:** O(K*N)，其中 K 为小于或等于 N 的完美方块数*
***辅助空间:** O(K*N)***