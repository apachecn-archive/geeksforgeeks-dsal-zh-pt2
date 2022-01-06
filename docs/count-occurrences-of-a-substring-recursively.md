# 递归计算子串的出现次数

> 原文:[https://www . geesforgeks . org/count-出现次数-子串-递归/](https://www.geeksforgeeks.org/count-occurrences-of-a-substring-recursively/)

给定两个字符串 str1 和 str2，任务是使用递归计算“str1”中“str2”出现的次数。
**例:**

```
Input : str1 = "geeksforgeeks", str2 = "geek"
Output : 2

Input: kanekihiishishi
Output: 3
```

假设问题有 n 个部分，将问题划分为 n-1 个已经完成的部分，之后要执行的操作仅限于一个部分。从而将递归方法分为两种情况，即基本情况和递归情况。
在这个特殊的问题中，基本情况涉及到如果 str1 的长度小于 str2 的长度。
现在，说说递归的情况，将 str1 的第一个子串与 str2 进行比较，对剩余的 str1 进行递归。

## C++

```
// Recursive C++ program for counting number of substrings
#include <iostream>
#include <string>
using namespace std;

// Recursive function to count
// the number of occurrences of "hi" in str.
int countSubstrig(string str1, string str2)
{
    int n1 = str1.length();
    int n2 = str2.length();

    // Base Case
    if (n1 == 0 || n1 < n2)
        return 0;

    // Recursive Case
    // Checking if the first substring matches
    if (str1.substr(0, n2).compare(str2) == 0)
        return countSubstrig(str1.substr(n2-1), str2) + 1;

    // Otherwise, return the count from
    // the remaining index
    return countSubstrig(str1.substr(n2-1), str2);
}

// Driver function
int main()
{
    string str1 = "geeksforgeeks", str2 = "geeks";
    cout << countSubstrig(str1, str2) << endl;

    str1 = "hikakashi", str2 = "hi";
    cout << countSubstrig(str1, str2) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Recursive Java program for
// counting number of substrings
class GFG
{

// Recursive function to
// count the number of
// occurrences of "hi" in str.
static int countSubstrig(String str1,
                         String str2)
{
    int n1 = str1.length();
    int n2 = str2.length();

    // Base Case
    if (n1 == 0 || n1 < n2)
        return 0;

    // Recursive Case
    // Checking if the first
    // substring matches
    if (str1.substring(0, n2).equals(str2))
        return countSubstrig(str1.substring(n2 - 1),
                                            str2) + 1;

    // Otherwise, return the count
    // from the remaining index
    return countSubstrig(str1.substring(n2 - 1),
                                        str2);
}

// Driver Code
public static void main(String args[])
{
    String str1 = "geeksforgeeks",
           str2 = "geeks";
    System.out.println(countSubstrig(str1,
                                     str2));

    str1 = "hikakashi";
    str2 = "hi";
    System.out.println(countSubstrig(str1,
                                     str2));

}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Recursive Python3 program for
# counting number of substrings

# Recursive function to
# count the number of
# occurrences of "hi" in str.
def countSubstrig(str1, str2):

    n1 = len(str1);
    n2 = len(str2);

    # Base Case
    if (n1 == 0 or n1 < n2):
        return 0;

    # Recursive Case
    # Checking if the first
    # substring matches
    if (str1[0 : n2] == str2):
        return countSubstrig(str1[n2 - 1:],
                             str2) + 1;

    # Otherwise, return the count
    # from the remaining index
    return countSubstrig(str1[n2 - 1:],
                         str2);

# Driver Code
if __name__ == '__main__':

    str1 = "geeksforgeeks";
    str2 = "geeks";
    print(countSubstrig(str1, str2));

    str1 = "hikakashi";
    str2 = "hi";
    print(countSubstrig(str1, str2));

# This code is contributed by Princi Singh
```

## C#

```
// Recursive C# program for
// counting number of substrings
using System;
class GFG
{

// Recursive function to
// count the number of
// occurrences of "hi" in str.
static int countSubstrig(String str1,
                         String str2)
{
    int n1 = str1.Length;
    int n2 = str2.Length;

    // Base Case
    if (n1 == 0 || n1 < n2)
        return 0;

    // Recursive Case
    // Checking if the first
    // substring matches
    if (str1.Substring(0, n2).Equals(str2))
        return countSubstrig(str1.Substring(n2 - 1),
                                            str2) + 1;

    // Otherwise, return the
    // count from the remaining
    // index
    return countSubstrig(str1.Substring(n2 - 1),
                                        str2);
}

// Driver Code
public static void Main()
{
    string str1 = "geeksforgeeks",
           str2 = "geeks";
    Console.Write(countSubstrig(str1,
                                str2));
    Console.Write("\n");

    str1 = "hikakashi";
    str2 = "hi";
    Console.Write(countSubstrig(str1,
                                str2));

}
}

// This code is contributed
// by Smita
```

## java 描述语言

```
<script>

// Recursive js program for counting number of substrings

// Recursive function to count
// the number of occurrences of "hi" in str.
function countSubstrig( str1, str2){
    let n1 = str1.length;
    let n2 = str2.length;

    // Base Case
    if (n1 == 0 || n1 < n2)
        return 0;

    // Recursive Case
    // Checking if the first substring matches
    if (str1.substr(0, n2) == (str2))
        return countSubstrig(str1.substr(n2-1), str2) + 1;

    // Otherwise, return the count from
    // the remaining index
    return countSubstrig(str1.substr(n2-1), str2);
}

// Driver function
let str1 = "geeksforgeeks", str2 = "geeks";
document.write( countSubstrig(str1, str2),'<br>');
str1 = "hikakashi", str2 = "hi";
document.write( countSubstrig(str1, str2),'<br>');

</script>
```

**Output:** 

```
2
2
```