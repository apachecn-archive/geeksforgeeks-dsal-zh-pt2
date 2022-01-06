# 总共 n 个字母所需的最小字母数

> 原文:[https://www . geeksforgeeks . org/总共需要最少数量的字母/](https://www.geeksforgeeks.org/minimum-number-of-letters-needed-to-make-a-total-of-n/)

给定一个整数 **n** ，让 **a = 1，b = 2，c= 3，…..，z = 26** 。任务是找到使总数达到 **n** 所需的最小字母数。
**举例:**

> **输入:** n = 48
> **输出:** 2
> 48 可以写成 z + v，其中 z = 26，v = 22
> **输入:** n = 23
> **输出:** 1

**方法:**有两种可能的情况:

1.  如果 **n** 被 **26** 整除，那么答案就是 **n / 26** 。
2.  如果 **n** 不能被 **26** 整除，那么答案就是 **(n / 26) + 1** 。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum letters
// required to make a total of n
int minLettersNeeded(int n)
{
    if (n % 26 == 0)
        return (n / 26);
    else
        return ((n / 26) + 1);
}

// Driver code
int main()
{
    int n = 52;
    cout << minLettersNeeded(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum letters
    // required to make a total of n
    static int minLettersNeeded(int n)
    {
        if (n % 26 == 0)
            return (n / 26);
        else
            return ((n / 26) + 1);
    }

    // Driver code
    public static void main(String args[])
    {
        int n = 52;
        System.out.print(minLettersNeeded(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum letters
# required to make a total of n
def minLettersNeeded(n):

    if n % 26 == 0:
        return (n//26)
    else:
        return ((n//26) + 1)

# Driver code
n = 52
print(minLettersNeeded(n))
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the minimum letters
    // required to make a total of n
    static int minLettersNeeded(int n)
    {
        if (n % 26 == 0)
            return (n / 26);
        else
            return ((n / 26) + 1);
    }

    // Driver code
    public static void Main()
    {
        int n = 52;
        Console.Write(minLettersNeeded(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum
// letters required to make a
// total of n
function minLettersNeeded($n)
{
    if ($n % 26 == 0)
        return floor(($n / 26));
    else
        return floor(($n / 26) + 1);
}

// Driver code
$n = 52;

echo minLettersNeeded($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to return the minimum letters
// required to make a total of n
function minLettersNeeded(n)
{
    if (n % 26 == 0)
        return parseInt(n / 26);
    else
        return (parseInt(n / 26) + 1);
}

// Driver code
var n = 52;
document.write(minLettersNeeded(n));

// This code is contributed by noob2000
</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(1)