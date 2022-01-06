# 计算 IEEE 754 格式浮点数平方根倒数的快速方法

> 原文:[https://www . geesforgeks . org/fast-method-calculate-reverse-square-root-floating-number-IEEE-754-format/](https://www.geeksforgeeks.org/fast-method-calculate-inverse-square-root-floating-point-number-ieee-754-format/)

给定一个以 [IEEE 754 浮点格式](http://en.wikipedia.org/wiki/Single_precision_floating-point_format#IEEE_754_single_precision_binary_floating-point_format:_binary32)存储的 32 位浮点数 x，求 x 的平方根倒数，即 x <sup>-1/2</sup> 。
一个简单的解决办法是做浮点运算。下面是示例函数。

## 卡片打印处理机（Card Print Processor 的缩写）

```
#include <iostream>
#include <cmath>
using namespace std;

float InverseSquareRoot(float x)
{
    return 1/sqrt(x);
}

int main()
{
    cout << InverseSquareRoot(0.5) << endl;
    cout << InverseSquareRoot(3.6) << endl;
    cout << InverseSquareRoot(1.0) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;

class GFG {

    static float InverseSquareRoot(float x)
    {
        return 1 / (float)Math.sqrt(x);
    }

    public static void main(String[] args)
    {
        System.out.println(InverseSquareRoot(0.5f));
        System.out.println(InverseSquareRoot(3.6f));
        System.out.println(InverseSquareRoot(1.0f));
    }
}

// This code is contributed by souravmahato348.
```

## C#

```
using System;

class GFG {

    static float InverseSquareRoot(float x)
    {
        return 1 / (float)Math.Sqrt(x);
    }

    public static void Main()
    {
        Console.WriteLine(InverseSquareRoot(0.5f));
        Console.WriteLine(InverseSquareRoot(3.6f));
        Console.WriteLine(InverseSquareRoot(1.0f));
    }
}

// This code is contributed by subham348.
```

输出:

```
1.41421
0.527046
1
```

下面是一个基于同样的**快速有趣的方法**。详见[本](http://en.wikipedia.org/wiki/Fast_inverse_square_root)。

## C

```
#include <iostream>
using namespace std;

// This is fairly tricky and complex process. For details, see
// http://en.wikipedia.org/wiki/Fast_inverse_square_root
float InverseSquareRoot(float x)
{
    float xhalf = 0.5f*x;
    int i = *(int*)&x;
    i = 0x5f3759d5 - (i >> 1);
    x = *(float*)&i;
    x = x*(1.5f - xhalf*x*x);
    return x;
}

int main()
{
    cout << InverseSquareRoot(0.5) << endl;
    cout << InverseSquareRoot(3.6) << endl;
    cout << InverseSquareRoot(1.0) << endl;
    return 0;
}
```

输出:

```
1.41386
0.526715
0.998307
```

**来源:**
http://en.wikipedia.org/wiki/Fast_inverse_square_root
本文由 **Shalki Agarwal** 供稿。如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息