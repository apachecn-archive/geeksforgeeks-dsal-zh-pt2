# 用另一个给定的单词替换文本中的一个单词的程序

> 原文:[https://www . geesforgeks . org/c-program-replace-word-text-other-given-word/](https://www.geeksforgeeks.org/c-program-replace-word-text-another-given-word/)

给定三个字符串“str”、“oldW”和“newW”。任务是找到所有出现的单词“oldW”，然后替换为单词“newW”。
**例:**

```
Input : str[] = "xxforxx xx for xx", 
        oldW[] = "xx", 
        newW[] = "geeks"
Output : geeksforgeeks geeks for geeks

```

其思想是遍历原始字符串，并计算旧单词在字符串中出现的次数。现在制作一个足够大的新字符串，以便替换新单词。现在用单词替换将原始字符串复制到新字符串。

```
// C program to search and replace
// all occurrences of a word with
// other word.
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to replace a string with another
// string
char* replaceWord(const char* s, const char* oldW,
                  const char* newW)
{
    char* result;
    int i, cnt = 0;
    int newWlen = strlen(newW);
    int oldWlen = strlen(oldW);

    // Counting the number of times old word
    // occur in the string
    for (i = 0; s[i] != '\0'; i++) {
        if (strstr(&s[i], oldW) == &s[i]) {
            cnt++;

            // Jumping to index after the old word.
            i += oldWlen - 1;
        }
    }

    // Making new string of enough length
    result = (char*)malloc(i + cnt * (newWlen - oldWlen) + 1);

    i = 0;
    while (*s) {
        // compare the substring with the result
        if (strstr(s, oldW) == s) {
            strcpy(&result[i], newW);
            i += newWlen;
            s += oldWlen;
        }
        else
            result[i++] = *s++;
    }

    result[i] = '\0';
    return result;
}

// Driver Program
int main()
{
    char str[] = "xxforxx xx for xx";
    char c[] = "xx";
    char d[] = "Geeks";

    char* result = NULL;

    // oldW string
    printf("Old string: %s\n", str);

    result = replaceWord(str, c, d);
    printf("New String: %s\n", result);

    free(result);
    return 0;
}
```

**Output:**

```
Old string: xxforxx xx for xx
New String: GeeksforGeeks Geeks for Geeks

```