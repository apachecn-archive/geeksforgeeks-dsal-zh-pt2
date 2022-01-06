# 大数除以 12

> 原文:[https://www . geeksforgeeks . org/大数除以 12/](https://www.geeksforgeeks.org/divisibility-by-12-for-a-large-number/)

给定一个大的数，任务是检查这个数是否能被 12 整除。

**示例:**

```
Input : 12244824607284961224
Output : Yes

Input : 92387493287593874594898678979792
Output : No
```

这是非常简单的方法。如果一个数能被 4 和 3 整除，那么这个数就能被 12 整除。
**点 1** 。如果这个数的最后两位数能被 4 整除，那么这个数就能被 4 整除。详见[大数除以 4](https://www.geeksforgeeks.org/check-large-number-divisible-4-not/)。

**第 2 点**。如果一个数所有数字的和除以 3，那么这个数可以被 3 整除。详见[大数除以 3](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)。

## C++

```
// C++ Program to check if
// number is divisible by 12
#include <iostream>
using namespace std;

bool isDvisibleBy12(string num)
{
    // if number greater then 3
    if (num.length() >= 3) {

        // find last digit
        int d1 = (int)num[num.length() - 1];

        // no is odd
        if (d1 % 2 != 0)
            return (0);

        // find second last digit
        int d2 = (int)num[num.length() - 2];

        // find sum of all digits
        int sum = 0;
        for (int i = 0; i < num.length(); i++)
            sum += num[i];           

        return (sum % 3 == 0 && (d2 * 10 + d1) % 4 == 0);           
    }

    else {

        // if number is less then
        // or equal to 100
        int number = stoi(num);
        return (number % 12 == 0);
    }
}

// Driver function
int main()
{
    string num = "12244824607284961224"; 
    if (isDvisibleBy12(num))
        cout << "Yes" << endl;
    else
        cout << "No" << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if
// number is divisible by 12

import java.io.*;

class GFG {
static boolean isDvisibleBy12(String num)
{
    // if number greater then 3
    if (num.length() >= 3) {

        // find last digit
        int d1 = (int)num.charAt(num.length() - 1);

        // no is odd
        if (d1 % 2 != 0)
            return false;

        // find second last digit
        int d2 = (int)num.charAt(num.length() - 2);

        // find sum of all digits
        int sum = 0;
        for (int i = 0; i < num.length(); i++)
            sum += num.charAt(i);           

        return (sum % 3 == 0 &&
               (d2 * 10 + d1) % 4 == 0);           
    }

    else {

        // if number is less then
        // or equal to 100
        int number = Integer.parseInt(num);
        return (number % 12 == 0);
    }

// driver function
}
    public static void main (String[] args) {

    String num = "12244824607284961224"; 
    if (isDvisibleBy12(num))
        System.out.print("Yes");
    else
        System.out.print("No");

    }
}

// This code is contributed by Gitanjali.
```

## 蟒蛇 3

```
# Python Program to check if
# number is divisible by 12

import math

def isDvisibleBy12( num):

    # if number greater then 3
    if (len(num) >= 3):

        # find last digit
        d1 = int(num[len(num) - 1]);

        # no is odd
        if (d1 % 2 != 0):
            return False

        # find second last digit
        d2 = int(num[len(num) - 2])

        # find sum of all digits
        sum = 0
        for  i in range(0, len(num) ):
            sum += int(num[i])          

        return (sum % 3 == 0 and
               (d2 * 10 + d1) % 4 == 0)           

    else :

        # f number is less then
        # r equal to 100
        number = int(num)
        return (number % 12 == 0)

num = "12244824607284961224" 
if(isDvisibleBy12(num)):
       print("Yes")
else:
       print("No")

# This code is contributed by Gitanjali.
```

## C#

```
// C# Program to check if
// number is divisible by 12
using System;

class GFG
{
static bool isDvisibleBy12(string num)
{
    // if number greater then 3
    if (num.Length >= 3) {

        // find last digit
        int d1 = (int)num[num.Length - 1];

        // no is odd
        if (d1 % 2 != 0)
            return false;

        // find second last digit
        int d2 = (int)num[num.Length - 2];

        // find sum of all digits
        int sum = 0;
        for (int i = 0; i < num.Length; i++)
            sum += num[i];        

        return (sum % 3 == 0 &&
            (d2 * 10 + d1) % 4 == 0);        
    }

    else {

        // if number is less then
        // or equal to 100
        int number = int.Parse(num);
        return (number % 12 == 0);
    }
}

    // Driver function
    public static void Main ()
    {
       String num = "12244824607284961224";
       if (isDvisibleBy12(num))
          Console.Write("Yes");
       else
          Console.Write("No");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to check if
// number is divisible by 12

function isDvisibleBy12($num)
{

    // if number greater then 3
    if (strlen($num) >= 3)
    {

        // find last digit
        $d1 = (int)$num[strlen($num) - 1];

        // no is odd
        if ($d1 % 2 != 0)
            return (0);

        // find second last digit
        $d2 = (int)$num[strlen($num) - 2];

        // find sum of all digits
        $sum = 0;
        for ($i = 0; $i < strlen($num); $i++)
            $sum += $num[$i];    

        return ($sum % 3 == 0 &&
               ($d2 * 10 + $d1) % 4 == 0);        
    }

    else {

        // if number is less then
        // or equal to 100
        $number = stoi($num);
        return ($number % 12 == 0);
    }
}

// Driver Code
$num = "12244824607284961224";
if (isDvisibleBy12($num))
    echo("Yes");
else
    echo("No");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>

// Javascript program to check if
// number is divisible by 12
function isDvisibleBy12(num)
{

    // If number greater then 3
    if (num.length >= 3)
    {

        // Find last digit
        let d1 = num[num.length - 1].charCodeAt();

        // No is odd
        if (d1 % 2 != 0)
            return false;

        // Find second last digit
        let d2 = num[num.length - 2].charCodeAt();

        // Find sum of all digits
        let sum = 0;
        for(let i = 0; i < num.length; i++)
            sum += num[i].charCodeAt();        

        return ((sum % 3 == 0) &&
                 (d2 * 10 + d1) % 4 == 0);        
    }

    else
    {

        // If number is less then
        // or equal to 100
        let number = parseInt(num, 10);
        document.write(number);
        return(number % 12 == 0);
    }
}

// Driver code
let num = "12244824607284961224";
if (isDvisibleBy12(num))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by divyeshrabadiya07

</script>
```

输出:

```
Yes
```