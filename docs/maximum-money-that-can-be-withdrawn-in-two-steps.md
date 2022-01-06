# 分两步可以提取的最大金额

> 原文:[https://www . geeksforgeeks . org/分两步提取最高金额/](https://www.geeksforgeeks.org/maximum-money-that-can-be-withdrawn-in-two-steps/)

有两个现金柜，一个有 **X** 个硬币，另一个有 **Y** 个硬币，最多可以取款两次，当您从一个柜中取款时，您将获得该柜的总钱，如果该柜最初有 **Z** 个硬币，该柜将被重新装满**Z–1**个硬币。任务是找到你能得到的最大硬币数。
**举例:**

> **输入:** X = 6，Y = 3
> T3】输出: 11
> 从储物柜 X 即 6
> 取现在，X = 5，Y = 3
> 从储物柜 X 即 5 再次取。
> **输入:** X = 4，Y = 4
> **输出:** 8

**进场:**为了最大化硬币数量，从最大值的储物柜中取，然后更新储物柜，再次从最大值的储物柜中取。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum coins we can get
int maxCoins(int X, int Y)
{

    // Update elements such that X > Y
    if (X < Y)
        swap(X, Y);

    // Take from the maximum
    int coins = X;

    // Refill
    X--;

    // Again, take the maximum
    coins += max(X, Y);

    return coins;
}

// Driver code
int main()
{

    int X = 7, Y = 5;

    cout << maxCoins(X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {
    // Function to return the maximum coins we can get
    static int maxCoins(int X, int Y)
    {

        // Update elements such that X > Y
        if (X < Y) {
            swap(X, Y);
        }

        // Take from the maximum
        int coins = X;

        // Refill
        X--;

        // Again, take the maximum
        coins += Math.max(X, Y);

        return coins;
    }

    static void swap(int X, int Y)
    {
        int temp = X;
        X = Y;
        Y = temp;
    }

    // Driver code
    public static void main(String[] args)
    {
        int X = 7, Y = 5;
        System.out.println(maxCoins(X, Y));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum coins we can get
def maxCoins(X, Y) :

    # Update elements such that X > Y
    if (X < Y) :
        X, Y = Y, X;

    # Take from the maximum
    coins = X;

    # Refill
    X -= 1;

    # Again, take the maximum
    coins += max(X, Y);

    return coins;

# Driver code
if __name__ == "__main__" :

    X = 7; Y = 5;

    print(maxCoins(X, Y));

    # This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG {
    // Function to return the maximum coins we can get
    static int maxCoins(int X, int Y)
    {

        // Update elements such that X > Y
        if (X < Y) {
            swap(X, Y);
        }

        // Take from the maximum
        int coins = X;

        // Refill
        X--;

        // Again, take the maximum
        coins += Math.Max(X, Y);

        return coins;
    }

    static void swap(int X, int Y)
    {
        int temp = X;
        X = Y;
        Y = temp;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int X = 7, Y = 5;
        Console.WriteLine(maxCoins(X, Y));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum coins we can get
function maxCoins($X, $Y)
{
    // Update elements such that X > Y
    if ($X < $Y)
        swap($X, $Y);

    // Take from the maximum
    $coins = $X;

    // Refill
    $X--;

    // Again, take the maximum
    $coins += max($X, $Y);

    return $coins;
}

// Driver code

$X = 7;
$Y = 5;

echo maxCoins($X, $Y);

// This code is contributed by Naman_Garg.

?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the maximum coins we can get
function maxCoins(X, Y)
{

    // Update elements such that X > Y
    if (X < Y) {
        let temp = X;
        X = Y;
        Y = temp;
    }

    // Take from the maximum
    let coins = X;

    // Refill
    X--;

    // Again, take the maximum
    coins += Math.max(X, Y);

    return coins;
}

// Driver code

    let X = 7, Y = 5;

    document.write(maxCoins(X, Y));

</script>
```

**Output:** 

```
13
```

**时间复杂度:** O(1)

**辅助空间:** O(1)