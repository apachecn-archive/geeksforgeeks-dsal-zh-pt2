# 使用 N 段

可在七段显示器上显示的最大数量

> 原文:[https://www . geeksforgeeks . org/七段显示使用 n 段的最大显示数量/](https://www.geeksforgeeks.org/maximum-number-that-can-be-display-on-seven-segment-display-using-n-segments/)

给定正整数 **N** 。任务是找到使用 N 个段在七个段显示器上可以显示的最大数量。
**七段显示器**:七段显示器(SSD)，或七段指示器，是一种显示十进制数字的电子显示设备，是更复杂的点阵显示器的替代品。

![](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/7_Segment_Display_with_Labeled_Segments.svg/648px-7_Segment_Display_with_Labeled_Segments.svg.png)

七段显示的各个段
***图片来源*** : [维基百科](https://upload.wikimedia.org/wikipedia/commons/thumb/e/ed/7_Segment_Display_with_Labeled_Segments.svg/330px-7_Segment_Display_with_Labeled_Segments.svg.png)。

**Examples:** 

```
Input : N = 5 
Output : 71
On 7-segment display, 71 will look like:
_
 | |
 | |

Input : N = 4
Output : 11
```

请注意，位数比其他数字多的数字将具有更大的价值。因此，我们将尝试使用给定的“N”段来产生一个具有最大可能长度(位数)的数字。
还要注意，为了增加数字的长度，我们会尽量在每个数字上使用较少的分段。因此，数字“1”只使用 2 个段来表示一个数字。没有其他数字使用少于 2 段。
所以，如果 N 是偶数，答案是 1s 的 N/2 次。
在 N 为奇数的情况下，如果我们使 1 为 N/2 的次数，我们就不能使用所有的线段。同样，如果我们用 3 个段组成一个 7 的数字和(N-3)/2 的 1 数，那么形成的数的值将大于 N/2 的 1 数形成的数。
以下是本办法的实施情况:

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function to print maximum number that can be formed
// using N segments
void printMaxNumber(int n)
{
    // If n is odd
    if (n & 1) {
        // use 3 three segment to print 7
        cout << "7";

        // remaining to print 1
        for (int i = 0; i < (n - 3) / 2; i++)
            cout << "1";
    }

    // If n is even
    else {
        // print n/2 1s.
        for (int i = 0; i < n / 2; i++)
            cout << "1";
    }
}

// Driver's Code
int main()
{
    int n = 5;

    printMaxNumber(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above approach
class GFG {

    // Function to print maximum number that
    // can be formed using N segments
    public static void printMaxNumber(int n)
    {
        // If n is odd
        if (n % 2 != 0) {
            // use 3 three segment to print 7
            System.out.print("7");

            // remaining to print 1
            for (int i = 0; i < (n - 3) / 2; i++)
                System.out.print("1");
        }

        // If n is even
        else {

            // print n/2 1s.
            for (int i = 0; i < n / 2; i++)
                System.out.print("1");
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 5;
        printMaxNumber(n);
    }
}

// This code is contributed by princiraj1992
```

## 蟒蛇 3

```
# Function to print maximum number that can be formed
# using N segments
def printMaxNumber(n):

    # If n is odd
    if (n % 2 == 1):

        # use 3 three segment to print 7
        print("7",end="");

        # remaining to print 1
        for i in range(int((n - 3) / 2)):
            print("1",end="");

    # If n is even
    else:

        # print n/2 1s.
        for i in range(n/2):
            print("1",end="");

# Driver's Code
n = 5;
printMaxNumber(n);

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of above approach
using System;

class GFG
{

    // Function to print maximum number that
    // can be formed using N segments
    public static void printMaxNumber(int n)
    {
        // If n is odd
        if (n % 2 != 0)
        {
            // use 3 three segment to print 7
            Console.Write("7");

            // remaining to print 1
            for (int i = 0; i < (n - 3) / 2; i++)
                Console.Write("1");
        }

        // If n is even
        else
        {

            // print n/2 1s.
            for (int i = 0; i < n / 2; i++)
                Console.Write("1");
        }
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int n = 5;
        printMaxNumber(n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code implementation of above code

// Function to print maximum number that can be formed
// using N segments
function printMaxNumber($n)
{
    // If n is odd
    if ($n & 1)
    {
        // use 3 three segment to print 7
        echo "7";

        // remaining to print 1
        for ($i = 0; $i < ($n - 3) / 2; $i++)
            echo "1";
    }

    // If n is even
    else
    {
        // print n/2 1s.
        for ($i = 0; $i < $n / 2; $i++)
            echo "1";
    }
}

// Driver's Code
$n = 5;

printMaxNumber($n);

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>

// Function to print maximum number that can be formed
// using N segments
function printMaxNumber(n)
{
    // If n is odd
    if (n & 1) {
        // use 3 three segment to print 7
        document.write( "7");

        // remaining to print 1
        for (var i = 0; i < (n - 3) / 2; i++)
            document.write( "1");
    }

    // If n is even
    else {
        // print n/2 1s.
        for (var i = 0; i < n / 2; i++)
            document.write( "1");
    }
}

// Driver's Code
var n = 5;
printMaxNumber(n);

</script>
```

**Output:** 

```
71
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*