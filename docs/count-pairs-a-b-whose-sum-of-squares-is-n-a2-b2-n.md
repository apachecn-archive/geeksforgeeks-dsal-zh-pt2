# 计数平方和为 N (a^2 + b^2 = N)的对(a，b)

> 原文:[https://www . geesforgeks . org/count-pairs-a-b-其平方和为-n-a2-b2-n/](https://www.geeksforgeeks.org/count-pairs-a-b-whose-sum-of-squares-is-n-a2-b2-n/)

给定一个数字 n，任务是对满足条件 a^2 + b^2 = N 的所有‘a’和‘b’进行计数。
**注意:-** (a，b)和(b，a)将被视为两个不同的对，并且(a，a)也是有效的并且只被考虑一次。
**示例:**

```
Input: N = 10
Output:  2
1^2 + 3^2 = 9
3^2 + 1^2 = 9

Input: N = 8
Output: 1
2^2 + 2^2 = 8
```

**进场:**

1.  从 1 到 n 的平方根的导线数
    *   从 N 中减去当前数的平方，检查它们的差是否是一个完美的平方。
    *   如果它是完美的正方形，那么增加计数。
2.  返回计数。

以下是上述方法的实现:

## C++

```
// C++ program to count pairs whose sum
// of squares is N
#include <bits/stdc++.h>
using namespace std;

// Function to count the pairs satisfying
// a ^ 2 + b ^ 2 = N
int countPairs(int N)
{
    int count = 0;

    // Check for each number 1 to sqrt(N)
    for (int i = 1; i <= sqrt(N); i++) {

        // Store square of a number
        int sq = i * i;

        // Subtract the square from given N
        int diff = N - sq;

        // Check if the difference is also
        // a perfect square
        int sqrtDiff = sqrt(diff);

        // If yes, then increment count
        if (sqrtDiff * sqrtDiff == diff)
            count++;
    }

    return count;
}

// Driver code
int main()
{
    // Loop to Count no. of pairs satisfying
    // a ^ 2 + b ^ 2 = i for N = 1 to 10
    for (int i = 1; i <= 10; i++)
        cout << "For n = " << i << ", "
             << countPairs(i) << " pair exists\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count pairs whose sum
// of squares is N

import java.io.*;

class GFG {

// Function to count the pairs satisfying
// a ^ 2 + b ^ 2 = N
static int countPairs(int N)
{
    int count = 0;

    // Check for each number 1 to sqrt(N)
    for (int i = 1; i <= (int)Math.sqrt(N); i++)
    {

        // Store square of a number
        int sq = i * i;

        // Subtract the square from given N
        int diff = N - sq;

        // Check if the difference is also
        // a perfect square
        int sqrtDiff = (int)Math.sqrt(diff);

        // If yes, then increment count
        if (sqrtDiff * sqrtDiff == diff)
            count++;
    }

    return count;
}

    // Driver code
    public static void main (String[] args)
    {
    // Loop to Count no. of pairs satisfying
    // a ^ 2 + b ^ 2 = i for N = 1 to 10
    for (int i = 1; i <= 10; i++)
        System.out.println( "For n = " + i + ", "
            + countPairs(i) + " pair exists\n");
    }
}
// This code is contributed by inder_verma.
```

## 蟒蛇 3

```
# Python 3 program to count pairs whose sum
# of squares is N

# From math import everything
from math import *

# Function to count the pairs satisfying
# a ^ 2 + b ^ 2 = N
def countPairs(N) :
    count = 0

    # Check for each number 1 to sqrt(N)
    for i in range(1, int(sqrt(N)) + 1) :

        # Store square of a number
        sq = i * i

        # Subtract the square from given N
        diff = N - sq

        #  Check if the difference is also
        # a perfect square
        sqrtDiff = int(sqrt(diff))

        # If yes, then increment count
        if sqrtDiff * sqrtDiff == diff :
            count += 1

    return count

# Driver code    
if __name__ == "__main__" :

    # Loop to Count no. of pairs satisfying
    # a ^ 2 + b ^ 2 = i for N = 1 to 10
    for i in range(1,11) :
        print("For n =",i,", ",countPairs(i),"pair exists")

# This code is contributed by ANKITRAI1
```

## C#

```
// C# program to count pairs whose sum
// of squares is N

using System;
class GFG {

// Function to count the pairs satisfying
// a ^ 2 + b ^ 2 = N
static int countPairs(int N)
{
    int count = 0;

    // Check for each number 1 to Sqrt(N)
    for (int i = 1; i <= (int)Math.Sqrt(N); i++)
    {

        // Store square of a number
        int sq = i * i;

        // Subtract the square from given N
        int diff = N - sq;

        // Check if the difference is also
        // a perfect square
        int sqrtDiff = (int)Math.Sqrt(diff);

        // If yes, then increment count
        if (sqrtDiff * sqrtDiff == diff)
            count++;
    }

    return count;
}

    // Driver code
    public static void Main ()
    {
    // Loop to Count no. of pairs satisfying
    // a ^ 2 + b ^ 2 = i for N = 1 to 10
    for (int i = 1; i <= 10; i++)
        Console.Write( "For n = " + i + ", "
            + countPairs(i) + " pair exists\n");
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count pairs
// whose sum of squares is N

// Function to count the pairs
// satisfying a ^ 2 + b ^ 2 = N
function countPairs($N)
{
    $count = 0;
    $i = 0;

    // Check for each number 1 to sqrt(N)
    for ($i = 1; $i <= sqrt($N); $i++)
    {

        // Store square of a number
        $sq = $i * $i;

        // Subtract the square
        // from given N
        $diff =$N - $sq;

        // Check if the difference
        // is also a perfect square
        $sqrtDiff = sqrt($diff);

        // If yes, then increment count
        if ($sqrtDiff * $sqrtDiff == $diff)
            $count++;
    }

    return $count;
}

// Driver code

// Loop to Count no. of pairs satisfying
// a ^ 2 + b ^ 2 = i for N = 1 to 10
for ($i = 1; $i <= 10; $i++)
    echo "For n = " . $i . ", " .
          countPairs($i) . " pair exists\n";

// This code is contributed by Raj
?>
```

## java 描述语言

```
<script>
// Javascript program to count pairs whose sum
// of squares is N

// Function to count the pairs satisfying
// a ^ 2 + b ^ 2 = N
function countPairs(N)
{
    let count = 0;

    // Check for each number 1 to sqrt(N)
    for (let i = 1; i <= Math.sqrt(N); i++) {

        // Store square of a number
        let sq = i * i;

        // Subtract the square from given N
        let diff = N - sq;

        // Check if the difference is also
        // a perfect square
        let sqrtDiff = Math.sqrt(diff);

        // If yes, then increment count
        if (sqrtDiff * sqrtDiff == diff)
            count++;
    }

    return count;
}

// Driver code
    // Loop to Count no. of pairs satisfying
    // a ^ 2 + b ^ 2 = i for N = 1 to 10
    for (let i = 1; i <= 10; i++)
        document.write("For n = " + i + ", "
             + countPairs(i) + " pair exists<br>");

// This code is contributed by rishavmahato348.
</script>
```

**Output:** 

```
For n = 1, 1 pair exists
For n = 2, 1 pair exists
For n = 3, 0 pair exists
For n = 4, 1 pair exists
For n = 5, 2 pair exists
For n = 6, 0 pair exists
For n = 7, 0 pair exists
For n = 8, 1 pair exists
For n = 9, 1 pair exists
For n = 10, 2 pair exists
```

**时间复杂度:** O(sqrt(N))