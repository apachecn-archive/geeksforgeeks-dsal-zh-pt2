# 二进制字符串中的最大分割，这样每个子字符串都可以被给定的奇数除尽

> 原文:[https://www . geesforgeks . org/maximum-splits-in-binary-string-so-每个子串都可以被给定的奇数除尽/](https://www.geeksforgeeks.org/maximum-splits-in-binary-string-such-that-each-substring-is-divisible-by-given-odd-number/)

给定二进制字符串 **str** ，任务是计算最大可能的拆分，使每个子字符串可以被给定的奇数 **K** 整除。
**例:**

> **输入:** str = "110111001 "，K = 9
> **输出:** 2
> **解释:**
> 两个可能的子串分别是“11011”和“1001”。等价的十进制值分别是 27 和 9，它们可以被 9 整除。
> **输入:** str = "10111001 "，K = 5
> **输出:** 2
> **解释:**
> 两个可能的子串分别是“101”和“11001”。等价的十进制值分别是 5 和 25，它们可以被 5 整除。

**方法:**为了解决这个问题，我们从字符串的末尾开始遍历，并生成遍历长度的总和。一旦总和被 **K** 整除，我们将**计数**增加 1，并将**总和**重置为 0，向前遍历并重复相同的过程。在字符串的整个遍历中，如果**和**已被重置为 0，则**计数的值**给出所需的最大可能拆分。否则，打印*“不可能”*，因为所有线段都不能被 **K** 整除。
以下代码是上述方法的实现:

## C++

```
// C++ Program to split
// a given binary string
// into maximum possible
// segments divisible by
// given odd number K

#include <bits/stdc++.h>
using namespace std;
// Function to calculate
// maximum splits possible
void max_segments(string str, int K)
{
    int n = str.length();
    int s = 0, sum = 0, count = 0;
    for (int i = n - 1; i >= 0; i--) {
        int a = str[i] - '0';
        sum += a * pow(2, s);

        s++;
        if (sum != 0 && sum % K == 0) {
            count++;
            sum = 0;
            s = 0;
        }
    }
    if (sum != 0)
        cout << "-1" << endl;
    else
        cout << count << endl;
}

// Driver code
int main()
{
    string str = "10111001";
    int K = 5;
    max_segments(str, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to split a given
// binary string into maximum
// possible segments divisible
// by given odd number K
import java.io.*;
import java.util.*;

class GFG{

// Function to calculate
// maximum splits possible
static void rearrange(String str, int K)
{
    int n = str.length();
    int s = 0, sum = 0, count = 0;

    for(int i = n - 1; i >= 0; i--)
    {
       int a = str.charAt(i) - '0';
       sum += a * Math.pow(2, s);
       s++;

       if (sum != 0 && sum % K == 0)
       {
           count++;
           sum = 0;
             s = 0;
       }
    }

    if (sum != 0)
        System.out.println("-1");   
    else
        System.out.println(count);
}

// Driver code
public static void main(String[] args)
{
    String str = "10111001";
    int K = 5;

    rearrange(str, K);
}
}

// This code is contributed by coder001
```

## 蟒蛇 3

```
# Python3 program to split
# a given binary string
# into maximum possible
# segments divisible by
# given odd number K

# Function to calculate
# maximum splits possible
def max_segments(st, K):

    n = len(st)
    s, sum, count = 0, 0, 0

    for i in range(n - 1, -1, -1):
        a = ord(st[i]) - 48
        sum += a * pow(2, s)
        s += 1

        if (sum != 0 and sum % K == 0):
            count += 1
            sum = 0
            s = 0

    if (sum != 0):
        print("-1")
    else:
        print(count)

# Driver code
if __name__ == "__main__":

    st = "10111001"
    K = 5
    max_segments(st, K)

# This code is contributed by chitranayal
```

## C#

```
// C# program to split a given
// binary string into maximum
// possible segments divisible by
// given odd number K
using System;

class GFG{

// Function to calculate
// maximum splits possible
static void max_segments(string str, int K)
{
    int n = str.Length;
    int s = 0;
    int sum = 0;
    int count = 0;

    for(int i = n - 1; i >= 0; i--)
    {
       int a = str[i] - '0';
       sum += a * (int)Math.Pow(2, s);
       s++;

       if (sum != 0 && sum % K == 0)
       {
           count++;
           sum = 0;
             s = 0;
       }
    }
    if (sum != 0)
    {
        Console.Write("-1");
    }
    else
    {
        Console.Write(count);
    }
}

// Driver code
public static void Main()
{
    string str = "10111001";
    int K = 5;

    max_segments(str, K);
}
}

// This code is contributed by sayesha   
```

## java 描述语言

```
<script>

// Javascript code to split a given
// binary string into maximum
// possible segments divisible
// by given odd number K

// Function to calculate
// maximum splits possible
function rearrange(str , K)
{
    var n = str.length;
    var s = 0, sum = 0, count = 0;

    for(var i = n - 1; i >= 0; i--)
    {
       var a = str.charAt(i) - '0';
       sum += a * Math.pow(2, s);
       s++;

       if (sum != 0 && sum % K == 0)
       {
           count++;
           sum = 0;
             s = 0;
       }
    }

    if (sum != 0)
        document.write("-1");   
    else
        document.write(count);
}

// Driver code
var str = "10111001";
var K = 5;

rearrange(str, K);

// This code contributed by shikhasingrajput

</script>
```

**Output:** 

```
2
```

时间复杂度:0(n)

辅助空间:0(1)