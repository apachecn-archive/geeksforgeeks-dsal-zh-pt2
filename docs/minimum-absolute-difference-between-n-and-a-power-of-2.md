# N 和 2 的幂之间的最小绝对差

> 原文:[https://www . geeksforgeeks . org/n 和 2 的幂的最小绝对差/](https://www.geeksforgeeks.org/minimum-absolute-difference-between-n-and-a-power-of-2/)

给定一个整数 **N** ，任务是找出 **N** 和 **2** 的幂之间的最小绝对差。
**举例:**

> **输入:** N = 4
> **输出:** 0
> 最接近 4 的 2 次方为 4。因此，最小可能差值为 0。
> **输入:** N = 9
> **输出:** 1
> 最接近 9 的 2 的幂是 8，9–8 = 1

**进场:**找到最靠近其左侧 **N** 的 **2** 的力量，**左侧= 2 <sup>楼层(log2(N))</sup>** 则 **N 的**右侧最靠近 **2** 的力量将为**左侧* 2** 。现在最小绝对差将是**N–左**和**右–N**的最小值。
以下是上述办法的实施:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum difference
// between N and a power of 2
int minAbsDiff(int n)
{
    // Power of 2 closest to n on its left
    int left = pow(2, floor(log2(n)));

    // Power of 2 closest to n on its right
    int right = left * 2;

    // Return the minimum abs difference
    return min((n - left), (right - n));
}

// Driver code
int main()
{
    int n = 15;
    cout << minAbsDiff(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to return the minimum difference
// between N and a power of 2
static int minAbsDiff(int n)
{
    // Power of 2 closest to n on its left
    int left = (int)Math.pow(2, (int)(Math.log(n) /
                                Math.log(2)));

    // Power of 2 closest to n on its right
    int right = left * 2;

    // Return the minimum abs difference
    return Math.min((n - left), (right - n));
}

// Driver code
public static void main(String args[])
{
    int n = 15;
    System.out.println(minAbsDiff(n));
}
}

// This code is contributed by
// Surendra_Gangwar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# from math lib import floor
# and log2 function
from math import floor, log2

# Function to return the minimum
# difference between N and a power of 2
def minAbsDiff(n) :

    # Power of 2 closest to n on its left
    left = pow(2, floor(log2(n)))

    # Power of 2 closest to n on its right
    right = left * 2

    # Return the minimum abs difference
    return min((n - left), (right - n))

# Driver code
if __name__ == "__main__" :

    n = 15
    print(minAbsDiff(n))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{
// Function to return the minimum difference
// between N and a power of 2
static double minAbsDiff(double n)
{
    // Power of 2 closest to n on its left
    double left = Math.Pow(2,
                Math.Floor(Math.Log(n, 2)));

    // Power of 2 closest to n on its right
    double right = left * 2;

    // Return the minimum abs difference
    return Math.Min((n - left), (right - n));
}

// Driver code
public static void Main()
{
    double n = 15;
    Console.Write(minAbsDiff(n));
}
}

// This code is contributed by
// Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the minimum difference
// between N and a power of 2
function minAbsDiff($n)
{
    // Power of 2 closest to n on its left
    $left = pow(2, floor(log($n, 2)));

    // Power of 2 closest to n on its right
    $right = $left * 2;

    // Return the minimum abs difference
    return min(($n - $left), ($right - $n));
}

// Driver code
$n = 15;
echo minAbsDiff($n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

    // Javascript implementation of the above approach

    // Function to return the minimum difference
    // between N and a power of 2
    function minAbsDiff(n)
    {
        // Power of 2 closest to n on its left
        let left = Math.pow(2, Math.floor(Math.log2(n, 2)));

        // Power of 2 closest to n on its right
        let right = left * 2;

        // Return the minimum abs difference
        return Math.min((n - left), (right - n));
    }

    let n = 15;
    document.write(minAbsDiff(n));

</script>
```

**Output:** 

```
1
```

我们可以使用[左移运算符](https://www.geeksforgeeks.org/left-shift-right-shift-operators-c-cpp/)来优化实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum difference
// between N and a power of 2
int minAbsDiff(int n)
{
    // Power of 2 closest to n on its left
    int left = 1 << ((int)floor(log2(n)));

    // Power of 2 closest to n on its right
    int right = left * 2;

    // Return the minimum abs difference
    return min((n - left), (right - n));
}

// Driver code
int main()
{
    int n = 15;
    cout << minAbsDiff(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
class GFG
{

// Function to return the minimum difference
// between N and a power of 2
static int minAbsDiff(int n)
{
    // Power of 2 closest to n on its left
    int left = 1 << ((int)Math.floor(Math.log(n) / Math.log(2)));

    // Power of 2 closest to n on its right
    int right = left * 2;

    // Return the minimum abs difference
    return Math.min((n - left), (right - n));
}

// Driver code
public static void main (String[] args)
{
    int n = 15;
    System.out.println(minAbsDiff(n));
}
}

// This code is contributed by chandan_jnu
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
import math

# Function to return the minimum
# difference between N and a power of 2
def minAbsDiff(n):

    # Power of 2 closest to n on its left
    left = 1 << (int)(math.floor(math.log2(n)))

    # Power of 2 closest to n on its right
    right = left * 2

    # Return the minimum abs difference
    return min((n - left), (right - n))

# Driver code
if __name__ == "__main__":
    n = 15
    print(minAbsDiff(n))

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# implementation of the above approach
using System;

public class GFG
{

// Function to return the minimum difference
// between N and a power of 2
static int minAbsDiff(int n)
{
    // Power of 2 closest to n on its left
    int left = 1 << ((int)Math.Floor(Math.Log(n) / Math.Log(2)));

    // Power of 2 closest to n on its right
    int right = left * 2;

    // Return the minimum abs difference
    return Math.Min((n - left), (right - n));
}

// Driver code
static public void Main ()
{
    int n = 15;
    Console.WriteLine(minAbsDiff(n));
}
}

// This code is contributed by jit_t.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to return the minimum difference
// between N and a power of 2
function minAbsDiff($n)
{
    // Power of 2 closest to n on its left
    $left = 1 << ((floor(log($n) / log(2))));

    // Power of 2 closest to n on its right
    $right = $left * 2;

    // Return the minimum abs difference
    return min(($n - $left), ($right - $n));
}

// Driver code
$n = 15;
echo minAbsDiff($n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to return the minimum difference
    // between N and a power of 2
    function minAbsDiff(n)
    {
        // Power of 2 closest to n on its left
        let left = 1 << (Math.floor(Math.log(n) / Math.log(2)));

        // Power of 2 closest to n on its right
        let right = left * 2;

        // Return the minimum abs difference
        return Math.min((n - left), (right - n));
    }

    let n = 15;
    document.write(minAbsDiff(n));

</script>
```

**Output:** 

```
1
```