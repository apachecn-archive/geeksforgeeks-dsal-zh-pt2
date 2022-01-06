# 计数奇数和偶数的 N 次旋转

> 原文:[https://www . geeksforgeeks . org/count-rotations-of-n-哪些是奇数和偶数/](https://www.geeksforgeeks.org/count-rotations-of-n-which-are-odd-and-even/)

给定一个数 **n** ，任务是统计给定数的所有奇数和偶数的旋转。
**例:**

```
Input: n = 1234
Output: Odd = 2, Even = 2
Total rotations: 1234, 2341, 3412, 4123
Odd rotations: 2341 and 4123
Even rotations: 1234 and 3412

Input: n = 246
Output: Odd = 0, Even = 3
```

**高效进场**:对于大数，很难旋转，每次旋转都要检查是否奇数。因此，在这种方法中，检查数字中奇数和偶数的计数。这些将是这个问题的答案。
以下是上述办法的实施:
**实施:**

## C++

```
// C++ implementation of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count of all rotations
// which are odd and even
void countOddRotations(int n)
{
    int odd_count = 0, even_count = 0;
    do {
        int digit = n % 10;
        if (digit % 2 == 1)
            odd_count++;
        else
            even_count++;
        n = n / 10;
    } while (n != 0);

    cout << "Odd = " << odd_count << endl;
    cout << "Even = " << even_count << endl;
}

// Driver Code
int main()
{
    int n = 1234;
    countOddRotations(n);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

class Solution {

    // Function to count of all rotations
    // which are odd and even
    static void countOddRotations(int n)
    {
        int odd_count = 0, even_count = 0;
        do {
            int digit = n % 10;
            if (digit % 2 == 1)
                odd_count++;
            else
                even_count++;
            n = n / 10;
        } while (n != 0);

        System.out.println("Odd = " + odd_count);
        System.out.println("Even = " + even_count);
    }

    public static void main(String[] args)
    {
        int n = 1234;
        countOddRotations(n);
    }
}
```

## 蟒蛇 3

```
# Python implementation of the above approach

# Function to count of all rotations
# which are odd and even
def countOddRotations(n):
    odd_count = 0; even_count = 0
    while n != 0:
        digit = n % 10
        if digit % 2 == 0:
            odd_count += 1
        else:
            even_count += 1
        n = n//10
    print("Odd =", odd_count)
    print("Even =", even_count)

# Driver code
n = 1234
countOddRotations(n)

# This code is contributed by Shrikant13
```

## C#

```
// CSharp implementation of the above approach

using System;
class Solution {

    // Function to count of all rotations
    // which are odd and even
    static void countOddRotations(int n)
    {
        int odd_count = 0, even_count = 0;
        do {
            int digit = n % 10;
            if (digit % 2 == 1)
                odd_count++;
            else
                even_count++;
            n = n / 10;
        } while (n != 0);

        Console.WriteLine("Odd = " + odd_count);
        Console.WriteLine("Even = " + even_count);
    }

    public static void Main()
    {
        int n = 1234;
        countOddRotations(n);
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count of all rotations
// which are odd and even
function countOddRotations($n)
{
    $odd_count = 0;
    $even_count = 0;
    do {
        $digit = $n % 10;
        if ($digit % 2 == 1)
            $odd_count++;
        else
            $even_count++;
        $n = (int)($n / 10);
    } while ($n != 0);

    echo "Odd = ", $odd_count, "\n";
    echo "Even = ", $even_count, "\n";
}

// Driver Code
$n = 1234;
countOddRotations($n);

// This code is contributed by ajit..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to count of all rotations
// which are odd and even
function countOddRotations(n)
{
    var odd_count = 0, even_count = 0;
    do {
        var digit = n % 10;
        if (digit % 2 == 1)
            odd_count++;
        else
            even_count++;
        n = parseInt(n / 10);
    } while (n != 0);

    document.write("Odd = " + odd_count + "<br>");
    document.write("Even = " + even_count + "<br>");
}

// Driver Code
var n = 1234;
countOddRotations(n);

// This code is contributed by rutvik_56.

</script>
```

**Output:** 

```
Odd = 2
Even = 2
```

**时间复杂度:** O(n)