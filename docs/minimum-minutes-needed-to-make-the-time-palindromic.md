# 使时间回文所需的最小分钟数

> 原文:[https://www . geesforgeks . org/最少需要几分钟才能完成回文时间/](https://www.geeksforgeeks.org/minimum-minutes-needed-to-make-the-time-palindromic/)

给定[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，该字符串将时间以 24 小时格式存储为**“HH:****MM”**。任务是找到使时间回文所需增加的最小分钟数。

**示例:**

> **输入:** str = "05:39"
> **输出:** 11
> **说明:**分钟值变为 50 需要 11 分钟，05:50 是回文时间
> 
> **示例:**
> **输入:** str = "13:31"
> **输出:** 0
> **说明:**既然，13:31 已经是回文了因此，需要 0 分钟

**进场:**
思路是贪婪地递增分钟值，直到时间值变成回文。运行一个 while 循环来增加分钟值，同时检查小时值和分钟值是否形成[回文](https://www.geeksforgeeks.org/c-program-check-given-string-palindrome/)。
增加分钟和小时值时，确保当分钟值为 **60** 和小时值为 **24** 时，检查基础条件。
以下是上述方法的实施:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to get the required minutes
int get_palindrome_time(string str)
{
    int hh, mm;

    // Storing hour and minute value
    // in integral form
    hh
        = (str[0] - 48) * 10
        + (str[1] - 48);
    mm
        = (str[3] - 48) * 10
        + (str[4] - 48);

    int requiredTime = 0;

    // Keep iterating till first digit
    // hour becomes equal to second
    // digit of minute and second digit
    // of hour becomes equal to first
    // digit of minute
    while (hh % 10 != mm / 10
        || hh / 10 != mm % 10) {

        ++mm;

        // If mins is 60, increase hour, and
        // reinitilialized to 0
        if (mm == 60) {
            mm = 0;
            ++hh;
        }

        // If hours is 60, reinitialized to 0
        if (hh == 24)
            hh = 0;
        ++requiredTime;
    }

    // Return the required time
    return requiredTime;
}

// Driver Code
int main()
{
    // Given Time as a string
    string str = "05:39";

    // Function Call
    cout << get_palindrome_time(str)
        << endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to get the required minutes
public static int get_palindrome_time(String str)
{
    int hh, mm;

    // Storing hour and minute value
    // in integral form
    hh = (str.charAt(0) - 48) * 10 +
        (str.charAt(1) - 48);
    mm = (str.charAt(3) - 48) * 10 +
        (str.charAt(4) - 48);

    int requiredTime = 0;

    // Keep iterating till first digit
    // hour becomes equal to second
    // digit of minute and second digit
    // of hour becomes equal to first
    // digit of minute
    while (hh % 10 != mm / 10 ||
        hh / 10 != mm % 10)
    {
        ++mm;

        // If mins is 60, increase hour, and
        // reinitilialized to 0
        if (mm == 60)
        {
            mm = 0;
            ++hh;
        }

        // If hours is 60, reinitialized to 0
        if (hh == 24)
            hh = 0;
        ++requiredTime;
    }

    // Return the required time
    return requiredTime;
}

// Driver code
public static void main(String[] args)
{

    // Given Time as a string
    String str = "05:39";

    // Function Call
    System.out.println(get_palindrome_time(str));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to get the required minutes 
def get_palindrome_time(str):

    # Storing hour and minute value
    # in integral form
    hh = ((ord(str[0]) - 48) * 10 +
          (ord(str[1]) - 48))
    mm = ((ord(str[3]) - 48) * 10 +
          (ord(str[4]) - 48))

    requiredTime = 0

    # Keep iterating till first digit
    # hour becomes equal to second
    # digit of minute and second digit
    # of hour becomes equal to first
    # digit of minute
    while (hh % 10 != mm // 10 or
          hh // 10 != mm % 10):
        mm += 1

        # If mins is 60, increase hour, and
        # reinitilialized to 0
        if (mm == 60):
            mm = 0
            hh += 1

        # If hours is 60, reinitialized to 0
        if (hh == 24):
            hh = 0

        requiredTime += 1;

    # Return the required time
    return requiredTime

if __name__=="__main__":

    # Given Time as a string
    str = "05:39";

    # Function call
    print(get_palindrome_time(str));

# This code is contributed by rutvik_56
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to get the required minutes
public static int get_palindrome_time(string str)
{
    int hh, mm;

    // Storing hour and minute value
    // in integral form
    hh = (str[0] - 48) * 10 +
        (str[1] - 48);
    mm = (str[3] - 48) * 10 +
        (str[4] - 48);

    int requiredTime = 0;

    // Keep iterating till first digit
    // hour becomes equal to second
    // digit of minute and second digit
    // of hour becomes equal to first
    // digit of minute
    while (hh % 10 != mm / 10 ||
        hh / 10 != mm % 10)
    {
        ++mm;

        // If mins is 60, increase hour,
        // and reinitilialized to 0
        if (mm == 60)
        {
            mm = 0;
            ++hh;
        }

        // If hours is 60, reinitialized to 0
        if (hh == 24)
            hh = 0;
        ++requiredTime;
    }

    // Return the required time
    return requiredTime;
}

// Driver code
public static void Main(string[] args)
{

    // Given Time as a string
    string str = "05:39";

    // Function Call
    Console.Write(get_palindrome_time(str));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to get the required minutes
function get_palindrome_time(str)
{
    let hh, mm;

    // Storing hour and minute value
    // in letegral form
    hh = (str[0].charCodeAt() - 48) * 10 +
        (str[1].charCodeAt() - 48);
    mm = (str[3].charCodeAt() - 48) * 10 +
        (str[4].charCodeAt() - 48);

    let requiredTime = 0;

    // Keep iterating till first digit
    // hour becomes equal to second
    // digit of minute and second digit
    // of hour becomes equal to first
    // digit of minute
    while (hh % 10 != Math.floor(mm / 10) ||
        Math.floor(hh / 10) != mm % 10)
    {
        ++mm;

        // If mins is 60, increase hour, and
        // reinitilialized to 0
        if (mm == 60)
        {
            mm = 0;
            ++hh;
        }

        // If hours is 60, reinitialized to 0
        if (hh == 24)
            hh = 0;
        ++requiredTime;
    }

    // Return the required time
    return requiredTime;
}
// Driver Code

    // Given Time as a string
    let str = "05:39";

    // Function Call
    document.write(get_palindrome_time(str.split('')));

</script>
```

**Output:** 

```
11
```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*