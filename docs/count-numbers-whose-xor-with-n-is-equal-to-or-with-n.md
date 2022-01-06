# 计数与 N 的异或等于与 N 的或的数

> 原文:[https://www . geesforgeks . org/count-numbers-其-xor-with-n-等于-or-with-n/](https://www.geeksforgeeks.org/count-numbers-whose-xor-with-n-is-equal-to-or-with-n/)

给定一个数字 N，任务是找到 X 的计数使得**N XOR X**=**N OR X**，其中 0 < =X < =N
**示例:**

> **输入** : N = 5
> **输出** : 2
> 对于 N = 5，
> 5 异或 2 == 5 或 2
> 5 异或 0 == 5 或 0
> 因此，计数为 2。
> **输入** : N = 7
> **输出** : 1
> 对于 N = 7，
> 7 异或 0 == 7 或 0
> 这样，计数为 1。

**方法:**想法是将给定的数转换为二进制，然后对其中未设置的位进行计数。 **2^count** 给了我们 x 的个数使得**n xor x**=**n 或者 X** 。
以下是上述方法的实施:

## C++

```
// C++ program to find
// the XOR equals OR count
#include<iostream>
#include<math.h>
using namespace std;

class gfg {

    // Function to calculate count
    // of numbers with XOR equals OR
    public:
    int xorEqualsOrCount(int N)
    {

        // variable to store count of unset bits
        int count = 0;
        int bit;
        while (N > 0) {

            bit = N % 2;
            if (bit == 0)
                count++;
            N = N / 2;
        }
        return (int)pow(2, count);
    } };

    // Driver code
    int main()
    {
        gfg g ;
        int N = 7;
        cout<<g.xorEqualsOrCount(N);
        return 0;
    }

// This code is contributed by Soumik
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the XOR equals OR count
import java.io.*;
import java.util.*;

class GFG {

    // Function to calculate count of numbers with XOR equals OR
    static int xorEqualsOrCount(int N)
    {
        // variable to store count of unset bits
        int count = 0;
        int bit;
        while (N > 0) {
            bit = N % 2;
            if (bit == 0)
                count++;
            N = N / 2;
        }
        return (int)Math.pow(2, count);
    }

    // Driver code
    public static void main(String args[])
    {
        int N = 7;
        System.out.println(xorEqualsOrCount(N));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find
# the XOR equals OR count

# Function to calculate count
# of numbers with XOR equals OR
def xorEqualsOrCount(N) :

    # variable to store
    # count of unset bits
    count = 0

    while(N > 0) :

        bit = N % 2

        if bit == 0 :
            count += 1

        N //= 2

    return int(pow(2, count))

# Driver code    
if __name__ == "__main__" :

    N = 7
    print(xorEqualsOrCount(N))

# This code is contributed by
# ANKITRAI1
```

## C#

```
// C# program to find
// the XOR equals OR count
using System;

class GFG {

    // Function to calculate count
    // of numbers with XOR equals OR
    static int xorEqualsOrCount(int N)
    {

        // variable to store count of unset bits
        int count = 0;
        int bit;
        while (N > 0) {

            bit = N % 2;
            if (bit == 0)
                count++;
            N = N / 2;
        }
        return (int)Math.Pow(2, count);
    }

    // Driver code
    public static void Main()
    {
        int N = 7;
        Console.WriteLine(xorEqualsOrCount(N));
    }
}

// This code is contributed by inder_verma..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the XOR
// equals OR count

// Function to calculate count
// of numbers with XOR equals OR
function xorEqualsOrCount($N)
{

    // variable to store count
    // of unset bits
    $count = 0;
    while ($N > 0)
    {
        $bit = $N % 2;
        if ($bit == 0)
            $count++;
        $N = intval($N / 2);
    }
    return pow(2, $count);
}

// Driver code
$N = 7;
echo xorEqualsOrCount($N);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to find
// the XOR equals OR count

    // Function to calculate count
    // of numbers with XOR equals OR
    function xorEqualsOrCount(N)
    {

        // variable to store count of unset bits
        let count = 0;
        let bit;
        while (N > 0) {

            bit = N % 2;
            if (bit == 0)
                count++;
            N = parseInt(N / 2);
        }
        return Math.pow(2, count);
    }

    // Driver code
        let N = 7;
        document.write(xorEqualsOrCount(N));

</script>
```

**Output:** 

```
1
```