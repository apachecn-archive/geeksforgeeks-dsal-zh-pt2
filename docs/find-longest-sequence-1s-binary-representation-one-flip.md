# 用一次翻转找到二进制表示中最长的 1 序列

> 原文:[https://www . geesforgeks . org/find-最长序列-1s-二进制-表示-一-翻转/](https://www.geeksforgeeks.org/find-longest-sequence-1s-binary-representation-one-flip/)

给一个整数 n，我们正好可以翻转一位。编写代码，找出您可以创建的最长 1 s 序列的长度。

**示例:**

```
Input : 1775         
Output : 8 
Binary representation of 1775 is 11011101111.
After flipping the highlighted bit, we get 
consecutive 8 bits. 11011111111.

Input : 12         
Output : 3 

Input : 15
Output : 5

Input : 71
Output: 4

Binary representation of 71 is 1000111.
After flipping the highlighted bit, we get 
consecutive 4 bits. 1001111\. 
```

一个**简单的解决方案**是将给定数字的二进制表示存储在二进制数组中。一旦我们在二进制数组中有了元素，我们就可以应用这里讨论的方法。

一个有效的解决方案是遍历给定数字的二进制表示中的位。我们跟踪当前 1 的序列长度和先前 1 的序列长度。当我们看到一个零，更新之前的长度:

1.  如果下一位是 1，则前一个长度应设置为当前长度。
2.  如果下一位是 0，那么我们不能将这些序列合并在一起。因此，将之前的长度设置为 0。

我们通过比较以下两项来更新最大长度:

1.  最大长度的当前值
2.  当前长度+以前长度。

*   **结果=返回最大长度+1** (//翻转位计数加 1)

下面是上述想法的实现:

## C++

```
// C++ program to find maximum consecutive
// 1's in binary representation of a number
// after flipping one bit.
#include<bits/stdc++.h>
using namespace std;

int flipBit(unsigned a)
{
    /* If all bits are l, binary representation
       of 'a' has all 1s */
    if (~a == 0)
        return 8*sizeof(int);

    int currLen = 0, prevLen = 0, maxLen = 0;
    while (a!= 0)
    {
        // If Current bit is a 1 then increment currLen++
        if ((a & 1) == 1)
            currLen++;

        // If Current bit is a 0 then check next bit of a
        else if ((a & 1) == 0)
        {
            /* Update prevLen to 0 (if next bit is 0)
            or currLen (if next bit is 1). */
            prevLen = (a & 2) == 0? 0 : currLen;

            // If two consecutively bits are 0
            // then currLen also will be 0.
            currLen = 0;
        }

        // Update maxLen if required
        maxLen = max(prevLen + currLen, maxLen);

        // Remove last bit (Right shift)
        a >>= 1;
    }

    // We can always have a sequence of
    // at least one 1, this is flipped bit
    return maxLen+1;
}

// Driver code
int main()
{
    // input 1
    cout << flipBit(13);
    cout << endl;

    // input 2
    cout << flipBit(1775);
    cout << endl;

    // input 3
    cout << flipBit(15);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum consecutive
// 1's in binary representation of a number
// after flipping one bit.

class GFG
{

    static int flipBit(int a)
    {
        /* If all bits are l, binary representation
        of 'a' has all 1s */
        if (~a == 0)
        {
            return 8 * sizeof();
        }

        int currLen = 0, prevLen = 0, maxLen = 0;
        while (a != 0)
        {
            // If Current bit is a 1
            // then increment currLen++
            if ((a & 1) == 1)
            {
                currLen++;
            }

            // If Current bit is a 0 then
            // check next bit of a
            else if ((a & 1) == 0)
            {
                /* Update prevLen to 0 (if next bit is 0)
                or currLen (if next bit is 1). */
                prevLen = (a & 2) == 0 ? 0 : currLen;

                // If two consecutively bits are 0
                // then currLen also will be 0.
                currLen = 0;
            }

            // Update maxLen if required
            maxLen = Math.max(prevLen + currLen, maxLen);

            // Remove last bit (Right shift)
            a >>= 1;
        }

        // We can always have a sequence of
        // at least one 1, this is flipped bit
        return maxLen + 1;
    }

    static byte sizeof()
    {
        byte sizeOfInteger = 8;
        return sizeOfInteger;
    }

    // Driver code
    public static void main(String[] args)
    {
        // input 1
        System.out.println(flipBit(13));

        // input 2
        System.out.println(flipBit(1775));

        // input 3
        System.out.println(flipBit(15));
    }
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find maximum
# consecutive 1's in binary
# representation of a number
# after flipping one bit.
def flipBit(a):

    # If all bits are l,
    # binary representation
    # of 'a' has all 1s
    if (~a == 0):
        return 8 * sizeof();

    currLen = 0;
    prevLen = 0;
    maxLen = 0;
    while (a > 0):

        # If Current bit is a 1
        # then increment currLen++
        if ((a & 1) == 1):
            currLen += 1;

        # If Current bit is a 0
        # then check next bit of a
        elif ((a & 1) == 0):

            # Update prevLen to 0
            # (if next bit is 0)
            # or currLen (if next
            # bit is 1). */
            prevLen = 0 if((a & 2) == 0) else currLen;

            # If two consecutively bits
            # are 0 then currLen also
            # will be 0.
            currLen = 0;

        # Update maxLen if required
        maxLen = max(prevLen + currLen, maxLen);

        # Remove last bit (Right shift)
        a >>= 1;

    # We can always have a sequence
    # of at least one 1, this is
    # flipped bit
    return maxLen + 1;

# Driver code
# input 1
print(flipBit(13));

# input 2
print(flipBit(1775));

# input 3
print(flipBit(15));

# This code is contributed by mits
```

## C#

```
// C# program to find maximum consecutive
// 1's in binary representation of a number
// after flipping one bit.
using System;

class GFG
{

    static int flipBit(int a)
    {
        /* If all bits are l, binary representation
        of 'a' has all 1s */
        if (~a == 0)
        {
            return 8 * sizeof(int);
        }

        int currLen = 0, prevLen = 0, maxLen = 0;
        while (a != 0)
        {
            // If Current bit is a 1
            // then increment currLen++
            if ((a & 1) == 1)
            {
                currLen++;
            }

            // If Current bit is a 0 then
            // check next bit of a
            else if ((a & 1) == 0)
            {
                /* Update prevLen to 0 (if next bit is 0)
                or currLen (if next bit is 1). */
                prevLen = (a & 2) == 0 ? 0 : currLen;

                // If two consecutively bits are 0
                // then currLen also will be 0.
                currLen = 0;
            }

            // Update maxLen if required
            maxLen = Math.Max(prevLen + currLen, maxLen);

            // Remove last bit (Right shift)
            a >>= 1;
        }

        // We can always have a sequence of
        // at least one 1, this is flipped bit
        return maxLen + 1;
    }

    // Driver code
    public static void Main(String[] args)
    {
        // input 1
        Console.WriteLine(flipBit(13));

        // input 2
        Console.WriteLine(flipBit(1775));

        // input 3
        Console.WriteLine(flipBit(15));
    }
}

// This code contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum consecutive
// 1's in binary representation of a number
// after flipping one bit.

function flipBit($a)
{
    /* If all bits are l,
       binary representation
       of 'a' has all 1s */
    if (~$a == 0)
        return 8 * sizeof();

    $currLen = 0;
    $prevLen = 0;
    $maxLen = 0;
    while ($a!= 0)
    {

        // If Current bit is a 1
        // then increment currLen++
        if (($a & 1) == 1)
            $currLen++;

        // If Current bit is a 0
        // then check next bit of a
        else if (($a & 1) == 0)
        {

            /* Update prevLen to 0
               (if next bit is 0)
               or currLen (if next
               bit is 1). */
            $prevLen = ($a & 2) == 0? 0 : $currLen;

            // If two consecutively bits are 0
            // then currLen also will be 0.
            $currLen = 0;
        }

        // Update maxLen if required
        $maxLen = max($prevLen + $currLen, $maxLen);

        // Remove last bit (Right shift)
        $a >>= 1;
    }

    // We can always have a sequence of
    // at least one 1, this is flipped bit
    return $maxLen+1;
}

    // Driver code
    // input 1
    echo flipBit(13);
    echo "\n";

    // input 2
    echo flipBit(1775);
    echo "\n";

    // input 3
    echo flipBit(15);

// This code is contributed by aj_36
?>
```

## java 描述语言

```
<script>

    // Javascript program to
    // find maximum consecutive
    // 1's in binary representation
    // of a number
    // after flipping one bit.

    function flipBit(a)
    {
        /* If all bits are l,
        binary representation
        of 'a' has all 1s */
        if (~a == 0)
        {
            return 8 * sizeof(int);
        }

        let currLen = 0, prevLen = 0, maxLen = 0;
        while (a != 0)
        {
            // If Current bit is a 1
            // then increment currLen++
            if ((a & 1) == 1)
            {
                currLen++;
            }

            // If Current bit is a 0 then
            // check next bit of a
            else if ((a & 1) == 0)
            {
                /* Update prevLen to 0
                (if next bit is 0)
                or currLen (if next bit is 1). */
                prevLen = (a & 2) == 0 ? 0 : currLen;

                // If two consecutively bits are 0
                // then currLen also will be 0.
                currLen = 0;
            }

            // Update maxLen if required
            maxLen = Math.max(prevLen + currLen, maxLen);

            // Remove last bit (Right shift)
            a >>= 1;
        }

        // We can always have a sequence of
        // at least one 1, this is flipped bit
        return maxLen + 1;
    }

    // input 1
    document.write(flipBit(13) + "</br>");

    // input 2
    document.write(flipBit(1775) + "</br>");

    // input 3
    document.write(flipBit(15));

</script>
```

**输出:**

```
4
8
5
```

本文由 Somesh Awasthi 先生供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。