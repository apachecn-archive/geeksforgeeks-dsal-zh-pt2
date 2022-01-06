# 将一个数表示为连续|集合 2 的和(使用奇数因子)

> 原文:[https://www . geesforgeks . org/count-way-express-number-sum-continuous-numbers scan-merge-https www-geesforgeks-org count-way-express-number-sum-continuous-numbers/](https://www.geeksforgeeks.org/count-ways-express-number-sum-consecutive-numberscan-merge-httpswww-geeksforgeeks-orgcount-ways-express-number-sum-consecutive-numbers/)

给定一个数 n，找出将这个数表示为两个或两个以上连续自然数之和的方法。

**示例:**

```
Input : n = 15 
Output : 3
15 can be represented as:
1 + 2 + 3 + 4 + 5
4 + 5 + 6
7 + 8

Input :10
Output :2
10 can only be represented as:
1 + 2 + 3 + 4

```

我们已经在下面的帖子中讨论了一种方法。
[用连续数的和来表示一个数的计数方式](https://www.geeksforgeeks.org/count-ways-express-number-sum-consecutive-numbers/)

这里讨论一种新的方法。假设我们讨论的是从 X 到 Y 的数的和，即[X，X+1，…，Y-1，Y]
，那么算术和是

```
(Y+X)(Y-X+1)/2 
```

如果这应该是 N，那么

```
2N = (Y+X)(Y-X+1)
```

请注意，其中一个因素应该是偶数，另一个因素应该是奇数，因为 Y-X+1 和 Y+X 应该具有相反的奇偶校验，因为 Y-X 和 Y+X 具有相同的奇偶校验。因为 2N 反正是偶数，所以我们找到了 n 的奇数因子的数量。例如，n = 15，15 的所有奇数因子都是 1 3 和 5，所以答案是 3。

## C++

```
// C++ program to count number of ways to express
// N as sum of consecutive numbers.
#include <bits/stdc++.h>
using namespace std;

// returns the number of odd factors
int countOddFactors(long long n)
{
    int odd_factors = 0;

    for (int i = 1; 1ll * i * i <= n; i++) {
        if (n % i == 0) {

            // If i is an odd factor and
            // n is a perfect square
            if (1ll * i * i == n) {
                if (i & 1)
                    odd_factors++;
            }

            // If n is not perfect square
            else {
                if (i & 1)
                    odd_factors++;

                int factor = n / i;
                if (factor & 1)
                    odd_factors++;
            }
        }
    }
    return odd_factors - 1;
}

// Driver Code
int main()
{
    // N as sum of consecutive numbers
    long long int N = 15;
    cout << countOddFactors(N) << endl;

    N = 10;
    cout << countOddFactors(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number 
// of ways to express N as sum 
// of consecutive numbers.
import java.io.*;

class GFG
{
// returns the number
// of odd factors
static int countOddFactors(long n)
{
    int odd_factors = 0;

    for (int i = 1; 1 * i * i <= n; i++) 
    {
        if (n % i == 0) 
        {

            // If i is an odd factor and
            // n is a perfect square
            if (1 * i * i == n) 
            {
                if ((i & 1) == 1)
                    odd_factors++;
            }

            // If n is not 
            // perfect square
            else {
                if ((i & 1) == 1)
                    odd_factors++;

                int factor = (int)n / i;
                if ((factor & 1) == 1)
                    odd_factors++;
            }
        }
    }
    return odd_factors - 1;
}

// Driver Code
public static void main(String args[])
{
    // N as sum of consecutive numbers
    long N = 15;
    System.out.println(countOddFactors(N));

    N = 10;
    System.out.println(countOddFactors(N));
}
}

// This code is contributed by 
// Manish Shaw(manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to count number 
# of ways to express N as sum
# of consecutive numbers.

# returns the number
# of odd factors
def countOddFactors(n) :
    odd_factors = 0
    i = 1
    while((1 * i * i) <= n) :
        if (n % i == 0) :

            # If i is an odd factor and
            # n is a perfect square
            if (1 * i * i == n) :
                if (i & 1) :
                    odd_factors = odd_factors + 1

            # If n is not perfect square
            else :
                if ((i & 1)) :
                    odd_factors = odd_factors + 1

                factor = int(n / i)
                if (factor & 1) :
                    odd_factors = odd_factors + 1
        i = i + 1
    return odd_factors - 1

# Driver Code

# N as sum of consecutive numbers
N = 15
print (countOddFactors(N))

N = 10
print (countOddFactors(N))

# This code is contributed by 
# Manish Shaw(manishshaw1)
```

## C#

```
// C# program to count number of 
// ways to express N as sum of 
// consecutive numbers.
using System;

class GFG
{
    // returns the number
    // of odd factors
    static int countOddFactors(long n)
    {
        int odd_factors = 0;

        for (int i = 1; 1 * i * i <= n; i++) 
        {
            if (n % i == 0) 
            {

                // If i is an odd factor and
                // n is a perfect square
                if (1 * i * i == n) 
                {
                    if ((i & 1) == 1)
                        odd_factors++;
                }

                // If n is not 
                // perfect square
                else {
                    if ((i & 1) == 1)
                        odd_factors++;

                    int factor = (int)n / i;
                    if ((factor & 1) == 1)
                        odd_factors++;
                }
            }
        }
        return odd_factors - 1;
    }

    // Driver Code
    static void Main()
    {
        // N as sum of consecutive numbers
        long N = 15;
        Console.WriteLine(countOddFactors(N));

        N = 10;
        Console.WriteLine(countOddFactors(N));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number 
// of ways to express N as sum
// of consecutive numbers.

// returns the number
// of odd factors
function countOddFactors($n)
{
    $odd_factors = 0;

    for ($i = 1; 1 * $i * $i <= $n; $i++) 
    {
        if ($n % $i == 0) 
        {

            // If i is an odd factor and
            // n is a perfect square
            if (1 * $i * $i == $n) 
            {
                if ($i & 1)
                    $odd_factors++;
            }

            // If n is not perfect square
            else {
                if ($i & 1)
                    $odd_factors++;

                $factor = $n / $i;
                if ($factor & 1)
                    $odd_factors++;
            }
        }
    }
    return $odd_factors - 1;
}

// Driver Code

// N as sum of consecutive numbers
$N = 15;
echo (countOddFactors($N) . ("\n"));

$N = 10;
echo (countOddFactors($N));

// This code is contributed by 
// Manish Shaw(manishshaw1)
?>
```

**Output :**

```
3
1

```

这个项目的时间复杂度是 O(N^0.5).