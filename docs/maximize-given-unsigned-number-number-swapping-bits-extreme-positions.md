# 通过在给定的无符号数的极端位置交换位来最大化该数。

> 原文:[https://www . geesforgeks . org/maximum-给定-无符号-数字-数字-交换-位-极端-位置/](https://www.geeksforgeeks.org/maximize-given-unsigned-number-number-swapping-bits-extreme-positions/)

给定一个数，通过在它的极限位置，即第一个和最后一个位置，第二个和第二个最后一个位置等位置交换位来最大化它。
**例:**

```
Input : 4 (0000...0100)
Output : 536870912 (0010...0000)
In the above example swapped 3rd and 3rd last
bit to maximize the given unsigned number.

Input : 12 (00000...1100)
Output : 805306368 (0011000...0000)

In the above example 3rd and 3rd last bit and
4th and 4th last bit are swapped to maximize 
the given unsigned number.
```

**天真的做法:**
**1。**将数字转换为其位表示，并将其位表示存储在数组中。
**2。**从两端遍历数组，如果位表示的低有效位大于高有效位，即如果低有效位为 1，高有效位为 0，则交换它们，否则不采取任何行动。
**3。**将获得的二进制表示转换回数字。
**高效途径:**
**1。**创建原始数字的副本，因为原始数字会被修改，迭代获取极端位置的位。
**2。**如果较低有效位为 1，较高有效位为 0，则仅交换该位中的位，继续该过程，直到较低有效位的位置小于较高有效位的位置。
T21【3】。显示最大化数字。

## C++

```
// C++ program to find maximum number by
// swapping extreme bits.
#include <bits/stdc++.h>
using namespace std;

#define ull unsigned long long int

ull findMax(ull num)
{
    ull num_copy = num;

    /* Traverse bits from both extremes */
    int j = sizeof(unsigned long long int) * 8 - 1;
    int i = 0;
    while (i < j) {

        // Obtaining i-th and j-th bits
        int m = (num_copy >> i) & 1;
        int n = (num_copy >> j) & 1;

        /* Swapping the bits if lesser significant
           is greater than higher significant
           bit and accordingly modifying the number */
        if (m > n) {
            int x = (1 << i | 1 << j);
            num = num ^ x;
        }

        i++;
        j--;
    }
    return num;
}

// Driver code
int main()
{
    ull num = 4;
    cout << findMax(num);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number by
// swapping extreme bits.

class GFG {

    static int findMax(int num) {
        byte size_of_int = 4;
        int num_copy = num;

        /* Traverse bits from both extremes */
        int j = size_of_int * 8 - 1;
        int i = 0;
        while (i < j) {

            // Obtaining i-th and j-th bits
            int m = (num_copy >> i) & 1;
            int n = (num_copy >> j) & 1;

            /* Swapping the bits if lesser significant
        is greater than higher significant
        bit and accordingly modifying the number */
            if (m > n) {
                int x = (1 << i | 1 << j);
                num = num ^ x;
            }

            i++;
            j--;
        }
        return num;
    }

    // Driver code
    static public void main(String[] args) {
        int num = 4;
        System.out.println(findMax(num));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find maximum number
# by swapping extreme bits.

def findMax( num):
    num_copy = num

    # Traverse bits from both extremes
    j = 4 * 8 - 1;
    i = 0
    while (i < j) :

        # Obtaining i-th and j-th bits
        m = (num_copy >> i) & 1
        n = (num_copy >> j) & 1

        # Swapping the bits if lesser significant
        # is greater than higher significant
        # bit and accordingly modifying the number
        if (m > n) :
            x = (1 << i | 1 << j)
            num = num ^ x

        i += 1
        j -= 1
    return num

# Driver code
if __name__ == "__main__":

    num = 4
    print(findMax(num))

# This code is contributed by ita_c
```

## C#

```

// C# program to find maximum number by
// swapping extreme bits.
using System;
public class GFG {

    static int findMax(int num) {
        byte size_of_int = 4;
        int num_copy = num;

        /* Traverse bits from both extremes */
        int j = size_of_int * 8 - 1;
        int i = 0;
        while (i < j) {

            // Obtaining i-th and j-th bits
            int m = (num_copy >> i) & 1;
            int n = (num_copy >> j) & 1;

            /* Swapping the bits if lesser significant
        is greater than higher significant
        bit and accordingly modifying the number */
            if (m > n) {
                int x = (1 << i | 1 << j);
                num = num ^ x;
            }

            i++;
            j--;
        }
        return num;
    }

// Driver code
    static public void Main() {
        int num = 4;
        Console.Write(findMax(num));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program to find maximum number by
// swapping extreme bits.

function findMax(num)
{
    let num_copy = num;

    /* Traverse bits from both extremes */
    let j = 4 * 8 - 1;
    let i = 0;
    while (i < j) {

        // Obtaining i-th and j-th bits
        let m = (num_copy >> i) & 1;
        let n = (num_copy >> j) & 1;

        /* Swapping the bits if lesser significant
        is greater than higher significant
        bit and accordingly modifying the number */
        if (m > n) {
            let x = (1 << i | 1 << j);
            num = num ^ x;
        }

        i++;
        j--;
    }
    return num;
}

// Driver code

    let num = 4;
    document.write(findMax(num));

// This code is contributed by Manoj.
</script>
```

**输出:**

```
536870912
```

本文由 [**阿迪蒂亚·古普塔**](https://www.linkedin.com/in/aditya-gupta-437504a7?trk=hp-identity-name) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。