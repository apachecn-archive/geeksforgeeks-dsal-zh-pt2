# 二进制数组中最大连续 1(或 0)

> 原文:[https://www . geesforgeks . org/二进制数组中最大连续 1 或 0 数/](https://www.geeksforgeeks.org/maximum-consecutive-ones-or-zeros-in-a-binary-array/)

给定二进制数组，找出数组中出现的最大连续 1 个数。
**例:**

```
Input  : arr[] = {1, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 1}
Output : 4

Input  : arr[] = {0, 0, 1, 0, 1, 0, 1, 0, 1, 0, 1}
Output : 1
```

一个简单的解决方案是考虑每个子阵列，并在每个子阵列中计数 1。最后返回所有 1 的最大子阵列的返回大小。
一个**高效的解决方案**是从左到右遍历数组。如果我们看到一个 1，我们增加计数，并将其与最大值进行比较。如果我们看到一个 0，我们重置计数为 0。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to count maximum consecutive
// 1's in a binary array.
#include<bits/stdc++.h>
using namespace std;

// Returns count of maximum consecutive 1's
// in binary array arr[0..n-1]
int getMaxLength(bool arr[], int n)
{
    int count = 0; //initialize count
    int result = 0; //initialize max

    for (int i = 0; i < n; i++)
    {
        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;

        // If 1 is found, increment count
        // and update result if count becomes
        // more.
        else
        {
            count++;//increase count
            result = max(result, count);
        }
    }

    return result;
}

// Driver code
int main()
{
    bool arr[] = {1, 1, 0, 0, 1, 0, 1, 0,
                  1, 1, 1, 1};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << getMaxLength(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count maximum consecutive
// 1's in a binary array.
class GFG {

    // Returns count of maximum consecutive 1's
    // in binary array arr[0..n-1]
    static int getMaxLength(boolean arr[], int n)
    {

        int count = 0; //initialize count
        int result = 0; //initialize max

        for (int i = 0; i < n; i++)
        {

            // Reset count when 0 is found
            if (arr[i] == false)
                count = 0;

            // If 1 is found, increment count
            // and update result if count becomes
            // more.
            else
            {
                count++;//increase count
                result = Math.max(result, count);
            }
        }

        return result;
    }

    // Driver method
    public static void main(String[] args)
    {
        boolean arr[] = {true, true, false, false,
                         true, false, true, false,
                           true, true, true, true};

        int n = arr.length;

        System.out.println(getMaxLength(arr, n));
    }
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python 3 program to count
# maximum consecutive 1's
# in a binary array.

# Returns count of maximum
# consecutive 1's in binary
# array arr[0..n-1]
def getMaxLength(arr, n):

    # initialize count
    count = 0

    # initialize max
    result = 0

    for i in range(0, n):

        # Reset count when 0 is found
        if (arr[i] == 0):
            count = 0

        # If 1 is found, increment count
        # and update result if count
        # becomes more.
        else:

            # increase count
            count+= 1
            result = max(result, count)

    return result

# Driver code
arr = [1, 1, 0, 0, 1, 0, 1,
             0, 1, 1, 1, 1]
n = len(arr)

print(getMaxLength(arr, n))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to count maximum
// consecutive 1's in a binary array.
using System;

class GFG {

    // Returns count of maximum consecutive
    // 1's in binary array arr[0..n-1]
    static int getMaxLength(bool []arr, int n)
    {

        int count = 0; //initialize count
        int result = 0; //initialize max

        for (int i = 0; i < n; i++)
        {

            // Reset count when 0 is found
            if (arr[i] == false)
                count = 0;

            // If 1 is found, increment count
            // and update result if count
            // becomes more.
            else
            {
                count++; //increase count
                result = Math.Max(result, count);
            }
        }

        return result;
    }

    // Driver code
    public static void Main()
    {
        bool []arr = {true, true, false, false,
                      true, false, true, false,
                      true, true, true, true};

        int n = arr.Length;

        Console.Write(getMaxLength(arr, n));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count maximum
// consecutive 1's in a binary array.

// Returns count of maximum
// consecutive 1's in binary
// array arr[0..n-1]
function getMaxLength($arr, $n)
{
    // initialize count
    $count = 0;

    // initialize max
    $result = 0;

    for ($i = 0; $i < $n; $i++)
    {
        // Reset count when 0 is found
        if ($arr[$i] == 0)
            $count = 0;

        // If 1 is found, increment
        // count and update result
        // if count becomes more.
        else
        {
            // increase count
            $count++;
            $result = max($result, $count);
        }
    }

    return $result;
}

// Driver code
$arr = array(1, 1, 0, 0, 1, 0,
             1, 0, 1, 1, 1, 1);
$n = sizeof($arr) / sizeof($arr[0]);
echo getMaxLength($arr, $n) ;

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to count maximum
// consecutive 1's in a binary array.

// Returns count of maximum
// consecutive 1's in binary
// array arr[0..n-1]
function getMaxLength(arr, n) {
    // initialize count
    let count = 0;

    // initialize max
    let result = 0;

    for (let i = 0; i < n; i++) {
        // Reset count when 0 is found
        if (arr[i] == 0)
            count = 0;

        // If 1 is found, increment
        // count and update result
        // if count becomes more.
        else {
            // increase count
            count++;
            result = Math.max(result, count);
        }
    }

    return result;
}

// Driver code
let arr = new Array(1, 1, 0, 0, 1, 0,
    1, 0, 1, 1, 1, 1);
let n = arr.length;
document.write(getMaxLength(arr, n));

// This code is contributed by gfgking

</script>
```

**输出:**

```
4
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)
**练习:**
二进制数组中最大连续零。
本文由 **Smarak Chopdar** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如发现有不正确的地方，或想分享更多以上讨论话题的信息，请写评论”。