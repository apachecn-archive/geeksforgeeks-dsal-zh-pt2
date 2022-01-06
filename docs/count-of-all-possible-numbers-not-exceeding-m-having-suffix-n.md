# 不超过 M 的所有可能数字的计数，后缀为 N

> 原文:[https://www . geesforgeks . org/count-of-all-可能的数字-不超过-m-having-后缀-n/](https://www.geeksforgeeks.org/count-of-all-possible-numbers-not-exceeding-m-having-suffix-n/)

给定两个正整数 **N** 和 **M** ，任务是找出范围**【1，M】**内所有可能数字的计数，后缀为 **N** 。

**示例:**

> **输入:** N = 5，M = 15
> **输出:** 2
> **说明:**只有满足条件的数字才是{5，15}。
> **输入:** N = 25，M = 4500
> **输出** : 45

**天真方法:**最简单的方法是遍历**【1，M】**范围内的所有整数，检查后缀是否为 **N** 。
***时间复杂度:** O(M)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，需要进行以下观察:

> 设 **N** = 5 和 **M** = 100
> 后缀数为 5，15，25，35…95，组成**等差数列**第一项= 5，最后一项= 95，公差= N 的基数(如:6 有基数 10，45 有基数 100，这不过是形式 10 的幂运算 <sup>digitsOf(N)</sup> ，其中 digitsOf(N) =

因此，为了计算[1，M]范围内的可能数的计数，需要计算以下表达式:

> 数的计数=数列中的项数=**(t<sub>n</sub>–a)/d+1**，其中
> **t <sub>n</sub>** 为数列的最后一项， **a** 为数列的第一项， **d** 为公差=**(t<sub>I+1</sub>–t<sub>I</sub>，i = 1，2，3…**

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>

using namespace std;

// Function to count the
// no. of digits of N
int digitsOf(int num)
{
    return to_string(num).size();
}

// Function to count all possible
// numbers having Suffix as N
int count(int a, int tn)
{
    // Difference of the A.P
    int diff = pow(10, digitsOf(a));

    // Count of the number of terms
    return ((tn - a) / diff) + 1;
}

// Driver Code
int main()
{

    int n, m;
    n = 25, m = 4500;
    cout << count(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to count the
// no. of digits of N
static int digitsOf(int num)
{
    return Integer.toString(num).length();
}

// Function to count all possible
// numbers having Suffix as N
static int count(int a, int tn)
{

    // Difference of the A.P
    int diff = (int)Math.pow(10, digitsOf(a));

    // Count of the number of terms
    return ((tn - a) / diff) + 1;
}

// Driver code
public static void main (String[] args)
{
    int n = 25, m = 4500;

    System.out.println(count(n, m));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to count the
# no. of digits of N
def digitsOf(num):
    return len(str(num));

# Function to count all possible
# numbers having Suffix as N
def count(a, tn):

    # Difference of the A.P
    diff = int(pow(10, digitsOf(a)));

    # Count of the number of terms
    return ((tn - a) / diff) + 1;

# Driver code
if __name__ == '__main__':
    n = 25; m = 4500;

    print(int(count(n, m)));

# This code is contributed by sapnasingh4991
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count the
// no. of digits of N
static int digitsOf(int num)
{
    return num.ToString().Length;
}

// Function to count all possible
// numbers having Suffix as N
static int count(int a, int tn)
{

    // Difference of the A.P
    int diff = (int)Math.Pow(10, digitsOf(a));

    // Count of the number of terms
    return ((tn - a) / diff) + 1;
}

// Driver code
public static void Main(String[] args)
{
    int n = 25, m = 4500;

    Console.WriteLine(count(n, m));
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to count the
// no. of digits of N
function digitsOf(num)
{
    return num.toString().length;
}

// Function to count all possible
// numbers having Suffix as N
function count(a, tn)
{

    // Difference of the A.P
    let diff = Math.floor(Math.pow(10, digitsOf(a)));

    // Count of the number of terms
    return Math.floor((tn - a) / diff) + 1;
}

// Driver Code

    let n = 25, m = 4500;

    document.write(count(n, m));

</script>
```

**Output:** 

```
45
```

***时间复杂度:** O(1)*
***辅助空间:** O(1)*