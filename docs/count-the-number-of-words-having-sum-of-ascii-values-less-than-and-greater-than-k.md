# 统计 ASCII 值之和小于和大于 k 的单词数

> 原文:[https://www . geeksforgeeks . org/count-字数-ascii 值之和-小于和大于-k/](https://www.geeksforgeeks.org/count-the-number-of-words-having-sum-of-ascii-values-less-than-and-greater-than-k/)

给定一个字符串，任务是统计 Ascii 值之和小于等于给定 k 的单词数。
**示例:**

```
Input: str = "Learn how to code", k = 400
Output:
Number of words having sum of ascii less than k = 2
Number of words having sum of ascii greater than or equal to k = 2

Input: str = "Geeks for Geeks", k = 400
Output:
Number of words having sum of ascii less than k = 1
Number of words having sum of ascii greater than or equal to k = 2
```

**方法:**统计 ASCII 值之和小于 k 的单词数，从单词总数中减去，得到 ASCII 值之和大于或等于 k 的单词数，开始逐字母遍历字符串，将 ASCII 值加和。如果有一个空格，那么如果总和小于 k，则增加计数，并将总和设置为 0。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the words
void CountWords(string str, int k)
{
    // Sum of ascii values
    int sum = 0;

    int NumberOfWords = 0;

    // Number of words having
    // sum of ascii less than k
    int counter = 0;

    int len = str.length();

    for (int i = 0; i < len; ++i) {
        // If character is a space
        if (str[i] == ' ') {
            if (sum < k)
                counter++;

            sum = 0;
            NumberOfWords++;
        }
        else
            // Add the ascii value to sum
            sum += str[i];
    }

    // Handling the Last word separately
    NumberOfWords++;
    if (sum < k)
        counter++;

    cout << "Number of words having sum of ASCII"
            " values less than k = "
         << counter << endl;
    cout << "Number of words having sum of ASCII values"
            " greater than or equal to k = "
         << NumberOfWords - counter;
}

// Driver code
int main()
{
    string str = "Learn how to code";
    int k = 400;
    CountWords(str, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
class GFG
{

// Function to count the words
static void CountWords(String str, int k)
{
    // Sum of ascii values
    int sum = 0;

    int NumberOfWords = 0;

    // Number of words having
    // sum of ascii less than k
    int counter = 0;

    int len = str.length();

    for (int i = 0; i < len; ++i)
    {
        // If character is a space
        if (str.charAt(i) == ' ')
        {
            if (sum < k)
            {
                counter++;
            }

            sum = 0;
            NumberOfWords++;
        }

        else // Add the ascii value to sum
        {
            sum += str.charAt(i);
        }
    }

    // Handling the Last word separately
    NumberOfWords++;
    if (sum < k)
    {
        counter++;
    }

    System.out.println("Number of words having sum " +
                    "of ASCII values less than k = " +
                                             counter);
    System.out.println("Number of words having sum of " +
           "ASCII values greater than or equal to k = " +
                              (NumberOfWords - counter));
}

// Driver code
public static void main(String[] args)
{
    String str = "Learn how to code";
    int k = 400;
    CountWords(str, k);
}
}

// This code is contributed by RAJPUT-JI
```

## 蟒蛇 3

```
# Python 3 implementation of the
# above approach

# Function to count the words
def CountWords(str, k):

    # Sum of ascii values
    sum = 0

    NumberOfWords = 0

    # Number of words having
    # sum of ascii less than k
    counter = 0

    l = len(str)

    for i in range(l):

        # If character is a space
        if (str[i] == ' ') :
            if (sum < k):
                counter += 1

            sum = 0
            NumberOfWords += 1

        else:

            # Add the ascii value to sum
            sum += ord(str[i])

    # Handling the Last word separately
    NumberOfWords += 1
    if (sum < k):
        counter += 1

    print("Number of words having sum of ASCII",
          "values less than k =", counter)
    print("Number of words having sum of ASCII values",
                        "greater than or equal to k =",
                               NumberOfWords - counter)

# Driver code
if __name__ == "__main__":

    str = "Learn how to code"
    k = 400
    CountWords(str, k)

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# implementation of the
// above approach
using System;

class GFG
{

// Function to count the words
static void CountWords(String str,
                       int k)
{
    // Sum of ascii values
    int sum = 0;

    int NumberOfWords = 0;

    // Number of words having
    // sum of ascii less than k
    int counter = 0;

    int len = str.Length;

    for (int i = 0; i < len; ++i)
    {
        // If character is a space
        if (str[i]==' ')
        {
            if (sum < k)
            {
                counter++;
            }

            sum = 0;
            NumberOfWords++;
        }
        else // Add the ascii value to sum
        {
            sum += str[i];
        }
    }

    // Handling the Last word
    // separately
    NumberOfWords++;
    if (sum < k)
    {
        counter++;
    }

    Console.WriteLine("Number of words having sum " +
                      "of ASCII values less than k = " +
                                               counter);
    Console.WriteLine("Number of words having sum of " +
          "ASCII values greater than or equal to k = " +
                             (NumberOfWords - counter));
}

// Driver code
public static void Main(String[] args)
{
    String str = "Learn how to code";
    int k = 400;
    CountWords(str, k);
}
}

// This code is contributed by RAJPUT-JI
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to count the words
function CountWords($str, $k)
{
    // Sum of ascii values
    $sum = 0;

    $NumberOfWords = 0;

    // Number of words having
    // sum of ascii less than k
    $counter = 0;

    $len = strlen($str);

    for ($i = 0; $i < $len; ++$i)
    {
        // If character is a space
        if ($str[$i] == ' ')
        {
            if ($sum < $k)
                $counter++;

            $sum = 0;
            $NumberOfWords++;
        }
        else

            // Add the ascii value to sum
            $sum += ord($str[$i]);
    }

    // Handling the Last word separately
    $NumberOfWords++;
    if ($sum < $k)
        $counter++;

    echo "Number of words having sum of ASCII" .
         " values less than k = " . $counter . "\n";
    echo "Number of words having sum of ASCII " .
         "values greater than or equal to k = " .
                     ($NumberOfWords - $counter);
}

// Driver code
$str = "Learn how to code";
$k = 400;
CountWords($str, $k);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the
// above approach

// Function to count the words
function CountWords(str, k)
{
    // Sum of ascii values
    let sum = 0;

    let NumberOfWords = 0;

    // Number of words having
    // sum of ascii less than k
    let counter = 0;

    let len = str.length;

    for (let i = 0; i < len; ++i) {
        // If character is a space
        if (str[i] == " ") {
            if (sum < k) {
                counter++;
            }

            sum = 0;
            NumberOfWords++;
        }
        else {
            // Add the ascii value to sum
            sum += str.charCodeAt(i);
        }
    }

    // Handling the Last word separately
    NumberOfWords++;
    if (sum < k) {
        counter++;
    }

    document.write("Number of words having sum " +
                   "of ASCII values less than k = " +
                                   counter + "<br>");
    document.write("Number of words having sum of " +
         "ASCII values greater than or equal to k = " +
                   (NumberOfWords - counter) + "<br>");
}

// Driver code

    let str = "Learn how to code";
    let k = 400;
    CountWords(str, k);

// This code is contributed by Surbhi Tyagi.

</script>
```

**Output:** 

```
Number of words having sum of ASCII values less than k = 2
Number of words having sum of ASCII values greater than or equal to k = 2
```

**时间复杂度:** O(N)
***辅助空间** : O(1)*