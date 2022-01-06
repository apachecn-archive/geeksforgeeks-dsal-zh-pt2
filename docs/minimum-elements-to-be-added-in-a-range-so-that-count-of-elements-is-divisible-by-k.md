# 在一个范围内要添加的最少元素，这样元素的数量可以被 K 整除

> 原文:[https://www . geesforgeks . org/最小范围内要添加的元素数，以便元素数可被 k 整除/](https://www.geeksforgeeks.org/minimum-elements-to-be-added-in-a-range-so-that-count-of-elements-is-divisible-by-k/)

给定三个整数 **K** 、 **L** 和 **R** (范围**【L，R】**)，任务是找到该范围必须扩展的元素的最小数量，以便该范围内的元素数可被 **K** 整除。

**示例:**

> **输入:** K = 3，L = 10，R = 10
> **输出:**2
> L 到 R 中元素个数为 1。
> 所以要让它能被 3 整除，就要增加 2。
> 
> **输入:** K = 5，L = 9，R = 12
> T3】输出: 1

**进场:**

*   计算该范围内元素的总数，并将其存储在名为**count = R–L+1**的变量中。
*   现在，需要添加到范围中的元素的最小数量将是**K –(计数% K)。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int minimumMoves(int k, int l, int r)
{
    // Total elements in the range
    int count = r - l + 1;

    // If total elements are already divisible by k
    if (count % k == 0)
        return 0;

    // Value that must be added to count
    // in order to make it divisible by k
    return (k - (count % k));
}

// Driver Program to test above function
int main()
{
    int k = 3, l = 10, r = 10;
    cout << minimumMoves(k, l, r);

return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

 static int minimumMoves(int k, int l, int r)
{
    // Total elements in the range
    int count = r - l + 1;

    // If total elements are already divisible by k
    if (count % k == 0)
        return 0;

    // Value that must be added to count
    // in order to make it divisible by k
    return (k - (count % k));
}

// Driver Program to test above function
    public static void main (String[] args) {
    int k = 3, l = 10, r = 10;
    System.out.print(minimumMoves(k, l, r));
    }
}
// This code is contributed
// by inder_verma..
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

def minimumMoves(k, l, r):
    # Total elements in the range
    count = r - l + 1

    # If total elements are already divisible by k
    if (count % k == 0):
        return 0

    # Value that must be added to count
    # in order to make it divisible by k
    return (k - (count % k))

# Driver Program to test above function
if __name__ == '__main__':
    k = 3
    l = 10
    r = 10
    print(minimumMoves(k, l, r))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

static int minimumMoves(int k, int l, int r)
{
    // Total elements in the range
    int count = r - l + 1;

    // If total elements are already divisible by k
    if (count % k == 0)
        return 0;

    // Value that must be added to count
    // in order to make it divisible by k
    return (k - (count % k));
}

// Driver Program to test above function
    public static void Main () {
    int k = 3, l = 10, r = 10;
    Console.WriteLine(minimumMoves(k, l, r));
    }
}
// This code is contributed
// by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

function minimumMoves($k, $l, $r)
{
    // Total elements in the range
    $count = $r - $l + 1;

    // If total elements are already divisible by k
    if ($count % $k == 0)
        return 0;

    // Value that must be added to count
    // in order to make it divisible by k
    return ($k - ($count % $k));
}

// Driver Program to test above function

    $k = 3; $l = 10; $r = 10;
    echo minimumMoves($k, $l, $r);
// This code is contributed
// by inder_verma..

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
function minimumMoves(k, l, r)
{

    // Total elements in the range
    let count = r - l + 1;

    // If total elements are already
    // divisible by k
    if (count % k == 0)
        return 0;

    // Value that must be added to count
    // in order to make it divisible by k
    return (k - (count % k));
}

// Driver code
let k = 3, l = 10, r = 10;

document.write(minimumMoves(k, l, r));

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
2
```