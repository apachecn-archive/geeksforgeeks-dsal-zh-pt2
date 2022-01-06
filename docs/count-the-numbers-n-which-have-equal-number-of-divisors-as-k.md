# 计算与 K

有相同除数的数< N

> 原文:[https://www . geeksforgeeks . org/count-the-numbers-n-with-equal-number-of-dividers-as-k/](https://www.geeksforgeeks.org/count-the-numbers-n-which-have-equal-number-of-divisors-as-k/)

给定两个整数 **N** 和 **K** ，任务是计算所有与 **K** 具有相同正整数个数的数字 **< N** 。
**举例:**

> **输入:** n = 10，k = 5
> **输出:** 3
> 2，3，7 是仅有的有 2 除数的数< 10(等于 5 的除数)
> **输入:** n = 500，k = 6
> **输出:** 148

**进场:**

*   计算每个数 **< N** 的除数，并将结果存储在数组中，其中**arr【I】**包含 **i** 的除数。
*   遍历 **arr[]** ，如果 **arr[i] = arr[K]** 则更新**计数=计数+ 1** 。
*   最后打印**计数**的值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the
// divisors of a number
int countDivisors(int n)
{
    // Count the number of
    // 2s that divide n
    int x = 0, ans = 1;
    while (n % 2 == 0) {
        x++;
        n = n / 2;
    }
    ans = ans * (x + 1);

    // n must be odd at this point.
    // So we can skip one element
    for (int i = 3; i <= sqrt(n); i = i + 2) {

        // While i divides n
        x = 0;
        while (n % i == 0) {
            x++;
            n = n / i;
        }
        ans = ans * (x + 1);
    }

    // This condition is to
    // handle the case when
    // n is a prime number > 2
    if (n > 2)
        ans = ans * 2;

    return ans;
}

int getTotalCount(int n, int k)
{
    int k_count = countDivisors(k);

    // Count the total elements
    // that have divisors exactly equal
    // to as that of k's
    int count = 0;
    for (int i = 1; i < n; i++)
        if (k_count == countDivisors(i))
            count++;

    // Exclude k from the result if it
    // is smaller than n.
    if (k < n)
       count = count - 1;

    return count;
}

// Driver code
int main()
{
    int n = 500, k = 6;
    cout << getTotalCount(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

public class GFG{

    // Function to return the count of the
    // divisors of a number
    static int countDivisors(int n)
    {
        // Count the number of
        // 2s that divide n
        int x = 0, ans = 1;
        while (n % 2 == 0) {
            x++;
            n = n / 2;
        }
        ans = ans * (x + 1);

        // n must be odd at this point.
        // So we can skip one element
        for (int i = 3; i <= Math.sqrt(n); i = i + 2) {

            // While i divides n
            x = 0;
            while (n % i == 0) {
                x++;
                n = n / i;
            }
            ans = ans * (x + 1);
        }

        // This condition is to
        // handle the case when
        // n is a prime number > 2
        if (n > 2)
            ans = ans * 2;

        return ans;
    }

    static int getTotalCount(int n, int k)
    {
        int k_count = countDivisors(k);

        // Count the total elements
        // that have divisors exactly equal
        // to as that of k's
        int count = 0;
        for (int i = 1; i < n; i++)
            if (k_count == countDivisors(i))
                count++;

        // Exclude k from the result if it
        // is smaller than n.
        if (k < n)
        count = count - 1;

        return count;
    }

    // Driver code
     public static void main(String []args)
    {
        int n = 500, k = 6;
        System.out.println(getTotalCount(n, k));
    }
    // This code is contributed by Ryuga
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# the divisors of a number
def countDivisors(n):

    # Count the number of 2s that divide n
    x, ans = 0, 1
    while (n % 2 == 0):
        x += 1
        n = n / 2
    ans = ans * (x + 1)

    # n must be odd at this point.
    # So we can skip one element
    for i in range(3, int(n ** 1 / 2) + 1, 2):

        # While i divides n
        x = 0
        while (n % i == 0):
            x += 1
            n = n / i
        ans = ans * (x + 1)

    # This condition is to handle the
    # case when n is a prime number > 2
    if (n > 2):
        ans = ans * 2

    return ans

def getTotalCount(n, k):
    k_count = countDivisors(k)

    # Count the total elements that
    # have divisors exactly equal
    # to as that of k's
    count = 0
    for i in range(1, n):
        if (k_count == countDivisors(i)):
            count += 1

    # Exclude k from the result if it
    # is smaller than n.
    if (k < n):
        count = count - 1

    return count

# Driver code
if __name__ == '__main__':
    n, k = 500, 6
    print(getTotalCount(n, k))

# This code is contributed
# by 29AjayKumar
```

## C#

```
// C# implementation of the approach
using System;

public class GFG{

    // Function to return the count of the
    // divisors of a number
    static int countDivisors(int n)
    {
        // Count the number of
        // 2s that divide n
        int x = 0, ans = 1;
        while (n % 2 == 0) {
            x++;
            n = n / 2;
        }
        ans = ans * (x + 1);

        // n must be odd at this point.
        // So we can skip one element
        for (int i = 3; i <= Math.Sqrt(n); i = i + 2) {

            // While i divides n
            x = 0;
            while (n % i == 0) {
                x++;
                n = n / i;
            }
            ans = ans * (x + 1);
        }

        // This condition is to
        // handle the case when
        // n is a prime number > 2
        if (n > 2)
            ans = ans * 2;

        return ans;
    }

    static int getTotalCount(int n, int k)
    {
        int k_count = countDivisors(k);

        // Count the total elements
        // that have divisors exactly equal
        // to as that of k's
        int count = 0;
        for (int i = 1; i < n; i++)
            if (k_count == countDivisors(i))
                count++;

        // Exclude k from the result if it
        // is smaller than n.
        if (k < n)
        count = count - 1;

        return count;
    }

    // Driver code
     public static void Main()
    {
        int n = 500, k = 6;
        Console.WriteLine(getTotalCount(n, k));
    }   
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP  implementation of the approach
// Function to return the count of the
// divisors of a number

function  countDivisors($n)
{
    // Count the number of
    // 2s that divide n
    $x = 0;
    $ans = 1;
    while ($n % 2 == 0) {
        $x++;
        $n = $n / 2;
    }
    $ans = $ans * ($x + 1);

    // n must be odd at this point.
    // So we can skip one element
    for ($i = 3; $i <= sqrt($n); $i = $i + 2) {

        // While i divides n
        $x = 0;
        while ($n % $i == 0) {
            $x++;
            $n = $n / $i;
        }
        $ans = $ans * ($x + 1);
    }

    // This condition is to
    // handle the case when
    // n is a prime number > 2
    if ($n > 2)
        $ans = $ans * 2;

    return $ans;
}

function  getTotalCount($n, $k)
{
    $k_count = countDivisors($k);

    // Count the total elements
    // that have divisors exactly equal
    // to as that of k's
    $count = 0;
    for ($i = 1; $i < $n; $i++)
        if ($k_count == countDivisors($i))
            $count++;

    // Exclude k from the result if it
    // is smaller than n.
    if ($k < $n)
    $count = $count - 1;

    return $count;
}

// Driver code

    $n = 500;
    $k = 6;
    echo  getTotalCount($n, $k);

#This code is contributed by Sachin..
?>
```

## java 描述语言

```
<script>

//Javascript implementation of the approach

// Function to return the count of the
// divisors of a number
function countDivisors(n)
{
    // Count the number of
    // 2s that divide n
    var x = 0, ans = 1;
    while (n % 2 == 0) {
        x++;
        n = n / 2;
    }
    ans = ans * (x + 1);

    // n must be odd at this point.
    // So we can skip one element
    for (var i = 3; i <= Math.sqrt(n); i = i + 2)
    {

        // While i divides n
        x = 0;
        while (n % i == 0) {
            x++;
            n = n / i;
        }
        ans = ans * (x + 1);
    }

    // This condition is to
    // handle the case when
    // n is a prime number > 2
    if (n > 2)
        ans = ans * 2;

    return ans;
}

function getTotalCount( n, k)
{
    var k_count = countDivisors(k);

    // Count the total elements
    // that have divisors exactly equal
    // to as that of k's
    var count = 0;
    for (var i = 1; i < n; i++)
        if (k_count == countDivisors(i))
            count++;

    // Exclude k from the result if it
    // is smaller than n.
    if (k < n)
       count = count - 1;

    return count;
}

var n = 500, k = 6;
document.write(getTotalCount(n, k));

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
148
```

**优化:**
以上解决方案可以使用[筛选技术](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)进行优化。详见[计算小于等于 N 的整数个数，正好有 9 个除数](https://www.geeksforgeeks.org/count-number-of-integers-less-than-or-equal-to-n-which-has-exactly-9-divisors/)。