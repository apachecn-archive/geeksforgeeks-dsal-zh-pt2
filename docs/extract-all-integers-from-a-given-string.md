# 从给定字符串中提取所有整数

> 原文:[https://www . geesforgeks . org/从给定字符串中提取所有整数/](https://www.geeksforgeeks.org/extract-all-integers-from-a-given-string/)

给定一个[字符串](https://www.geeksforgeeks.org/string-data-structure/) **字符串**，从中提取所有整数单词。

**示例:**

> **输入:** str = "1Hello2 & *你好吗
> **输出:** 1 2 5
> 
> **输入:** str = "嘿，各位，我有 500 卢比，我会花 100 "
> T3】输出: 500 100

**方法:**要解决此问题，请执行以下步骤:

1.  创建一个字符串 **tillNow** ，它将存储到目前为止所有创建的整数。用空字符串初始化它。
2.  现在开始遍历字符串**字符串**，在每次迭代中:
    1.  如果一个字符是一个数字，将其添加到字符串**至**中。
    2.  否则，检查字符串**至**是否为空。如果不为空，则将其转换为整数，并在打印后清空。
3.  现在，循环结束后，再次检查字符串**至**是否为空。如果不是，那么将其转换为整数并打印出来。

下面是上述方法的实现

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to extract integers from
// the string str
void extractIntegers(string str)
{
    int n = str.size();

    // This variable will store each founded
    // integer temporarily
    string tillNow = "";

    for (int i = 0; i < n; i++) {

        // If current character is an integer, then
        // add it to string tillNow
        if (str[i] - '0' >= 0 and str[i] - '0' <= 9) {
            tillNow += str[i];
        }

        // Otherwise, check if tillNow is empty or not
        // If it isn't then convert tillNow to integer
        // and empty it after printing
        else {
            if (tillNow.size() > 0) {
                cout << stoi(tillNow) << ' ';

                tillNow = "";
            }
        }
    }

    // if tillNow isn't empty then convert tillNow
    // to integer and print it
    if (tillNow.size() > 0) {
        cout << stoi(tillNow) << ' ';
    }
}

// Driver Code
int main()
{
    string str = "Hey everyone, "
                 "I have 500 rupees and"
                 " I would spend a 100";
    extractIntegers(str);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

// Function to extract integers from
// the String str
static void extractIntegers(char []str)
{
    int n = str.length;

    // This variable will store each founded
    // integer temporarily
    String tillNow = "";

    for (int i = 0; i < n; i++) {

        // If current character is an integer, then
        // add it to String tillNow
        if (str[i] - '0' >= 0 && str[i] - '0' <= 9) {
            tillNow += str[i];
        }

        // Otherwise, check if tillNow is empty or not
        // If it isn't then convert tillNow to integer
        // and empty it after printing
        else {
            if (tillNow.length() > 0) {
                System.out.print(Integer.parseInt(tillNow) +" ");

                tillNow = "";
            }
        }
    }

    // if tillNow isn't empty then convert tillNow
    // to integer and print it
    if (tillNow.length() > 0) {
        System.out.print(Integer.parseInt(tillNow) +" ");
    }
}

// Driver Code
public static void main(String[] args)
{
    String str = "Hey everyone, "
                 +"I have 500 rupees and"
                 +" I would spend a 100";
    extractIntegers(str.toCharArray());
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to extract integers from
# the string str
def extractIntegers(string) :

    n = len(string);

    # This variable will store each founded
    # integer temporarily
    tillNow = "";

    for i in range(n) :

        # If current character is an integer, then
        # add it to string tillNow
        if (ord(string[i]) - ord('0') >= 0 and ord(string[i]) - ord('0') <= 9) :
            tillNow += string[i];

        # Otherwise, check if tillNow is empty or not
        # If it isn't then convert tillNow to integer
        # and empty it after printing
        else :
            if (len(tillNow) > 0) :
                print(int(tillNow),end = ' ');

                tillNow = "";

    # if tillNow isn't empty then convert tillNow
    # to integer and print it
    if (len(tillNow) > 0) :
        print(int(tillNow),end = ' ');

# Driver Code
if __name__ == "__main__" :

    string  = "Hey everyone, I have 500 rupees and I would spend a 100";

    extractIntegers(string);

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

    // Function to extract integers from
    // the String str
    static void extractIntegers(char[] str)
    {
        int n = str.Length;

        // This variable will store each founded
        // integer temporarily
        String tillNow = "";

        for (int i = 0; i < n; i++)
        {

            // If current character is an integer, then
            // add it to String tillNow
            if (str[i] - '0' >= 0 && str[i] - '0' <= 9)
            {
                tillNow += str[i];
            }

            // Otherwise, check if tillNow is empty or not
            // If it isn't then convert tillNow to integer
            // and empty it after printing
            else
            {
                if (tillNow.Length > 0)
                {
                    Console.Write(int.Parse(tillNow) + " ");

                    tillNow = "";
                }
            }
        }

        // if tillNow isn't empty then convert tillNow
        // to integer and print it
        if (tillNow.Length > 0)
        {
            Console.Write(int.Parse(tillNow) + " ");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        String str = "Hey everyone, "
                     + "I have 500 rupees and"
                     + " I would spend a 100";
        extractIntegers(str.ToCharArray());
    }
}

// This code is contributed by Saurabh Jaiswal
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to extract integers from
// the string str
function extractIntegers(str) {
  let n = str.length;

  // This variable will store each founded
  // integer temporarily
  let tillNow = "";

  for (let i = 0; i < n; i++) {

    // If current character is an integer, then
    // add it to string tillNow
    if (str[i].charCodeAt(0) - '0'.charCodeAt(0) >= 0 && str[i].charCodeAt(0) - '0'.charCodeAt(0) <= 9) {
      tillNow += str[i];
    }

    // Otherwise, check if tillNow is empty or not
    // If it isn't then convert tillNow to integer
    // and empty it after printing
    else {
      if (tillNow.length > 0) {
        document.write(tillNow + ' ');
        tillNow = "";
      }
    }
  }

  // if tillNow isn't empty then convert tillNow
  // to integer and print it
  if (tillNow.length > 0) {
    document.write(tillNow + ' ');
  }
}

// Driver Code
let str = "Hey everyone, I have 500 rupees and I would spend a 100";
extractIntegers(str);

// This code is contributed by gfgking.
</script>
```

**Output**

```
500 100 
```

**时间复杂度:**O(N)
T3】辅助空间: O(N)