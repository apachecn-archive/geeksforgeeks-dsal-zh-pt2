# 提取任意一对分隔符之间的子字符串

> 原文:[https://www . geeksforgeeks . org/extract-任何分隔符对之间的子字符串/](https://www.geeksforgeeks.org/extract-substrings-between-any-pair-of-delimiters/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) [字符串](https://www.geeksforgeeks.org/string-data-structure/)，任务是提取出现在两个分隔符之间的子字符串，即**“[”**和**“]”**。

**示例:**

> **输入:** str =“【这是一个要提取的字符串】”
> **输出:**这是一个要提取的字符串
> **解释:**方括号**'['****']'**作为给定字符串中的分隔符。
> 
> **输入:** str=【这是第一个】忽略的文本【这是第二个】
> **输出:**
> 这是第一个
> 这是第二个
> **解释:**方括号**“[”**和**“**用作给定字符串中的分隔符。

[**堆栈**](https://www.geeksforgeeks.org/stack-data-structure/)**-基于方法:** [迭代字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)的字符，并将遇到的每个 **'['** 的索引插入堆栈。对于遇到的每一个 **']'** ，只需[弹出](https://www.geeksforgeeks.org/stack-pop-method-in-java/)栈顶[存储的索引](https://www.geeksforgeeks.org/stack-top-c-stl/)并打印中间的子串。

下面是上述方法的实现

## C++14

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print strings present
// between any pair of delimiters
void printSubsInDelimiters(string str)
{
    // Stores the indices of
    stack<int> dels;
    for (int i = 0; i < str.size(); i++) {
        // If opening delimiter
        // is encountered
        if (str[i] == '[') {
            dels.push(i);
        }

        // If closing delimiter
        // is encountered
        else if (str[i] == ']' && !dels.empty()) {

            // Extract the position
            // of opening delimiter
            int pos = dels.top();

            dels.pop();

            // Length of substring
            int len = i - 1 - pos;

            // Extract the substring
            string ans = str.substr(
                pos + 1, len);

            cout << ans << endl;
        }
    }
}

// Driver Code
int main()
{

    string str = "[This is first] ignored text [This is second]";

    printSubsInDelimiters(str);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to print Strings present
// between any pair of delimiters
static void printSubsInDelimiters(String str)
{

    // Stores the indices of
    Stack<Integer> dels = new Stack<Integer>();
    for(int i = 0; i < str.length(); i++)
    {

        // If opening delimiter
        // is encountered
        if (str.charAt(i) == '[')
        {
            dels.add(i);
        }

        // If closing delimiter
        // is encountered
        else if (str.charAt(i) == ']' &&
                 !dels.isEmpty())
        {

            // Extract the position
            // of opening delimiter
            int pos = dels.peek();

            dels.pop();

            // Length of subString
            int len = i - 1 - pos;

            // Extract the subString
            String ans = str.substring(
                pos + 1, pos + 1 + len);

            System.out.print(ans + "\n");
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "[This is first] ignored text [This is second]";

    printSubsInDelimiters(str);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach

# Function to print strings present
# between any pair of delimiters
def printSubsInDelimiters(string) :

    # Stores the indices
    dels = [];
    for i in range(len(string)):

        # If opening delimiter
        # is encountered
        if (string[i] == '[') :
            dels.append(i);

        # If closing delimiter
        # is encountered
        elif (string[i] == ']' and len(dels) != 0) :

            # Extract the position
            # of opening delimiter
            pos = dels[-1];
            dels.pop();

            # Length of substring
            length = i - 1 - pos;

            # Extract the substring
            ans = string[pos + 1 : pos + 1 + length];

            print(ans);

# Driver Code
if __name__ == "__main__" :

    string = "[This is first] ignored text [This is second]";

    printSubsInDelimiters(string);

    # This code is contributed by AnkThon
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;

class GFG{

// Function to print strings present
// between any pair of delimiters
static void printSubsInDelimiters(string str)
{

    // Stores the indices of
    Stack dels = new Stack();
    for(int i = 0; i < str.Length; i++)
    {

        // If opening delimiter
        // is encountered
        if (str[i] == '[')
        {
            dels.Push(i);
        }

        // If closing delimiter
        // is encountered
        else if (str[i] == ']' && dels.Count > 0)
        {

            // Extract the position
            // of opening delimiter
            int pos = (int)dels.Peek();

            dels.Pop();

            // Length of substring
            int len = i - 1 - pos;

            // Extract the substring
            string ans = str.Substring(
                pos + 1, len);

            Console.WriteLine(ans);
        }
    }
}

// Driver Code
static void Main()
{
    string str = "[This is first] ignored text [This is second]";

    printSubsInDelimiters(str);
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>
    // Javascript program to implement
    // the above approach

    // Function to print strings present
    // between any pair of delimiters
    function printSubsInDelimiters(str)
    {

        // Stores the indices of
        let dels = [];
        for(let i = 0; i < str.length; i++)
        {

            // If opening delimiter
            // is encountered
            if (str[i] == '[')
            {
                dels.push(i);
            }

            // If closing delimiter
            // is encountered
            else if ((str[i] == ']') &&
                     (dels.length > 0))
            {

                // Extract the position
                // of opening delimiter
                let pos = dels[dels.length - 1];

                dels.pop();

                // Length of substring
                let len = i - 1 - pos;

                // Extract the substring
                let ans;
                if(pos < len)
                {
                    ans = str.substring(pos + 1,
                                       len + 1);
                }
                else{
                    ans = str.substring(pos + 1,
                          len + pos + 1);
                }
                document.write(ans + "</br>");
            }
        }
    }

    let str = "[This is first] ignored text [This is second]";

    printSubsInDelimiters(str);

</script>
```

**Output:** 

```
This is first
This is second
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)

**节省空间的方法:**想法是用 [**正则表达式**](https://www.geeksforgeeks.org/regular-expressions-in-java/) 来解决这个问题。创建一个正则表达式，将两个分隔符之间的字符串提取为 regex = "\\[(。*?)\\]"并将给定的字符串与正则表达式匹配。打印形成的子序列。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
#include <regex>
using namespace std;

// Function to print Strings present
// between any pair of delimiters
void printSubsInDelimiters(string str)
{

    // Regex to extract the string
    // between two delimiters
    const regex pattern("\\[(.*?)\\]");

    for(sregex_iterator it = sregex_iterator(
        str.begin(), str.end(), pattern);
        it != sregex_iterator(); it++)
    {

        // flag type for determining the
        // matching behavior here it is
        // for matches on 'string' objects
        smatch match;
        match = *it;

        cout << match.str(1) << endl;
    }
    return;
}

// Driver Code
int main()
{

    // Input String
    string str = "[This is first] ignored text [This is second]";

    // Function Call
    printSubsInDelimiters(str);

    return 0;
}

// This code is contributed by yuvraj_chandra
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.regex.*;

class GFG{

// Function to print Strings present
// between any pair of delimiters
public static void printSubsInDelimiters(String str)
{

    // Regex to extract the string
    // between two delimiters
    String regex = "\\[(.*?)\\]";

    // Compile the Regex.
    Pattern p = Pattern.compile(regex);

    // Find match between given string
    // and regular expression
    // using Pattern.matcher()
    Matcher m = p.matcher(str);

    // Get the subsequence
    // using find() method
    while (m.find())
    {
        System.out.println(m.group(1));
    }
}

// Driver code
public static void main(String args[])
{

    // Input String
    String str = "[This is first] ignored text [This is second]";

    // Function Call
    printSubsInDelimiters(str);
}
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import re

# Function to print Strings present
# between any pair of delimiters
def printSubsInDelimiters(str):

    # Regex to extract the string
    # between two delimiters
    regex = "\\[(.*?)\\]"

    # Find match between given string
    # and regular expression
    # using re.findall()
    matches = re.findall(regex, str)

    # Print the matches
    for match in matches:
        print(match)

# Driver code

# Input String
str = "[This is first] ignored text [This is second]"

# Function Call
printSubsInDelimiters(str)

# This code is contributed by yuvraj_chandra
```

**Output:** 

```
This is first
This is second
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)