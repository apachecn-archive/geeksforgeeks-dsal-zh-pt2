# C++程序不使用*、/、+、-、%运算符将一个数除以 3

> 原文:[https://www . geesforgeks . org/除数-3-不使用运算符/](https://www.geeksforgeeks.org/divide-number-3-without-using-operators/)

对于给定的正数，我们需要在不使用任何*、/、+、–%运算符的情况下将一个数除以 3
示例:

```
Input : 48 
Output : 16

Input : 16  
Output : 5 
```

**算法**

1.  取一个数字 num，sum = 0
2.  while(num>3)，将数字左移 2 位，sum = add(num >> 2，sum)。创建一个函数 add(x，y)，通过按位运算符将两个数字相加
    *   取 x，y
    *   运行 do while 循环，直到 a 不为零
    *   a = x & y，b = x ^ y；，y = b；
    *   终止循环后，返回 b 的值，该值给出 x 和 y 的和
3.  取 num 与 3
    的按位“与”，新 num = add( num > > 2，num & 3)
4.  循环结束后，打印给出最终结果的和值。

> 例如，如果您的数字是 10，则转换为二进制 10 => 00001010
> 如果 10 > 3，则将二进制数字移动 2 位，现在 num 将是 00000010，即 2
> 现在 sum 将是 2
> num =(将数字移动 2 位)+(数字按位 AND 3)
> num = 2+2
> 现在数字将是 4， 4 > 3 = >真所以循环将被重复
> 4 = > 00000100 然后将二进制数 2 位移位
> 现在 sum = 2 + 1 ie，sum = 3(该值被返回)
> num =(将数字(00000100)移位 2 位)+(number BITWISE AND 3)
> num = 1+0
> ie 余数= 1

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program for divided a number by
// 3 without using operator
#include <bits/stdc++.h>
using namespace std;

// A function to add 2 numbers without using +
int add(int x, int y)
{
    int a, b;
    do {
        a = x & y;
        b = x ^ y;
        x = a << 1;
        y = b;
    } while (a);

    return b;
}

// Function to divide by 3
int divideby3(int num)
{
    int sum = 0;

    while (num > 3) {
        sum = add(num >> 2, sum);
        num = add(num >> 2, num & 3);
    }

    if (num == 3)
        sum = add(sum, 1);

    return sum;
}

// Driver program
int main(void)
{
    int num = 48;
    cout << "The number divided by 3 is ";
    cout << divideby3(num);

    return 0;
}
```

**Output:** 

```
The number divided by 3 is 16
```

本文由**丹麦语 _RAZA** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。