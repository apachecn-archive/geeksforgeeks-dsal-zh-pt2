# 计算给定长度 N 的特殊字符串的数量

> 原文:[https://www . geesforgeks . org/count-给定长度的特殊字符串数-n/](https://www.geeksforgeeks.org/count-the-number-of-special-strings-of-a-given-length-n/)

给定字符串的**长度 N** ，我们必须找到长度 N 的特殊字符串的数量。
如果一个字符串只由**小写字母 A 和 b** 组成，并且**在字符串**的两个 A 之间至少有一个 b，则该字符串称为特殊字符串。由于字符串的数量可能非常大，因此以 10^9+7.为模打印
**示例:**

> **输入:** N = 2
> **输出:** 3
> **解释:**
> 特殊串 so 长度 2 的个数为 3 即“ab”、“ba”、“bb”
> **输入:** N = 3
> **输出:** 5
> **解释:**
> 特殊串 so 长度 3 的个数为 5 即“abb”、“aba”、“bab”、“bba”、“BBA”

**方法:**
要解决上面提到的问题，首先观察到的是，如果整数 N 是 0，那么只能有一个空字符串作为答案，如果 N 是 1，那么可以有两个字符串“a”或“b”作为答案，但是如果 N 的值大于 1，那么答案等于前面两个项的和。现在为了找到特殊字符串的计数，我们运行一个循环，对于每个整数，长度为 I 的特殊字符串的计数等于长度为 i-1 的特殊字符串的计数和长度为 i-2 的特殊字符串的计数之和。将每个整数的值存储在数组中，并返回所需的答案。
以下是上述办法的实施:

## C++

```
// C++ Program to Count the number
// of Special Strings of a given length N
#include <bits/stdc++.h>
using namespace std;
#define mod 1000000007

// Function to return count of special strings
long count_special(long n)
{
    // stores the answer for a
    // particular value of n
    long fib[n + 1];

    // for n = 0 we have empty string
    fib[0] = 1;

    // for n = 1 we have
    // 2 special strings
    fib[1] = 2;

    for (int i = 2; i <= n; i++) {

        // calculate count of special string of length i
        fib[i] = (fib[i - 1] % mod + fib[i - 2] % mod) % mod;
    }

    // fib[n] stores the count
    // of special strings of length n
    return fib[n];
}

// Driver code
int main()
{

    // initialise n
    long n = 3;

    cout << count_special(n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number of
// special strings of a given length N
import java.util.*;

class GFG{

static final int mod = 1000000007;

// Function to return count of
// special Strings
static int count_special(int n)
{

    // Stores the answer for a
    // particular value of n
    int []fib = new int[n + 1];

    // For n = 0 we have empty String
    fib[0] = 1;

    // For n = 1 we have
    // 2 special Strings
    fib[1] = 2;

    for(int i = 2; i <= n; i++)
    {

       // Calculate count of special
       // String of length i
       fib[i] = (fib[i - 1] % mod +
                 fib[i - 2] % mod) % mod;
    }

    // fib[n] stores the count of
    // special Strings of length n
    return fib[n];
}

// Driver code
public static void main(String[] args)
{

    // Initialise n
    int n = 3;

    System.out.print(count_special(n) + "\n");
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to count the number
# of special strings of a given length N
mod = 1000000007

# Function to return count of
# special strings
def count_special(n):

    # Stores the answer for a
    # particular value of n
    fib = [0 for i in range(n + 1)]

    # For n = 0 we have empty string
    fib[0] = 1

    # For n = 1 we have
    # 2 special strings
    fib[1] = 2

    for i in range(2, n + 1, 1):

        # Calculate count of special
        # string of length i
        fib[i] = (fib[i - 1] % mod +
                  fib[i - 2] % mod) % mod

    # fib[n] stores the count
    # of special strings of length n
    return fib[n]

# Driver code
if __name__ == '__main__':

    # Initialise n
    n = 3

    print(count_special(n))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to count the number of
// special strings of a given length N
using System;
class GFG{

const int mod = 1000000007;

// Function to return count of
// special Strings
static int count_special(int n)
{

    // Stores the answer for a
    // particular value of n
    int []fib = new int[n + 1];

    // For n = 0 we have empty String
    fib[0] = 1;

    // For n = 1 we have
    // 2 special Strings
    fib[1] = 2;

    for(int i = 2; i <= n; i++)
    {

        // Calculate count of special
        // String of length i
        fib[i] = (fib[i - 1] % mod +
                  fib[i - 2] % mod) % mod;
    }

    // fib[n] stores the count of
    // special Strings of length n
    return fib[n];
}

// Driver code
public static void Main()
{

    // Initialise n
    int n = 3;

    Console.Write(count_special(n) + "\n");
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>
      // JavaScript Program to Count the number
      // of Special Strings of a given length N

      var mod = 1000000007;

      // Function to return count of special strings
      function count_special(n) {
        // stores the answer for a
        // particular value of n
        var fib = [...Array(n + 1)];

        // for n = 0 we have empty string
        fib[0] = 1;

        // for n = 1 we have
        // 2 special strings
        fib[1] = 2;

        for (var i = 2; i <= n; i++) {
          // calculate count of special string of length i
          fib[i] = ((fib[i - 1] % mod) + (fib[i - 2] % mod)) % mod;
        }

        // fib[n] stores the count
        // of special strings of length n
        return fib[n];
      }

      // Driver code
      // initialise n
      var n = 3;
      document.write(count_special(n) + "<br>");
    </script>
```

**Output:** 

```
5
```