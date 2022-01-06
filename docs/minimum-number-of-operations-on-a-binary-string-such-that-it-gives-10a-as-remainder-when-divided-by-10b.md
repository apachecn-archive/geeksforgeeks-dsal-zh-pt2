# 二进制字符串上的最小运算次数，这样当被 10^B 除时，10^A 就是余数

> 原文:[https://www . geeksforgeeks . org/二进制字符串的最小操作数，以便在除以 10b 时给出 10a 作为余数/](https://www.geeksforgeeks.org/minimum-number-of-operations-on-a-binary-string-such-that-it-gives-10a-as-remainder-when-divided-by-10b/)

给定一个长度为 **N** 的二进制字符串**和两个整数 **A** 和 **B** ，使得 **0 ≤ A < B < n** 。任务是计算钻柱上的最小操作次数，使其在除以 10 <sup>B</sup> 时得出 10 <sup>A</sup> 作为余数。操作是指将 **1** 变为 **0** 或 **0** 变为 **1** 。**

**示例:**

> **输入:** str = "1001011001 "，A = 3，B = 6
> **输出:**2
> 2 次运算后的字符串为 1001001000。
> 1001001000% 10<sup>6</sup>= 10<sup>3</sup>
> 
> **输入:** str = "11010100101 "，A = 1，B = 5
> **输出:** 3

**方法:**为了让数字在除以 **10 <sup>B</sup>** 时给出**10<sup>A</sup>T5】作为余数，字符串的最后一个 **B** 数字必须是 **0** ，除了从最后一个应该是 **1** 的 **(A + 1) <sup>第</sup>** 位置的数字。因此，检查字符串的最后一个 **B** 数字是否符合上述条件，并为每个不匹配的数字增加 1。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// of operations on a binary string such that
// it gives 10^A as remainder when divided by 10^B
int findCount(string s, int n, int a, int b)
{
    // Initialize result
    int res = 0;

    // Loop through last b digits
    for (int i = 0; i < b; i++) {
        if (i == a)
            res += (s[n - i - 1] != '1');
        else
            res += (s[n - i - 1] != '0');
    }

    return res;
}

// Driver code
int main()
{
    string str = "1001011001";
    int N = str.size();
    int A = 3, B = 6;

    cout << findCount(str, N, A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the minimum number
    // of operations on a binary string such that
    // it gives 10^A as remainder when divided by 10^B
    static int findCount(String s, int n, int a, int b)
    {
        // Initialize result
        int res = 0;
        char []s1 = s.toCharArray();

        // Loop through last b digits
        for (int i = 0; i < b; i++)
        {

            if (i == a)
            {
                if (s1[n - i - 1] != '1')
                    res += 1;
            }
            else
            {
                if (s1[n - i - 1] != '0')
                        res += 1 ;
            }

        }

        return res;
    }

    // Driver code
    static public void main (String []args)
    {

        String str = "1001011001";
        int N = str.length() ;
        int A = 3, B = 6;

        System.out.println(findCount(str, N, A, B));

    }
}

// This code is contributed by ChitraNayal
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the minimum number
# of operations on a binary string such that
# it gives 10^A as remainder when divided by 10^B
def findCount(s, n, a, b):
    # Initialize result
    res = 0

    # Loop through last b digits
    for i in range(b):
        if (i == a):
            res += (s[n - i - 1] != '1')
        else:
            res += (s[n - i - 1] != '0')

    return res

# Driver code
if __name__ == '__main__':
    str = "1001011001"
    N = len(str)
    A = 3
    B = 6

    print(findCount(str, N, A, B))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the minimum number
    // of operations on a binary string such that
    // it gives 10^A as remainder when divided by 10^B
    static int findCount(string s, int n, int a, int b)
    {
        // Initialize result
        int res = 0;

        // Loop through last b digits
        for (int i = 0; i < b; i++)
        {

            if (i == a)
            {
                if (s[n - i - 1] != '1')
                    res += 1;
            }
            else
            {
                if (s[n - i - 1] != '0')
                        res += 1 ;
            }

        }

        return res;
    }

    // Driver code
    static public void Main ()
    {

        string str = "1001011001";
        int N = str.Length ;
        int A = 3, B = 6;

        Console.WriteLine(findCount(str, N, A, B));

    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum number
// of operations on a binary string such that
// it gives 10^A as remainder when divided by 10^B
function findCount(s, n, a, b)
{

    // Initialize result
    var res = 0;

    // Loop through last b digits
    for(var i = 0; i < b; i++)
    {
        if (i == a)
            res += (s[n - i - 1] != '1');
        else
            res += (s[n - i - 1] != '0');
    }
    return res;
}

// Driver code
var str = "1001011001";
var N = str.length;
var A = 3, B = 6;

document.write(findCount(str, N, A, B));

// This code is contributed by itsok

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(N)

**辅助空间:** O(N)