# 最小化要在 X 和 Y 方向翻转的位，使它们的位“或”等于 Z

> 原文:[https://www . geeksforgeeks . org/最小化 x 和 y 中要翻转的位，以便它们的位或等于 z/](https://www.geeksforgeeks.org/minimize-bits-to-be-flipped-in-x-and-y-such-that-their-bitwise-or-is-equal-to-z/)

给定三个正整数 **X** 、 **Y** 和 **Z** ，任务是计算在 **X** 和 **Y** 中需要翻转的最小位数，使得 **X 或 Y (X | Y)** 等于 **Z** 。

**示例:**

```
Input : X = 5   Y = 8   Z = 6
Output : 3
Explanation : 
        Before          After 
        Flipping        Flipping 
X   ::  0101            0100 
Y   ::  1000            0010
       ------           ----- 
Z   ::  0110            0110
So we need to flip 3 bits in order 
to make (X | Y) = Z .

Input : X = 1   Y = 2   Z = 3
Output : 0
```

**方法:**
为了解决这个问题，我们需要观察到只在以下情况下需要翻转 X 或 Y 位:

*   如果 Z 中的当前位被设置，而 X 和 Y 中的对应位都没有被设置，我们需要在 X 或 Y 中设置一个位。
*   如果 Z 中的当前位未置位，我们需要将 A 和 B 中的对应位置位，以设置的为准。如果两者都已设置，则取消设置。

因此，我们需要遍历 X、Y 和 Z 的位，并按照上述两个步骤来获得所需的结果。

下面是上述方法的实现:

## C++

```
// C++ Program to minimize
// number of bits to be flipped
// in X or Y such that their
// bitwise or is equal to minimize

#include <bits/stdc++.h>
using namespace std;

// This function returns minimum
// number of bits to be flipped in
// X and Y to make X | Y = Z
int minimumFlips(int X, int Y, int Z)
{
    int res = 0;
    while (X > 0 || Y > 0 || Z > 0) {

        // If current bit in Z is set and is
        // also set in either of X or Y or both
        if (((X & 1) || (Y & 1)) && (Z & 1)) {
            X = X >> 1;
            Y = Y >> 1;
            Z = Z >> 1;
            continue;
        }
        // If current bit in Z is set
        // and is unset in both X and Y
        else if (!(X & 1) && !(Y & 1) && (Z & 1)) {
            // Set that bit in either X or Y
            res++;
        }

        else if ((X & 1) || (Y & 1) == 1)
        {
            // If current bit in Z is unset
            // and is set in both X and Y
            if ((X & 1) && (Y & 1) && !(Z & 1)) {
                // Unset the bit in both X and Y
                res += 2;
            }
            // If current bit in Z is unset and
            // is set in either X or Y
            else if (((X & 1) || (Y & 1)) && !(Z & 1))
            {
                // Unset that set bit
                res++;
            }
        }
        X = X >> 1;
        Y = Y >> 1;
        Z = Z >> 1;
    }
    return res;
}

// Driver Code
int main()
{
    int X = 5, Y = 8, Z = 6;
    cout << minimumFlips(X, Y, Z);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to minimize
// number of bits to be flipped
// in X or Y such that their
// bitwise or is equal to minimize
import java.util.*;

class GFG{

// This function returns minimum
// number of bits to be flipped in
// X and Y to make X | Y = Z
static int minimumFlips(int X, int Y, int Z)
{
    int res = 0;
    while (X > 0 || Y > 0 || Z > 0)
    {

        // If current bit in Z is set and is
        // also set in either of X or Y or both
        if (((X % 2 == 1) ||
             (Y % 2 == 1)) &&
             (Z % 2 == 1))
        {
            X = X >> 1;
            Y = Y >> 1;
            Z = Z >> 1;
            continue;
        }

        // If current bit in Z is set
        // and is unset in both X and Y
        else if (!(X % 2 == 1) &&
                 !(Y % 2 == 1) &&
                  (Z % 2 == 1))
        {

            // Set that bit in either X or Y
            res++;
        }

        else if ((X % 2 == 1) || (Y % 2 == 1))
        {

            // If current bit in Z is unset
            // and is set in both X and Y
            if ((X % 2 == 1) &&
                (Y % 2 == 1) &&
               !(Z % 2 == 1))
            {

                // Unset the bit in both X and Y
                res += 2;
            }

            // If current bit in Z is unset and
            // is set in either X or Y
            else if (((X % 2 == 1) ||
                      (Y % 2 == 1)) &&
                     !(Z % 2 == 1))
            {

                // Unset that set bit
                res++;
            }
        }
        X = X >> 1;
        Y = Y >> 1;
        Z = Z >> 1;
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int X = 5, Y = 8, Z = 6;

    System.out.print(minimumFlips(X, Y, Z));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python 3 Program to minimize
# number of bits to be flipped
# in X or Y such that their
# bitwise or is equal to minimize

# This function returns minimum
# number of bits to be flipped in
# X and Y to make X | Y = Z
def minimumFlips(X, Y, Z):

    res = 0
    while (X > 0 or Y > 0 or
           Z > 0):

        # If current bit in Z is
        # set and is also set in
        # either of X or Y or both
        if (((X & 1) or (Y & 1)) and
             (Z & 1)):
            X = X >> 1
            Y = Y >> 1
            Z = Z >> 1
            continue

        # If current bit in Z is set
        # and is unset in both X and Y
        elif (not (X & 1) and not(Y & 1) and
                  (Z & 1)):

            # Set that bit in either
            # X or Y
            res += 1

        elif ((X & 1) or (Y & 1) == 1):

            # If current bit in Z is unset
            # and is set in both X and Y
            if ((X & 1) and (Y & 1) and
                 not(Z & 1)):

                # Unset the bit in both
                # X and Y
                res += 2

            # If current bit in Z is
            # unset and is set in
            # either X or Y
            elif (((X & 1) or (Y & 1)) and
                    not(Z & 1)):

                # Unset that set bit
                res += 1

        X = X >> 1
        Y = Y >> 1
        Z = Z >> 1

    return res

# Driver Code
if __name__ == "__main__":

    X = 5
    Y = 8
    Z = 6
    print(minimumFlips(X, Y, Z))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to minimize
// number of bits to be flipped
// in X or Y such that their
// bitwise or is equal to minimize
using System;
class GFG{

// This function returns minimum
// number of bits to be flipped in
// X and Y to make X | Y = Z
static int minimumFlips(int X, int Y, int Z)
{
    int res = 0;
    while (X > 0 || Y > 0 || Z > 0)
    {

        // If current bit in Z is set and is
        // also set in either of X or Y or both
        if (((X % 2 == 1) ||
             (Y % 2 == 1)) &&
             (Z % 2 == 1))
        {
            X = X >> 1;
            Y = Y >> 1;
            Z = Z >> 1;
            continue;
        }

        // If current bit in Z is set
        // and is unset in both X and Y
        else if (!(X % 2 == 1) &&
                 !(Y % 2 == 1) &&
                  (Z % 2 == 1))
        {

            // Set that bit in either X or Y
            res++;
        }

        else if ((X % 2 == 1) || (Y % 2 == 1))
        {

            // If current bit in Z is unset
            // and is set in both X and Y
            if ((X % 2 == 1) &&
                (Y % 2 == 1) &&
               !(Z % 2 == 1))
            {

                // Unset the bit in both X and Y
                res += 2;
            }

            // If current bit in Z is unset and
            // is set in either X or Y
            else if (((X % 2 == 1) ||
                      (Y % 2 == 1)) &&
                     !(Z % 2 == 1))
            {

                // Unset that set bit
                res++;
            }
        }
        X = X >> 1;
        Y = Y >> 1;
        Z = Z >> 1;
    }
    return res;
}

// Driver Code
public static void Main()
{
    int X = 5, Y = 8, Z = 6;

    Console.Write(minimumFlips(X, Y, Z));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript Program to minimize
// number of bits to be flipped
// in X or Y such that their
// bitwise or is equal to minimize

// This function returns minimum
// number of bits to be flipped in
// X and Y to make X | Y = Z
function minimumFlips(X, Y, Z)
{
    var res = 0;
    while (X > 0 || Y > 0 || Z > 0) {

        // If current bit in Z is set and is
        // also set in either of X or Y or both
        if (((X & 1) || (Y & 1)) && (Z & 1))
        {
            X = X >> 1;
            Y = Y >> 1;
            Z = Z >> 1;
            continue;
        }
        // If current bit in Z is set
        // and is unset in both X and Y
        else if ((X & 1)==0 && (Y & 1)==0 &&
                (Z & 1))
        {
            // Set that bit in either X or Y
            res++;
        }

        else if ((X & 1) || (Y & 1) == 1)
        {
            // If current bit in Z is unset
            // and is set in both X and Y
            if ((X & 1) && (Y & 1) && (Z & 1)==0)
            {
                // Unset the bit in both X and Y
                res += 2;
            }
            // If current bit in Z is unset and
            // is set in either X or Y
            else if (((X & 1) || (Y & 1)) &&
                      (Z & 1)==0)
            {
                // Unset that set bit
                res++;
            }
        }
        X = X >> 1;
        Y = Y >> 1;
        Z = Z >> 1;
    }
    return res;
}

// Driver Code

    var X = 5, Y = 8, Z = 6;
    document.write(minimumFlips(X, Y, Z));

</script>
```

**Output:** 

```
3
```