# 计算可被 4 整除的旋转数

> 原文:[https://www.geeksforgeeks.org/count-rotations-divisible-4/](https://www.geeksforgeeks.org/count-rotations-divisible-4/)

给定一个大的正数作为字符串，计算给定数字中可被 4 整除的所有旋转。

**示例:**

```
Input: 8
Output: 1

Input: 20
Output: 1
Rotation: 20 is divisible by 4
          02 is not divisible by 4

Input : 13502
Output : 0
No rotation is divisible by 4

Input : 43292816
Output : 5
5 rotations are : 43292816, 16432928, 81643292
                  92816432, 32928164 
```

对于大数来说，很难将每个数旋转并除以 4。因此，使用了“可被 4 整除”的属性，即如果一个数的最后 2 位数字可被 4 整除，则该数可被 4 整除。这里，我们实际上并不旋转数字并检查最后 2 位的可除性，而是计算可被 4 整除的连续对(以循环方式)。

<u>插图:</u>T3]

```
Consider a number 928160
Its rotations are 928160, 092816, 609281, 160928, 
    816092, 281609.
Now form pairs from the original number 928160
as mentioned in the approach.
Pairs: (9,2), (2,8), (8,1), (1,6), 
         (6,0), (0,9)
We can observe that the 2-digit number formed by the these 
pairs, i.e., 92, 28, 81, 16, 60, 09, are present in the last
2 digits of some rotation.
Thus, checking divisibility of these pairs gives the required
number of rotations. 

Note: A single digit number can directly
be checked for divisibility.
```

下面是该方法的实现。

## C++

```
// C++ program to count all rotation divisible
// by 4.
#include <bits/stdc++.h>
using namespace std;

// Returns count of all rotations divisible
// by 4
int countRotations(string n)
{
    int len = n.length();

    // For single digit number
    if (len == 1)
    {
        int oneDigit = n.at(0)-'0';
        if (oneDigit%4 == 0)
            return 1;
        return 0;
    }

    // At-least 2 digit number (considering all
    // pairs)
    int twoDigit, count = 0;
    for (int i=0; i<(len-1); i++)
    {
        twoDigit = (n.at(i)-'0')*10 + (n.at(i+1)-'0');
        if (twoDigit%4 == 0)
            count++;
    }

    // Considering the number formed by the pair of
    // last digit and 1st digit
    twoDigit = (n.at(len-1)-'0')*10 + (n.at(0)-'0');
    if (twoDigit%4 == 0)
        count++;

    return count;
}

//Driver program
int main()
{
    string n = "4834";
    cout << "Rotations: " << countRotations(n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// all rotation divisible
// by 4.
import java.io.*;

class GFG {

    // Returns count of all
    // rotations divisible
    // by 4
    static int countRotations(String n)
    {
        int len = n.length();

        // For single digit number
        if (len == 1)
        {
          int oneDigit = n.charAt(0)-'0';

          if (oneDigit % 4 == 0)
              return 1;

          return 0;
        }

        // At-least 2 digit
        // number (considering all
        // pairs)
        int twoDigit, count = 0;
        for (int i = 0; i < (len-1); i++)
        {
          twoDigit = (n.charAt(i)-'0') * 10 +
                     (n.charAt(i+1)-'0');

          if (twoDigit%4 == 0)
              count++;
        }

        // Considering the number
        // formed by the pair of
        // last digit and 1st digit
        twoDigit = (n.charAt(len-1)-'0') * 10 +
                   (n.charAt(0)-'0');

        if (twoDigit%4 == 0)
            count++;

        return count;
    }

    //Driver program
    public static void main(String args[])
    {
        String n = "4834";
        System.out.println("Rotations: " +
                          countRotations(n));
    }
}

// This code is contributed by Nikita tiwari.
```

## 蟒蛇 3

