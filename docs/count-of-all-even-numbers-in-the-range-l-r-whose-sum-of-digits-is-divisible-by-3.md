# 数字之和可被 3 整除的[L，R]范围内所有偶数的计数

> 原文:[https://www . geesforgeks . org/范围内所有偶数的计数-l-r-其数字总和可被 3 整除/](https://www.geeksforgeeks.org/count-of-all-even-numbers-in-the-range-l-r-whose-sum-of-digits-is-divisible-by-3/)

给定两个整数 **L** 和 **R** 。任务是找出所有偶数在**【L，R】**范围内的计数，其位数之和可被 3 整除。
**举例:**

> **输入:** L = 18，R = 36
> **输出:** 4
> 18、24、30、36 是[18、36]范围内唯一为偶数且位数之和可被 3 整除的数字。
> **输入:** L = 7，R = 11
> **输出:** 0
> 在[7，11]范围内没有偶数，其位数之和可被 3 整除。

**天真方法:**初始化**计数= 0** 对于范围**【L，R】**中的每个数字，检查该数字是否可被 2 整除，其数字之和是否可被 3 整除。如果**是**，则增加计数。最后打印**计数**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the
// sum of digits of x
int sumOfDigits(int x)
{
    int sum = 0;
    while (x != 0) {
        sum += x % 10;
        x = x / 10;
    }
    return sum;
}

// Function to return the count
// of required numbers
int countNumbers(int l, int r)
{
    int count = 0;
    for (int i = l; i <= r; i++) {

        // If i is divisible by 2 and
        // sum of digits of i is divisible by 3
        if (i % 2 == 0 && sumOfDigits(i) % 3 == 0)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
int main()
{
    int l = 1000, r = 6000;
    cout << countNumbers(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the
// sum of digits of x
static int sumOfDigits(int x)
{
    int sum = 0;
    while (x != 0)
    {
        sum += x % 10;
        x = x / 10;
    }
    return sum;
}

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{
    int count = 0;
    for (int i = l; i <= r; i++)
    {

        // If i is divisible by 2 and
        // sum of digits of i is divisible by 3
        if (i % 2 == 0 && sumOfDigits(i) % 3 == 0)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
public static void main(String args[])
{
    int l = 1000, r = 6000;
    System.out.println(countNumbers(l, r));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# python implementation of the approach

# Function to return the
# sum of digits of x
def sumOfDigits(x):
    sum = 0
    while x != 0:
        sum += x % 10
        x = x//10
    return sum

# Function to return the count
# of required numbers
def countNumbers(l, r):
    count = 0
    for i in range(l, r + 1):

        # If i is divisible by 2 and
        # sum of digits of i is divisible by 3
        if i % 2 == 0 and sumOfDigits(i) % 3 == 0:
            count += 1
    return count

# Driver code
l = 1000; r = 6000
print(countNumbers(l, r))

# This code is contributed by Shrikant13
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// sum of digits of x
static int sumOfDigits(int x)
{
    int sum = 0;
    while (x != 0)
    {
        sum += x % 10;
        x = x / 10;
    }
    return sum;
}

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{
    int count = 0;
    for (int i = l; i <= r; i++)
    {

        // If i is divisible by 2 and
        // sum of digits of i is divisible by 3
        if (i % 2 == 0 && sumOfDigits(i) % 3 == 0)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
public static void Main()
{
    int l = 1000, r = 6000;
    Console.WriteLine(countNumbers(l, r));
}
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the sum of
// digits of x
function sumOfDigits( $x)
{
    $sum = 0;
    while ($x != 0)
    {
        $sum += $x % 10;
        $x = $x / 10;
    }
    return $sum;
}

// Function to return the count
// of required numbers
function countNumbers($l, $r)
{
    $count = 0;
    for ($i = $l; $i <= $r; $i++)
    {

        // If i is divisible by 2 and
        // sum of digits of i is divisible by 3
        if ($i % 2 == 0 &&
            sumOfDigits($i) % 3 == 0)
            $count++;
    }

    // Return the required count
    return $count;
}

// Driver code
$l = 1000;
$r = 6000;
echo countNumbers($l, $r);

// This code is contributed by princiraj1992
?>
```

## java 描述语言

```
<script>
// JavaScript implementation of the approach

// Function to return the
// sum of digits of x
function sumOfDigits(x)
{
    let sum = 0;
    while (x != 0) {
        sum += x % 10;
        x = Math.floor(x / 10);
    }
    return sum;
}

// Function to return the count
// of required numbers
function countNumbers(l, r)
{
    let count = 0;
    for (let i = l; i <= r; i++) {

        // If i is divisible by 2 and
        // sum of digits of i is divisible by 3
        if (i % 2 == 0 && sumOfDigits(i) % 3 === 0)
            count++;
    }

    // Return the required count
    return count;
}

// Driver code
    let l = 1000, r = 6000;
    document.write(countNumbers(l, r));

// This code is contributed by Manoj.
</script>
```

**Output:** 

```
834
```

**时间复杂度:**O(r–l)
**高效进场:**

1.  我们必须检查这个数是否能被 2 整除。
2.  我们必须检查数字的和是否能被 3 整除，这意味着这个数能被 3 整除。

所以总的来说，我们必须检查一个数是否能被 2 和 3 整除，因为 2 和 3 都是同素的，所以我们必须检查一个数是否能被它们的乘积整除，即 6。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of required numbers
int countNumbers(int l, int r)
{

    // Count of numbers in range
    // which are divisible by 6
    return ((r / 6) - (l - 1) / 6);
}

// Driver code
int main()
{
    int l = 1000, r = 6000;
    cout << countNumbers(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{

    // Count of numbers in range
    // which are divisible by 6
    return ((r / 6) - (l - 1) / 6);
}

// Driver code
public static void main(String[] args)
{
    int l = 1000, r = 6000;
    System.out.println(countNumbers(l, r));
}
}

// This code is contributed by princiraj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of required numbers
def countNumbers(l, r) :

    # Count of numbers in range
    # which are divisible by 6
    return ((r // 6) - (l - 1) // 6);

# Driver code
if __name__ == "__main__" :

    l = 1000; r = 6000;
    print(countNumbers(l, r));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;    

class GFG
{

// Function to return the count
// of required numbers
static int countNumbers(int l, int r)
{

    // Count of numbers in range
    // which are divisible by 6
    return ((r / 6) - (l - 1) / 6);
}

// Driver code
public static void Main(String[] args)
{
    int l = 1000, r = 6000;
    Console.WriteLine(countNumbers(l, r));
}
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of required numbers
function countNumbers($l, $r)
{

    // Count of numbers in range
    // which are divisible by 6
    return ((int)($r / 6) -
            (int)(($l - 1) / 6));
}

// Driver code
$l = 1000; $r = 6000;
echo(countNumbers($l, $r));

// This code is contributed
// by Code_Mech.
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of required numbers
function countNumbers(l, r)
{

    // Count of numbers in range
    // which are divisible by 6
    return (parseInt(r / 6) - parseInt((l - 1) / 6));
}

// Driver code
var l = 1000, r = 6000;
document.write(countNumbers(l, r));

</script>
```

**Output:** 

```
834
```

**时间复杂度:** O(1)