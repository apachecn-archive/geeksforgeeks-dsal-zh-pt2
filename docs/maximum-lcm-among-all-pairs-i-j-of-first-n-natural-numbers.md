# 前 N 个自然数的所有对(I，j)中的最大 LCM

> 原文:[https://www . geesforgeks . org/maximum-LCM-all-pairs-I-j-of-first-n-natural-numbers/](https://www.geeksforgeeks.org/maximum-lcm-among-all-pairs-i-j-of-first-n-natural-numbers/)

给定一个正整数 **N > 1** ，任务是在所有对 **(i，j)** 中找到最大 [LCM](https://www.geeksforgeeks.org/lcm-gq/) ，使得 **i < j ≤ N** 。
**举例:**

> **输入:** N = 3
> **输出:** 6
> LCM(1，2) = 2
> LCM(1，3) = 3
> LCM(2，3) = 6
> **输入:** N = 4
> **输出:** 12

**方法:**由于两个连续元素的 LCM 等于它们的倍数，那么很明显最大 LCM 将是一对 **(N，N–1)**，即**(N *(N–1))**。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum LCM
// among all the pairs(i, j) of
// first n natural numbers
int maxLCM(int n)
{
    return (n * (n - 1));
}

// Driver code
int main()
{
    int n = 3;

    cout << maxLCM(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the maximum LCM
// among all the pairs(i, j) of
// first n natural numbers
static int maxLCM(int n)
{
    return (n * (n - 1));
}

// Driver code
public static void main(String[] args)
{
    int n = 3;

    System.out.println(maxLCM(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum LCM
# among all the pairs(i, j) of
# first n natural numbers
def maxLCM(n) :

    return (n * (n - 1));

# Driver code
if __name__ == "__main__" :

    n = 3;

    print(maxLCM(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the maximum LCM
// among all the pairs(i, j) of
// first n natural numbers
static int maxLCM(int n)
{
    return (n * (n - 1));
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;

    Console.WriteLine(maxLCM(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum LCM
// among all the pairs(i, j) of
// first n natural numbers
function maxLCM(n)
{
    return (n * (n - 1));
}

// Driver code
var n = 3;
document.write(maxLCM(n));

</script>
```

**Output:** 

```
6
```

**时间复杂度:** O(1)