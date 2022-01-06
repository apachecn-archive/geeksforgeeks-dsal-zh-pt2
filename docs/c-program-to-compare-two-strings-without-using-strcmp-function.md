# 不使用 strcmp()函数比较两个字符串的 C 程序

> 原文:[https://www . geesforgeks . org/c-程序比较两个字符串-不使用-strcmp-function/](https://www.geeksforgeeks.org/c-program-to-compare-two-strings-without-using-strcmp-function/)

给定两个字符串 **s1** 和 **s2** ，任务是编写 [C 程序](https://www.geeksforgeeks.org/c/)比较两个字符串而不使用 [strcmp()函数](https://www.geeksforgeeks.org/strcmp-in-c-cpp/)。如果字符串相等，则打印**“相等字符串”**，否则打印**“不相等字符串”**。

**示例:**

> **输入:** s1 =“极客”, s2 =“极客”
> T3】输出:不等字符串
> 
> **输入:**S1 =“geesforgeks”，S2 =“geesforgeks”
> T3】输出:等字符串

**方法:**当我们比较两个字符串时，有三种可能的情况发生:

1.  两个字符串是相同的意思是两个字符串之间的 **ASCII** 值的差值是 **0** 。
2.  两个字符串不同意味着第一个字符串中第一个不匹配字符的 **ASCII** 值小于第二个字符串，则两个字符串之间的差异为 **( < 0)** 。
3.  两个字符串不同意味着第一个字符串中第一个不匹配字符的 ASCII 值大于第二个字符串，那么两个字符串之间的差异是 **( > 0)** 。

基于以上三个条件，想法是每当条件 2 或 3 出现时，逐个比较给定字符串的每个字符，然后打印**“不等字符串”**否则打印**“等字符串”**。

下面是上述方法的实现:

## C

```
// C program to compare the two strings
// without using strcmp() function
#include <stdio.h>

// Function that compares the two string
void compareStrings(char* x, char* y)
{
    int flag = 0;

    // Iterate a loop till the end
    // of both the strings
    while (*x != '\0' || *y != '\0') {
        if (*x == *y) {
            x++;
            y++;
        }

        // If two characters are not same
        // print the difference and exit
        else if ((*x == '\0' && *y != '\0')
                 || (*x != '\0' && *y == '\0')
                 || *x != *y) {
            flag = 1;
            printf("Unequal Strings\n");
            break;
        }
    }

    // If two strings are exactly same
    if (flag == 0) {
        printf("Equal Strings\n");
    }
}

// Driver Code
int main(void)
{
    // Given strings s1 and s2
    char s1[20] = "python";
    char s2[20] = "dsa";

    // Function Call
    compareStrings(s1, s2);
    return 0;
}
```

**Output**

```
Unequal Strings
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)