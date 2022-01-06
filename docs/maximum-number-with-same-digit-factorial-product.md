# 同位数阶乘乘积的最大值

> 原文:[https://www . geesforgeks . org/同位数最大值-阶乘-乘积/](https://www.geeksforgeeks.org/maximum-number-with-same-digit-factorial-product/)

给定一个代表整数的字符串 **str** ，任务是找到最大的数字*，该数字没有任何前导或尾随的 0 或 1*，其位数的阶乘乘积等于 **str** 位数的阶乘乘积。
**举例:**

> **输入:**N = 4370
> T3】输出: 73322
> 4！* 3!* 7!* 0!= 7!* 3!* 3!* 2!* 2!= 725760
> **输入:** N = 1280
> **输出:** 72222
> 1！* 2!* 8!* 0!= 7!* 2!* 2!* 2!* 2!= 80640

**进场:**

*   将**字符串**的每个数字的阶乘表示为素数阶乘的*乘积。*
*   如果**字符串**仅包含 **0** 或 **1** 作为其数字，则显示给定的数字，因为没有前导和尾随的 0 或 1 是不可能输出的。
*   如果遇到数字 **1、2、3、5 或 7** ，则需要将它们作为数字包含在结果数字中。
*   如果遇到数字 **4、6、8 或 9** ，则将它们表示为素数阶乘的乘积，
    *   4!可以表示为 3！* 2!* 2!。
    *   6!可以表示为 5！* 3!。
    *   8!可以表示为 7！* 2!* 2!* 2!。
    *   还有 9！可以表示为 7！* 3!* 3!* 2!。
*   最后，通过将生成的数字按降序排列来形成数字，以获得满足条件的最大数字。

**插图:**

> 让我们考虑给定的输入 4370。它的每个数字的阶乘如下:
> 4！= 24 = 2!* 2 !* 3!
> 3！= 6 = 3!
> 7！= 5040 = 7!
> 因此最大数字的位数频率为:
> 
> *   **7** 的频率为 **1** 。
> 
> *   **3** 的频率为 **2** 。
> 
> *   **2** 的频率为 **2** 。
> 
> 因此输出是 73322。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required number
string getNumber(string s)
{
    int number_of_digits = s.length();

    int freq[10] = { 0 };

    // Count the frequency of each digit
    for (int i = 0; i < number_of_digits; i++) {
        if (s[i] == '1'
            || s[i] == '2'
            || s[i] == '3'
            || s[i] == '5'
            || s[i] == '7') {
            freq[s[i] - 48] += 1;
        }

        // 4! can be expressed as 2! * 2! * 3!
        if (s[i] == '4') {
            freq[2] += 2;
            freq[3]++;
        }

        // 6! can be expressed as 5! * 3!
        if (s[i] == '6') {
            freq[5]++;
            freq[3]++;
        }

        // 8! can be expressed as 7! * 2! * 2! * 2!

        if (s[i] == '8') {
            freq[7]++;
            freq[2] += 3;
        }

        // 9! can be expressed as 7! * 3! * 3! * 2!

        if (s[i] == '9') {
            freq[7]++;
            freq[3] += 2;
            freq[2]++;
        }
    }

    // To store the required number
    string t = "";

    // If number has only either 1 and 0 as its digits
    if (freq[1] == number_of_digits
        || freq[0] == number_of_digits
        || (freq[0] + freq[1]) == number_of_digits) {
        return s;
    }
    else {

        // Generate the greatest number possible
        for (int i = 9; i >= 2; i--) {
            int ctr = freq[i];
            while (ctr--) {
                t += (char)(i + 48);
            }
        }

        return t;
    }
}

// Driver code
int main()
{
    string s = "1280";
    cout << getNumber(s);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

import java.io.*;

class GFG {

// Function to return the required number
static String getNumber(String s)
{
    int number_of_digits = s.length();

    int freq[] = new int[10];

    // Count the frequency of each digit
    for (int i = 0; i < number_of_digits; i++) {
        if (s.charAt(i) == '1'
            || s.charAt(i) == '2'
            || s.charAt(i) == '3'
            || s.charAt(i) == '5'
            || s.charAt(i) == '7') {
            freq[s.charAt(i) - 48] += 1;
        }

        // 4! can be expressed as 2! * 2! * 3!
        if (s.charAt(i) == '4') {
            freq[2] += 2;
            freq[3]++;
        }

        // 6! can be expressed as 5! * 3!
        if (s.charAt(i) == '6') {
            freq[5]++;
            freq[3]++;
        }

        // 8! can be expressed as 7! * 2! * 2! * 2!

        if (s.charAt(i) == '8') {
            freq[7]++;
            freq[2] += 3;
        }

        // 9! can be expressed as 7! * 3! * 3! * 2!

        if (s.charAt(i) == '9') {
            freq[7]++;
            freq[3] += 2;
            freq[2]++;
        }
    }

    // To store the required number
    String t = "";

    // If number has only either 1 and 0 as its digits
    if (freq[1] == number_of_digits
        || freq[0] == number_of_digits
        || (freq[0] + freq[1]) == number_of_digits) {
        return s;
    }
    else {

        // Generate the greatest number possible
        for (int i = 9; i >= 2; i--) {
            int ctr = freq[i];
            while ((ctr--)>0) {
                t += (char)(i + 48);
            }
        }

        return t;
    }
}

    // Driver code

    public static void main (String[] args) {
            String s = "1280";
    System.out.println(getNumber(s));
    }
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required number
def getNumber(s):

    number_of_digits = len(s);

    freq=[0]*10;

    # Count the frequency of each digit
    for i in range(number_of_digits):
        if (s[i] == '1'    or s[i] == '2' or s[i] == '3' or s[i] == '5' or s[i] == '7'):
            freq[ord(s[i]) - 48] += 1;

        # 4! can be expressed as 2! * 2! * 3!
        if (s[i] == '4'):
            freq[2] += 2;
            freq[3]+=1;

        # 6! can be expressed as 5! * 3!
        if (s[i] == '6'):
            freq[5]+=1;
            freq[3]+=1;

        # 8! can be expressed as 7! * 2! * 2! * 2!

        if (s[i] == '8'):
            freq[7]+=1;
            freq[2] += 3;

        # 9! can be expressed as 7! * 3! * 3! * 2!

        if (s[i] == '9'):
            freq[7]+=1;
            freq[3] += 2;
            freq[2]+=1;

    # To store the required number
    t = "";

    # If number has only either 1 and 0 as its digits
    if (freq[1] == number_of_digits or freq[0] == number_of_digits or (freq[0] + freq[1]) == number_of_digits):
        return s;
    else:

        # Generate the greatest number possible
        for i in range(9,1,-1):
            ctr = freq[i];
            while (ctr>0):
                t += chr(i + 48);
                ctr-=1;

        return t;

# Driver code

s = "1280";
print(getNumber(s));

# This code is contributed by mits
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the
// required number
static String getNumber(string s)
{
    int number_of_digits = s.Length;

    int []freq = new int[10];

    // Count the frequency of each digit
    for (int i = 0;
             i < number_of_digits; i++)
    {
        if (s[i] == '1' || s[i] == '2' ||
            s[i] == '3' || s[i] == '5' ||
            s[i] == '7')
        {
            freq[s[i] - 48] += 1;
        }

        // 4! can be expressed as 2! * 2! * 3!
        if (s[i] == '4')
        {
            freq[2] += 2;
            freq[3]++;
        }

        // 6! can be expressed as 5! * 3!
        if (s[i] == '6')
        {
            freq[5]++;
            freq[3]++;
        }

        // 8! can be expressed as 7! * 2! * 2! * 2!
        if (s[i] == '8')
        {
            freq[7]++;
            freq[2] += 3;
        }

        // 9! can be expressed as 7! * 3! * 3! * 2!
        if (s[i] == '9')
        {
            freq[7]++;
            freq[3] += 2;
            freq[2]++;
        }
    }

    // To store the required number
    string t = "";

    // If number has only either 1
    // and 0 as its digits
    if (freq[1] == number_of_digits ||
        freq[0] == number_of_digits ||
       (freq[0] + freq[1]) == number_of_digits)
    {
        return s;
    }
    else
    {

        // Generate the greatest number possible
        for (int i = 9; i >= 2; i--)
        {
            int ctr = freq[i];
            while ((ctr--)>0)
            {
                t += (char)(i + 48);
            }
        }

        return t;
    }
}

// Driver code
public static void Main ()
{
    string s = "1280";
    Console.WriteLine(getNumber(s));
}
}

// This code is contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required number
function getNumber($s)
{
    $number_of_digits = strlen($s);

    $freq=array_fill(0,10,0);

    // Count the frequency of each digit
    for ($i = 0; $i < $number_of_digits; $i++) {
        if ($s[$i] == '1'
            || $s[$i] == '2'
            || $s[$i] == '3'
            || $s[$i] == '5'
            || $s[$i] == '7') {
            $freq[ord($s[$i]) - 48] += 1;
        }

        // 4! can be expressed as 2! * 2! * 3!
        if ($s[$i] == '4') {
            $freq[2] += 2;
            $freq[3]++;
        }

        // 6! can be expressed as 5! * 3!
        if ($s[$i] == '6') {
            $freq[5]++;
            $freq[3]++;
        }

        // 8! can be expressed as 7! * 2! * 2! * 2!

        if ($s[$i] == '8') {
            $freq[7]++;
            $freq[2] += 3;
        }

        // 9! can be expressed as 7! * 3! * 3! * 2!

        if ($s[$i] == '9') {
            $freq[7]++;
            $freq[3] += 2;
            $freq[2]++;
        }
    }

    // To store the required number
    $t = "";

    // If number has only either 1 and 0 as its digits
    if ($freq[1] == $number_of_digits
        || $freq[0] == $number_of_digits
        || ($freq[0] + $freq[1]) == $number_of_digits) {
        return $s;
    }
    else {

        // Generate the greatest number possible
        for ($i = 9; $i >= 2; $i--) {
            $ctr = $freq[$i];
            while ($ctr--) {
                $t .= chr($i + 48);
            }
        }

        return $t;
    }
}

// Driver code

    $s = "1280";
    echo getNumber($s);

// this code is contributed by mits
?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the
    // required number
    function getNumber(s)
    {
        let number_of_digits = s.length;

        let freq = new Array(10);
        freq.fill(0);

        // Count the frequency of each digit
        for (let i = 0; i < number_of_digits; i++)
        {
            if (s[i] == '1' || s[i] == '2' ||
                s[i] == '3' || s[i] == '5' ||
                s[i] == '7')
            {
                freq[s[i].charCodeAt() - 48] += 1;
            }

            // 4! can be expressed as 2! * 2! * 3!
            if (s[i] == '4')
            {
                freq[2] += 2;
                freq[3]++;
            }

            // 6! can be expressed as 5! * 3!
            if (s[i] == '6')
            {
                freq[5]++;
                freq[3]++;
            }

            // 8! can be expressed as 7! * 2! * 2! * 2!
            if (s[i] == '8')
            {
                freq[7]++;
                freq[2] += 3;
            }

            // 9! can be expressed as 7! * 3! * 3! * 2!
            if (s[i] == '9')
            {
                freq[7]++;
                freq[3] += 2;
                freq[2]++;
            }
        }

        // To store the required number
        let t = "";

        // If number has only either 1
        // and 0 as its digits
        if (freq[1] == number_of_digits ||
            freq[0] == number_of_digits ||
           (freq[0] + freq[1]) == number_of_digits)
        {
            return s;
        }
        else
        {

            // Generate the greatest number possible
            for (let i = 9; i >= 2; i--)
            {
                let ctr = freq[i];
                while ((ctr--)>0)
                {
                    t += String.fromCharCode(i + 48);
                }
            }

            return t;
        }
    }

    let s = "1280";
    document.write(getNumber(s));

</script>
```

**Output:** 

```
72222
```