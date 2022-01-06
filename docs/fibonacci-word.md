# 斐波那契字

> 原文:[https://www.geeksforgeeks.org/fibonacci-word/](https://www.geeksforgeeks.org/fibonacci-word/)

像[斐波那契数字](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，一个[斐波那契字](https://en.wikipedia.org/wiki/Fibonacci_word)。是二进制数字(或任何两个字母的字母表中的符号)的特定序列。斐波那契字是通过重复连接形成的，就像斐波那契数是通过重复相加形成的一样。但与斐波那契数不同的是，斐波那契字的前两个术语互不相同。

```
In Fibonacci word,
  S(0) = 0, 
  S(1) = 01, 
  S(2) = 010,
  S(3) = 01001
   ..... 
where S(n) = S(n-1) + S(n-2) and + 
represents the concatenation of 
strings. 
```

任务是为给定的数字 n 找到第 n 个斐波那契字

```
Input : n = 4
Output : S(4) = 01001010

Input : n = 2
Output : S(2) = 010
```

就像在斐波那契数的程序中一样，我们在这里使用寻找第 n 个斐波那契数的迭代概念，对于寻找第 n 个斐波那契字，我们可以使用迭代概念。因此，为了找到第 n 个斐波那契字，我们将取两个字符串 Sn 和 Sn_1，分别表示 S(n)和 S(n-1)，在每次迭代中，我们将更新 tmp = Sn，Sn = Sn + Sn_1 和 Sn_1 = tmp，这样我们就可以找到第 n 个斐波那契字。

## C++

```
// program for nth Fibonacci word
#include<bits/stdc++.h>
using namespace std;

// Returns n-th Fibonacci word
string fibWord(int n)
{
    string Sn_1 = "0";
    string Sn = "01";
    string tmp;
    for (int i=2; i<=n; i++)
    {
        tmp = Sn;
        Sn += Sn_1;
        Sn_1 = tmp;
    }

    return Sn;
}

// driver program
int main()
{
    int n = 6;
    cout << fibWord(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for nth Fibonacci word
import java.util.*;

class Eulerian
{
    // Returns n-th Fibonacci word
    public static String fibWord(int n)
    {
        String Sn_1 = "0";
        String Sn = "01";
        String tmp;
        for (int i=2; i<=n; i++)
        {
            tmp = Sn;
            Sn += Sn_1;
            Sn_1 = tmp;
        }

        return Sn;
    }

    // driver code
    public static void main(String[] args)
    {
        int n = 6;
        System.out.print(fibWord(n));
    }
}

// This code is contributed by rishabh_jain
```

## 蟒蛇 3

```
# Python3 program for nth Fibonacci word

# Returns n-th Fibonacci word
def fibWord(n):
    Sn_1 = "0"
    Sn = "01"
    tmp = ""
    for i in range(2, n + 1):
        tmp = Sn
        Sn += Sn_1
        Sn_1 = tmp
    return Sn

# driver program
n = 6
print (fibWord(n))

# This code is contributed by Sachin Bisht
```

## C#

```
// C# program for nth Fibonacci word
using System;

class GFG
{
    // Returns n-th Fibonacci word
    public static String fibWord(int n)
    {
        String Sn_1 = "0";
        String Sn = "01";
        String tmp;
        for (int i = 2; i <= n; i++)
        {
            tmp = Sn;
            Sn += Sn_1;
            Sn_1 = tmp;
        }

        return Sn;
    }

    // Driver code
    public static void Main()
    {
        int n = 6;
        Console.WriteLine(fibWord(n));
    }
}

// This code is contributed by vt_m
```

## java 描述语言

```
<script>

// program for nth Fibonacci word

// Returns n-th Fibonacci word
function fibWord(n)
{
    var Sn_1 = "0";
    var Sn = "01";
    var tmp;
    for (var i = 2; i <= n; i++)
    {
        tmp = Sn;
        Sn += Sn_1;
        Sn_1 = tmp;
    }

    return Sn;
}

// driver program
var n = 6;
document.write( fibWord(n));

// This code is contributed by noob2000.
</script>
```

输出:

```
010010100100101001010
```