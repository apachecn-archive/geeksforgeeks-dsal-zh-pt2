# 给定字符串的每个可能长度的不同排列的计数

> 原文:[https://www . geeksforgeeks . org/给定字符串的每个可能长度的不同排列计数/](https://www.geeksforgeeks.org/count-of-distinct-permutations-of-every-possible-length-of-given-string/)

给定一个字符串 **S，**的任务是计算给定字符串的每个可能长度的不同排列。

**注意:**字符串中不允许重复字符。

> **输入:** S = "abc"
> **输出:** 15
> **解释:**
> 每个长度的可能排列有:
> {“a”、“b”、“c”、“ab”、“bc”、“ac”、“ba”、“ca”、“cb”、“abc”、“acb”、“bac”、“bca”、“cab”、“CBA”}
> 
> **输入:**S = " xz "
> T3】输出: 4

**方法:**想法是找到字符串的每个可能长度的组合的计数，它们的总和是不同长度的可能的不同排列的总数。因此，对于 N 长度的字符串，不同长度的不同排列的总数是:

> 可能的组合总数:<sup>n</sup>P<sub>1</sub>+<sup>n</sup>P<sub>2</sub>+<sup>n</sup>P<sub>3</sub>+<sup>n</sup>P<sub>4</sub>+……+<sup>n</sup>P<sub>n</sub>

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
#include <iostream>
using namespace std;

// Function to find the factorial
// of a number
int fact(int a)
{
    int i, f = 1;

    // Loop to find the factorial
    // of the given number
    for (i = 2; i <= a; i++)
        f = f * i;
    return f;
}

// Function to find the number
// of permutations possible
// for a given string
int permute(int n, int r)
{
    int ans = 0;
    ans = (fact(n) / fact(n - r));
    return ans;
}

// Function to find the total
// number of combinations possible
int findPermutations(int n)
{
    int sum = 0, P;
    for (int r = 1; r <= n; r++) {
        P = permute(n, r);
        sum = sum + P;
    }
    return sum;
}

// Driver Code
int main()
{
    string str = "xz";
    int result, n;
    n = str.length();

    cout << findPermutations(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG{

// Function to find the factorial
// of a number
static int fact(int a)
{
    int i, f = 1;

    // Loop to find the factorial
    // of the given number
    for(i = 2; i <= a; i++)
        f = f * i;

    return f;
}

// Function to find the number
// of permutations possible
// for a given String
static int permute(int n, int r)
{
    int ans = 0;
    ans = (fact(n) / fact(n - r));
    return ans;
}

// Function to find the total
// number of combinations possible
static int findPermutations(int n)
{
    int sum = 0, P;
    for(int r = 1; r <= n; r++)
    {
        P = permute(n, r);
        sum = sum + P;
    }
    return sum;
}

// Driver Code
public static void main(String[] args)
{
    String str = "xz";
    int result, n;
    n = str.length();

    System.out.print(findPermutations(n));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the factorial
# of a number
def fact(a):

    f = 1

    # Loop to find the factorial
    # of the given number
    for i in range(2, a + 1):
        f = f * i

    return f

# Function to find the number
# of permutations possible
# for a given string
def permute(n, r):

    ans = 0
    ans = fact(n) // fact(n - r)

    return ans

# Function to find the total
# number of combinations possible
def findPermutations(n):

    sum = 0
    for r in range(1, n + 1):
        P = permute(n, r)
        sum = sum + P

    return sum

# Driver Code
str = "xz"
n = len(str)

# Function call
print(findPermutations(n))

# This code is contributed by Shivam Singh
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG{

// Function to find the factorial
// of a number
static int fact(int a)
{
    int i, f = 1;

    // Loop to find the factorial
    // of the given number
    for(i = 2; i <= a; i++)
        f = f * i;

    return f;
}

// Function to find the number
// of permutations possible
// for a given String
static int permute(int n, int r)
{
    int ans = 0;
    ans = (fact(n) / fact(n - r));
    return ans;
}

// Function to find the total
// number of combinations possible
static int findPermutations(int n)
{
    int sum = 0, P;
    for(int r = 1; r <= n; r++)
    {
        P = permute(n, r);
        sum = sum + P;
    }
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "xz";
    int n;
    n = str.Length;

    Console.Write(findPermutations(n));
}
}

// This code is contributed by amal kumar choubey
```

## java 描述语言

```
<script>

// Javascript implementation of the
// above approach

// Function to find the factorial
// of a number
function fact(a)
{
    var i, f = 1;

    // Loop to find the factorial
    // of the given number
    for (i = 2; i <= a; i++)
        f = f * i;
    return f;
}

// Function to find the number
// of permutations possible
// for a given string
function permute(n, r)
{
    var ans = 0;
    ans = (fact(n) / fact(n - r));
    return ans;
}

// Function to find the total
// number of combinations possible
function findPermutations(n)
{
    var sum = 0, P;
    for (var r = 1; r <= n; r++) {
        P = permute(n, r);
        sum = sum + P;
    }
    return sum;
}

// Driver Code
var str = "xz";
var result, n;
n = str.length;
document.write( findPermutations(n));

</script>
```

**Output:** 

```
4
```