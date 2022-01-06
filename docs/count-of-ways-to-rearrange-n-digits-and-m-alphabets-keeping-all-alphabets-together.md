# 重新排列 N 位数字和 M 个字母的方法计数，将所有字母保持在一起

> 原文:[https://www . geeksforgeeks . org/重新排列 n 位和 m 位字母的方法计数-将所有字母保留在一起/](https://www.geeksforgeeks.org/count-of-ways-to-rearrange-n-digits-and-m-alphabets-keeping-all-alphabets-together/)

给定两个正整数 **N** 和 **M** ，分别表示一个[字符串](https://www.geeksforgeeks.org/string-data-structure/)中不同数字和字母的计数，计数的任务是重新排列字符串中的字符，使所有字母相邻。

**示例:**

> **输入:** N = 2，M = 2
> **输出:** 12
> **解释:**重新排列字符串中的字符使所有字母相邻的可能方法:{ { N<sub>1</sub>N<sub>2</sub>M<sub>2</sub>M<sub>1</sub>，N<sub>2</sub>N<sub>1</sub>M<sub>2</sub>M N<sub>2</sub>N<sub>1</sub>M<sub>1</sub>M<sub>2</sub>，N<sub>1</sub>N<sub>2</sub>M<sub>1</sub>M<sub>2</sub>，M<sub>2</sub>M<sub>1</sub>N<sub>1</sub>N<sub>2</sub>，M <sub>M<sub>1</sub>M<sub>2</sub>N<sub>1</sub>N<sub>2</sub>，M<sub>2</sub>M<sub>1</sub>N<sub>2</sub>N<sub>1</sub>，N<sub>1</sub>M<sub>1</sub>M<sub>2 N<sub>1</sub>M<sub>2</sub>M<sub>1</sub>N<sub>2</sub>，N<sub>2</sub>M<sub>2</sub>M<sub>1</sub>N<sub>1</sub>}。</sub></sub>
> 
> **输入:** N = 2，M = 4
> T3】输出: 144

**天真方法:**解决这个问题最简单的方法是制作一个由 **N** 个不同的数字字符和 **M** 个不同的字母组成的字符串。现在，[生成字符串的所有可能排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)并检查字符串的所有字母是否相邻。如果发现为真，则增加计数。最后，打印获得的计数。

***时间复杂度:** O((N + M)！)*
***辅助空间:** O(N + M)*

**有效方法:**可以根据以下观察结果解决问题:

> 由于所有字母都是相邻的，因此将所有字母视为一个字符。
> 因此，通过将所有字母考虑到一个字符来重新排列字符串的方法总数= ((N + 1)！)* (M！)

按照以下步骤解决问题:

1.  [计算 **N + 1** 的阶乘](https://www.geeksforgeeks.org/program-for-factorial-of-a-number/)说， **X** 和 **M** 的阶乘说， **Y** 。
2.  最后打印 **(X * Y)** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to find the factorial
// of the given number
int fact(int n)
{
    int ans = 1;

    for(int i = 2; i <= n; i++)
        ans = ans * i;
    return ans;
}

// Function to count ways to rearrange
// characters of the string such that
// all alphabets are adjacent.
int findComb(int N, int M)
{

    // Stores factorial of (N + 1)
    int x = fact(N + 1);

    // Stores factorial of
    int y = fact(M);
    return (x * y);

}

// Driver Code
int main()
{

// Given a and b
int N = 2;
int M = 2;// Function call
cout<<findComb(N, M);
}

// This code is contributed by ipg2016107
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the factorial
// of the given number
static int fact(int n)
{
    int ans = 1;

    for(int i = 2; i <= n; i++)
        ans = ans * i;

    return ans;
}

// Function to count ways to rearrange
// characters of the String such that
// all alphabets are adjacent.
static int findComb(int N, int M)
{

    // Stores factorial of (N + 1)
    int x = fact(N + 1);

    // Stores factorial of
    int y = fact(M);
    return (x * y);
}

// Driver Code
public static void main(String[] args)
{

    // Given a and b
    int N = 2;
    int M = 2;

    // Function call
    System.out.print(findComb(N, M));
}
}

// This code is contributed by umadevi9616
```

## 蟒蛇 3

```
# Python program of the above approach

import math

# Function to find the factorial
# of the given number

def fact(a):
    return math.factorial(a)

# Function to count ways to rearrange
# characters of the string such that
# all alphabets are adjacent.
def findComb(N, M):

    # Stores factorial of (N + 1)
    x = fact(N + 1)

    # Stores factorial of
    y = fact(M)
    return (x * y)

# Driver Code
if __name__ == "__main__":

    # Given a and b
    N = 2
    M = 2

    # Function call
    print(findComb(N, M))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{
    // Function to find the factorial
// of the given number
static int fact(int n)
{
    int ans = 1;

    for(int i = 2; i <= n; i++)
        ans = ans * i;
    return ans;
}

// Function to count ways to rearrange
// characters of the string such that
// all alphabets are adjacent.
static int findComb(int N, int M)
{

    // Stores factorial of (N + 1)
    int x = fact(N + 1);

    // Stores factorial of
    int y = fact(M);
    return (x * y);

}

// Driver Code
public static void Main()
{

// Given a and b
int N = 2;
int M = 2;// Function call
Console.Write(findComb(N, M));

}
}

// This code is contributed by bgangwar59.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the factorial
        // of the given number
        function fact(n)
        {
            var ans = 1;

            for (var i = 2; i <= n; i++)
                ans = ans * i;
            return ans;
        }

        // Function to count ways to rearrange
        // characters of the string such that
        // all alphabets are adjacent.
        function findComb(N, M)
        {

            // Stores factorial of (N + 1)
            var x = fact(N + 1)

            // Stores factorial of
            var y = fact(M)
            return (x * y)

        }

        // Driver Code

        // Given a and b
        var N = 2
        var M = 2

        // Function call
        document.write(findComb(N, M))

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
12
```

***时间复杂度:** O(N + M)*
***辅助空间:** O(1)*