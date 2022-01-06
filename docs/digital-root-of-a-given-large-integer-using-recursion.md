# 使用递归的给定大整数的数字根

> 原文:[https://www . geesforgeks . org/digital-给定大整数的根使用递归/](https://www.geeksforgeeks.org/digital-root-of-a-given-large-integer-using-recursion/)

正整数的 [**数字根**](https://www.geeksforgeeks.org/digital-rootrepeated-digital-sum-given-integer/) 是通过对整数的数字求和得到的。如果结果值是个位数，那么这个位数就是数字根。如果结果值包含两位或两位以上的数字，则将这些数字相加，并重复该过程。为了获得一个位数，这种情况会持续很长时间。
给定大量 **N** ，任务是找到它的数字根。输入的数字可能很大，即使我们使用 long long int 也可能无法存储。
**示例:**

> **输入:**N = 67598789078975654568907098676987
> **输出:** 5
> **说明:**
> 上述数字的单个数字之和= 212
> 212 的单个数字之和= 5
> 所以数字根为 5
> **输入:**num = 876598755

**进场:**

1.  找出一个数字的所有[数字。](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)
2.  把所有的数字一个一个加起来。
3.  如果最终和包含一个以上的数字，再次调用[递归函数](https://www.geeksforgeeks.org/recursive-functions/)使其成为一个位数。
4.  以一位数获得的结果是数字的数字根。

以下是上述方法的实现:

## C++

```
// C++ program to print the digital
// root of a given very large number

#include <iostream>
using namespace std;

// Function to convert given
// sum into string
string convertToString(int sum)
{
    string str = "";
    // Loop to extract digit one by one
    // from the given sum and concatenate
    // into the string
    while (sum) {
        // Type casting for concatenation
        str = str + (char)((sum % 10) + '0');
        sum = sum / 10;
    }
    // Return converted string
    return str;
}

// Function to get individual digit
// sum from string
string GetIndividulaDigitSum(string str,
                             int len)
{
    int sum = 0;
    // Loop to get individual digit sum
    for (int i = 0; i < len; i++) {
        sum = sum + str[i] - '0';
    }
    // Function call to convert
    // sum into string
    return convertToString(sum);
}

// Function to calculate the digital
// root of a very large number
int GetDigitalRoot(string str)
{
    // Base condition
    if (str.length() == 1) {
        return str[0] - '0';
    }
    // Function call to get
    // individual digit sum
    str = GetIndividulaDigitSum(
        str,
        str.length());
    // Recursive function to get digital
    // root of a very large number
    return GetDigitalRoot(str);
}
int main()
{
    string str
        = "675987890789756545689070986776987";

    // Function to print final digit
    cout << GetDigitalRoot(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the digital
// root of a given very large number
class GFG{

// Function to convert given
// sum into String
static String convertToString(int sum)
{
    String str = "";

    // Loop to extract digit one by one
    // from the given sum and concatenate
    // into the String
    while (sum > 0) {

        // Type casting for concatenation
        str = str + (char)((sum % 10) + '0');
        sum = sum / 10;
    }

    // Return converted String
    return str;
}

// Function to get individual digit
// sum from String
static String GetIndividulaDigitSum(String str,
                             int len)
{
    int sum = 0;

    // Loop to get individual digit sum
    for (int i = 0; i < len; i++) {
        sum = sum + str.charAt(i) - '0';
    }

    // Function call to convert
    // sum into String
    return convertToString(sum);
}

// Function to calculate the digital
// root of a very large number
static int GetDigitalRoot(String str)
{
    // Base condition
    if (str.length() == 1) {
        return str.charAt(0) - '0';
    }

    // Function call to get
    // individual digit sum
    str = GetIndividulaDigitSum(
        str,
        str.length());

    // Recursive function to get digital
    // root of a very large number
    return GetDigitalRoot(str);
}

// Driver code
public static void main(String[] args)
{
    String str
        = "675987890789756545689070986776987";

    // Function to print final digit
    System.out.print(GetDigitalRoot(str));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 program to print the digital
# root of a given very large number

# Function to convert given
# sum into string
def convertToString(sum):
    str1 = ""

    # Loop to extract digit one by one
    # from the given sum and concatenate
    # into the string
    while (sum):

        # Type casting for concatenation
        str1 = str1 + chr((sum % 10) + ord('0'))
        sum = sum // 10

    # Return converted string
    return str1

# Function to get individual digit
# sum from string
def GetIndividulaDigitSum(str1, len1):
    sum = 0
    # Loop to get individual digit sum
    for i in range(len1):
        sum = sum + ord(str1[i]) - ord('0')

    # Function call to convert
    # sum into string
    return convertToString(sum)

# Function to calculate the digital
# root of a very large number
def GetDigitalRoot(str1):
    # Base condition
    if (len(str1) == 1):
        return ord(str1[0] ) - ord('0')

    # Function call to get
    # individual digit sum
    str1 = GetIndividulaDigitSum(str1,len(str1))
    # Recursive function to get digital
    # root of a very large number
    return GetDigitalRoot(str1)

if __name__ == '__main__':
    str1 = "675987890789756545689070986776987"

    # Function to print final digit
    print(GetDigitalRoot(str1))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# program to print the digital
// root of a given very large number
using System;
class GFG{

// Function to convert given
// sum into String
static String convertToString(int sum)
{
  String str = "";

  // Loop to extract digit one by one
  // from the given sum and concatenate
  // into the String
  while (sum > 0)
  {
    // Type casting for concatenation
    str = str + (char)((sum % 10) + '0');
    sum = sum / 10;
  }

  // Return converted String
  return str;
}

// Function to get individual digit
// sum from String
static String GetIndividulaDigitSum(String str,
                                    int len)
{
  int sum = 0;

  // Loop to get individual digit sum
  for (int i = 0; i < len; i++)
  {
    sum = sum + str[i] - '0';
  }

  // Function call to convert
  // sum into String
  return convertToString(sum);
}

// Function to calculate the digital
// root of a very large number
static int GetDigitalRoot(String str)
{
  // Base condition
  if (str.Length == 1)
  {
    return str[0] - '0';
  }

  // Function call to get
  // individual digit sum
  str = GetIndividulaDigitSum(str,
                              str.Length);

  // Recursive function to get digital
  // root of a very large number
  return GetDigitalRoot(str);
}

// Driver code
public static void Main(String[] args)
{
  String str =
         "675987890789756545689070986776987";

  // Function to print readonly digit
  Console.Write(GetDigitalRoot(str));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to print the digital
    // root of a given very large number

    // Function to convert given
    // sum into string
    function convertToString(sum)
    {
        let str = "";
        // Loop to extract digit one by one
        // from the given sum and concatenate
        // into the string
        while (sum > 0)
        {

            // Type casting for concatenation
            str = str + String.fromCharCode((sum % 10) + '0'.charCodeAt());
            sum = parseInt(sum / 10, 10);
        }
        // Return converted string
        return str;
    }

    // Function to get individual digit
    // sum from string
    function GetIndividulaDigitSum(str, len)
    {
        let sum = 0;

        // Loop to get individual digit sum
        for (let i = 0; i < len; i++) {
            sum = sum + str[i].charCodeAt() - '0'.charCodeAt();
        }

        // Function call to convert
        // sum into string
        return convertToString(sum);
    }

    // Function to calculate the digital
    // root of a very large number
    function GetDigitalRoot(str)
    {
        // Base condition
        if (str.length == 1) {
            return (str[0].charCodeAt() - '0'.charCodeAt());
        }

        // Function call to get
        // individual digit sum
        str = GetIndividulaDigitSum(str, str.length);

        // Recursive function to get digital
        // root of a very large number
        return GetDigitalRoot(str);
    }

    let str = "675987890789756545689070986776987";

    // Function to print final digit
    document.write(GetDigitalRoot(str));

// This code is contributed by mukesh07.
</script>
```

**Output:** 

```
5
```