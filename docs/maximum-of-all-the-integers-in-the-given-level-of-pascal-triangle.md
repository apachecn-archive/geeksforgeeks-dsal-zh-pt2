# 帕斯卡三角形给定级别内所有整数的最大值

> 原文:[https://www . geesforgeks . org/给定帕斯卡三角中所有整数的最大值/](https://www.geeksforgeeks.org/maximum-of-all-the-integers-in-the-given-level-of-pascal-triangle/)

给定一个整数 **L** ，任务是在[帕斯卡三角形](https://www.geeksforgeeks.org/pascal-triangle/)中找到给定级别上所有整数的最大值。
6 层帕斯卡三角形如下图所示:

> 1
> 1 1
> 1 2 1
> 1 3 3 1
> 1 4 6 4 1
> 1 5 10 10 5 1

**示例:**

> **输入:**L = 3
> T3】输出: 3
> 0 <sup>th</sup> 级->T8】1T10】1<sup>ST</sup>级->T13】1 1T15】2<sup>nd</sup>级->T18】1 2 1T20】3<sup>rd</sup>级->T23】1
> 
> **输入:**L = 5
> T3】输出: 10

**方法:**众所周知，帕斯卡三角形中的每一行都是二项式系数，等级 **n** 的二项式展开中的 **k <sup>第</sup>T5】系数是**T9】nC<sub>k</sub>T13】。而且，任何级别的中间元素总是最大的，那就是 **k = floor(n / 2)** 。
因此，在帕斯卡三角形中给定级别存在的所有整数的最大值是**binomialcoffef(n，n / 2)** 。****

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function for the binomial coefficient
int binomialCoeff(int n, int k)
{
    int C[n + 1][k + 1];
    int i, j;

    // Calculate value of Binomial Coefficient
    // in bottom up manner
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= min(i, k); j++) {

            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously
            // stored values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }

    return C[n][k];
}

// Function to return the maximum
// value in the nth level
// of the Pascal's triangle
int findMax(int n)
{
    return binomialCoeff(n, n / 2);
}

// Driver code
int main()
{
    int n = 5;

    cout << findMax(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG
{
    // Function for the binomial coefficient
    static int binomialCoeff(int n, int k)
    {
        int [][] C = new int[n + 1][k + 1];
        int i, j;

        // Calculate value of Binomial Coefficient
        // in bottom up manner
        for (i = 0; i <= n; i++) {
            for (j = 0; j <= Math.min(i, k); j++) {

                // Base Cases
                if (j == 0 || j == i)
                    C[i][j] = 1;

                // Calculate value using previously
                // stored values
                else
                    C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
            }
        }

        return C[n][k];
    }

    // Function to return the maximum
    // value in the nth level
    // of the Pascal's triangle
    static int findMax(int n)
    {
        return binomialCoeff(n, n / 2);
    }

    // Driver code
    public static void main (String[] args) {

        int n = 5;

        System.out.println(findMax(n));

    }

}

// This code is contributed by ihritik
```

## C#

```
// C# implementation of the approach

using System;
class GFG
{
    // Function for the binomial coefficient
    static int binomialCoeff(int n, int k)
    {
        int [ , ] C = new int[n + 1, k + 1];
        int i, j;

        // Calculate value of Binomial Coefficient
        // in bottom up manner
        for (i = 0; i <= n; i++) {
            for (j = 0; j <= Math.Min(i, k); j++) {

                // Base Cases
                if (j == 0 || j == i)
                    C[i, j] = 1;

                // Calculate value using previously
                // stored values
                else
                    C[i, j] = C[i - 1, j - 1] + C[i - 1, j];
            }
        }

        return C[n, k];
    }

    // Function to return the maximum
    // value in the nth level
    // of the Pascal's triangle
    static int findMax(int n)
    {
        return binomialCoeff(n, n / 2);
    }

    // Driver code
    public static void Main () {

        int n = 5;

        Console.WriteLine(findMax(n));

    }

}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function for the binomial coefficient
def binomialCoeff(n, k):
    C = [[0 for i in range(k + 1)]
            for i in range(n + 1)]

    # Calculate value of Binomial Coefficient
    # in bottom up manner
    for i in range(n + 1):
        for j in range(min(i, k) + 1):

            # Base Cases
            if (j == 0 or j == i):
                C[i][j] = 1

            # Calculate value using previously
            # stored values
            else:
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j]

    return C[n][k]

# Function to return the maximum
# value in the nth level
# of the Pascal's triangle
def findMax(n):
    return binomialCoeff(n, n // 2)

# Driver code
n = 5

print(findMax(n))

# This code is contributed by Mohit Kumar
```

## java 描述语言

```
<script>
// Javascript implementation of the
// above approach

// Function for the binomial coefficient
function binomialCoeff(n, k)
{

    var C = new Array(n + 1);
    // Loop to create 2D array using 1D array
    for (var i = 0; i < C.length; i++) {
        C[i] = new Array(k + 1);
    }
    var i, j;

    // Calculate value of Binomial Coefficient
    // in bottom up manner
    for (i = 0; i <= n; i++) {
        for (j = 0; j <= Math.min(i, k); j++) {
            // Base Cases
            if (j == 0 || j == i)
                C[i][j] = 1;

            // Calculate value using previously
            // stored values
            else
                C[i][j] = C[i - 1][j - 1] + C[i - 1][j];
        }
    }

    return C[n][k];
}

// Function to return the maximum
// value in the nth level
// of the Pascal's triangle
function findMax(n)
{
    return binomialCoeff(n, Math.floor(n / 2));
}

// Driver code
var n = 5;
document.write(binomialCoeff(n, Math.floor(n / 2)));

// This code is contributed by ShubhamSingh10
</script>
```

**Output:** 

```
10
```