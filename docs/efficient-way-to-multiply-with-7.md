# 与 7 相乘的有效方法

> 原文:[https://www . geeksforgeeks . org/高效乘以 7 的方法/](https://www.geeksforgeeks.org/efficient-way-to-multiply-with-7/)

我们可以使用按位运算符将一个数乘以 7。首先将数字左移 3 位(您将得到 8n)，然后从移位的数字中减去原始数字并返回差值(8n–n)。
**节目:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
# include<bits/stdc++.h>

using namespace std;
 //c++ implementation 
long multiplyBySeven(long n)
{  
    /* Note the inner bracket here. This is needed 
       because precedence of '-' operator is higher 
       than '<<' */
    return ((n<<3) - n);
}

/* Driver program to test above function */
int main()
{
    long n = 4;

    cout<<multiplyBySeven(n);

    return 0;
}
```

## C

```
# include<stdio.h>

int multiplyBySeven(unsigned int n)
{ 
    /* Note the inner bracket here. This is needed
       because precedence of '-' operator is higher
       than '<<' */
    return ((n<<3) - n);
}

/* Driver program to test above function */
int main()
{
    unsigned int n = 4;
    printf("%u", multiplyBySeven(n));

    getchar();
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to multiply any
// positive number to 7

class GFG {

    static int multiplyBySeven(int n)
    {
        /* Note the inner bracket here.
        This is needed because precedence
        of '-' operator is higher
        than '<<' */
        return ((n << 3) - n);
    }

    // Driver code
    public static void main (String arg[])
    {
        int n = 4;

        System.out.println(multiplyBySeven(n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 计算机编程语言

```
# Python program to multiply any
# positive number to 7

# Function to multiply any number with 7
def multiplyBySeven(n):

    # Note the inner bracket here.
    # This is needed because
    # precedence of '-' operator is
    # higher than '<<'
    return ((n << 3) - n)

# Driver code
n = 4
print(multiplyBySeven(n))

# This code is contributed by Danish Raza
```

## C#

```
// C# program to multiply any
// positive number to 7
using System;

class GFG
{
    static int multiplyBySeven(int n)
    {
        /* Note the inner bracket here. This is needed
        because precedence of '-' operator is higher
        than '<<' */
        return ((n << 3) - n);
    }

    // Driver code
    public static void Main ()
    {
        int n = 4;
        Console.Write(multiplyBySeven(n));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php

function multiplyBySeven($n)
{

    // Note the inner bracket here.
    // This is needed because
    // precedence of '-' operator 
    // is higherthan '<<'
    return (($n<<3) - $n);
}

    // Driver Code
    $n = 4;
    echo multiplyBySeven($n);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>

function multiplyBySeven(n)
{ 

    /* Note the inner bracket here. This is needed
      because precedence of '-' operator is higher
      than '<<' */

    return ((n << 3) - n);
}

// Driver program to test above function

     n = 4;
    document.write(multiplyBySeven(n));

  // This code is contributed by simranarora5sos
</script>
```

**输出:**

```
28
```

**时间复杂度:**O(1)
T3】空间复杂度: O(1)
注:仅对正整数有效。
同样的概念可以用于 9 或其他数字的快速乘法。