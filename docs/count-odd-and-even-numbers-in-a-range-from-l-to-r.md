# 计算从 L 到 R 范围内的奇数和偶数

> 原文:[https://www . geesforgeks . org/count-从 l 到 r 范围内的奇数和偶数/](https://www.geeksforgeeks.org/count-odd-and-even-numbers-in-a-range-from-l-to-r/)

给定两个数字 L 和 R，任务是计算 L 到 R 范围内奇数的数量
**示例:**

> **输入:** l = 3，r = 7
> **输出:** 3 2
> 奇数计数为 3 即 3，5，7
> 偶数计数为 2 即 4，6
> **输入:** l = 4，r = 8
> **输出:** 2

**方法:**该范围内的总数为**(R–L+1)**，即

1.  如果 N 是偶数，那么奇数和偶数的计数都是 **N/2** 。
2.  如果 N 是奇数，
    *   如果 L 或 R 是奇数，那么奇数的计数将是 **N/2 + 1** ，偶数=**N–countofOdd**。
    *   否则，奇数的计数将是 **N/2** ，偶数=**N–countofOdd**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

using namespace std;

// Return the number of odd numbers
// in the range [L, R]
int countOdd(int L, int R){

    int N = (R - L) / 2;

    // if either R or L is odd
    if (R % 2 != 0 || L % 2 != 0)
        N += 1;

    return N;
}

// Driver code
int main()
{
    int L = 3, R = 7;
    int odds = countOdd(L, R);
    int evens = (R - L + 1) - odds;

    cout << "Count of odd numbers is " << odds << endl;
    cout << "Count of even numbers is " << evens << endl;
    return 0;
}

// This code is contributed by Rituraj Jain
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class GFG {

    // Return the number of odd numbers
    // in the range [L, R]
    static int countOdd(int L, int R)
    {
        int N = (R - L) / 2;

        // if either R or L is odd
        if (R % 2 != 0 || L % 2 != 0)
            N++;

        return N;
    }

    // Driver code
    public static void main(String[] args)
    {
        int L = 3, R = 7;

        int odds = countOdd(L, R);
        int evens = (R - L + 1) - odds;
        System.out.println("Count of odd numbers is " + odds);
        System.out.println("Count of even numbers is " + evens);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Return the number of odd numbers
# in the range [L, R]
def countOdd(L, R):

    N = (R - L) // 2

    # if either R or L is odd
    if (R % 2 != 0 or L % 2 != 0):
        N += 1

    return N

# Driver code
if __name__ == "__main__":

    L = 3
    R = 7

    odds = countOdd(L, R)
    evens = (R - L + 1) - odds
    print("Count of odd numbers is", odds)
    print("Count of even numbers is", evens)

# This code is contributed by ita_c
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Return the number of odd numbers
    // in the range [L, R]
    static int countOdd(int L, int R)
    {
        int N = (R - L) / 2;

        // if either R or L is odd
        if (R % 2 != 0 || L % 2 != 0)
            N++;

        return N;
    }

    // Driver code
    public static void Main()
    {
        int L = 3, R = 7;

        int odds = countOdd(L, R);
        int evens = (R - L + 1) - odds;
        Console.WriteLine("Count of odd numbers is " + odds);
        Console.WriteLine("Count of even numbers is " + evens);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Return the number of odd numbers
// in the range [L, R]
function countOdd($L, $R)
{
    $N = ($R - $L) / 2;

    // if either R or L is odd
    if ($R % 2 != 0 || $L % 2 != 0)
        $N++;

    return $N;
}

// Driver code
$L = 3; $R = 7;

$odds = countOdd($L, $R);
$evens = ($R - $L + 1) - $odds;
echo "Count of odd numbers is " . $odds . "\n";
echo "Count of even numbers is " . $evens;

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// Javascript implementation
// of the above approach

// Return the number of odd numbers
// in the range [L, R]
function countOdd( L, R){

    let N = Math.floor((R - L) / 2);

    // if either R or L is odd
    if (R % 2 != 0 || L % 2 != 0)
        N += 1;

    return N;
}

    // Driver Code

    let L = 3, R = 7;
    let odds = countOdd(L, R);
    let evens = (R - L + 1) - odds;

    document.write(
    "Count of odd numbers is " + odds + "</br>"
    );
    document.write(
    "Count of even numbers is " + evens + "</br>"
    );

</script>
```

**Output:** 

```
Count of odd numbers is 3
Count of even numbers is 2
```