# 在 C/C++中复制字符串的不同方式

> 原文:[https://www . geeksforgeeks . org/differential-to-copy-a-string-in-c/](https://www.geeksforgeeks.org/different-ways-to-copy-a-string-in-c-c/)

### <u>使用内置功能</u>

### strcpy（）：

使用内置函数 [strcpy()](https://www.geeksforgeeks.org/strcpy-in-c-cpp/) 从 [**string.h**](https://www.geeksforgeeks.org/commonly-used-string-functions-in-c-c-with-examples/) 头文件中复制一个字符串到另一个字符串。strcpy()接受指向目标数组和源数组的指针作为参数，并在复制后返回指向目标字符串的指针。使用%s，我们可以打印字符串(%s 打印从基地址到空字符的字符串)。

下面是使用上述方法的实现:

## C

```
// C program to copy the string using
// strcpy function

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to copy the string
char* copyString(char s[])
{
    char* s2;
    s2 = (char*)malloc(20);

    strcpy(s2, s);
    return (char*)s2;
}

// Driver Code
int main()
{
    char s1[20] = "GeeksforGeeks";
    char* s2;

    // Function Call
    s2 = copyString(s1);
    printf("%s", s2);
    return 0;
}
```

**Output:** 

```
GeeksforGeeks
```

### memcpy():

[memcpy](https://www.geeksforgeeks.org/memcpy-in-cc/) ()也在 string.h 头中定义，用于从源复制到目的地，无论源数据包含什么。memcpy()需要传递一个大小参数。

主要区别在于 memcpy()总是复制指定字节的确切数目；另一方面，strcpy()和其他 str 方法将复制，直到它读取到一个 NULL(“\ 0”)字节，然后停止。strcpy()不打算用于以零结尾的 C 字符串。

memcpy()经过硬件优化，复制速度更快，可以处理任何类型的源数据(如:二进制或加密字节)。strcpy()绝对不应该使用，除非有什么具体原因，而且如果你知道字符串的长度， **memcpy()是更好的选择**。

## C

```
// C program to copy the string using
// memcpy function
#include <stdio.h>
#include <string.h>

// Driver Code
int main()
{
    char s1[20] = "GeeksforGeeks";
    char s2[20];

    // Function
    memcpy(s2, s1, strlen(s1));

    printf("%s\n", s1);

    return 0;
}
```

**Output**

```
GeeksforGeeks
```

### <u>使用循环</u>

想法是使用 for 循环将第一个数组的内容逐个复制到第二个数组。

下面是使用上述方法的实现:

## C

```
// C program to copy string using loops

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to copy the string
char* copyString(char s[])
{
    int i;
    char* s2;
    s2 = (char*)malloc(20);

    // Executing till null character
    // is found
    for (i = 0; s[i] != '\0'; i++) {

        // Copy the character one
        // by one from s1 to s2
        s2[i] = s[i];
    }

    // Return the pointer of newly
    // created string
    return (char*)s2;
}

// Driver Code
int main()
{
    char s1[20] = "GeeksforGeeks";
    char* s2;

    // Function Call
    s2 = copyString(s1);
    printf("%s", s2);
    return 0;
}
```

**Output:** 

```
GeeksforGeeks
```

### <u>使用</u> [<u>指针</u>](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/)

想法是使用指针将字符串数组的内容复制到另一个数组中，并通过遍历新指针来打印结果字符串。

下面是使用上述方法的实现:

## C

```
// C program to copy the string
// using pointers

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Function to copy the string
char* copyString(char s[])
{

    char *s2, *p1, *p2;

    s2 = (char*)malloc(20);
    p1 = s;
    p2 = s2;

    // Executing till the null
    // character is found
    while (*p1 != '\0') {

        // Copy the content of s1 to s2
        *p2 = *p1;
        p1++;
        p2++;
    }
    *p2 = '\0';

    return s2;
}

// Driver Code
int main()
{
    char s1[20] = "GeeksforGeeks";
    char* s2;

    s2 = copyString(s1);
    printf("%s", s2);
    return 0;
}
```

**Output:** 

```
GeeksforGeeks
```

### <u>使用指针和后增量</u>

其思想是使用 while 循环将字符串数组 1 的内容逐个赋给字符串数组 2，并在返回 [ASCII 值](https://www.geeksforgeeks.org/program-print-ascii-value-character/)时使用[后置运算符](https://www.geeksforgeeks.org/pre-increment-and-post-increment-in-c/)递增，这样条件将为真，并在循环中传递，直到条件为假，我们将退出循环。

下面是使用上述方法的实现:

## C

```
// C program to copy the string

#include <stdio.h>
#include <stdlib.h>

// Function to copy the string
void copyString(char* t, char* s)
{
    // (return ASCII value which is True,
    // therefore will be in the loop
    // till the condition is False
    while (*t++ = *s++)
        ;
}

// Driver Code
int main()
{
    char s2[20] = "GeeksforGeeks";
    char s1[20];

    // Function Call
    copyString(s1, s2);
    printf("%s", s1);
    return 0;
}
```

**Output:** 

```
GeeksforGeeks
```

### 使用 sprintf()

我们可以不在输出缓冲区中打印字符串，而是将其存储在指定的字符缓冲区中，或者在 [sprintf](https://www.geeksforgeeks.org/sprintf-in-c/) ()中存储目标字符串来复制字符串。

## C

```
// C program to copy the string using
// sprintf function
#include <stdio.h>

// Driver Code
int main()
{
    char s1[20] = "GeeksforGeeks";
    char s2[20];

    // Function
    sprintf(s2, "%s", s1);

    printf("%s\n", s1);

    return 0;
}
```

**Output**

```
GeeksforGeeks
```

**注意:**在上述所有方法中，目标数组的大小必须大于源字符串的长度才能复制所有字符。