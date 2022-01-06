# 将一个大数字分成相差 k 的两部分

> 原文:[https://www . geesforgeks . org/divide-big-number-two-parts-one-number-greater-k-number/](https://www.geeksforgeeks.org/divide-big-number-two-parts-one-number-greater-k-number/)

给定一个大正数 **N** 。该任务将 N 分为两个数字**‘A’**和**‘B’**，它们之间差值为**K**(1<= K<= 10<sup>100</sup>)即 A–B = K

**示例:**

```
Input : N = 10, K = 2
Output : A = 6 B = 4

Input : N = 20, K = 4
Output : A = 12 B = 8
```

让两个必需的数字为“A”和“B”。所以，我们知道‘A’和‘B’的和将结束于 N.
所以，一个等式变成了，
A + B = N
并且，我们希望‘A’和‘B’之间的差等于‘K’。
那么，另一个方程就变成了，
A–B = K
把两个方程相加，我们得到
2*A = N + K
那么，A = (N + K)/2
那么我们就可以通过，**B =(N–A)**
找到 B 了现在，为了处理大整数，我们已经把整数存储在字符数组中，并定义了一个函数来对它们执行运算。

下面是这种方法的 C 实现:

## C++

```
// C++ program to Divide a Big
// Number into two parts
#include <bits/stdc++.h>
using namespace std;
#define MAX 100

// Function to adds two Numbers
// represented as array of character.
void add(char v1[], char v2[])
{
    int i, d, c = 0;

    // length of string
    int l1 = strlen(v1);
    int l2 = strlen(v2);

    // initializing extra character
    // position to 0
    for (i = l1; i < l2; i++)
        v1[i] = '0';

    for (i = l2; i < l1; i++)
        v2[i] = '0';

    // Adding each element of character
    // and storing the carry.
    for (i = 0; i < l1 || i < l2; i++) {
        d = (v1[i] - '0') + (v2[i] - '0') + c;
        c = d / 10;
        d %= 10;
        v1[i] = '0' + d;
    }

    // If remainder remains.
    while (c) {
        v1[i] = '0' + (c % 10);
        c /= 10;
        i++;
    }

    v1[i] = '\0';
    v2[l2] = '\0';
}

// Function to subtracts two numbers
// represented by string.
void subs(char v1[], char v2[])
{
    int i, d, c = 0;

    // Finding the length of the string.
    int l1 = strlen(v1);
    int l2 = strlen(v2);

    // initializing extra character position to 0.
    for (i = l2; i < l1; i++)
        v2[i] = '0';

    // Substrating each element of character.
    for (i = 0; i < l1; i++) {
        d = (v1[i] - '0' - c) - (v2[i] - '0');

        if (d < 0) {
            d += 10;
            c = 1;
        }
        else
            c = 0;

        v1[i] = '0' + d;
    }

    v2[l2] = '\0';
    i = l1 - 1;

    while (i > 0 && v1[i] == '0')
        i--;

    v1[i + 1] = '\0';
}

// Function divides a number represented by
// character array a constant.
int divi(char v[], int q)
{
    int i, l = strlen(v);

    int c = 0, d;

    // Dividing each character element by constant.
    for (i = l - 1; i >= 0; i--) {
        d = c * 10 + (v[i] - '0');
        c = d % q;
        d /= q;
        v[i] = '0' + d;
    }

    i = l - 1;

    while (i > 0 && v[i] == '0')
        i--;

    v[i + 1] = '\0';
    return c;
}

// Function to reverses the character array.
void rev(char v[])
{
    int l = strlen(v);
    int i;
    char cc;

    // Reversing the array.
    for (i = 0; i < l - 1 - i; i++) {
        cc = v[i];
        v[i] = v[l - 1 - i];
        v[l - i - 1] = cc;
    }
}

// Wrapper Function
void divideWithDiffK(char a[], char k[])
{

    // Reversing the character array.
    rev(a);
    rev(k);

    // Adding the each element of both array
    // and storing the sum in array a[].
    add(a, k);

    // Dividing the array a[] by 2.
    divi(a, 2);

    // Reversing the character array to get output.
    rev(a);
    cout <<" "<< a;

    // Substracting each element of array
    // i.e calculating a = a - b
    rev(a);
    subs(a, k);

    // Reversing the character array to get output.
    rev(a);
    cout <<" "<< a;
}

// Driven Program
int main()
{
    char a[MAX] = "100", k[MAX] = "20";
    divideWithDiffK(a, k);
    return 0;
}
// this code is contributed by shivanisinghss2110
```

## C

```
// C program to Divide a Big
// Number into two parts
#include <stdio.h>
#include <string.h>
#define MAX 100

// Function to adds two Numbers
// represented as array of character.
void add(char v1[], char v2[])
{
    int i, d, c = 0;

    // length of string
    int l1 = strlen(v1);
    int l2 = strlen(v2);

    // initializing extra character
    // position to 0
    for (i = l1; i < l2; i++)
        v1[i] = '0';

    for (i = l2; i < l1; i++)
        v2[i] = '0';

    // Adding each element of character
    // and storing the carry.
    for (i = 0; i < l1 || i < l2; i++) {
        d = (v1[i] - '0') + (v2[i] - '0') + c;
        c = d / 10;
        d %= 10;
        v1[i] = '0' + d;
    }

    // If remainder remains.
    while (c) {
        v1[i] = '0' + (c % 10);
        c /= 10;
        i++;
    }

    v1[i] = '\0';
    v2[l2] = '\0';
}

// Function to subtracts two numbers
// represented by string.
void subs(char v1[], char v2[])
{
    int i, d, c = 0;

    // Finding the length of the string.
    int l1 = strlen(v1);
    int l2 = strlen(v2);

    // initializing extra character position to 0.
    for (i = l2; i < l1; i++)
        v2[i] = '0';

    // Substrating each element of character.
    for (i = 0; i < l1; i++) {
        d = (v1[i] - '0' - c) - (v2[i] - '0');

        if (d < 0) {
            d += 10;
            c = 1;
        }
        else
            c = 0;

        v1[i] = '0' + d;
    }

    v2[l2] = '\0';
    i = l1 - 1;

    while (i > 0 && v1[i] == '0')
        i--;

    v1[i + 1] = '\0';
}

// Function divides a number represented by
// character array a constant.
int divi(char v[], int q)
{
    int i, l = strlen(v);

    int c = 0, d;

    // Dividing each character element by constant.
    for (i = l - 1; i >= 0; i--) {
        d = c * 10 + (v[i] - '0');
        c = d % q;
        d /= q;
        v[i] = '0' + d;
    }

    i = l - 1;

    while (i > 0 && v[i] == '0')
        i--;

    v[i + 1] = '\0';
    return c;
}

// Function to reverses the character array.
void rev(char v[])
{
    int l = strlen(v);
    int i;
    char cc;

    // Reversing the array.
    for (i = 0; i < l - 1 - i; i++) {
        cc = v[i];
        v[i] = v[l - 1 - i];
        v[l - i - 1] = cc;
    }
}

// Wrapper Function
void divideWithDiffK(char a[], char k[])
{

    // Reversing the character array.
    rev(a);
    rev(k);

    // Adding the each element of both array
    // and storing the sum in array a[].
    add(a, k);

    // Dividing the array a[] by 2.
    divi(a, 2);

    // Reversing the character array to get output.
    rev(a);
    printf("%s ", a);

    // Substracting each element of array
    // i.e calculating a = a - b
    rev(a);
    subs(a, k);

    // Reversing the character array to get output.
    rev(a);
    printf("%s", a);
}

// Driven Program
int main()
{
    char a[MAX] = "100", k[MAX] = "20";
    divideWithDiffK(a, k);
    return 0;
}
```

**Output:** 

```
60 40
```