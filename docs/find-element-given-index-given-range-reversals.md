# 在给定范围反转后，在给定索引处查找元素

> 原文:[https://www . geesforgeks . org/find-element-给定-index-给定-range-reverses/](https://www.geeksforgeeks.org/find-element-given-index-given-range-reversals/)

给出了一个由 N 个元素组成的数组。我们在独特的范围内做了几次反转..R]。任务是打印给定索引处的元素。
**例:**

```
Input : 
arr[] : 10 20 30 40 50
ranges[] = {{1, 4}, {0, 2}}
Query Index = 1
Output : 50
Explanation : 
Reverse range[1..4] : 10 50 40 30 20
Reverse range[0..2] : 40 50 10 30 20
So we have 50 at index 1
```

**蛮力**方法实际上是反转一系列元素，然后回答查询。
**高效方法:**如果我们观察，范围的逆转【L..R]的结果如下:
索引将变为**右+左–索引**。
通过这样做，我们可以很容易地计算出指数。

## C++

```
// Program to find index of an element after
// given range reversals.
#include <bits/stdc++.h>
using namespace std;

// Function to compute the element at query index
int answer(int arr[], int ranges[][2], int reversals,
           int index)
{
    for (int i = reversals - 1; i >= 0; i--) {
        // Range[left...right]
        int left = ranges[i][0], right = ranges[i][1];

        // If doesn't satisfy, reversal won't
        // have any effect
        if (left <= index && right >= index)
            index = right + left - index;
    }

    // Returning element at modified index
    return arr[index];
}

// Driver
int main()
{
    int arr[] = { 10, 20, 30, 40, 50 };

    // reversals
    int reversals = 2;
    int ranges[reversals][2] = { { 1, 4 }, { 0, 2 } };

    int index = 1;
    cout << answer(arr, ranges, reversals, index);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Program to find index of an element
// after given range reversals.
import java.util.Arrays;

class GFG {
    // Function to compute the element at
    // query index
    static int answer(int[] arr, int[][] ranges,
                      int reversals, int index)
    {
        for (int i = reversals - 1; i >= 0; i--) {
            // Range[left...right]
            int left = ranges[i][0],
                right = ranges[i][1];

            // If doesn't satisfy, reversal
            // won't have any effect
            if (left <= index && right >= index)
                index = right + left - index;
        }

        // Returning element at modified index
        return arr[index];
    }

    // Driver code
    public static void main(String[] args)
    {

        int[] arr = { 10, 20, 30, 40, 50 };

        // reversals
        int reversals = 2;
        int[][] ranges = { { 1, 4 }, { 0, 2 } };

        int index = 1;
        System.out.println(answer(arr, ranges,
                                  reversals, index));
    }
}

/* This code is contributed by Mr. Somesh Awasthi */
```

## 蟒蛇 3

```
# Program to find index of an element
# after given range reversals.

# Function to compute the element
# at query index
def answer(arr, ranges, reversals, index):
    i = reversals - 1
    while(i >= 0):

        # Range[left...right]
        left = ranges[i][0]
        right = ranges[i][1]

        # If doesn't satisfy, reversal won't
        # have any effect
        if (left <= index and right >= index):
            index = right + left - index

        i -= 1

    # Returning element at modified index
    return arr[index]

# Driver Code
if __name__ == '__main__':
    arr = [10, 20, 30, 40, 50]

    # reversals
    reversals = 2
    ranges = [ [ 1, 4 ], [ 0, 2 ] ]

    index = 1
    print(answer(arr, ranges,
                 reversals, index))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find index of an element
// after given range reversals.
using System;

class GFG {

    // Function to compute the element at
    // query index
    static int answer(int[] arr, int[, ] ranges,
                       int reversals, int index)
    {
        for (int i = reversals - 1; i >= 0; i--)
        {

            // Range[left...right]
            int left = ranges[i, 0],
                right = ranges[i, 1];

            // If doesn't satisfy, reversal
            // won't have any effect
            if (left <= index && right >= index)
                index = right + left - index;
        }

        // Returning element at modified index
        return arr[index];
    }

    // Driver code
    public static void Main()
    {

        int[] arr = { 10, 20, 30, 40, 50 };

        // reversals
        int reversals = 2;
        int[, ] ranges = { { 1, 4 }, { 0, 2 } };

        int index = 1;
        Console.WriteLine(answer(arr, ranges,
                                reversals, index));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Program to find index
// of an element after
// given range reversals.

// Function to compute the
// element at query index
function answer($arr, $ranges,
                $reversals, $index)
{
    for ($i = $reversals - 1;
              $i >= 0; $i--)
    {
        // Range[left...right]
        $left = $ranges[$i][0];
        $right = $ranges[$i][1];

        // If doesn't satisfy,
        // reversal won't have
        // any effect
        if ($left <= $index &&
            $right >= $index)
            $index = $right + $left -
                              $index;
    }

    // Returning element
    // at modified index
    return $arr[$index];
}

// Driver Code
$arr = array( 10, 20, 30, 40, 50 );

// reversals
$reversals = 2;
$ranges = array(array( 1, 4 ),
                array( 0, 2 ));

$index = 1;
echo answer($arr, $ranges,
            $reversals, $index);

// This code is contributed
// by nitin mittal.
?>
```

## java 描述语言

```
<script>

    // Program to find index of an element
    // after given range reversals.

    // Function to compute the element at
    // query index
    function answer(arr, ranges, reversals, index)
    {
        for (let i = reversals - 1; i >= 0; i--) {
            // Range[left...right]
            let left = ranges[i][0],
                right = ranges[i][1];

            // If doesn't satisfy, reversal
            // won't have any effect
            if (left <= index && right >= index)
                index = right + left - index;
        }

        // Returning element at modified index
        return arr[index];
    }

    let arr = [ 10, 20, 30, 40, 50 ];

    // reversals
    let reversals = 2;
    let ranges = [ [ 1, 4 ], [ 0, 2 ] ];

    let index = 1;
    document.write(answer(arr, ranges, reversals, index));

</script>
```

**输出:**

```
50
```

本文由 [**罗希特·塔普利亚尔**](https://www.hackerrank.com/rohit_thapliyal) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。