# 使用指针比较两个字符串的 C++程序

> 原文:[https://www . geeksforgeeks . org/c-程序使用指针比较两个字符串/](https://www.geeksforgeeks.org/c-program-to-compare-two-string-using-pointers/)

给定两个字符串，使用指针比较字符串

**示例:**

```
Input: str1 = geeks, str2 = geeks
Output: Both are equal

Input: str1 = hello, str2 = hellu
Output: Both are not equal
As their length are same but characters are different
```

其思想是取消对给定指针的引用，比较值并推进两者。

**程序:**

```
// C++ Program to compare two strings using
// Pointers
#include <iostream>
using namespace std;

// Method to compare two string
// using pointer
bool compare(char *str1, char *str2)
{
    while (*str1 == *str2)
    {
        if (*str1 == '\0' && *str2 == '\0')
            return true;
        str1++;
        str2++;
    }      

    return false;
}

int main()
{
    // Declare and Initialize two strings
    char str1[] = "geeks";
    char str2[] = "geeks";

    if (compare(str1, str2) == 1)
        cout << str1 << " " << str2 << " are Equal";
    else
        cout << str1 << " " << str2 << " are not Equal";
}
```

**Output:**

```
geeks geeks are Equal

```