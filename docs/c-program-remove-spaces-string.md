# 从字符串中删除空格的 C++程序

> 原文:[https://www . geesforgeks . org/c-program-remove-spaces-string/](https://www.geeksforgeeks.org/c-program-remove-spaces-string/)

给定一个字符串，删除其中的所有空格。例如“g e e . e . k”应该转换成“极客”，“g . e”应该转换成“g e”。

想法是从左到右遍历字符串，并在遍历时忽略空格。我们需要跟踪两个索引，一个用于当前红色字符，另一个用于输出中的当前索引。

```
// C++ program to evaluate a given expression
#include <iostream>
using namespace std;

char *removeSpaces(char *str)
{
    int i = 0, j = 0;
    while (str[i])
    {
        if (str[i] != ' ')
           str[j++] = str[i];
        i++;
    }
    str[j] = '\0';
    return str;
}

// Driver program to test above function
int main()
{
    char str1[] = "gee    k   ";
    cout << removeSpaces(str1) << endl;

    char str2[] = " g e e k ";
    cout << removeSpaces(str2);
    return 0;
}
```

输出:

```
geek
geek
```

上述实现的时间复杂度为 O(n)，其中 n 是输入字符串中的字符数。

如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论