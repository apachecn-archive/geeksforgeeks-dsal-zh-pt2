# 从二进制数组中的每个索引开始的最长交替子数组

> 原文:[https://www . geeksforgeeks . org/最长-交替-子数组-开始-每个索引-二进制-数组/](https://www.geeksforgeeks.org/longest-alternating-sub-array-starting-every-index-binary-array/)

给定一个只包含 0 和 1 的数组。对于每个索引“**I**”(0 索引)，找出从“ **i** ”到“ **j** 的最长交替子阵列的长度，即 **a <sub>i..j</sub>** 为 **i < = j < n** 。交替子阵列意味着任何两个相邻的元素应该不同。

**示例:**

```
Input: arr[] = {1, 0, 1, 0, 0, 1}
Output: 4 3 2 1 2 1 
Explanation
Length for index '0': {1 0 1 0} => 4
Length for index '1': {0 1 0}   => 3
Length for index '2': {1 0}     => 2
Length for index '3': {0}       => 1
Length for index '4': {0 1}     => 2
Length for index '5': {1}       => 1
```

**简单的方法**是通过使用两个“for 循环”来寻找每个索引的长度，从而对每个索引进行迭代。外部循环选择一个起点“I”，内部循环考虑从“I”开始的所有子数组。这种方法的时间复杂度为 0(n<sup>2</sup>，这对于大的“n”值是不够的。

**更好的方法**是使用**动态编程**。首先，让我们看看如何检查交替子阵列。为了检查两个元素是否交替，我们可以简单地对它们进行异或运算，然后与“0”和“1”进行比较。

*   如果异或为“0”，这意味着两个数字不是交替的(相等的元素)。
*   如果异或为“1”，这意味着两者是交替的(不同的元素)

Let len[i]表示从位置“I”开始的交替子阵列的长度。如果 arr[i]和 arr[i+1]具有不同的值，那么 len[i]将比 len[i+1]多一个。否则，如果它们是相同的元素，len[i]将仅为 1。

下面是上述方法的实现:

## C++

```
// C++ program to calculate longest alternating
// sub-array for each index elements
#include <bits/stdc++.h>
using namespace std;

// Function to calculate alternating sub-
// array for each index of array elements
void alternateSubarray(bool arr[], int n)
{
    int len[n];

    // Initialize the base state of len[]
    len[n - 1] = 1;

    // Calculating value for each element
    for (int i = n - 2; i >= 0; --i) {
        // If both elements are different
        // then add 1 to next len[i+1]
        if (arr[i] ^ arr[i + 1] == 1)
            len[i] = len[i + 1] + 1;

        // else initialize to 1
        else
            len[i] = 1;
    }

    // Print lengths of binary subarrays.
    for (int i = 0; i < n; ++i)
        cout << len[i] << " ";
}

// Driver program
int main()
{
    bool arr[] = { 1, 0, 1, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    alternateSubarray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate longest alternating
// sub-array for each index elements

class GFG {

// Function to calculate alternating sub-
// array for each index of array elements
static void alternateSubarray(boolean arr[], int n)
{
    int len[] = new int[n];

    // Initialize the base state of len[]
    len[n - 1] = 1;

    // Calculating value for each element
    for (int i = n - 2; i >= 0; --i) {

    // If both elements are different
    // then add 1 to next len[i+1]
    if (arr[i] ^ arr[i + 1] == true)
        len[i] = len[i + 1] + 1;

    // else initialize to 1
    else
        len[i] = 1;
    }

    // Print lengths of binary subarrays.
    for (int i = 0; i < n; ++i)
    System.out.print(len[i] + " ");
}

// Driver code
public static void main(String[] args)
{
    boolean arr[] = {true, false, true, false, false, true};
    int n = arr.length;
    alternateSubarray(arr, n);
}
}

// This code is contributed by Anant Agarwal.
```

## 蟒蛇 3

```
# Python program to calculate
# longest alternating
# sub-array for each index elements

# Function to calculate alternating sub-
# array for each index of array elements
def alternateSubarray(arr,n):

    len=[]
    for i in range(n+1):
        len.append(0)

    # Initialize the base state of len[]
    len[n - 1] = 1

    # Calculating value for each element
    for i in range(n - 2,-1,-1):

        # If both elements are different
        # then add 1 to next len[i+1]
        if (arr[i] ^ arr[i + 1] == True):
            len[i] = len[i + 1] + 1

        # else initialize to 1
        else:
            len[i] = 1

    # Print lengths of binary subarrays.
    for i in range(n):
        print(len[i] , " ",end="")

# Driver code

arr = [ True,False, True, False, False, True ]
n = len(arr)

alternateSubarray(arr, n)

# This code is contributed
# by Anant Agarwal.
```

## C#

```
// C# program to calculate longest
// alternating sub-array for each
// index elements
using System;

class GFG {

    // Function to calculate alternating sub-
    // array for each index of array elements
    static void alternateSubarray(bool []arr,
                                        int n)
    {

        int []len = new int[n];

        // Initialize the base state of len[]
        len[n - 1] = 1;

        // Calculating value for each element
        for (int i = n - 2; i >= 0; --i)
        {

            // If both elements are different
            // then add 1 to next len[i+1]
            if (arr[i] ^ arr[i + 1] == true)
                len[i] = len[i + 1] + 1;

            // else initialize to 1
            else
                len[i] = 1;
        }

        // Print lengths of binary subarrays.
        for (int i = 0; i < n; ++i)
            Console.Write(len[i] + " ");
    }

    // Driver code
    public static void Main()
    {
        bool []arr = {true, false, true,
                         false, false, true};
        int n = arr.Length;

        alternateSubarray(arr, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate longest alternating
// sub-array for each index elements

// Function to calculate alternating sub-
// array for each index of array elements
function alternateSubarray(&$arr, $n)
{
    $len = array_fill(0, $n, NULL);

    // Initialize the base state of len[]
    $len[$n - 1] = 1;

    // Calculating value for each element
    for ($i = $n - 2; $i >= 0; --$i)
    {
        // If both elements are different
        // then add 1 to next len[i+1]
        if ($arr[$i] ^ $arr[$i + 1] == 1)
            $len[$i] = $len[$i + 1] + 1;

        // else initialize to 1
        else
            $len[$i] = 1;
    }

    // Print lengths of binary subarrays.
    for ($i = 0; $i < $n; ++$i)
        echo $len[$i] . " ";
}

// Driver Code
$arr = array(1, 0, 1, 0, 0, 1);
$n = sizeof($arr);
alternateSubarray($arr, $n);

// This code is contributed by ita_c
?>
```

## java 描述语言

```
<script>
// JavaScript program to calculate longest alternating
// sub-array for each index elements

// Function to calculate alternating sub-
// array for each index of array elements
function alternateSubarray(arr, n)
{
    let len = new Array(n);

    // Initialize the base state of len[]
    len[n - 1] = 1;

    // Calculating value for each element
    for (let i = n - 2; i >= 0; --i)
    {

        // If both elements are different
        // then add 1 to next len[i+1]
        if (arr[i] ^ arr[i + 1] == 1)
            len[i] = len[i + 1] + 1;

        // else initialize to 1
        else
            len[i] = 1;
    }

    // Prlet lengths of binary subarrays.
    for (let i = 0; i < n; ++i)
        document.write(len[i] + " ");
}

// Driver program
    let arr = [ 1, 0, 1, 0, 0, 1 ];
    let n = arr.length;
    alternateSubarray(arr, n);

// This code is contributed by Surbhi Tyagi.
</script>
```

**输出:**

```
4 3 2 1 2 1
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)

另一种**高效的方法**是，我们可以直接打印出来，直到发现不匹配(相邻元素相等)，而不是把所有的子阵列元素都存储在 len[]数组中。当发现不匹配时，我们打印从当前值到 0 的计数。

## C++

```
// C++ program to calculate longest alternating
// sub-array for each index elements
#include <bits/stdc++.h>
using namespace std;

// Function to calculate alternating sub-array
// for each index of array elements
void alternateSubarray(bool arr[], int n)
{
    // Initialize count variable for storing
    // length of sub-array
    int count = 1;

    // Initialize 'prev' variable which
    // indicates the previous element
    // while traversing for index 'i'
    int prev = arr[0];
    for (int i = 1; i < n; ++i) {

        // If both elements are same
        // print elements because alternate
        // element is not found for current
        // index
        if ((arr[i] ^ prev) == 0)
        {
            // print count and decrement it.
            while (count)
                cout << count-- << " ";
        }

        // Increment count for next element
        ++count;

        // Re-initialize previous variable
        prev = arr[i];
    }

    // If elements are still available after
    // traversing whole array, print it
    while (count)
        cout << count-- << " ";
}

// Driver program
int main()
{
    bool arr[] = { 1, 0, 1, 0, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    alternateSubarray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to calculate longest alternating
// sub-array for each index elements
class GFG {

// Function to calculate alternating sub-array
// for each index of array elements
    static void alternateSubarray(boolean arr[], int n) {
        // Initialize count variable for storing
        // length of sub-array
        int count = 1;

        // Initialize 'prev' variable which
        // indicates the previous element
        // while traversing for index 'i'
        boolean prev = arr[0];
        for (int i = 1; i < n; ++i) {

            // If both elements are same
            // print elements because alternate
            // element is not found for current
            // index
            if ((arr[i] ^ prev) == false) {
                // print count and decrement it.
                while (count > 0) {
                    System.out.print(count-- + " ");
                }
            }

            // Increment count for next element
            ++count;

            // Re-initialize previous variable
            prev = arr[i];
        }

        // If elements are still available after
        // traversing whole array, print it
        while (count != 0) {
            System.out.print(count-- + " ");
        }
    }

// Driver program
    public static void main(String args[]) {
        boolean arr[] = {true, false, true, false, false, true};
        int n = arr.length;
        alternateSubarray(arr, n);
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 蟒蛇 3

```
# Python 3 program to calculate longest
# alternating sub-array for each index elements

# Function to calculate alternating sub-array
# for each index of array elements
def alternateSubarray(arr, n):

    # Initialize count variable for
    # storing length of sub-array
    count = 1

    # Initialize 'prev' variable which
    # indicates the previous element
    # while traversing for index 'i'
    prev = arr[0]
    for i in range(1, n):

        # If both elements are same, print
        # elements because alternate element
        # is not found for current index
        if ((arr[i] ^ prev) == 0):

            # print count and decrement it.
            while (count):
                print(count, end = " ")
                count -= 1

        # Increment count for next element
        count += 1

        # Re-initialize previous variable
        prev = arr[i]

    # If elements are still available after
    # traversing whole array, print it
    while (count):
        print(count, end = " ")
        count -= 1

# Driver Code
if __name__ == '__main__':
    arr = [1, 0, 1, 0, 0, 1]
    n = len(arr)
    alternateSubarray(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to calculate longest alternating
// sub-array for each index elements
using System;

public class Test{

// Function to calculate alternating sub-array
// for each index of array elements
    static void alternateSubarray(bool []arr, int n) {
        // Initialize count variable for storing
        // length of sub-array
        int count = 1;

        // Initialize 'prev' variable which
        // indicates the previous element
        // while traversing for index 'i'
        bool prev = arr[0];
        for (int i = 1; i < n; ++i) {

            // If both elements are same
            // print elements because alternate
            // element is not found for current
            // index
            if ((arr[i] ^ prev) == false) {
                // print count and decrement it.
                while (count > 0) {
                    Console.Write(count-- + " ");
                }
            }

            // Increment count for next element
            ++count;

            // Re-initialize previous variable
            prev = arr[i];
        }

        // If elements are still available after
        // traversing whole array, print it
        while (count != 0) {
            Console.Write(count-- + " ");
        }
    }

// Driver program
    public static void Main() {
        bool []arr = {true, false, true, false, false, true};
        int n = arr.Length;
        alternateSubarray(arr, n);
    }
}
/*This code is contributed by 29AjayKumar*/
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to calculate longest alternating
// sub-array for each index elements

// Function to calculate alternating sub-array
// for each index of array elements
function alternateSubarray($arr, $n)
{

    // Initialize count variable for storing
    // length of sub-array
    $count = 1;

    // Initialize 'prev' variable which
    // indicates the previous element
    // while traversing for index 'i'
    $prev = $arr[0];
    for ($i = 1; $i < $n; ++$i)
    {

        // If both elements are same
        // print elements because alternate
        // element is not found for current
        // index
        if (($arr[$i] ^ $prev) == 0)
        {
            // print count and decrement it.
            while ($count)
                echo $count-- , " ";
        }

        // Increment count for next element
        ++$count;

        // Re-initialize previous variable
        $prev = $arr[$i];
    }

    // If elements are still available after
    // traversing whole array, print it
    while ($count)
        echo $count-- , " ";
}

    // Driver Code
    $arr = array(1, 0, 1, 0, 0, 1);
    $n = sizeof($arr) ;
    alternateSubarray($arr, $n);

// This code is contributed by jit_t.
?>
```

## java 描述语言

```
<script>

// Javascript program to calculate longest
// alternating sub-array for each index elements

// Function to calculate alternating sub-array
// for each index of array elements
function alternateSubarray(arr, n)
{

    // Initialize count variable for storing
    // length of sub-array
    let count = 1;

    // Initialize 'prev' variable which
    // indicates the previous element
    // while traversing for index 'i'
    let prev = arr[0];

    for(let i = 1; i < n; ++i)
    {

        // If both elements are same
        // print elements because alternate
        // element is not found for current
        // index
        if ((arr[i] ^ prev) == false)
        {

            // Print count and decrement it.
            while (count > 0)
            {
                document.write(count-- + " ");
            }
        }

        // Increment count for next element
        ++count;

        // Re-initialize previous variable
        prev = arr[i];
    }

    // If elements are still available after
    // traversing whole array, print it
    while (count != 0)
    {
        document.write(count-- + " ");
    }
}

// Driver code
let arr = [ true, false, true, false, false, true ];
let n = arr.length;

alternateSubarray(arr, n);

// This code is contributed by suresh07

</script>
```

**输出:**

```
4 3 2 1 2 1
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。