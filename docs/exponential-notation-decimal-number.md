# 十进制数的指数记数法

> 原文:[https://www . geesforgeks . org/index-批注-十进制-数字/](https://www.geeksforgeeks.org/exponential-notation-decimal-number/)

给定一个正十进制数，求给定数的简单指数表示法(x = a 10^b)。

示例:

```
Input : 100.0
Output : 1E2
Explanation:
The exponential notation of 100.0 is 1E2.

Input :19
Output :1.9E1
Explanation:
The exponential notation of 16 is 1.6E1.

```

**逼近:**
最简单的方法就是找到第一个非零数字的位置和点的位置。这两个位置之间的差值是 b 的值(如果该值为正，您也应该将其减少 1)。

下面是上述方法的实现:

```
// C++ code to find the exponential notation
#include <bits/stdc++.h>
using namespace std;

// function to calculate the exponential
// notation
void FindExponent(char s[], int n)
{
    int i, j, b, c;
    for (i = 0; s[i] == '0' || s[i] == '.'; i++)
        ;
    for (j = n - 1; s[j] == '0' || s[j] == '.'; j--)
        ;

    c = find(s, s + n, '.') - s;
    putchar(s[i]);

    if (i != j)
        putchar('.');

    for (int k = i + 1; k <= j; k++)
        if (s[k] != '.')
            putchar(s[k]);
    if (i < c)
        b = c - i - 1;
    else
        b = c - i;
    if (b)
        printf("E%d", b);
}

// main function
int main()
{
    char s[] = "100";
    int n = strlen(s);
    FindExponent(s, n);
}
```

输出:

```
1E2

```