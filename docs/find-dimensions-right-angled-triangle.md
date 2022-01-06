# 求直角三角形的尺寸

> 原文:[https://www . geesforgeks . org/find-dimensions-直角三角形/](https://www.geeksforgeeks.org/find-dimensions-right-angled-triangle/)

给定直角三角形的 H(斜边)和 A(面积)，求直角三角形的尺寸，使斜边长度为 H，面积为 A。如果不存在这样的三角形，打印“不可能”。

示例:

```
Input : H = 10, A = 24
Output : P = 6.00, B = 8.00

Input : H = 13, A = 36
Output : Not Possible
```

**逼近:**
在进入精确解之前，我们先做一些与直角三角形性质相关的数学计算。
假设 **H** =斜边， **P** =垂直， **B** =底边， **A** =直角三角形面积。

我们有一些等式如下:

```
P^2 + B^2 = H^2
P * B = 2 * A
(P+B)^2 = P^2 + B^2 + 2*P*B = H^2 + 4*A
(P+B) = sqrt(H^2 + 4*A)  ----1
(P-B)^2 = P^2 + B^2 - 2*P*B = H^2 - 4*A
mod(P-B) = sqrt(H^2 - 4*A)  ----2
from equation (2) we can conclude that if 
H^2 < 4*A then no solution is possible.

Further from (1)+(2) and (1)-(2) we have :
P = (sqrt(H^2 + 4*A) + sqrt(H^2 - 4*A) ) / 2
B = (sqrt(H^2 + 4*A) - sqrt(H^2 - 4*A) ) / 2
```

下面是上述方法的实现:

## C++

```
// CPP program to find dimensions of
// Right angled triangle
#include <bits/stdc++.h>
using namespace std;

// function to calculate dimension
void findDimen(int H, int A)
{
    // P^2+B^2 = H^2
    // P*B = 2*A
    // (P+B)^2 = P^2+B^2+2*P*B = H^2+4*A
    // (P-B)^2 = P^2+B^2-2*P*B = H^2-4*A
    // P+B = sqrt(H^2+4*A)
    // |P-B| = sqrt(H^2-4*A)

    if (H * H < 4 * A) {
        cout << "Not Possible\n";
        return;
    }

    // sqrt value of H^2 + 4A and H^2- 4A
    double apb = sqrt(H * H + 4 * A);
    double asb = sqrt(H * H - 4 * A);

    // Set precision
    cout.precision(2);

    cout << "P = " << fixed
         << (apb - asb) / 2.0 << "\n";
    cout << "B = " << (apb + asb) / 2.0;
}

// driver function
int main()
{
    int H = 5;
    int A = 6;
    findDimen(H, A);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find dimensions of
// Right angled triangle
class GFG {

    // function to calculate dimension
    static void findDimen(int H, int A)
    {

        // P^2+B^2 = H^2
        // P*B = 2*A
        // (P+B)^2 = P^2+B^2+2*P*B = H^2+4*A
        // (P-B)^2 = P^2+B^2-2*P*B = H^2-4*A
        // P+B = sqrt(H^2+4*A)
        // |P-B| = sqrt(H^2-4*A)
        if (H * H < 4 * A) {
            System.out.println("Not Possible");
            return;
        }

        // sqrt value of H^2 + 4A and H^2- 4A
        double apb = Math.sqrt(H * H + 4 * A);
        double asb = Math.sqrt(H * H - 4 * A);

        System.out.println("P = " + Math.round(((apb - asb) / 2.0) * 100.0) / 100.0);
        System.out.print("B = " + Math.round(((apb + asb) / 2.0) * 100.0) / 100.0);
    }

    // Driver function
    public static void main(String[] args)
    {
        int H = 5;
        int A = 6;

        findDimen(H, A);
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python code to find dimensions
# of Right angled triangle

# importing the math package
# to use sqrt function
from math import sqrt

# function to find the dimensions
def findDimen( H, A):

    # P ^ 2 + B ^ 2 = H ^ 2
    # P * B = 2 * A
    # (P + B)^2 = P ^ 2 + B ^ 2 + 2 * P*B = H ^ 2 + 4 * A
    # (P-B)^2 = P ^ 2 + B ^ 2-2 * P*B = H ^ 2-4 * A
    # P + B = sqrt(H ^ 2 + 4 * A)
    # |P-B| = sqrt(H ^ 2-4 * A)
    if H * H < 4 * A:
        print("Not Possible")
        return

    # sqrt value of H ^ 2 + 4A and H ^ 2- 4A
    apb = sqrt(H * H + 4 * A)
    asb = sqrt(H * H - 4 * A)

    # printing the dimensions
    print("P = ", "%.2f" %((apb - asb) / 2.0))
    print("B = ", "%.2f" %((apb + asb) / 2.0))

# driver code
H = 5 # assigning value to H
A = 6 # assigning value to A
findDimen(H, A) # calling function

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find dimensions of
// Right angled triangle
using System;

class GFG {

    // function to calculate dimension
    static void findDimen(int H, int A)
    {

        // P^2+B^2 = H^2
        // P*B = 2*A
        // (P+B)^2 = P^2+B^2+2*P*B = H^2+4*A
        // (P-B)^2 = P^2+B^2-2*P*B = H^2-4*A
        // P+B = sqrt(H^2+4*A)
        // |P-B| = sqrt(H^2-4*A)
        if (H * H < 4 * A) {
            Console.WriteLine("Not Possible");
            return;
        }

        // sqrt value of H^2 + 4A and H^2- 4A
        double apb = Math.Sqrt(H * H + 4 * A);
        double asb = Math.Sqrt(H * H - 4 * A);

        Console.WriteLine("P = " + Math.Round(
          ((apb - asb) / 2.0) * 100.0) / 100.0);

        Console.WriteLine("B = " + Math.Round(
          ((apb + asb) / 2.0) * 100.0) / 100.0);
    }

    // Driver function
    public static void Main()
    {
        int H = 5;
        int A = 6;

        findDimen(H, A);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find dimensions
// of Right angled triangle

// function to calculate dimension
function findDimen($H, $A)
{

    // P^2+B^2 = H^2
    // P*B = 2*A
    // (P+B)^2 = P^2+B^2+2*P*B = H^2+4*A
    // (P-B)^2 = P^2+B^2-2*P*B = H^2-4*A
    // P+B = sqrt(H^2+4*A)
    // |P-B| = sqrt(H^2-4*A)
    if ($H * $H < 4 * $A)
    {
        echo "Not Possible\n";
        return;
    }

    // sqrt value of H^2 + 4A and
    // H^2- 4A
    $apb = sqrt($H * $H + 4 * $A);
    $asb = sqrt($H * $H - 4 * $A);

    echo "P = " , $fixed
        , ($apb - $asb) / 2.0 , "\n";
    echo "B = " , ($apb + $asb) / 2.0;
}

    // Driver Code
    $H = 5;
    $A = 6;
    findDimen($H, $A);

// This code is contributed by vt_m.
?>
```

## java 描述语言

```
<script>
// java script  program to find dimensions
// of Right angled triangle

// function to calculate dimension
function findDimen(H, A)
{

    // P^2+B^2 = H^2
    // P*B = 2*A
    // (P+B)^2 = P^2+B^2+2*P*B = H^2+4*A
    // (P-B)^2 = P^2+B^2-2*P*B = H^2-4*A
    // P+B = sqrt(H^2+4*A)
    // |P-B| = sqrt(H^2-4*A)
    if (H * H < 4 * A)
    {
        document.write( "Not Possible");
        return;
    }

    // sqrt value of H^2 + 4A and
    // H^2- 4A
    let apb = Math.sqrt(H * H + 4 * A);
    let asb = Math.sqrt(H * H - 4 * A);

    document.write( "P = " +((apb - asb) / 2.0).toFixed(2), "<br>");
    document.write( "B = " +((apb + asb) / 2.0).toFixed(2));
}

    // Driver Code
    let H = 5;
    let A = 6;
    findDimen(H, A);
// This code is contributed by Gottumukkala Bobby
</script>
```

输出:

```
P = 3.00
B = 4.00
```