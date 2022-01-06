# 创建一个元素异或为 y 的序列

> 原文:[https://www . geeksforgeeks . org/create-a-sequence-what-xor-of-elements-y/](https://www.geeksforgeeks.org/create-a-sequence-whose-xor-of-elements-is-y/)

给定两个整数 **N** 和 **Y** ，任务是生成一个由 **N** 个不同的非负整数组成的序列，该序列中所有元素的按位异或等于 **Y** ，即**a<sub>1</sub>^ a<sub>2</sub>^ a<sub>3</sub>^…..^ A <sub>N</sub> = Y** ，其中 **^** 表示按位异或。如果没有这样的顺序，则打印 **-1** 。
**举例:**

> **输入:** N = 4，Y = 3
> **输出:**1 131072 131074 0
> (1 ^ 131072 ^ 131074 ^ 0)= 3，四个元素截然不同。
> **输入:** N = 10，Y = 6
> **输出:** 1 2 3 4 5 6 7 131072 131078 0

**方法:**这是一个建设性的问题，可能包含多个解决方案。按照以下步骤生成所需的序列:

1.  首先将**N–3**元素作为序列的一部分，即 **1，2，3，4，…，(N–3)**
2.  让所选元素的异或为 **x** ，**数**为尚未选择的整数。现在有两种情况:
    *   如果 **x = y** 那么我们可以将 **num** 、 **num * 2** 和 **(num ^ (num * 2))** 加到最后 3 个剩余的数字上，因为**num ^(num * 2)^(num ^(num * 2))= 0**和 **x ^ 0 = x**
    *   如果 **x！= y** 那么我们可以加上 **0** 、 **num** 和 **(num ^ x ^ y)** 因为 **0 ^ num ^ (num ^ x ^ y) = x ^ y** 和**x ^ x y = y**

**注意:**序列在 **N = 2** 和 **Y = 0** 时是不可能的，因为这个条件只能由两个相等的数字满足，这是不允许的。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find and print
// the required sequence
void Findseq(int n, int x)
{
    const int pw1 = (1 << 17);
    const int pw2 = (1 << 18);

    // Base case
    if (n == 1)
        cout << x << endl;

    // Not allowed case
    else if (n == 2 && x == 0)
        cout << "-1" << endl;
    else if (n == 2)
        cout << x << " "
             << "0" << endl;
    else {
        int i;
        int ans = 0;

        // XOR of first N - 3 elements
        for (i = 1; i <= n - 3; i++) {
            cout << i << " ";
            ans = ans ^ i;
        }

        // Case 1: Add three integers whose XOR is 0
        if (ans == x)
            cout << pw1 + pw2 << " "
                 << pw1 << " " << pw2 << endl;

        // Case 2: Add three integers
        // whose XOR is equal to ans
        else
            cout << pw1 << " " << ((pw1 ^ x) ^ ans)
                 << " 0 " << endl;
    }
}

// Driver code
int main()
{
    int n = 4, x = 3;
    Findseq(n, x);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to find and print
    // the required sequence
    static void Findseq(int n, int x)
    {
        int pw1 = 1 << 17;
        int pw2 = (1 << 18);

        // Base case
        if (n == 1) {
            System.out.println(x);
        }

        // Not allowed case
        else if (n == 2 && x == 0) {
            System.out.println("-1");
        }
        else if (n == 2) {
            System.out.println(x + " "
                               + "");
        }
        else {
            int i;
            int ans = 0;

            // XOR of first N - 3 elements
            for (i = 1; i <= n - 3; i++) {
                System.out.print(i + " ");
                ans = ans ^ i;
            }

            // Case 1: Add three integers whose XOR is 0
            if (ans == x) {
                System.out.println(pw1 + pw2 + " " + pw1 + " " + pw2);
            }

            // Case 2: Add three integers
            // whose XOR is equal to ans
            else {
                System.out.println(pw1 + " " + ((pw1 ^ x) ^ ans)
                                   + " 0 ");
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 4, x = 3;
        Findseq(n, x);
    }
}

// This code contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find and print
# the required sequence
def Findseq(n, x) :

    pw1 = (1 << 17);
    pw2 = (1 << 18);

    # Base case
    if (n == 1) :
        print(x);

    # Not allowed case
    elif (n == 2 and x == 0) :
        print("-1");

    elif (n == 2) :
        print(x, " ", "0");

    else :

        ans = 0;

        # XOR of first N - 3 elements
        for i in range(1, n - 2) :
            print(i, end = " ");
            ans = ans ^ i;

        # Case 1: Add three integers whose XOR is 0
        if (ans == x) :
            print(pw1 + pw2, " ", pw1, " ", pw2);

        # Case 2: Add three integers
        # whose XOR is equal to ans
        else :
            print(pw1, " ", ((pw1 ^ x) ^ ans), " 0 ");

# Driver code
if __name__ == "__main__" :

    n = 4; x = 3;
    Findseq(n, x);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to find and print
    // the required sequence
    static void Findseq(int n, int x)
    {
        int pw1 = 1 << 17;
        int pw2 = (1 << 18);

        // Base case
        if (n == 1)
        {
            Console.WriteLine(x);
        }

        // Not allowed case
        else if (n == 2 && x == 0)
        {
            Console.WriteLine("-1");
        }
        else if (n == 2)
        {
            Console.WriteLine(x + " "
                            + "");
        }
        else
        {
            int i;
            int ans = 0;

            // XOR of first N - 3 elements
            for (i = 1; i <= n - 3; i++)
            {
                Console.Write(i + " ");
                ans = ans ^ i;
            }

            // Case 1: Add three integers whose XOR is 0
            if (ans == x)
            {
                Console.WriteLine(pw1 + pw2 + " " + pw1 + " " + pw2);
            }

            // Case 2: Add three integers
            // whose XOR is equal to ans
            else
            {
                Console.WriteLine(pw1 + " " + ((pw1 ^ x) ^ ans)
                                + " 0 ");
            }
        }
    }

    // Driver code
    public static void Main()
    {
        int n = 4, x = 3;
        Findseq(n, x);
    }
}

// This code contributed by anuj_67..
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
// Function to find and print
// the required sequence
function Findseq($n, $x)
{
    $pw1 = (1 << 17);
    $pw2 = (1 << 18);

    // Base case
    if ($n == 1)
        echo $x ,"\n";

    // Not allowed case
    else if ($n == 2 && $x == 0)
        echo "-1" ,"\n";
    else if ($n == 2)
        echo $x ," ",
            "0","\n";
    else
    {
        $i;
        $ans = 0;

        // XOR of first N - 3 elements
        for ($i = 1; $i <= $n - 3; $i++)
        {
            echo $i , " ";
            $ans = $ans ^ $i;
        }

        // Case 1: Add three integers whose XOR is 0
        if ($ans == $x)
            echo ($pw1 + $pw2) , " ",
                $pw1 ," " , $pw2,"\n";

        // Case 2: Add three integers
        // whose XOR is equal to ans
        else
            echo $pw1 , " " ,(($pw1 ^ $x) ^ $ans),
                " 0 " ,"\n";
    }
}

// Driver code

    $n = 4;
    $x = 3;
    Findseq($n, $x);

// This code is contributed BY @Tushil..
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find and print
// the required sequence
function Findseq(n, x)
{
    let pw1 = (1 << 17);
    let pw2 = (1 << 18);

    // Base case
    if (n == 1)
        document.write(x + "<br>");

    // Not allowed case
    else if (n == 2 && x == 0)
        document.write("-1<br>");
    else if (n == 2)
        document.write(x + " "
             + "0" + "<br>");
    else {
        let i;
        let ans = 0;

        // XOR of first N - 3 elements
        for (i = 1; i <= n - 3; i++) {
            document.write(i + " ");
            ans = ans ^ i;
        }

        // Case 1: Add three integers whose XOR is 0
        if (ans == x)
            document.write((pw1 + pw2) + " "
                 + pw1 + " " <+ pw2 + "<br>");

        // Case 2: Add three integers
        // whose XOR is equal to ans
        else
            document.write(pw1 + " " + ((pw1 ^ x) ^ ans)
                 + " 0 " + "<br>");
    }
}

// Driver code
    let n = 4, x = 3;
    Findseq(n, x)

</script>
```

**Output:** 

```
1 131072 131074 0
```

**时间复杂度:** O(N)