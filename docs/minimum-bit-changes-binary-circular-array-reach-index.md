# 二进制循环数组中达到索引的最小位变化

> 原文:[https://www . geesforgeks . org/minimum-bit-changes-binary-circular-array-reach-index/](https://www.geeksforgeeks.org/minimum-bit-changes-binary-circular-array-reach-index/)

给定大小为 **N** 个元素和两个正整数 **x** 和 **y** 的二进制圆形数组，表示圆形数组中的索引。任务是检查哪条路径，顺时针还是逆时针，从索引 x 到索引 y，我们面临最小数量的位翻转。输出“顺时针”或“逆时针”和最小位翻转值，在等计数的情况下输出“顺时针”。
**举例:**

```
Input : arr[] = { 0, 0, 0, 1, 1, 0 }
        x = 0, y = 5
Output : Anti-clockwise 0
The path 0 -> 1 -> 2 -> 3 -> 4 -> 5, we have only 1 value change i.e from index 2 to 3.
The path 0 -> 5 have 0 value change.
So, the answer is Anti-clockwise 0.

Input : s = { 1, 1, 0, 1, 1 }
        x = 2, y = 0
Output : Clockwise 1
```

想法是顺时针旋转一次并存储计数 1，然后逆时针旋转并存储计数 2。然后通过比较 count1 和 count2 输出。
顺时针还是逆时针怎么走？
在 x > y 所在的数组中很难顺时针移动，而在 y > x 所在的数组中很难逆时针移动。因此，我们将给定的二进制数组存储在字符串“S”中。为了使它成为圆形，我们将 S 附加到 S 上，即 S = S + S。我们将在 x 和 y 方向进行调整，使其顺时针或逆时针移动。
现在，如果 y > x 又往顺时针方向走，将很容易从 x 迭代到 y 并计算翻转位数。
如果 y > x，并且要逆时针，我们将把|S|加到 x 上，然后从 y 迭代到 x，并计算翻转位数。
现在，如果 x > y，我们将交换 x 和 y，并使用上述方法计算答案。然后输出相反的结果。
要计算翻转位数，只需存储索引的当前位，并检查下一个索引是否与当前位相同。如果是，则不做任何其他操作，将当前位更改为下一个索引的位，并将最小位增加 1。
以下是该方法的实现:

## C++

```
// CPP program to find direction with minimum flips
#include <bits/stdc++.h>
using namespace std;

// finding which path have minimum flip bit and
// the minimum flip bits
void minimumFlip(string s, int x, int y)
{
    // concatenating given string to itself,
    // to make it circular
    s = s + s;

    // check x is greater than y.
    // marking if output need to
    // be opposite.
    bool isOpposite = false;   
    if (x > y) {
        swap(x, y);
        isOpposite = true;
    }

    // iterate Clockwise
    int valClockwise = 0;
    char cur = s[x];
    for (int i = x; i <= y; i++) {

        // if current bit is not equal
        // to next index bit.
        if (s[i] != cur) {
            cur = s[i];
            valClockwise++;
        }
    }

    // iterate Anti-Clockwise
    int valAnticlockwise = 0;
    cur = s[y];
    x += s.length();
    for (int i = y; i <= x; i++) {

        // if current bit is not equal
        // to next index bit.
        if (s[i] != cur) {
            cur = s[i];
            valAnticlockwise++;
        }
    }

    // Finding whether Clockwise or Anti-clockwise
    // path take minimum flip.
    if (valClockwise <= valAnticlockwise) {
        if (!isOpposite)
            cout << "Clockwise "
                << valClockwise << endl;
        else
            cout << "Anti-clockwise "
                 << valAnticlockwise << endl;
    }
    else {
        if (!isOpposite)
            cout << "Anti-clockwise "
                 << valAnticlockwise << endl;
        else
            cout << "Clockwise "
                 << valClockwise << endl;
    }
}

// Driven Program
int main()
{
    int x = 0, y = 8;
    string s = "000110";
    minimumFlip(s, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find direction
// with minimum flips
class GFG
{

    // finding which path have
    // minimum flip bit and
    // the minimum flip bits
    static void minimumFlip(String s,
                            int x, int y)
    {
        // concatenating given string to 
        // itself, to make it circular
        s = s + s;

        // check x is greater than y.
        // marking if output need to
        // be opposite.
        boolean isOpposite = false;
        if (x > y)
        {
            swap(x, y);
            isOpposite = true;
        }

        // iterate Clockwise
        int valClockwise = 0;
        char cur = s.charAt(x);
        for (int i = x; i <= y; i++)
        {

            // if current bit is not equal
            // to next index bit.
            if (s.charAt(i) != cur)
            {
                cur = s.charAt(i);
                valClockwise++;
            }
        }

        // iterate Anti-Clockwise
        int valAnticlockwise = 0;
        cur = s.charAt(y);
        x += s.length();
        for (int i = y; i < x; i++)
        {

            // if current bit is not equal
            // to next index bit.
            if (s.charAt(i) != cur)
            {
                cur = s.charAt(i);
                valAnticlockwise++;
            }
        }

        // Finding whether Clockwise
        // or Anti-clockwise path
        // take minimum flip.
        if (valClockwise <= valAnticlockwise)
        {
            if (!isOpposite)
            {
                System.out.println("Clockwise " +
                                    valClockwise);
            }
            else
            {
                System.out.println("Anti-clockwise " +
                                    valAnticlockwise);
            }

        }
        else if (!isOpposite)
        {
            System.out.println("Anti-clockwise " +
                                valAnticlockwise);
        }
        else
        {
            System.out.println("Clockwise " +
                                valClockwise);
        }
    }

    static void swap(int a, int b)
    {
        int c = a;
        a = b;
        b = c;
    }

    // Driver code
    public static void main(String[] args)
    {
        int x = 0, y = 8;
        String s = "000110";
        minimumFlip(s, x, y);
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to find direction
# with minimum flips

# finding which path have minimum flip bit
# and the minimum flip bits
def minimumFlip(s, x, y):

    # concatenating given string to itself,
    # to make it circular
    s = s + s

    # check x is greater than y.
    # marking if output need to
    # be opposite.
    isOpposite = False
    if (x > y):
        temp = y
        y = x;
        x = temp
        isOpposite = True

    # iterate Clockwise
    valClockwise = 0
    cur = s[x]
    for i in range(x, y + 1, 1):

        # if current bit is not equal
        # to next index bit.
        if (s[i] != cur):
            cur = s[i]
            valClockwise += 1

    # iterate Anti-Clockwise
    valAnticlockwise = 0
    cur = s[y]
    x += len(s) - 1
    for i in range(y, x + 1, 1):

        # if current bit is not equal
        # to next index bit.
        if (s[i] != cur):
            cur = s[i]
            valAnticlockwise += 1

    # Finding whether Clockwise or Anti-clockwise
    # path take minimum flip.
    if (valClockwise <= valAnticlockwise):
        if (isOpposite == False):
            print("Clockwise", valClockwise)
        else:
            print("Anti-clockwise",
                   valAnticlockwise)

    else:
        if (isOpposite == False):
            print("Anti-clockwise",
                   valAnticlockwise)

        else:
            print("Clockwise", valClockwise)

# Driver Code
if __name__ == '__main__':
    x = 0
    y = 8
    s = "000110"
    minimumFlip(s, x, y)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find direction
// with minimum flips
using System;

class GFG
{

    // finding which path have
    // minimum flip bit and
    // the minimum flip bits
    static void minimumFlip(String s,
                            int x, int y)
    {
        // concatenating given string to
        // itself, to make it circular
        s = s + s;

        // check x is greater than y.
        // marking if output need to
        // be opposite.
        bool isOpposite = false;
        if (x > y)
        {
            swap(x, y);
            isOpposite = true;
        }

        // iterate Clockwise
        int valClockwise = 0;
        char cur = s[x];
        for (int i = x; i <= y; i++)
        {

            // if current bit is not equal
            // to next index bit.
            if (s[i] != cur)
            {
                cur = s[i];
                valClockwise++;
            }
        }

        // iterate Anti-Clockwise
        int valAnticlockwise = 0;
        cur = s[y];
        x += s.Length;
        for (int i = y; i < x; i++)
        {

            // if current bit is not equal
            // to next index bit.
            if (s[i] != cur)
            {
                cur = s[i];
                valAnticlockwise++;
            }
        }

        // Finding whether Clockwise
        // or Anti-clockwise path
        // take minimum flip.
        if (valClockwise <= valAnticlockwise)
        {
            if (!isOpposite)
            {
                Console.WriteLine("Clockwise " +
                                    valClockwise);
            }
            else
            {
                Console.WriteLine("Anti-clockwise " +
                                    valAnticlockwise);
            }

        }
        else if (!isOpposite)
        {
            Console.WriteLine("Anti-clockwise " +
                                valAnticlockwise);
        }
        else
        {
            Console.WriteLine("Clockwise " +
                                valClockwise);
        }
    }

    static void swap(int a, int b)
    {
        int c = a;
        a = b;
        b = c;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int x = 0, y = 8;
        String s = "000110";
        minimumFlip(s, x, y);
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to find direction with minimum flips

// finding which path have minimum flip bit and
// the minimum flip bits
function minimumFlip(s, x, y)
{
    // concatenating given string to itself,
    // to make it circular
    s = s + s;

    // check x is greater than y.
    // marking if output need to
    // be opposite.
    var isOpposite = false;   
    if (x > y) {
        swap(x, y);
        isOpposite = true;
    }

    // iterate Clockwise
    var valClockwise = 0;
    var cur = s[x];
    for (var i = x; i <= y; i++) {

        // if current bit is not equal
        // to next index bit.
        if (s[i] != cur) {
            cur = s[i];
            valClockwise++;
        }
    }

    // iterate Anti-Clockwise
    var valAnticlockwise = 0;
    cur = s[y];
    x += s.length;
    for (var i = y; i <= x; i++) {

        // if current bit is not equal
        // to next index bit.
        if (s[i] != cur) {
            cur = s[i];
            valAnticlockwise++;
        }
    }

    // Finding whether Clockwise or Anti-clockwise
    // path take minimum flip.
    if (valClockwise <= valAnticlockwise) {
        if (!isOpposite)
            document.write( "Clockwise "
                + valClockwise + "<br>");
        else
            document.write( "Anti-clockwise "
                 + valAnticlockwise + "<br>");
    }
    else {
        if (!isOpposite)
            document.write( "Anti-clockwise "
                 + valAnticlockwise + "<br>");
        else
            document.write( "Clockwise "
                 + valClockwise + "<br>");
    }
}

// Driven Program
var x = 0, y = 8;
var s = "000110";
minimumFlip(s, x, y);

// This code is contributed by rrrtnx.
</script>
```

**输出:**

```
Clockwise 2
```