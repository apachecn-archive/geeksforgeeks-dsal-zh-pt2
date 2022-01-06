# 使用查找表

计算整数中的设置位

> 原文:[https://www . geesforgeks . org/count-set-bits-integer-use-lookup-table/](https://www.geeksforgeeks.org/count-set-bits-integer-using-lookup-table/)

写一个有效的程序来计算整数的二进制表示中的 1 的个数。

例子

```
Input : n = 6
Output : 2
Binary representation of 6 is 110 
and has 2 set bits

Input : n = 13
Output : 3
Binary representation of 11 is 1101 
and has 3 set bits

```

在[之前的帖子](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)中，我们看到了在 O(log n)时间内解决这个问题的不同方法。在这篇文章中，我们使用查找表在 O(1)中求解。这里我们假设 INT 的大小是 32 位。使用查找表很难一次计数全部 32 位(“因为创建大小为 2 <sup>32</sup> -1】的查找表是不可行的”)。因此**我们将 32 位分成 8 位的块(ow 大小的查找表(2 <sup>8</sup> -1)索引:0-255)。**

**查找表**
在查找表中，我们存储范围(0-255)
LookupTable[0] = 0 |二进制 00000000 CountSetBits 0
LookUp Table[1]= 1 |二进制 00000001 CountSetBits 1
LookUp Table[2]= 1 |二进制 000000010 CountSetBits 1
LookUp Table[3]= 2

**我们举一个查找表如何工作的例子。**

```
Let's number be : 354 
in Binary : 0000000000000000000000101100010

Split it into 8 bits chunks  :
In Binary  :  00000000 | 00000000 | 00000001 | 01100010
In decimal :     0          0          1         98

Now Count Set_bits using LookupTable
LookupTable[0] = 0
LookupTable[1] = 1
LookupTable[98] = 3

so Total bits count : 4 

```

```
// c++ count to count number of set bits
// using lookup table in O(1) time

#include <iostream>
using namespace std;

// Generate a lookup table for 32 bit integers
#define B2(n) n, n + 1, n + 1, n + 2
#define B4(n) B2(n) \, B2(n + 1), B2(n + 1), B2(n + 2)
#define B6(n) B4(n) \, B4(n + 1), B4(n + 1), B4(n + 2)

// Lookup table that store the reverse of each table
unsigned int lookuptable[256] = { B6(0), B6(1), B6(1), B6(2) };

// function countset Bits Using lookup table
// ans return set bits count
unsigned int countSetBits(int N)
{
    // first chunk of 8 bits from right
    unsigned int count = lookuptable[N & 0xff] +

                         // second chunk from  right
                         lookuptable[(N >> 8) & 0xff] + 

                         // third and fourth chunks
                         lookuptable[(N >> 16) & 0xff] + 
                         lookuptable[(N >> 24) & 0xff];
    return count;
}

int main()
{
    // generate lookup table
    for (int i = 0; i < 256; i++)
        lookuptable[i] = (i & 1) + lookuptable[i / 2];

    unsigned int N = 354;
    cout << countSetBits(N) << endl;

    return 0;
}
```

输出:

```
4 

```

时间复杂度:0(1)