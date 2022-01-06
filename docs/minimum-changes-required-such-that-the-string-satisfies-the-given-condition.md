# 使管柱满足给定条件所需的最小变化量

> 原文:[https://www . geeksforgeeks . org/最小-更改-要求-这样-字符串满足给定条件/](https://www.geeksforgeeks.org/minimum-changes-required-such-that-the-string-satisfies-the-given-condition/)

给定二进制字符串**字符串**。在一次操作中，我们可以将任意**“1”**更改为**“0”**或任意**“0”**更改为**“1”**。任务是对字符串进行最小数量的更改，这样如果我们采用字符串的任何前缀，则 **1 的数量**应该大于或等于 **0 的数量**。
**举例:**

> **输入:** str = "10001"
> **输出:** 1
> 我们可以将 str[2]从‘0’更改为‘1’。
> **输入:** str = "0000"
> **输出:** 2

**进场:**问题可以贪婪地解决。字符串的第一个字符必须是 **1** 。然后对于字符串的其余部分，我们逐个字符遍历字符串，检查所需条件是否满足，如果不满足，则增加所需更改的计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum
// changes required
int minChanges(string str, int n)
{

    // To store the count of minimum changes,
    // number of ones and the number of zeroes
    int count = 0, zeros = 0, ones = 0;

    // First character has to be '1'
    if (str[0] != '1') {
        count++;
        ones++;
    }

    for (int i = 1; i < n; i++) {
        if (str[i] == '0')
            zeros++;
        else
            ones++;

        // If condition fails
        // changes need to be made
        if (zeros > ones) {
            zeros--;
            ones++;
            count++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    string str = "0000";
    int n = str.length();
    cout << minChanges(str, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the minimum
// changes required
static int minChanges(char[] str, int n)
{

    // To store the count of minimum changes,
    // number of ones and the number of zeroes
    int count = 0, zeros = 0, ones = 0;

    // First character has to be '1'
    if (str[0] != '1')
    {
        count++;
        ones++;
    }

    for (int i = 1; i < n; i++)
    {
        if (str[i] == '0')
            zeros++;
        else
            ones++;

        // If condition fails
        // changes need to be made
        if (zeros > ones)
        {
            zeros--;
            ones++;
            count++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
public static void main(String[] args)
{
    char []str = "0000".toCharArray();
    int n = str.length;
    System.out.print(minChanges(str, n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# changes required
def minChanges(str, n):

    # To store the count of minimum changes,
    # number of ones and the number of zeroes
    count, zeros, ones = 0, 0, 0

    # First character has to be '1'
    if (ord(str[0])!= ord('1')):
        count += 1
        ones += 1

    for i in range(1, n):
        if (ord(str[i]) == ord('0')):
            zeros += 1
        else:
            ones += 1

        # If condition fails
        # changes need to be made
        if (zeros > ones):
            zeros -= 1
            ones += 1
            count += 1

    # Return the required count
    return count

# Driver code
if __name__ == '__main__':
    str = "0000"
    n = len(str)
    print(minChanges(str, n))

# This code contributed by PrinciRaj1992
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the minimum
// changes required
static int minChanges(char[] str, int n)
{

    // To store the count of minimum changes,
    // number of ones and the number of zeroes
    int count = 0, zeros = 0, ones = 0;

    // First character has to be '1'
    if (str[0] != '1')
    {
        count++;
        ones++;
    }

    for (int i = 1; i < n; i++)
    {
        if (str[i] == '0')
            zeros++;
        else
            ones++;

        // If condition fails
        // changes need to be made
        if (zeros > ones)
        {
            zeros--;
            ones++;
            count++;
        }
    }

    // Return the required count
    return count;
}

// Driver code
public static void Main(String[] args)
{
    char []str = "0000".ToCharArray();
    int n = str.Length;
    Console.Write(minChanges(str, n));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// changes required
function minChanges($str, $n)
{

    // To store the count of minimum changes,
    // number of ones and the number of zeroes
    $count = $zeros = $ones = 0;

    // First character has to be '1'
    if ($str[0] != '1')
    {
        $count++;
        $ones++;
    }

    for ($i = 1; $i < $n; $i++)
    {
        if ($str[$i] == '0')
            $zeros++;
        else
            $ones++;

        // If condition fails
        // changes need to be made
        if ($zeros > $ones)
        {
            $zeros--;
            $ones++;
            $count++;
        }
    }

    // Return the required count
    return $count;
}

// Driver code
$str = "0000";
$n = strlen($str);
echo minChanges($str, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum
// changes required
function minChanges(str, n)
{

    // To store the count of minimum changes,
    // number of ones and the number of zeroes
    let count = 0, zeros = 0, ones = 0;

    // First character has to be '1'
    if (str[0] != '1')
    {
        count++;
        ones++;
    }

    for (let i = 1; i < n; i++)
    {
        if (str[i] == '0')
            zeros++;
        else
            ones++;

        // If condition fails
        // changes need to be made
        if (zeros > ones)
        {
            zeros--;
            ones++;
            count++;
        }
    }

    // Return the required count
    return count;
} 

// Driver Code

     let str = "0000".split('');
    let n = str.length;
     document.write(minChanges(str, n));

</script>
```

**Output:** 

```
2
```