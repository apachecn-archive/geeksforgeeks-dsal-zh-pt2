# 小而大的 Endian 之谜

> 原文:[https://www . geesforgeks . org/little-and-big-endian-神秘学/](https://www.geeksforgeeks.org/little-and-big-endian-mystery/)

**这些是什么？**
小字节和大字节是存储多字节数据类型(int、float 等)的两种方式。在小端机器中，首先存储多字节数据类型的二进制表示的最后一个字节。另一方面，在大端机器中，多字节数据类型的二进制表示的第一个字节首先被存储。
假设整数存储为 4 字节(对于使用基于 DOS 的编译器如 C++ 3.0 的编译器，整数为 2 字节)，那么值为 0x01234567 的变量 x 将存储如下。

![Little and Big Endian Mystery](http://4.bp.blogspot.com/_IEmaCFe3y9g/SO3GGEF4UkI/AAAAAAAAAAc/z7waF2Lwg0s/s400/lb.GIF)

**如何在机器上看到多字节数据类型的内存表示？**
下面是一个 C 代码示例，展示了 int、float 和指针的字节表示。

## c

```
#include <stdio.h>

/* function to show bytes in memory, from location start to start+n*/
void show_mem_rep(char *start, int n) 
{
    int i;
    for (i = 0; i < n; i++)
         printf(" %.2x", start[i]);
    printf("\n");
}

/*Main function to call above function for 0x01234567*/
int main()
{
   int i = 0x01234567;
   show_mem_rep((char *)&i, sizeof(i));
   getchar();
   return 0;
}
```

当上述程序在小端机器上运行时，给出“67 45 23 01”作为输出，而如果在大端机器上运行，给出“01 23 45 67”作为输出。
**有没有快速确定机器字符顺序的方法？**
有 n 种方法可以确定机器的字符顺序。这里有一个快速的方法。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int main() 
{ 
    unsigned int i = 1; 
    char *c = (char*)&i; 
    if (*c) 
        cout<<"Little endian"; 
    else
        cout<<"Big endian"; 
    return 0; 
} 

// This code is contributed by rathbhupendra
```

## C

```
#include <stdio.h>
int main() 
{
   unsigned int i = 1;
   char *c = (char*)&i;
   if (*c)    
       printf("Little endian");
   else
       printf("Big endian");
   getchar();
   return 0;
}
```

**输出:**

```
Little endian
```

**时间复杂度:** O(1)

**辅助空间:** O(1)

在上面的程序中，一个字符指针 c 指向一个整数 I。因为当字符指针被去引用时，字符的大小是 1 字节，所以它将只包含整数的第一个字节。如果机器是小端字节，那么*c 将是 1(因为最后一个字节是先存储的)，如果机器是大端字节，那么*c 将是 0。
**字符顺序对程序员来说重要吗？**
大多数情况下编译器会处理字节序，但是，在以下情况下，字节序会成为一个问题。
这在网络编程中很重要:假设你在一个小端机器上写整数文件，然后把这个文件转移到一个大端机器上。除非有小端到大端的转换，否则大端机器会以相反的顺序读取文件。你可以在这里找到这样一个实际的例子。
网络的标准字节顺序是大端序，也称为网络字节顺序。在网络上传输数据之前，数据首先转换为网络字节顺序(大端)。
有时候使用类型铸造很重要，下面的程序就是一个例子。

## c

```
#include <stdio.h>
int main()
{
    unsigned char arr[2] = {0x01, 0x00};
    unsigned short int x = *(unsigned short int *) arr;
    printf("%d", x);
    getchar();
    return 0;
}
```

在上面的程序中，char 数组被类型转换为无符号短整数类型。当我在小端机器上运行上述程序时，我得到 1 作为输出，而如果我在大端机器上运行它，我得到 256。为了使程序的字符顺序独立，应该避免上述编程风格。
**什么是双端？**
双端处理器可以在小端和大端两种模式下运行。
**小端、大端、双端机有哪些例子？**
基于英特尔的处理器是小端字节序。ARM 处理器是小端字节序。当前一代 ARM 处理器是双端的。
摩托罗拉 68K 处理器是大端。PowerPC(由制造)和 SPARK(由孙制造)处理器是大端字节序。这些处理器的当前版本是双端的。
**字符顺序是否影响文件格式？**
以 1 字节为基本单位的文件格式与字符顺序无关，例如 ASCII 文件。其他文件格式使用一些固定的字符顺序格式，例如，JPEG 文件以大字符顺序格式存储。
**小端和大端哪个更好？**
小端和大端这个词来源于乔纳森·斯威夫特的《格列佛游记》。两组人不能就鸡蛋应该打开到哪一端达成一致——小的还是大的。就像鸡蛋问题一样，没有技术上的理由选择单字节排序惯例，因此争论退化为关于社会政治问题的争吵。只要选择了其中一个惯例并始终如一地遵守，这个选择就是任意的。