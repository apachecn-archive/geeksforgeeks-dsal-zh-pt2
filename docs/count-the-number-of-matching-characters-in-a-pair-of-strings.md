# 统计一对字符串中匹配字符的数量

> 原文:[https://www . geesforgeks . org/count-字符串对中匹配字符的数量/](https://www.geeksforgeeks.org/count-the-number-of-matching-characters-in-a-pair-of-strings/)

给定一对非空字符串 **str1** 和 **str2** ，任务是计算这些字符串中匹配字符的数量。考虑字符串中重复字符的单个计数。
**例:**

> **输入:**str 1 =“abcdef”，str 2 =“defghia”
> T3】输出: 4
> 匹配字符为:a、d、e、f
> **输入:**str 1 =“aabcddekl 12”，str 2 =“bb22ll @ 55k”
> **输出:** 5
> 匹配字符为:b、1、2、@、k

**进场:**

1.  用 0 初始化计数器变量。
2.  从起始字符到结束字符迭代第一个字符串。
3.  如果在第二个字符串中找到从第一个字符串中提取的字符，则将计数器的值增加 1。
4.  最终答案将是 count/2，因为不考虑重复项。
5.  输出计数器的值

下面是上述方法的实现。

## C++

```
// C++ code to count number of matching
// characters in a pair of strings

#include <bits/stdc++.h>
using namespace std;

// Function to count the matching characters
void count(string str1, string str2)
{
    int c = 0, j = 0;

    // Traverse the string 1 char by char
    for (int i = 0; i < str1.length(); i++) {

        // This will check if str1[i]
        // is present in str2 or not
        // str2.find(str1[i]) returns -1 if not found
        // otherwise it returns the starting occurrence
        // index of that character in str2
        if (str2.find(str1[i]) >= 0
            and j == str1.find(str1[i]))
            c += 1;
        j += 1;
    }
    cout << "No. of matching characters are: "
         << c / 2;
}

// Driver code
int main()
{
    string str1 = "aabcddekll12@";
    string str2 = "bb2211@55k";

    count(str1, str2);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to count number of matching
// characters in a pair of strings
class GFG
{

    // Function to count the matching characters
    static void count(String str1, String str2)
    {
        int c = 0, j = 0;

        // Traverse the string 1 char by char
        for (int i = 0; i < str1.length(); i++)
        {

            // This will check if str1[i]
            // is present in str2 or not
            // str2.find(str1[i]) returns -1 if not found
            // otherwise it returns the starting occurrence
            // index of that character in str2
            if (str2\. indexOf(str1.charAt(i)) >= 0)
            {
                c += 1;
        }
    }
        System.out.println("No. of matching characters are: " + c);
    }

    // Driver code
    public static void main (String[] args)
    {
        String str1 = "aabcddekll12@";
        String str2 = "bb2211@55k";

        count(str1, str2);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 code to count number of matching
# characters in a pair of strings

# Function to count the matching characters
def count(str1, str2) :

    c = 0; j = 0;

    # Traverse the string 1 char by char
    for i in range(len(str1)) :

        # This will check if str1[i]
        # is present in str2 or not
        # str2.find(str1[i]) returns -1 if not found
        # otherwise it returns the starting occurrence
        # index of that character in str2
        if str1[i] in str2 :
            c += 1;
            #print(str1[i])
        j += 1;

    print("No. of matching characters are: ", c );

# Driver code
if __name__ == "__main__" :
    str1 = "aabcddekll12@";
    str2 = "bb2211@55k";

    count(str1, str2);

# This code is contributed by AnkitRai01
```

## C#

```
// C# code to count number of matching
// characters in a pair of strings
using System;

class GFG
{

    // Function to count the matching characters
    static void count(string str1, string str2)
    {
        int c = 0, j = 0;

        // Traverse the string 1 char by char
        for (int i = 0; i < str1.Length; i++)
        {

            // This will check if str1[i]
            // is present in str2 or not
            // str2.find(str1[i]) returns -1 if not found
            // otherwise it returns the starting occurrence
            // index of that character in str2
            if (str2.IndexOf(str1[i]) >= 0)
            {
                c += 1;
        }
    }
        Console.WriteLine("No. of matching characters are: " + c);
    }

    // Driver code
    public static void Main()
    {
        string str1 = "aabcddekll12@";
        string str2 = "bb2211@55k";

        count(str1, str2);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// JavaScript code to count number of matching
// characters in a pair of strings

// Function to count the matching characters
function count(str1, str2)
{
    var c = 0;

    // Traverse the string 1 char by char
    for (var i = 0; i < str1.length; i++) {

        // This will check if str1[i]
        // is present in str2 or not
        // str2.find(str1[i]) returns -1 if not found
        // otherwise it returns the starting occurrence
        // index of that character in str2
        if (str2.includes(str1[i]))
            c += 1;
    }
    document.write( "No. of matching characters are: " +
         + parseInt(c));
}

// Driver code

var str1 = "aabcddekll12@";
var str2 = "bb2211@55k";
count(str1, str2);

</script>
```

**Output:** 

```
No. of matching characters are: 5
```