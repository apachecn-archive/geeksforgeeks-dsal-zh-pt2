# 将一个数字表示为两个数字之和的计数方式

> 原文:[https://www . geesforgeks . org/count-way-to-express-a-number-as-sum-of-two-numbers/](https://www.geeksforgeeks.org/count-ways-to-express-a-number-as-sum-of-exactly-two-numbers/)

给定正整数 **N** 。任务是找到将 N 表示为两个数字之和的方法数量 **A** 和 **B** (N = A + B)，其中 A > 0，B > 0 和 B > A

**示例:**

```
Input: N = 8
Output: 3
Explanation:
N = 8 can be expressed as (1, 7), (2, 6), (3, 5)

Input: N = 14
Output: 6 
```

**进场:**

*   这里的一个观察是，对于每一个数 N，如果我们取一个小于 N/2 的数 A，那么必然有一个大于 N/2 的数 B，A + B = N.

*   这就产生了一个简单的求 B 或 a 的计数的方法。因此，地板值(N-1)/2 将产生这个方法。

## C++

```
// C++ program to Count ways to
// express a number as sum of
// two numbers.
#include <bits/stdc++.h>
using namespace std;

// Function returns the count
// of ways express a number
// as sum of two numbers.
int CountWays(int n)
{
    int ans = (n - 1) / 2;

    return ans;
}

// Driver code
int main()
{
   int N = 8;

    cout << CountWays(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count ways to
// express a number as sum of
// two numbers.
class GFG{

// Function returns the count
// of ways express a number
// as sum of two numbers.
static int CountWays(int n)
{
    int ans = (n - 1) / 2;

    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 8;
    System.out.print(CountWays(N));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to Count ways to
# express a number as sum of
# two numbers.

# Function returns the count
# of ways express a number
# as sum of two numbers.
def CountWays(n) :
    ans = (n - 1) // 2
    return ans

# Driver code
N = 8
print(CountWays(N))

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# program to count ways to
// express a number as sum of
// two numbers.
using System;
class GFG{

// Function returns the count
// of ways express a number
// as sum of two numbers.
static int CountWays(int n)
{
    int ans = (n - 1) / 2;

    return ans;
}

// Driver code
public static void Main()
{
    int N = 8;
    Console.Write(CountWays(N));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count ways to
// express a number as sum of
// two numbers.

// Function returns the count
// of ways express a number
// as sum of two numbers.
function CountWays(n)
{
    let ans = Math.floor((n - 1) / 2);

    return ans;
}

// Driver Code

    let N = 8;
    document.write(CountWays(N));

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)