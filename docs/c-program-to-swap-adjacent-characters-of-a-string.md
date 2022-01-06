# 交换字符串相邻字符的 C 程序

> 原文:[https://www . geeksforgeeks . org/c-程序到交换字符串的相邻字符/](https://www.geeksforgeeks.org/c-program-to-swap-adjacent-characters-of-a-string/)

给定一个字符串，任务是在 c 语言中交换这个字符串的相邻字符。

**示例:**

```
Input: str = "geeks"
Output: NA
Not possible as the string length is odd

Input: str = "geek"
Output: egke

```

**进场:**

1.  检查字符串的长度是偶数还是奇数。
2.  如果长度是奇数，交换就不能进行。
3.  如果长度为偶数，则逐个取字符串的每个字符，并将其与相邻字符交换。

下面是上述方法的实现:

```
// C program to swap
// adjacent characters of a String

#include <stdio.h>
#include <string.h>

// Function to swap adjacent characters
void swap(char* str)
{

    char c = 0;
    int length = 0, i = 0;

    // Find the length of the string
    length = strlen(str);

    // Check if the length of the string
    // is even or odd
    if (length % 2 == 0) {

        // swap the characters with
        // the adjacent character
        for (i = 0; i < length; i += 2) {
            c = str[i];
            str[i] = str[i + 1];
            str[i + 1] = c;
        }

        // Print the swapped character string
        printf("%s\n", str);
    }
    else {

        // Print NA as the string length is odd
        printf("NA\n");
    }
}

// Driver code
int main()
{

    // Get the string
    char str1[] = "Geek";
    char str2[] = "Geeks";

    swap(str1);
    swap(str2);

    return 0;
}
```

**Output:**

```
eGke
NA

```