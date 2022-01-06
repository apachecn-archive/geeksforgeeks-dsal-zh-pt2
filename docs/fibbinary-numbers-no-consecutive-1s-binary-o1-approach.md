# 二进制数(二进制中没有连续的 1)–0(1)接近

> 原文:[https://www . geesforgeks . org/fib binary-numbers-no-continuous-1s-binary-O1-approach/](https://www.geeksforgeeks.org/fibbinary-numbers-no-consecutive-1s-binary-o1-approach/)

给定正整数 **n** 。问题是检查这个数是否是二进制数。Fibbinary 数是二进制表示不包含连续 1 的整数。
**例:**

```
Input : 10
Output : Yes
Explanation: 1010 is the binary representation 
             of 10 which does not contains any 
             consecutive 1's.

Input : 11
Output : No
Explanation: 1011 is the binary representation 
             of 11, which contains consecutive 
             1's.
```

**方法:**如果(n & (n > > 1)) == 0，那么“n”是一个二进制数，否则不是。

## C++

```
// C++ implementation to check whether a number
// is fibbinary or not
#include <bits/stdc++.h>
using namespace std;

// function to check whether a number
// is fibbinary or not
bool isFibbinaryNum(unsigned int n) {

  // if the number does not contain adjacent ones
  // then (n & (n >> 1)) operation results to 0
  if ((n & (n >> 1)) == 0)
    return true;

  // not a fibbinary number
  return false;
}

// Driver program to test above
int main() {
  unsigned int n = 10;
  if (isFibbinaryNum(n))
    cout << "Yes";
  else
    cout << "No";
  return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check whether
// a number is fibbinary or not
class GFG {

    // function to check whether a number
    // is fibbinary or not
    static boolean isFibbinaryNum(int n) {

        // if the number does not contain
        // adjacent ones then (n & (n >> 1))
        // operation results to 0
        if ((n & (n >> 1)) == 0)
            return true;

        // not a fibbinary number
        return false;
    }

    // Driver program to test above
    public static void main(String[] args) {

        int n = 10;

        if (isFibbinaryNum(n) == true)
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by
// Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python3 program to check if a number
# is fibinnary number or not

# function to check whether a number
# is fibbinary or not
def isFibbinaryNum( n):

    # if the number does not contain adjacent
    # ones then (n & (n >> 1)) operation
    # results to 0
    if ((n & (n >> 1)) == 0):
        return 1

    # Not a fibbinary number
    return 0

# Driver code
n = 10

if (isFibbinaryNum(n)):
    print("Yes")
else:
    print("No")

# This code is contributed by sunnysingh
```

## C#

```
// C# implementation to check whether
// a number is fibbinary or not
using System;

class GFG {

    // function to check whether a number
    // is fibbinary or not
    static bool isFibbinaryNum(int n) {

        // if the number does not contain
        // adjacent ones then (n & (n >> 1))
        // operation results to 0
        if ((n & (n >> 1)) == 0)
            return true;

        // not a fibbinary number
        return false;
    }

    // Driver program to test above
    public static void Main() {

        int n = 10;

        if (isFibbinaryNum(n) == true)
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to check whether
// a number is fibbinary or not

// function to check whether a number
// is fibbinary or not
function isFibbinaryNum($n)
{

    // if the number does not contain
    // adjacent ones then (n & (n >> 1))
    // operation results to 0
    if (($n & ($n >> 1)) == 0)
        return true;

    // not a fibbinary number
    return false;
}

// Driver code
$n = 10;
if (isFibbinaryNum($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript program implementation to find  whether
// a number is fibbinary or not

  // function to check whether a number
    // is fibbinary or not
    function isFibbinaryNum(n) {

        // if the number does not contain
        // adjacent ones then (n & (n >> 1))
        // operation results to 0
        if ((n & (n >> 1)) == 0)
            return true;

        // not a fibbinary number
        return false;
    }

// Driver code

        let n = 10;

        if (isFibbinaryNum(n) == true)
            document.write("Yes");
        else
            document.write("No");

// This code is contributed by souravghosh0416.
</script>
```

**输出:**

```
Yes
```

时间复杂度:O(1)。