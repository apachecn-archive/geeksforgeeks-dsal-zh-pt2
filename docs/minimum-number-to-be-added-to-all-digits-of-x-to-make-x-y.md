# X 的所有数字相加的最小数，使 X > Y

> 原文:[https://www . geesforgeks . org/x-to-make-x-y 的所有数字的最小添加数/](https://www.geeksforgeeks.org/minimum-number-to-be-added-to-all-digits-of-x-to-make-x-y/)

给定两个相同长度的数字 **X** 和 **Y** ，任务是找出需要加到 **X** 所有数字上的最小数字 **d** ，使其大于 **Y** 。
**举例:**

> **输入:** X = 123，Y = 222
> **输出:** 1
> **解释:**
> 将 X
> 的所有数字加 1，那么 X 就变成了{2，3，4}，这在字典上比{2，2，2}大
> 。
> **输入:** X = 4512，Y = 2998
> **输出:** 0
> **解释:**
> X 在词典上已经比 Y 大了
> 所以答案会是 0。

**处理方式:**这个问题可以通过分解成三种情况
轻松解决

*   **情况 1:** 查找 X 在字典上是否已经大于 y，如果是，那么我们就不需要做任何事情。
*   **情况 2:** 否则将**(Y[0]–X[0])**添加到 X 的所有元素中，然后检查 X 在字典序上是否大于 Y。
*   **情况 3:** 如果还是不算大，那么答案就是**(Y[0]–X[0])+1**因为 X 的第一个元素变得比 Y 的第一个元素大就意味着 X[0] > Y[0]。

以下是上述方法的实现:

## C++

```
// C++ program to find Minimum number to be added
// to all digits of X to make X > Y

#include <bits/stdc++.h>
using namespace std;

// Function to check if X
// is lexicographically larger Y
bool IsLarger(int X[], int Y[], int n)
{
    for (int i = 0; i < n; i++) {

        // It is lexicographically larger
        if (X[i] < Y[i]) {
            return false;
        }
    }
    return true;
}

// Utility function to check
// minimum value of d
int solve(int X[], int Y[], int n)
{

    int ans = 0;
    // If X is already larger
    // do not need to add anything
    if (IsLarger(X, Y, n)) {
        ans = 0;
    }
    else {

        // Adding d to all elements of X
        int d = Y[0] - X[0];

        for (int i = 0; i < n; i++) {
            X[i] += d;
        }

        // If X is larger now
        // print d
        if (IsLarger(X, Y, n)) {
            ans = d;
        }
        // else print d + 1
        else {
            ans = d + 1;
        }
    }

    return ans;
}

// Driver Code
int main()
{

    // Taking the numbers as sequences
    int X[] = { 2, 3, 6, 9 };
    int Y[] = { 3, 4, 8, 1 };

    int n = sizeof(X) / sizeof(X[0]);
    cout << solve(X, Y, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Minimum number to be added
// to all digits of X to make X > Y
import java.util.*;

class GFG
{

    // Function to check if X
    // is lexicographically larger Y
    static boolean IsLarger(int[] X,
                            int[] Y, int n)
    {
        for (int i = 0; i < n; i++)
        {

            // It is lexicographically larger
            if (X[i] < Y[i])
            {
                return false;
            }
        }
        return true;
    }

    // Utility function to check
    // minimum value of d
    static int solve(int X[], int Y[], int n)
    {
        int ans = 0;

        // If X is already larger
        // do not need to add anything
        if (IsLarger(X, Y, n))
            ans = 0;
        else
        {

            // Adding d to all elements of X
            int d = Y[0] - X[0];

            for (int i = 0; i < n; i++)
                X[i] += d;

            // If X is larger now
            // print d
            if (IsLarger(X, Y, n))
                ans = d;

            // else print d + 1
            else
            {
                ans = d + 1;
            }
        }
        return ans;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Taking the numbers as sequences
        int X[] = { 2, 3, 6, 9 };
        int Y[] = { 3, 4, 8, 1 };

        int n = X.length;
        System.out.println(solve(X, Y, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find Minimum number to be added
# to all digits of X to make X > Y

# Function to check if X
# is lexicographically larger Y
def IsLarger(X, Y, n) :

    for i in range(n) :

        # It is lexicographically larger
        if (X[i] < Y[i]) :
            return False;

    return True;

# Utility function to check
# minimum value of d
def solve(X, Y, n) :

    ans = 0;

    # If X is already larger
    # do not need to add anything
    if (IsLarger(X, Y, n)) :
        ans = 0;

    else :

        # Adding d to all elements of X
        d = Y[0] - X[0];

        for i in range(n) :
            X[i] += d;

        # If X is larger now
        # print d
        if (IsLarger(X, Y, n)) :
            ans = d;
        # else print d + 1
        else :
            ans = d + 1;

    return ans;

# Driver Code
if __name__ == "__main__" :

    # Taking the numbers as sequences
    X = [ 2, 3, 6, 9 ];
    Y = [ 3, 4, 8, 1 ];

    n = len(X);
    print(solve(X, Y, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find Minimum number to be.Added
// to all digits of X to make X > Y
using System;

class GFG
{

    // Function to check if X
    // is lexicographically larger Y
    static bool IsLarger(int[] X,
                            int[] Y, int n)
    {
        for (int i = 0; i < n; i++)
        {

            // It is lexicographically larger
            if (X[i] < Y[i])
            {
                return false;
            }
        }
        return true;
    }

    // Utility function to check
    // minimum value of d
    static int solve(int []X, int []Y, int n)
    {
        int ans = 0;

        // If X is already larger
        // do not need to.Add anything
        if (IsLarger(X, Y, n))
            ans = 0;
        else
        {

            // Adding d to all elements of X
            int d = Y[0] - X[0];

            for (int i = 0; i < n; i++)
                X[i] += d;

            // If X is larger now
            // print d
            if (IsLarger(X, Y, n))
                ans = d;

            // else print d + 1
            else
            {
                ans = d + 1;
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Taking the numbers as sequences
        int []X = { 2, 3, 6, 9 };
        int []Y = { 3, 4, 8, 1 };

        int n = X.Length;
        Console.WriteLine(solve(X, Y, n));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// javascript program to find Minimum number to be added
// to all digits of X to make X > Y

// Function to check if X
// is lexicographically larger Y
function IsLarger(X, Y, n)
{
    for (let i = 0; i < n; i++) {

        // It is lexicographically larger
        if (X[i] < Y[i]) {
            return false;
        }
    }
    return true;
}

// Utility function to check
// minimum value of d
function solve(X, Y, n)
{

    let ans = 0;
    // If X is already larger
    // do not need to add anything
    if (IsLarger(X, Y, n)) {
        ans = 0;
    }
    else {

        // Adding d to all elements of X
        let d = Y[0] - X[0];

        for (let i = 0; i < n; i++) {
            X[i] += d;
        }

        // If X is larger now
        // print d
        if (IsLarger(X, Y, n)) {
            ans = d;
        }
        // else print d + 1
        else {
            ans = d + 1;
        }
    }

    return ans;
}

// Driver Code

    // Taking the numbers as sequences
    let X = [ 2, 3, 6, 9 ];
    let Y = [ 3, 4, 8, 1 ];

    let n = X.length;
    document.write(solve(X, Y, n));

// This code is contributed by souravmahato348.
</script>
```

**Output:** 

```
2
```

**时间复杂度:** ![O(N)   ](img/23f09f991be3459af525bfd21659fc83.png "Rendered by QuickLaTeX.com")，其中 N 为 X 或 Y 的长度