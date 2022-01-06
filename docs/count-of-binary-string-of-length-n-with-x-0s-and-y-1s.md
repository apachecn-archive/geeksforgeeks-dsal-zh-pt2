# 长度为 N、X 为 0、Y 为 1 的二进制字符串的计数

> 原文:[https://www . geesforgeks . org/count-of-binary-string-length-n-with-x-0s-and-y-1s/](https://www.geeksforgeeks.org/count-of-binary-string-of-length-n-with-x-0s-and-y-1s/)

给定正积分 **N** 、 **X** 和 **Y** 。任务是找到长度为 N 的**唯一的**二进制字符串的计数，这些字符串具有**X 0**和 **Y 1** s。

**示例:**

> **输入:** N=5，X=3，Y=2
> **输出:** 10
> **说明:**有 10 个长度为 5 的二进制字符串，有 3 个 0 和 2 个 1，如:
> 00011，00101，01001，10001，00110，01010，01100，10100，11000。
> 
> **输入:** N=3，X=1，Y=2
> **输出:** 3
> **说明:**有 3 个长度为 3 的二进制字符串，有 1 个 0 和 2 个 1，如:011，101，110

**天真的做法**:生成**所有长度为 N 的二进制字符串**，然后统计带有 X ^ 0 和 Y ^ 1 的字符串个数。
**时间复杂度:** O(2 <sup>N</sup> )
**辅助空间:** O(2 <sup>N</sup>

**更好的逼近**:这个问题也可以用 [**组合学**](https://www.geeksforgeeks.org/combinatorics-gq/) 来解决。如果长度是 N，给定的是 X ^ 0，那么会有 Y =(N–X)1。所以我们可以认为这是一个 N 长度的字符串，有 X 0s 和 Y ^ 1。我们需要找到这个的独特组合的数量，这可以作为 _{X}^{N}\textrm{C}或 _{Y}^{N}\textrm{C}.获得这可以使用 [**帕斯卡三角形**](https://www.geeksforgeeks.org/calculate-ncr-using-pascals-triangle/) 来计算组合的值。
**时间复杂度:** O(N)
**空间复杂度:** O(N <sup>2</sup> )
**注意:**如果对 X 和 y 有多个查询，这种方法是最好的，那么它也将具有相同的时间和空间复杂度。

**空间优化方法**:如果我们借助公式 _{X}^{N}\textrm{C} = N，可以优化上述方法中的空间消耗！/(X！*(N-X)！)并使用阶乘计算值。

下面是上述方法的实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to calculate factorial
long long int fact(int f)
{
    f++;
    long long int ans = 1;

    // Loop to calculate factorial of f
    while (--f > 0)
        ans = ans * f;
    return ans;
}

// Function to calculate combination nCr
long long int countWays(int N, int X, int Y)
{
    return (fact(N) / (fact(X) * fact(Y)));
}

// Driver code
int main()
{
    int N = 5, X = 3, Y = 2;
    cout << countWays(N, X, Y) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG{

    // Function to calculate factorial
    static int fact(int f)
    {
        f++;
        int ans = 1;

        // Loop to calculate factorial of f
        while (--f > 0)
            ans = ans * f;
        return ans;
    }

    // Function to calculate combination nCr
    static int countWays(int N, int X, int Y)
    {
        return (fact(N) / (fact(X) * fact(Y)));
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 5, X = 3, Y = 2;
        System.out.println(countWays(N, X, Y));
    }
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Function to calculate factorial
def fact(f):
  ans = 1;

  # Loop to calculate factorial of f
  while (f):
    ans = ans * f;
    f -= 1

  return ans;

# Function to calculate combination nCr
def countWays(N, X, Y):
  return fact(N) // (fact(X) * fact(Y));

# Driver code
N = 5
X = 3
Y = 2
print(countWays(N, X, Y))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate factorial
static int fact(int f)
{
    f++;
    int ans = 1;

    // Loop to calculate factorial of f
    while (--f > 0)
        ans = ans * f;
    return ans;
}

// Function to calculate combination nCr
static int countWays(int N, int X, int Y)
{
    return (fact(N) / (fact(X) * fact(Y)));
}

// Driver Code
public static void Main()
{
    int N = 5, X = 3, Y = 2;
    Console.Write(countWays(N, X, Y));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>
// Function to calculate factorial
function fact(f) {
  f++;
  let ans = 1;

  // Loop to calculate factorial of f
  while (--f > 0)
    ans = ans * f;
  return ans;
}

// Function to calculate combination nCr
function countWays(N, X, Y) {
  return Math.floor(fact(N) / (fact(X) * fact(Y)));
}

// Driver code
let N = 5, X = 3, Y = 2;
document.write(countWays(N, X, Y))

// This code is contributed by saurabh_jaiswal.
</script>
```

**Output**

```
10
```

**时间复杂度:** O(N)
**辅助空间:** O(1)
**注意:**在多个(Q)查询的情况下，这种方法将具有时间复杂度 O(Q*N)。