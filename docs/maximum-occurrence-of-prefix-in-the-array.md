# 数组中前缀的最大出现次数

> 原文:[https://www . geesforgeks . org/数组中前缀最大出现次数/](https://www.geeksforgeeks.org/maximum-occurrence-of-prefix-in-the-array/)

给定一个由小写英文字母组成的字符串。任务是统计非空[前缀](https://en.wikipedia.org/wiki/Prefix)作为[子串](https://en.wikipedia.org/wiki/Substring)在字符串中出现次数最多的次数。
**例:**

```
Input : str = "abbcdabbcd"
Output :  2
The prefix "abb" has maximum number of 
occurrences 2.

Input : str = "abc"
Output :  1
```

**方法:**想法是观察数组的每个前缀必须包含字符串的第一个字符，并且它的每个相应出现也将包含。此外，字符串的第一个字符是最小长度前缀。因此，出现次数最多的前缀将是字符串本身的第一个字符。因此，任务现在减少到查找给定字符串中第一个字符的频率。
以下是上述办法的实施情况:

## C++

```
// CPP program to find the number of occurrences
// of prefix which occurs maximum no. of time

#include <bits/stdc++.h>
using namespace std;

// Function to return the count of the
// required prefix
int prefixOccurrences(string str)
{
    char c = str[0];
    int countc = 0;

    // Find the frequency of first
    // character of string
    for (int i = 0; i < str.length(); i++) {
        if (str[i] == c)
            countc++;
    }

    return countc;
}

// Driver code
int main()
{
    string str = "abbcdabbcd";
    cout << prefixOccurrences(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number
// of occurrences of prefix which
// occurs maximum no. of time
class GFG
{

// Function to return the count of the
// required prefix
static int prefixOccurrences(String str)
{
    char c = str.charAt(0);
    int countc = 0;

    // Find the frequency of first
    // character of string
    for (int i = 0; i < str.length(); i++)
    {
        if (str.charAt(i) == c)
            countc++;
    }

    return countc;
}

// Driver code
public static void main(String args[])
{
    String str = "abbcdabbcd";
    System.out.println(prefixOccurrences(str));

}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 program to find the number
# of occurrences of prefix which
# occurs maximum no. of time

# Function to return the count
# of the required prefix
def prefixOccurrences(str1):

    c = str1[0]
    countc = 0

    # Find the frequency of first
    # character of str1ing
    for i in range(len(str1)):
        if (str1[i] == c):
            countc += 1

    return countc

# Driver code
str1 = "abbcdabbcd"
print(prefixOccurrences(str1))

# This code is contributed
# by mohit kumar
```

## C#

```
// C# program to find the number
// of occurrences of prefix which
// occurs maximum no. of time
using System;

class GFG
{

    // Function to return the count of the
    // required prefix
    static int prefixOccurrences(string str)
    {
        char c = str[0];
        int countc = 0;

        // Find the frequency of first
        // character of string
        for (int i = 0; i < str.Length; i++)
        {
            if (str[i] == c)
                countc++;
        }

        return countc;
    }

    // Driver code
    public static void Main()
    {
        string str = "abbcdabbcd";

        Console.WriteLine(prefixOccurrences(str));
    }
}

// This code is contributed by Ryuga
```

## java 描述语言

```
<script>

// JavaScript program to find the number
// of occurrences of prefix which
// occurs maximum no. of time

// Function to return the count of the
// required prefix
function prefixOccurrences(str)
{
    var c = str.charAt(0);
    var countc = 0;

    // Find the frequency of first
    // character of string
    for (var i = 0; i < str.length; i++)
    {
        if (str.charAt(i) == c)
            countc++;
    }

    return countc;
}

// Driver code

    var str = "abbcdabbcd";
    document.write(prefixOccurrences(str));

// This code is contributed by Amit Katiyar

</script>
```

**输出:**

```
2
```