```
# Python3 program to count
# all rotation divisible
# by 4.

# Returns count of all
# rotations divisible
# by 4
def countRotations(n) :

    l = len(n)

    # For single digit number
    if (l == 1) :
        oneDigit = (int)(n[0])

        if (oneDigit % 4 == 0) :
            return 1
        return 0

    # At-least 2 digit number
    # (considering all pairs)
    count = 0
    for i in range(0, l - 1) :
        twoDigit = (int)(n[i]) * 10 + (int)(n[i + 1])

        if (twoDigit % 4 == 0) :
            count = count + 1

    # Considering the number
    # formed by the pair of
    # last digit and 1st digit
    twoDigit = (int)(n[l - 1]) * 10 + (int)(n[0])
    if (twoDigit % 4 == 0) :
        count = count + 1

    return count

# Driver program
n = "4834"
print("Rotations: " ,
    countRotations(n))

# This code is contributed by Nikita tiwari.
```

## C#

```
// C# program to count all rotation
// divisible by 4.
using System;

class GFG {

    // Returns count of all
    // rotations divisible
    // by 4
    static int countRotations(String n)
    {
        int len = n.Length;

        // For single digit number
        if (len == 1)
        {
            int oneDigit = n[0] - '0';

            if (oneDigit % 4 == 0)
                return 1;

            return 0;
        }

        // At-least 2 digit
        // number (considering all
        // pairs)
        int twoDigit, count = 0;
        for (int i = 0; i < (len - 1); i++)
        {
            twoDigit = (n[i] - '0') * 10 +
                          (n[i + 1] - '0');

            if (twoDigit % 4 == 0)
                count++;
        }

        // Considering the number
        // formed by the pair of
        // last digit and 1st digit
        twoDigit = (n[len - 1] - '0') * 10 +
                               (n[0] - '0');

        if (twoDigit % 4 == 0)
            count++;

        return count;
    }

    //Driver program
    public static void Main()
    {
        String n = "4834";
        Console.Write("Rotations: " +
                    countRotations(n));
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count all
// rotation divisible by 4.

// Returns count of all
// rotations divisible
// by 4
function countRotations($n)
{
    $len = strlen($n);

    // For single digit number
    if ($len == 1)
    {
        $oneDigit = $n[0] - '0';

        if ($oneDigit % 4 == 0)
            return 1;

        return 0;
    }

    // At-least 2 digit
    // number (considering all
    // pairs)
    $twoDigit;$count = 0;
    for ($i = 0; $i < ($len - 1); $i++)
    {
        $twoDigit = ($n[$i] - '0') * 10 +
                    ($n[$i + 1] - '0');

        if ($twoDigit % 4 == 0)
            $count++;
    }

    // Considering the number
    // formed by the pair of
    // last digit and 1st digit
    $twoDigit = ($n[$len - 1] - '0') * 10 +
                ($n[0] - '0');

    if ($twoDigit % 4 == 0)
        $count++;

    return $count;
}

// Driver Code
$n = "4834";
echo "Rotations: " ,
      countRotations($n);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>

// Javascript program to count all
// rotation divisible by 4.

// Returns count of all
// rotations divisible
// by 4
function countRotations(n)
{
    let len = n.length;

    // For single digit number
    if (len == 1)
    {
        let oneDigit = n[0] - '0';

        if (oneDigit % 4 == 0)
            return 1;

        return 0;
    }

    // At-least 2 digit
    // number (considering all
    // pairs)
    let twoDigit;
    let count = 0;

    for(let i = 0; i < (len - 1); i++)
    {
        twoDigit = (n[i] - '0') * 10 +
                   (n[i + 1] - '0');

        if (twoDigit % 4 == 0)
            count++;
    }

    // Considering the number
    // formed by the pair of
    // last digit and 1st digit
    twoDigit = (n[len - 1] - '0') * 10 +
               (n[0] - '0');

    if (twoDigit % 4 == 0)
        count++;

    return count;
}

// Driver Code
let n = "4834";

document.write("Rotations: " +
               countRotations(n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
Rotations: 2
```

**时间复杂度:** O(n)，其中 n 为输入数字的位数。

本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。