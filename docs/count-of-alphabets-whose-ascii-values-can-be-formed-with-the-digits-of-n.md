# 【ASCII 值可以用 N 的数字构成的字母数

> 原文:[https://www . geeksforgeeks . org/字母计数-其 ascii 值可以用 n 位数构成/](https://www.geeksforgeeks.org/count-of-alphabets-whose-ascii-values-can-be-formed-with-the-digits-of-n/)

给定一个整数 **N** 。您可以从这个数字中选择任意两个数字(数字可以相同，但它们的位置应该不同)，并以两种可能的方式中的任何一种进行排序。对于这些方法中的每一种，您都可以从中创建一个两位数的数字(可能包含前导零)。然后，你会挑选一个与这个数字相等的 ASCII 值对应的字符，即数字 **65** 对应**‘A’**、 **66** 到**‘B’**等等。任务是统计可以用这种方式挑选的**英文字母**(小写或大写)的数量。
**示例:**

> **输入:** N = 656
> **输出:** 2
> 只有字符‘A’(65)和‘B’(66)是可能的。
> **输入:** N = 1623455078
> **输出:** 27

**方法:**思路是观察可能的字符总数为(26 个小写+ 26 个大写= 52)。因此，检查这 52 个字符的出现次数，而不是从 N 开始生成所有可能的两位数组合。
因此，计算每个数字在 **N** 中的出现次数，然后对于每个字符(小写或大写)，找到它的 ASCII 值，并检查它是否可以从给定的数字中选取。最后打印这些字母的数量。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>

using namespace std;

// Function that returns true if num
// can be formed with the digits in
// digits[] array
bool canBePicked(int digits[], int num)
{

    int copyDigits[10];

    // Copy of the digits array
    for(int i =0 ; i < 10;i++)
        copyDigits[i]=digits[i];

    while (num > 0)
    {
        // Get last digit
        int digit = num % 10;

        // If digit array doesn't contain
        // current digit
        if (copyDigits[digit] == 0)
            return false;

        // One occurrence is used
        else
            copyDigits[digit] -= 1;

        // Remove the last digit
        num = floor(num / 10);
    }

    return true;
}

// Function to return the count of
// required alphabets
int countAlphabets(long n)
{

    int count = 0;

    // To store the occurrences of
    // digits (0 - 9)
    int digits[10]= {0};
    while (n > 0)
    {

        // Get last digit
        int digit = n % 10;

        // Update the occurrence of the digit
        digits[digit] += 1;

        // Remove the last digit
        n = floor(n / 10);
    }

    // If any lowercase character can be
    // picked from the current digits
    for(int i = 97; i <= 122 ;i ++)
        if (canBePicked(digits, i))
            count += 1;

    // If any uppercase character can be
    // picked from the current digits
    for(int i = 65; i < 91;i++)
        if (canBePicked(digits, i))
            count += 1;

    // Return the required count
    // of alphabets
    return count;
}

// Driver code
int main()
{

    long n = 1623455078;
    cout<<(countAlphabets(n));
}

// This code is contributed by chitranayal
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function that returns true if num can be formed
    // with the digits in digits[] array
    static boolean canBePicked(int digits[], int num)
    {
        // Copy of the digits array
        int copyDigits[] = digits.clone();
        while (num > 0) {

            // Get last digit
            int digit = num % 10;

            // If digit array doesn't contain current digit
            if (copyDigits[digit] == 0)
                return false;

            // One occurrence is used
            else
                copyDigits[digit]--;

            // Remove the last digit
            num /= 10;
        }

        return true;
    }

    // Function to return the count of required alphabets
    static int countAlphabets(int n)
    {
        int i, count = 0;

        // To store the occurrences of digits (0 - 9)
        int digits[] = new int[10];
        while (n > 0) {

            // Get last digit
            int digit = n % 10;

            // Update the occurrence of the digit
            digits[digit]++;

            // Remove the last digit
            n /= 10;
        }

        // If any lowercase character can be picked
        // from the current digits
        for (i = 'a'; i <= 'z'; i++)
            if (canBePicked(digits, i))
                count++;

        // If any uppercase character can be picked
        // from the current digits
        for (i = 'A'; i <= 'Z'; i++)
            if (canBePicked(digits, i))
                count++;

        // Return the required count of alphabets
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 1623455078;
        System.out.println(countAlphabets(n));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import math

# Function that returns true if num
# can be formed with the digits in
# digits[] array
def canBePicked(digits, num):

    copyDigits = [];

    # Copy of the digits array
    for i in range(len(digits)):
        copyDigits.append(digits[i]);

    while (num > 0):

        # Get last digit
        digit = num % 10;

        # If digit array doesn't contain
        # current digit
        if (copyDigits[digit] == 0):
            return False;

        # One occurrence is used
        else:
            copyDigits[digit] -= 1;

        # Remove the last digit
        num = math.floor(num / 10);

    return True;

# Function to return the count of
# required alphabets
def countAlphabets(n):

    count = 0;

    # To store the occurrences of
    # digits (0 - 9)
    digits = [0] * 10;
    while (n > 0):

        # Get last digit
        digit = n % 10;

        # Update the occurrence of the digit
        digits[digit] += 1;

        # Remove the last digit
        n = math.floor(n / 10);

    # If any lowercase character can be
    # picked from the current digits
    for i in range(ord('a'), ord('z') + 1):
        if (canBePicked(digits, i)):
            count += 1;

    # If any uppercase character can be
    # picked from the current digits
    for i in range(ord('A'), ord('Z') + 1):
        if (canBePicked(digits, i)):
            count += 1;

    # Return the required count
    # of alphabets
    return count;

# Driver code
n = 1623455078;
print(countAlphabets(n));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true
    // if num can be formed with
    // the digits in digits[] array
    static bool canBePicked(int []digits, int num)
    {
        // Copy of the digits array
        int []copyDigits = (int[]) digits.Clone();
        while (num > 0)
        {

            // Get last digit
            int digit = num % 10;

            // If digit array doesn't
            // contain current digit
            if (copyDigits[digit] == 0)
                return false;

            // One occurrence is used
            else
                copyDigits[digit]--;

            // Remove the last digit
            num /= 10;
        }

        return true;
    }

    // Function to return the count
    // of required alphabets
    static int countAlphabets(int n)
    {
        int i, count = 0;

        // To store the occurrences
        // of digits (0 - 9)
        int[] digits = new int[10];
        while (n > 0)
        {

            // Get last digit
            int digit = n % 10;

            // Update the occurrence of the digit
            digits[digit]++;

            // Remove the last digit
            n /= 10;
        }

        // If any lowercase character can be 
        // picked from the current digits
        for (i = 'a'; i <= 'z'; i++)
            if (canBePicked(digits, i))
                count++;

        // If any uppercase character can be 
        // picked from the current digits
        for (i = 'A'; i <= 'Z'; i++)
            if (canBePicked(digits, i))
                count++;

        // Return the required count of alphabets
        return count;
    }

    // Driver code
    public static void Main()
    {
        int n = 1623455078;
        Console.WriteLine(countAlphabets(n));
    }
}

// This code is contributed by
// tufan_gupta2000
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function that returns true if num
// can be formed with the digits in
// digits[] array
function canBePicked($digits, $num)
{
    $copyDigits = array();

    // Copy of the digits array
    for($i = 0; $i < sizeof($digits); $i++)
        $copyDigits[$i] = $digits[$i];

    while ($num > 0)
    {

        // Get last digit
        $digit = $num % 10;

        // If digit array doesn't contain
        // current digit
        if ($copyDigits[$digit] == 0)
            return false;

        // One occurrence is used
        else
            $copyDigits[$digit]--;

        // Remove the last digit
        $num = floor($num / 10);
    }

    return true;
}

// Function to return the count of
// required alphabets
function countAlphabets($n)
{
    $count = 0;

    // To store the occurrences of
    // digits (0 - 9)
    $digits = array_fill(0, 10, 0);
    while ($n > 0)
    {

        // Get last digit
        $digit = $n % 10;

        // Update the occurrence of the digit
        $digits[$digit]++;

        // Remove the last digit
        $n = floor($n / 10);
    }

    // If any lowercase character can be
    // picked from the current digits
    for ($i = ord('a'); $i <= ord('z'); $i++)
        if (canBePicked($digits, $i))
            $count++;

    // If any uppercase character can be 
    // picked from the current digits
    for ($i = ord('A');
         $i <= ord('Z'); $i++)
        if (canBePicked($digits, $i))
            $count++;

    // Return the required count
    // of alphabets
    return $count;
}

// Driver code
$n = 1623455078;
echo countAlphabets($n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
 //Javascript implementation of the approach

// Function that returns true if num
// can be formed with the digits in
// digits[] array
function canBePicked( digits, num)
{

    var copyDigits = new Array(10);;

    // Copy of the digits array
    for(var i =0 ; i < 10;i++)
        copyDigits[i]=digits[i];

    while (num > 0)
    {
        // Get last digit
        var digit = num % 10;

        // If digit array doesn't contain
        // current digit
        if (copyDigits[digit] == 0)
            return false;

        // One occurrence is used
        else
            copyDigits[digit] -= 1;

        // Remove the last digit
        num = Math.floor(num / 10);
    }

    return true;
}

// Function to return the count of
// required alphabets
function countAlphabets( n)
{

    var count = 0;

    // To store the occurrences of
    // digits (0 - 9)
    var digits = new Array(10);
    digits.fill(0);

    while (n > 0)
    {

        // Get last digit
        var digit = n % 10;

        // Update the occurrence of the digit
        digits[digit] += 1;

        // Remove the last digit
        n = Math.floor(n / 10);
    }

    // If any lowercase character can be
    // picked from the current digits
    for(var i = 97; i <= 122 ;i ++)
        if (canBePicked(digits, i))
            count += 1;

    // If any uppercase character can be
    // picked from the current digits
    for(var i = 65; i < 91;i++)
        if (canBePicked(digits, i))
            count += 1;

    // Return the required count
    // of alphabets
    return count;
}

var n = 1623455078;
document.write(countAlphabets(n));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
27
```