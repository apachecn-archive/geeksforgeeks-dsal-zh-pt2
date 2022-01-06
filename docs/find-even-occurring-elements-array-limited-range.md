# 在有限范围的数组中找到均匀出现的元素

> 原文:[https://www . geeksforgeeks . org/find-偶数出现-元素-数组-有限范围/](https://www.geeksforgeeks.org/find-even-occurring-elements-array-limited-range/)

给定一个数组，该数组包含除少数出现偶数次的元素之外的所有数字的奇数次出现。在 O(n)时间复杂度和 O(1)额外空间中找到数组中出现次数均匀的元素。
假设数组包含 0 到 63 范围内的元素。
**例:**

```
Input: [9, 12, 23, 10, 12, 12, 15, 23, 14, 12, 15]
Output: 12, 23 and 15

Input: [1, 4, 7, 5, 9, 7, 3, 4, 6, 8, 3, 0, 3]
Output: 4 and 7

Input: [4, 4, 10, 10, 4, 4, 4, 4, 10, 10]
Output: 4 and 10
```

一个简单的方法是遍历数组，并在地图中存储其元素的频率。稍后，打印地图中有偶数的元素。该解决方案需要 O(n)个时间，但需要额外的空间来存储频率。下面是一个使用按位运算符解决这个问题的有趣方法。
该方法假设使用 64 位存储长整型。其思想是使用异或运算符。我们知道

```
1 XOR 1 = 0
1 XOR 0 = 1
0 XOR 1 = 1
0 XOR 0 = 0
```

考虑以下输入–

```
 1, 4, 7, 5, 9, 7, 3, 4, 6, 8, 3, 0, 3 
```

如果我们将数组中每个元素的值左移 1，并对所有项目进行异或运算，我们将得到二进制整数–

```
1101101011
```

右边第 I 个索引中的每个 1 代表元素 I 的奇数出现，右边第 I 个索引中的每个 0 代表数组中元素 I 的偶数出现或不出现。
0 出现在上述二进制数的第 2、4、7 位。但是我们的数组中没有 2。所以我们的答案是 4 和 7。
以下是以上想法的实现

## C++

```
// C++ Program to find the even occurring elements
// in given array
#include <iostream>
using namespace std;

// Function to find the even occurring elements
// in given array
void printRepeatingEven(int arr[], int n)
{
    long long _xor = 0L;
    long long pos;

    // do for each element of array
    for( int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of current element
        pos = 1 << arr[i];

        // Toggle the bit everytime element gets repeated
        _xor ^= pos;
    }

    // Traverse array again and use _xor to find even
    // occurring elements
    for (int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of current element
        pos = 1 << arr[i];

        // Each 0 in _xor represents an even occurrence
        if (!(pos & _xor))
        {
            // print the even occurring numbers
            cout << arr[i] << " ";

            // set bit as 1 to avoid printing duplicates
            _xor ^= pos;
        }
    }
}

// Driver code
int main()
{
    int arr[] = { 9, 12, 23, 10, 12, 12, 15, 23,
                 14, 12, 15 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printRepeatingEven(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to find the even occurring
// elements in given array
class GFG
{

// Function to find the even occurring
// elements in given array
static void printRepeatingEven(int arr[],
                               int n)
{
    long _xor = 0L;
    long pos;

    // do for each element of array
    for (int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Toggle the bit everytime
        // element gets repeated
        _xor ^= pos;
    }

    // Traverse array again and use _xor
    // to find even occurring elements
    for (int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Each 0 in _xor represents
        // an even occurrence
        if (!((pos & _xor)!=0))
        {
            // print the even occurring numbers
            System.out.print(arr[i] + " ");

            // set bit as 1 to avoid
            // printing duplicates
            _xor ^= pos;
        }
    }
}

// Driver code
public static void main(String args[])
{
    int arr[] = {9, 12, 23, 10, 12, 12,
                 15, 23, 14, 12, 15};
    int n = arr.length;

    printRepeatingEven(arr, n);
}
}

// This code is contributed
// by 29AjayKumar
```

## C#

```
// C# Program to find the even occurring
// elements in given array
using System;

class GFG
{

// Function to find the even occurring
// elements in given array
static void printRepeatingEven(int[] arr,
                               int n)
{
    long _xor = 0L;
    long pos;

    // do for each element of array
    for (int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Toggle the bit everytime
        // element gets repeated
        _xor ^= pos;
    }

    // Traverse array again and use _xor
    // to find even occurring elements
    for (int i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Each 0 in _xor represents
        // an even occurrence
        if (!((pos & _xor) != 0))
        {
            // print the even occurring numbers
            Console.Write(arr[i] + " ");

            // set bit as 1 to avoid
            // printing duplicates
            _xor ^= pos;
        }
    }
}

// Driver code
public static void Main()
{
    int[] arr = {9, 12, 23, 10, 12, 12,
                15, 23, 14, 12, 15};
    int n = arr.Length;

    printRepeatingEven(arr, n);
}
}

// This code is contributed
// by Mukul singh
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to find the even
// occurring elements in given array

// Function to find the even
// occurring elements in given array
function printRepeatingEven($arr, $n)
{
    $_xor = 0;
    $pos;

    // do for each element of array
    for( $i = 0; $i < $n; ++$i)
    {
        // left-shift 1 by value
        // of current element
        $pos = 1 << $arr[$i];

        // Toggle the bit everytime
        // element gets repeated
        $_xor ^= $pos;
    }

    // Traverse array again and
    // use _xor to find even
    // occurring elements
    for ($i = 0; $i < $n; ++$i)
    {
        // left-shift 1 by value
        // of current element
        $pos = 1 << $arr[$i];

        // Each 0 in _xor represents
        // an even occurrence
        if (!($pos & $_xor))
        {
            // print the even
            // occurring numbers
            echo $arr[$i], " ";

            // set bit as 1 to avoid
            // printing duplicates
            $_xor ^= $pos;
        }
    }
}

// Driver code
$arr = array(9, 12, 23, 10, 12, 12,
             15, 23, 14, 12, 15 );
$n = sizeof($arr);

printRepeatingEven($arr, $n);

// This code is contributed by aj_36
?>
```

## 蟒蛇 3

```
# Python 3 program to find the even
# occurring elements in given array

# Function to find the even occurring
# elements in given array
def printRepeatingEven(arr, n):

    axor = 0;

    # do for each element of array
    for i in range(0, n):

        # left-shift 1 by value of
        # current element
        pos = 1 << arr[i];

        # Toggle the bit every time
        # element gets repeated
        axor ^= pos;

    # Traverse array again and use _xor
    # to find even occurring elements
    for i in range(0, n - 1):

        # left-shift 1 by value of
        # current element
        pos = 1 << arr[i];

        # Each 0 in _xor represents an
        # even occurrence
        if (not(pos & axor)):

            # print the even occurring numbers
            print(arr[i], end = " ");

            # set bit as 1 to avoid printing
            # duplicates
            axor ^= pos;

# Driver code
arr = [9, 12, 23, 10, 12, 12,
          15, 23, 14, 12, 15 ];
n = len(arr) ;
printRepeatingEven(arr, n);

# This code is contributed
# by Shivi_Aggarwal
```

## java 描述语言

```
<script>

// Javascript Program to find the even occurring
// elements in given array

// Function to find the even occurring
// elements in given array
function printRepeatingEven(arr, n)
{
    let _xor = 0;
    let pos;

    // do for each element of array
    for (let i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Toggle the bit everytime
        // element gets repeated
        _xor ^= pos;
    }

    // Traverse array again and use _xor
    // to find even occurring elements
    for (let i = 0; i < n; ++i)
    {
        // left-shift 1 by value of
        // current element
        pos = 1 << arr[i];

        // Each 0 in _xor represents
        // an even occurrence
        if (!((pos & _xor)!=0))
        {
            // print the even occurring numbers
            document.write(arr[i] + " ");

            // set bit as 1 to avoid
            // printing duplicates
            _xor ^= pos;
        }
    }
}

// Driver Code

        let arr = [9, 12, 23, 10, 12, 12,
                 15, 23, 14, 12, 15];
        let n = arr.length;

        printRepeatingEven(arr, n);

</script>
```

**输出:**

```
12 23 15
```

***时间复杂度:** O(n)*

***辅助空间:** O(1)*

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息