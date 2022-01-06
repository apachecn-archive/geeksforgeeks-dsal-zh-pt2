# 大小都可以交换时最大化大

> 原文:[https://www . geeksforgeeks . org/最大化-大-当-大-小-都可以交换/](https://www.geeksforgeeks.org/maximize-big-when-both-big-and-small-can-be-exchanged/)

给予 **N** 大糖果和 **M** 小糖果。一颗大糖果可以通过支付 **X** 小糖果来购买。或者，一颗大糖果可以换成 **Y** 小糖果。任务是找到能买到的最大数量的大糖果。
**举例:**

> **输入:** N = 3，M = 10，X = 4，Y = 2
> **输出:** 5
> 8 颗小糖果换 2 颗大糖果。
> **输入:** N = 3，M = 10，X = 1，Y = 2
> **输出:** 16
> 把最初的大糖果全部卖掉，得到 6 颗小糖果。
> 现在 16 颗小糖果可以换 16 颗大糖果。

在第一个例子中，大糖果不能为了利润而出售。所以，只有剩下的小糖果可以换成大糖果。
在第二个例子中，大糖果可以出售以获取利润。
**进场:**如果初始大糖果可以盈利出售，即 **X < Y** 则出售大糖果并更新小糖果和大糖果的计数。然后，卖掉所有更新的小糖果，以购买大糖果。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

    // Function to return the maximum big
    // candies that can be bought
    int max_candies(int bigCandies,
        int smallCandies,int X, int Y)
    {
        // If initial big candies
        // can be sold for profit
        if (X < Y)
        {
            smallCandies += Y * bigCandies;
            bigCandies = 0;
        }

        // Update big candies that can be bought
        bigCandies += (smallCandies / X);

        return bigCandies;
    }

    // Driver code
    int main()
    {
        int N = 3, M = 10;
        int X = 4, Y = 2;
        cout << (max_candies(N, M, X, Y));
        return 0;
    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the maximum big candies
    // that can be bought
    static int max_candies(int bigCandies, int smallCandies,
                           int X, int Y)
    {
        // If initial big candies can be sold for profit
        if (X < Y) {

            smallCandies += Y * bigCandies;
            bigCandies = 0;
        }

        // Update big candies that can be bought
        bigCandies += (smallCandies / X);

        return bigCandies;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 3, M = 10;
        int X = 4, Y = 2;

        System.out.println(max_candies(N, M, X, Y));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum big candies
# that can be bought
def max_candies(bigCandies, smallCandies, X, Y):

    # If initial big candies can
    # be sold for profit
    if(X < Y):

        smallCandies += Y * bigCandies
        bigCandies = 0

    # Update big candies that can be bought
    bigCandies += (smallCandies // X)

    return bigCandies

# Driver code
N = 3
M = 10
X = 4
Y = 2
print(max_candies(N, M, X, Y))

# This code is contributed by Code_Mech
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the maximum
    // big candies that can be bought
    static int max_candies(int bigCandies,
                        int smallCandies,
                        int X, int Y)
    {
        // If initial big candies
        // can be sold for profit
        if (X < Y)
        {
            smallCandies += Y * bigCandies;
            bigCandies = 0;
        }

        // Update big candies that can be bought
        bigCandies += (smallCandies / X);

        return bigCandies;
    }

    // Driver code
    static public void Main ()
    {
        int N = 3, M = 10;
        int X = 4, Y = 2;
        Console.WriteLine(max_candies(N, M, X, Y));
    }
}

// This Code is contributed by ajit...
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the maximum big
// candies that can be bought
function max_candies($bigCandies,
                     $smallCandies, $X, $Y)
{
    // If initial big candies can be
    // sold for profit
    if ($X < $Y)
    {

        $smallCandies += $Y * $bigCandies;
        $bigCandies = 0;
    }

    // Update big candies that can be bought
    $bigCandies += (int)($smallCandies / $X);

    return $bigCandies;
}

// Driver code
$N = 3;
$M = 10;
$X = 4;
$Y = 2;

echo (max_candies($N, $M, $X, $Y));

// This code is contributed by akt_mit
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximum
    // big candies that can be bought
    function max_candies(bigCandies, smallCandies, X, Y)
    {
        // If initial big candies
        // can be sold for profit
        if (X < Y)
        {
            smallCandies += Y * bigCandies;
            bigCandies = 0;
        }

        // Update big candies that can be bought
        bigCandies += parseInt(smallCandies / X, 10);

        return bigCandies;
    }

    let N = 3, M = 10;
    let X = 4, Y = 2;
    document.write(max_candies(N, M, X, Y));

</script>
```

**Output:** 

```
5
```