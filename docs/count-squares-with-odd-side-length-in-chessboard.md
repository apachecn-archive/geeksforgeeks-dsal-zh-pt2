# 计算棋盘中边长为奇数的方块

> 原文:[https://www . geesforgeks . org/count-棋盘边长为奇数的正方形/](https://www.geeksforgeeks.org/count-squares-with-odd-side-length-in-chessboard/)

给定一个 **N * N** 棋盘，任务是计算边长为奇数的方块数。
**例:**

> **输入:** N = 3
> **输出:** 10
> 可以有 9 个边为 1
> 的正方形和一个边为 3
> 9 + 1 = 10
> **输入:** N = 8
> **输出:** 120

**逼近:**对于从 **1** 到 **N** 的所有奇数，然后计算具有该奇数边的可形成的方块数。对于 **i <sup>第</sup>** 边，方块数等于**(N–I+1)<sup>2</sup>**。此外，将所有这样的方块数相加。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of odd length squares possible
int count_square(int n)
{

    // To store the required count
    int count = 0;

    // For all odd values of i
    for (int i = 1; i <= n; i = i + 2) {

        // Add the count of possible
        // squares of length i
        int k = n - i + 1;
        count += (k * k);
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int N = 8;

    cout << count_square(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the count
    // of odd length squares possible
    static int count_square(int n)
    {

        // To store the required count
        int count = 0;

        // For all odd values of i
        for (int i = 1; i <= n; i = i + 2) {

            // Add the count of possible
            // squares of length i
            int k = n - i + 1;
            count += (k * k);
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int N = 8;

        System.out.println(count_square(N));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function to return the count
# of odd length squares possible
def count_square(n):

    # To store the required count
    count = 0;

    # For all odd values of i
    for i in range(1, n + 1, 2):

        # Add the count of possible
        # squares of length i
        k = n - i + 1;
        count += (k * k);

    # Return the required count
    return count;

# Driver code
N = 8;
print(count_square(N));

# This code has been contributed by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG {

    // Function to return the count
    // of odd length squares possible
    static int count_square(int n)
    {

        // To store the required count
        int count = 0;

        // For all odd values of i
        for (int i = 1; i <= n; i = i + 2) {

            // Add the count of possible
            // squares of length i
            int k = n - i + 1;
            count += (k * k);
        }

        // Return the required count
        return count;
    }

    // Driver code
    public static void Main()
    {
        int N = 8;

        Console.WriteLine(count_square(N));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of odd length squares possible
function count_square($n)
{

    // To store the required count
    $count = 0;

    // For all odd values of i
    for ($i = 1; $i <= $n; $i = $i + 2)
    {

        // Add the count of possible
        // squares of length i
        $k =$n - $i + 1;
        $count += ($k * $k);
    }

    // Return the required count
    return $count;
}

// Driver code
$N = 8;

echo count_square($N);

// This code is contributed by AnkitRai01
?>
```

## java 描述语言

```
<Script>

// Javascript implementation of the approach

// Function to return the count
// of odd length squares possible
function count_square(n)
{

    // To store the required count
    let count = 0;

    // For all odd values of i
    for (let i = 1; i <= n; i = i + 2) {

        // Add the count of possible
        // squares of length i
        let k = n - i + 1;
        count += (k * k);
    }

    // Return the required count
    return count;
}

// Driver code
    let N = 8;

    document.write(count_square(N));

</script>
```

**Output:** 

```
120
```