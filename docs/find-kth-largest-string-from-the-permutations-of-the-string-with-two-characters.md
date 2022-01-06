# 从两个字符的字符串排列中找出第 k 个最大的字符串

> 原文:[https://www . geeksforgeeks . org/find-kth-由两个字符组成的字符串排列中最大的字符串/](https://www.geeksforgeeks.org/find-kth-largest-string-from-the-permutations-of-the-string-with-two-characters/)

给定两个整数 **N** 和 **K** ，任务是从仅包含两个字符‘x’和‘y’的字符串集合中找到字典上最大的大小为 N 的第**K**个字符串，其中字符‘x’在字符串中出现(N–2)次，字符‘y’仅出现 2 次。
**举例:**

> **输入:** N = 4，K = 3
> **输出:**yxy
> **解释:**
> 大小为 4 的所有字符串–
> { xxyy，xyxy，xyyx，yxy，yyxx }
> 第 3 个 <sup>rd</sup> 最小的字符串将是–yxy
> **输入:** N = 3，K = 2
> **输出:【T11**

**方法:**
这个想法是观察字典上最大的字符串在开始时有 2 个“y”，后面跟着所有的“x”。字典中第二大的字符串将第二个“y”向前移动一个索引，即“yxyxxxx……”等等。
这个问题的关键观察是字符‘y’在字典上最大的字符串前面出现两次，然后在每一步中，第二个字符‘y’向前移动一步，直到它到达字符串的末尾，以生成下一个最小的字符串。一旦第二个“y”到达字符串末尾，下一个最小的字符串将在索引 1 和 2 处有两个“y”，然后该过程继续。
因此，想法是找到字符“y”的第一个和第二个位置，然后用“y”字符打印这些位置，所有其他位置用“x”字符填充。
以下是上述方法的实施:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// kth largest string
void kthString(int n, int k)
{
    int total = 0;
    int i = 1;

    // loop to iterate through
    // series
    while (total < k) {
        // total takes the position
        // of second y
        total = total + n - i;

        // i takes the position of
        // first y
        i++;
    }

    // calculating first y position
    int first_y_position = i - 1;

    // calculating second y position
    // from first y
    int second_y_position = k - (total - n + first_y_position);

    // print all x before first y
    for (int j = 1; j < first_y_position; j++)
        cout << "x";

    // print first y
    cout << "y";

    int j = first_y_position + 1;

    // print all x between first y
    // and second y
    while (second_y_position > 1) {
        cout << "x";
        second_y_position--;
        j++;
    }

    // print second y
    cout << "y";

    // print x which occur
    // after second y
    while (j < n) {
        cout << "x";
        j++;
    }
}

// Driver code
int main()
{
    int n = 5;

    int k = 7;

    kthString(n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG{

// Function to print the
// kth largest String
static void kthString(int n, int k)
{
    int total = 0;
    int i = 1;

    // loop to iterate through
    // series
    while (total < k) {
        // total takes the position
        // of second y
        total = total + n - i;

        // i takes the position of
        // first y
        i++;
    }

    // calculating first y position
    int first_y_position = i - 1;

    // calculating second y position
    // from first y
    int second_y_position = k - (total - n + first_y_position);

    // print all x before first y
    for (int j = 1; j < first_y_position; j++)
        System.out.print("x");

    // print first y
    System.out.print("y");

    int j = first_y_position + 1;

    // print all x between first y
    // and second y
    while (second_y_position > 1) {
        System.out.print("x");
        second_y_position--;
        j++;
    }

    // print second y
    System.out.print("y");

    // print x which occur
    // after second y
    while (j < n) {
        System.out.print("x");
        j++;
    }
}

// Driver code
public static void main(String[] args)
{
    int n = 5;

    int k = 7;

    kthString(n, k);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 implementation of above approach

# Function to print the
# kth largest string
def kthString(n,k):
    total = 0
    i = 1

    # loop to iterate through
    # series
    while (total < k):
        # total takes the position
        # of second y
        total = total + n - i

        # i takes the position of
        # first y
        i += 1

    # calculating first y position
    first_y_position = i - 1

    # calculating second y position
    # from first y
    second_y_position = k - (total - n + first_y_position)

    # print all x before first y
    for j in range(1,first_y_position,1):
        print("x",end = "")

    # print first y
    print("y",end = "")

    j = first_y_position + 1

    # print all x between first y
    # and second y
    while (second_y_position > 1):
        print("x",end = "")
        second_y_position -= 1
        j += 1

    # print second y
    print("y",end = "")

    # print x which occur
    # after second y
    while (j < n):
        print("x")
        j += 1

# Driver code
if __name__ == '__main__':
    n = 5
    k = 7
    kthString(n, k)

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# implementation of above approach
using System;

class GFG{

    // Function to print the
    // kth largest string
    static void kthString(int n, int k)
    {
        int total = 0;
        int i = 1;

        // loop to iterate through
        // series
        while (total < k) {
            // total takes the position
            // of second y
            total = total + n - i;

            // i takes the position of
            // first y
            i++;
        }

        // calculating first y position
        int first_y_position = i - 1;

        // calculating second y position
        // from first y
        int second_y_position = k - (total - n + first_y_position);

        int j;

        // print all x before first y
        for (j = 1; j < first_y_position; j++)
            Console.Write("x");

        // print first y
        Console.Write("y");

        j = first_y_position + 1;

        // print all x between first y
        // and second y
        while (second_y_position > 1) {
            Console.Write("x");
            second_y_position--;
            j++;
        }

        // print second y
        Console.Write("y");

        // print x which occur
        // after second y
        while (j < n) {
            Console.Write("x");
            j++;
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;

        int k = 7;

        kthString(n, k);
    }
}

// This code is contributed by shubhamsingh10
```

## java 描述语言

```
<script>

// Javascript implementation of above approach

// Function to print the
// kth largest string
function kthString(n, k)
{
    var total = 0;
    var i = 1;

    // loop to iterate through
    // series
    while (total < k) {
        // total takes the position
        // of second y
        total = total + n - i;

        // i takes the position of
        // first y
        i++;
    }

    // calculating first y position
    var first_y_position = i - 1;

    // calculating second y position
    // from first y
    var second_y_position = k - (total - n + first_y_position);

    // print all x before first y
    for (var j = 1; j < first_y_position; j++)
        document.write( "x");

    // print first y
    document.write( "y");

    var j = first_y_position + 1;

    // print all x between first y
    // and second y
    while (second_y_position > 1) {
        document.write( "x");
        second_y_position--;
        j++;
    }

    // print second y
    document.write( "y");

    // print x which occur
    // after second y
    while (j < n) {
        document.write( "x");
        j++;
    }
}

// Driver code
var n = 5;
var k = 7;
kthString(n, k);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
xyxxy
```