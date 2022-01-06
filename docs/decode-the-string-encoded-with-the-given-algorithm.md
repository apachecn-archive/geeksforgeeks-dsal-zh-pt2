# 解码用给定算法编码的字符串

> 原文:[https://www . geesforgeks . org/解码给定算法编码的字符串/](https://www.geeksforgeeks.org/decode-the-string-encoded-with-the-given-algorithm/)

给定一个解码后的字符串 **str** ，该字符串是用以下编码算法解码的:
记下字符串的中间字符，然后将其删除，并重复该过程，直到没有剩余的字符。例如**“阿爸”**将编码为**“bbaa”**。
**注意**当字符串长度为偶数时，中间字符是两个中间字符的第一个字符。
**示例:**

```
Input: "ofrsgkeeeekgs"
Output: geeksforgeeks

Input: str = "bbaa"
Output: abba
```

**方法:**可以观察到，在对字符串进行解码时，编码字符串的第一个字母成为解码字符串的中值。因此，首先，写入编码字符串的第一个字符，并将其从编码字符串中删除，然后开始将编码字符串的第一个字符先添加到解码字符串的左侧，再添加到右侧，并重复执行此任务，直到编码字符串变为空。
**例如:**

```
Encoded String          Decoded String
ofrsgkeeeekgs           o
frsgkeeeekgs            fo
rsgkeeeekgs             for
sgkeeeekgs              sfor
gkeeeekgs               sforg
keeeekgs                ksforg
eeeekgs                 ksforge
eeekgs                  eksforge
eekgs                   eksforgee
ekgs                    eeksforgee
kgs                     eeksforgeek
gs                      geeksgorgeek
s                       geeksforgeeks                     
```

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to decode and print
// the original string
void decodeStr(string str, int len)
{

    // To store the decoded string
    char c[len] = "";
    int med, pos = 1, k;

    // Getting the mid element
    if (len % 2 == 1)
        med = len / 2;
    else
        med = len / 2 - 1;

    // Storing the first element of the
    // string at the median position
    c[med] = str[0];

    // If the length is even then store
    // the second element also
    if (len % 2 == 0)
        c[med + 1] = str[1];

    // k represents the number of characters
    // that are already stored in the c[]
    if (len & 1)
        k = 1;
    else
        k = 2;

    for (int i = k; i < len; i += 2) {
        c[med - pos] = str[i];

        // If string length is odd
        if (len % 2 == 1)
            c[med + pos] = str[i + 1];

        // If it is even
        else
            c[med + pos + 1] = str[i + 1];
        pos++;
    }

    // Print the decoded string
    for (int i = 0; i < len; i++)
        cout << c[i];
}

// Driver code
int main()
{
    string str = "ofrsgkeeeekgs";
    int len = str.length();

    decodeStr(str, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG{

// Function to decode and print
// the original String
static void decodeStr(String str, int len)
{

    // To store the decoded String
    char []c = new char[len];
    int med, pos = 1, k;

    // Getting the mid element
    if (len % 2 == 1)
        med = len / 2;
    else
        med = len / 2 - 1;

    // Storing the first element of the
    // String at the median position
    c[med] = str.charAt(0);

    // If the length is even then store
    // the second element also
    if (len % 2 == 0)
        c[med + 1] = str.charAt(1);

    // k represents the number of characters
    // that are already stored in the c[]
    if (len % 2 == 1)
        k = 1;
    else
        k = 2;

    for(int i = k; i < len; i += 2)
    {
       c[med - pos] = str.charAt(i);

       // If String length is odd
       if (len % 2 == 1)
           c[med + pos] = str.charAt(i + 1);

       // If it is even
       else
           c[med + pos + 1] = str.charAt(i + 1);
       pos++;
    }

    // Print the decoded String
    for (int i = 0; i < len; i++)
        System.out.print(c[i]);
}

// Driver code
public static void main(String[] args)
{
    String str = "ofrsgkeeeekgs";
    int len = str.length();

    decodeStr(str, len);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to decode and print
# the original string
def decodeStr(str, len):

    # To store the decoded string
    c = ["" for i in range(len)]
    pos = 1

    # Getting the mid element
    if(len % 2 == 1):
        med = int(len / 2)
    else:
        med = int(len / 2 - 1)

    # Storing the first element 
    # of the string at the
    # median position
    c[med] = str[0]

    # If the length is even
    # then store the second
    # element also
    if(len % 2 == 0):
        c[med + 1] = str[1]

    # k represents the number
    # of characters that are
    # already stored in the c[]
    if(len & 1):
        k = 1
    else:
        k = 2

    for i in range(k, len, 2):
        c[med - pos] = str[i]

        # If string length is odd
        if(len % 2 == 1):
            c[med + pos] = str[i + 1]

        # If it is even
        else:
            c[med + pos + 1] = str[i + 1]
        pos += 1

    # Print the decoded string
    print(*c, sep = "")

# Driver code
str = "ofrsgkeeeekgs"
len = len(str)
decodeStr(str, len)

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to decode and print
// the original String
static void decodeStr(String str, int len)
{

    // To store the decoded String
    char []c = new char[len];

    int med, pos = 1, k;

    // Getting the mid element
    if (len % 2 == 1)
        med = len / 2;
    else
        med = len / 2 - 1;

    // Storing the first element of the
    // String at the median position
    c[med] = str[0];

    // If the length is even then store
    // the second element also
    if (len % 2 == 0)
        c[med + 1] = str[1];

    // k represents the number of characters
    // that are already stored in the c[]
    if (len % 2 == 1)
        k = 1;
    else
        k = 2;

    for(int i = k; i < len; i += 2)
    {
       c[med - pos] = str[i];

       // If String length is odd
       if (len % 2 == 1)
           c[med + pos] = str[i + 1];

       // If it is even
       else
           c[med + pos + 1] = str[i + 1];
       pos++;
    }

    // Print the decoded String
    for(int i = 0; i < len; i++)
       Console.Write(c[i]);
}

// Driver code
public static void Main(String[] args)
{
    String str = "ofrsgkeeeekgs";
    int len = str.Length;

    decodeStr(str, len);
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to decode and print
// the original string
function decodeStr(str, len)
{

    // To store the decoded string
    var c = Array(len).fill("");
    var med, pos = 1, k;

    // Getting the mid element
    if (len % 2 == 1)
        med = parseInt(len / 2);
    else
        med = parseInt(len / 2) - 1;

    // Storing the first element of the
    // string at the median position
    c[med] = str[0];

    // If the length is even then store
    // the second element also
    if (len % 2 == 0)
        c[med + 1] = str[1];

    // k represents the number of characters
    // that are already stored in the c[]
    if (len & 1)
        k = 1;
    else
        k = 2;

    for (var i = k; i < len; i += 2) {
        c[med - pos] = str[i];

        // If string length is odd
        if (len % 2 == 1)
            c[med + pos] = str[i + 1];

        // If it is even
        else
            c[med + pos + 1] = str[i + 1];
        pos++;
    }

    // Print the decoded string
    for (var i = 0; i < len; i++)
    {
        document.write(c[i]);
    }
}

// Driver code
var str = "ofrsgkeeeekgs";
var len = str.length;
decodeStr(str, len);

</script>
```

**Output:** 

```
geeksforgeeks
```

**复杂性:** O(n)