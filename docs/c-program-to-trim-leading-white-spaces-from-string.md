# C 程序修剪字符串的前导空格

> 原文:[https://www . geesforgeks . org/c-program-to-trim-leader-空格-from-string/](https://www.geeksforgeeks.org/c-program-to-trim-leading-white-spaces-from-string/)

给定字符串 **str** ，任务是编写 [C 程序](https://www.geeksforgeeks.org/c/) 从给定字符串中移除前导[空间。](https://www.geeksforgeeks.org/remove-spaces-from-a-given-string/)

**示例:**

> **输入**:str = " geeksforgeeks "
> T3【输出】 : geeksforgeeks
> 
> **输入** : str = "gfg"
> **输出** : gfg

**方法:**想法是对给定字符串中的前导空格进行计数，然后从该计数索引中将该索引中的字符复制到字符串的前面。以下是步骤:

1.  初始化计数= 0 以计算前导空格的数量。
2.  遍历给定的字符串，找到前导空格字符结束的索引(比如 **idx** )。
3.  遍历该索引 **idx** 中的所有字符，并将该索引中的每个字符复制到前面索引的末尾。
4.  最后，在新字符串的最后一个索引处放上“\0”以终止该字符串。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <stdio.h>

// Function to remove leading
// spaces from a given string
char* removeLeadingSpaces(char* str)
{
    static char str1[99];
    int count = 0, j, k;

    // Iterate String until last
    // leading space character
    while (str[count] == ' ') {
        count++;
    }

    // Putting string into another
    // string variable after
    // removing leading white spaces
    for (j = count, k = 0;
         str[j] != '\0'; j++, k++) {
        str1[k] = str[j];
    }
    str1[k] = '\0';

    return str1;
}

// Driver Code
int main()
{
    // Given string
    char str[] = "         geeksforgeeks";
    char* ptr;

    // Function call
    ptr = removeLeadingSpaces(str);

    // Print string without leading space
    printf("%s", ptr);
    return 0;
}
```

**Output:**

```
geeksforgeeks

```

***时间复杂度:****O(N)*
***辅助空间:****O(N)*