# 不使用 strcat

连接两个字符串的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-to-concatenate-two-strings-无需使用-strcat/](https://www.geeksforgeeks.org/c-program-to-concatenate-two-strings-without-using-strcat/)

给定两个字符串 str1 和 str2，任务是编写一个 C 程序来连接这两个字符串，而不使用 [strcat()函数](https://www.geeksforgeeks.org/strcat-vs-strncat-c/)

**示例:**

```
Input: str1 = "hello", str2 = "world"
Output: helloworld

Input: str1 = "Geeks", str2 = "World"
Output: GeeksWorld

```

**进场:**

*   获取要连接的两个字符串
*   声明一个新的字符串来存储连接的字符串
*   在新字符串中插入第一个字符串
*   在新字符串中插入第二个字符串
*   打印串联字符串

下面是上述方法的实现:

```
// C Program to concatenate
// two strings without using strcat

#include <stdio.h>

int main()
{

    // Get the two Strings to be concatenated
    char str1[100] = "Geeks", str2[100] = "World";

    // Declare a new Strings
    // to store the concatenated String
    char str3[100];

    int i = 0, j = 0;

    printf("\nFirst string: %s", str1);
    printf("\nSecond string: %s", str2);

    // Insert the first string in the new string
    while (str1[i] != '\0') {
        str3[j] = str1[i];
        i++;
        j++;
    }

    // Insert the second string in the new string
    i = 0;
    while (str2[i] != '\0') {
        str3[j] = str2[i];
        i++;
        j++;
    }
    str3[j] = '\0';

    // Print the concatenated string
    printf("\nConcatenated string: %s", str3);

    return 0;
}
```

**Output:**

```
First string: Geeks
Second string: World
Concatenated string: GeeksWorld

```