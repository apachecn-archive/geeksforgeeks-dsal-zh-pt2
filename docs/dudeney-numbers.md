# 杜德利数字

> 原文:[https://www.geeksforgeeks.org/dudeney-numbers/](https://www.geeksforgeeks.org/dudeney-numbers/)

给定一个整数 **n** ，任务是检查 **n** 是否为[杜德尼号](https://en.wikipedia.org/wiki/Dudeney_number)。杜德尼数是一个正整数，它是一个完美的立方体，其十进制数的总和等于该数的立方根。

**示例:**

> **输入:**N = 19683
> T3】输出:是
> 19683 = 27 <sup>3</sup> 和 1 + 9 + 6 + 8 + 3 = 27
> 
> **输入:**N = 75742
> T3】输出:否

**进场:**

*   检查 n 是否是一个完美的立方体，如果不是，那么它不能是一个杜德尼数。
*   如果 n 是一个完美的立方体，那么计算它的数字之和。如果它的位数之和等于它的立方根，那么它就是一个杜德尼数，否则就不是。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// n is a Dudeney number
bool isDudeney(int n)
{
    int cube_rt = int(round((pow(n, 1.0 / 3.0))));

    // If n is not a perfect cube
    if (cube_rt * cube_rt * cube_rt != n)
        return false;

    int dig_sum = 0;
    int temp = n;
    while (temp > 0) {

        // Last digit
        int rem = temp % 10;

        // Update the digit sum
        dig_sum += rem;

        // Remove the last digit
        temp /= 10;
    }

    // If cube root of n is not equal to
    // the sum of its digits
    if (cube_rt != dig_sum)
        return false;

    return true;
}

// Driver code
int main()
{
    int n = 17576;
    if (isDudeney(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;

class GFG
{

// Function that returns true if
// n is a Dudeney number
static boolean isDudeney(int n)
{
    int cube_rt = (int)(Math.round((Math.pow(n, 1.0 / 3.0))));

    // If n is not a perfect cube
    if (cube_rt * cube_rt * cube_rt != n)
        return false;

    int dig_sum = 0;
    int temp = n;
    while (temp > 0)
    {

        // Last digit
        int rem = temp % 10;

        // Update the digit sum
        dig_sum += rem;

        // Remove the last digit
        temp /= 10;
    }

    // If cube root of n is not equal to
    // the sum of its digits
    if (cube_rt != dig_sum)
        return false;

    return true;
}

// Driver code
public static void main(String[] args)
{
    int n = 17576;
    if (isDudeney(n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python implementation of the approach

# Function that returns true if
# n is a Dudeney number
def isDudeney(n):
    cube_rt = int(round((pow(n, 1.0 / 3.0))))

    # If n is not a perfect cube
    if cube_rt * cube_rt * cube_rt != n:
        return False

    dig_sum = 0
    temp = n
    while temp>0:

        # Last digit
        rem = temp % 10

        # Update the digit sum
        dig_sum += rem

        # Remove the last digit
        temp//= 10

    # If cube root of n is not equal to
    # the sum of its digits
    if cube_rt != dig_sum:
        return False

    return True

# Driver code
if __name__ == '__main__':

    n = 17576
    if isDudeney(n):
        print("Yes")
    else:
        print("No")
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if
// n is a Dudeney number
static bool isDudeney(int n)
{
    int cube_rt = (int)(Math.Round((Math.Pow(n, 1.0 / 3.0))));

    // If n is not a perfect cube
    if (cube_rt * cube_rt * cube_rt != n)
        return false;

    int dig_sum = 0;
    int temp = n;
    while (temp > 0)
    {

        // Last digit
        int rem = temp % 10;

        // Update the digit sum
        dig_sum += rem;

        // Remove the last digit
        temp /= 10;
    }

    // If cube root of n is not equal to
    // the sum of its digits
    if (cube_rt != dig_sum)
        return false;

    return true;
}

// Driver code
public static void Main()
{
    int n = 17576;
    if (isDudeney(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if
// n is a Dudeney number
function isDudeney($n)
{
    $cube_rt = floor(round((pow($n, 1.0 / 3.0))));

    // If n is not a perfect cube
    if ($cube_rt * $cube_rt * $cube_rt != $n)
        return false;

    $dig_sum = 0;
    $temp = $n;
    while ($temp > 0)
    {

        // Last digit
        $rem = $temp % 10;

        // Update the digit sum
        $dig_sum += $rem;

        // Remove the last digit
        $temp = $temp/10;
    }

    // If cube root of n is not equal to
    // the sum of its digits
    if ($cube_rt != $dig_sum)
        return false;

    return true;
}

// Driver code
$n = 17576;
if (isDudeney($n))
    echo "Yes";
else
    echo "No";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// n is a Dudeney number
function isDudeney(n)
{
    let cube_rt = parseInt(
        Math.round((Math.pow(n, 1.0 / 3.0))));

    // If n is not a perfect cube
    if (cube_rt * cube_rt * cube_rt != n)
        return false;

    let dig_sum = 0;
    let temp = n;

    while (temp > 0)
    {

        // Last digit
        let rem = temp % 10;

        // Update the digit sum
        dig_sum += rem;

        // Remove the last digit
        temp = parseInt(temp / 10);
    }

    // If cube root of n is not equal to
    // the sum of its digits
    if (cube_rt != dig_sum)
        return false;

    return true;
}

// Driver code
let n = 17576;

if (isDudeney(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by souravmahato348

</script>
```

**Output:** 

```
Yes
```