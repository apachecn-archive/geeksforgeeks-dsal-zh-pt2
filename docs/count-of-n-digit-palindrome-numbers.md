# N 位回文数字的计数

> 原文:[https://www . geeksforgeeks . org/n 位回文数字计数/](https://www.geeksforgeeks.org/count-of-n-digit-palindrome-numbers/)

给定一个整数 **N** ，任务是找到 **N 位** [回文数字](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)的个数。
**举例:**

> **输入:** N = 1
> **输出:** 9
> {1，2，3，4，5，6，7，8，9}都是可能的
> 个一位数回文数字。
> **输入:** N = 2
> **输出:** 9

**方法:**第一个数字可以是任何一个 **9** 数字(不是 0)，最后一个数字必须与第一个数字相同才能回文，第二个和第二个最后一个数字可以是任何一个 **10** 数字，其余数字也是如此。所以，对于 **N** 的任意值， **N 位**回文的个数为**9 * 10<sup>(N–1)/2</sup>**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of N-digit palindrome numbers
int nDigitPalindromes(int n)
{
    return (9 * pow(10, (n - 1) / 2));
}

// Driver code
int main()
{
    int n = 2;

    cout << nDigitPalindromes(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of N-digit palindrome numbers
static int nDigitPalindromes(int n)
{
    return (9 * (int)Math.pow(10,
           (n - 1) / 2));
}

// Driver code
public static void main(String []args)
{
    int n = 2;

    System.out.println(nDigitPalindromes(n));
}
}

// This code is contributed by Code_Mech
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of N-digit palindrome numbers
def nDigitPalindromes(n) :

    return (9 * pow(10, (n - 1) // 2));

# Driver code
if __name__ == "__main__" :

    n = 2;

    print(nDigitPalindromes(n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of N-digit palindrome numbers
static int nDigitPalindromes(int n)
{
    return (9 * (int)Math.Pow(10,
           (n - 1) / 2));
}

// Driver code
public static void Main(String []args)
{
    int n = 2;

    Console.WriteLine(nDigitPalindromes(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of N-digit palindrome numbers
function nDigitPalindromes(n)
{
    return (9 * Math.pow(10, parseInt((n - 1) / 2)));
}

// Driver code
var n = 2;
document.write(nDigitPalindromes(n));

</script>
```

**Output:** 

```
9
```