# 数组中最长的正整数序列

> 原文:[https://www . geesforgeks . org/最长序列-正整数-数组/](https://www.geeksforgeeks.org/longest-sequence-positive-integers-array/)

找出数组中运行时间最长的正序列。
示例:

```
Input : arr[] = {1, 2, -3, 2, 3, 4, -6, 1, 
                     2, 3, 4, 5, -8, 5, 6}
Output :Index : 7, length : 5

Input : arr[] = {-3, -6, -1, -3, -8}
Output : No positive sequence detected.
```

一个**简单的解决方案**是使用两个嵌套循环。在外环中，我们寻找正元素。在内部循环中，我们从外部循环选取的正元素开始计算正元素的数量。这个解决方案的时间复杂度是 O(n^2).
一个**高效的解决方案**是使用一个单循环。当我们看到正整数时，我们不断增加计数。看到负数后，我们将计数重置为 0。重置前，我们检查计数是否超过最大值。

## C++

```
// CPP program to find longest running sequence
// of positive integers.
#include <bits/stdc++.h>
using namespace std;

// Prints longest sequence of positive integers in
// an array.
void getLongestSeq(int a[], int n)
{
    // Variables to keep track of maximum length and
    // starting point of maximum length. And same
    // for current length.
    int maxIdx = 0, maxLen = 0, currLen = 0, currIdx = 0;

    for (int k = 0; k < n; k++) {
        if (a[k] > 0) {
            currLen++;

            // New sequence, store
            // beginning index.
            if (currLen == 1)
                currIdx = k;           
        }
        else {
            if (currLen > maxLen) {
                maxLen = currLen;
                maxIdx = currIdx;
            }
            currLen  = 0;
        }
    }

    if (maxLen > 0)
        cout << "Length " << maxLen
             << ", starting index " << maxIdx << endl;   
    else
        cout << "No positive sequence detected." << endl;

    return;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, -3, 2, 3, 4, -6,
               1, 2, 3, 4, 5, -8, 5, 6 };
    int n = sizeof(arr) / sizeof(int);
    getLongestSeq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find longest running
// sequence of positive integers
import java.io.*;

class GFG {

    // Prints longest sequence of
    // positive integers in an array.
    static void getLongestSeq(int a[], int n)
    {
        // Variables to keep track of maximum
        // length and  starting point of
        // maximum length. And same for current
        // length.
        int maxIdx = 0, maxLen = 0, currLen = 0, currIdx = 0;

        for (int k = 0; k < n; k++)
        {
            if (a[k] > 0)
            {
                currLen++;

                // New sequence, store
                // beginning index.
                if (currLen == 1)
                    currIdx = k;        
            }
            else
            {
                if (currLen > maxLen)
                {
                    maxLen = currLen;
                    maxIdx = currIdx;
                }
                currLen = 0;
            }
        }

        if (maxLen > 0)
        {
            System.out.print( "Length " + maxLen) ;
            System.out.print( ",starting index " + maxIdx );
        }
        else
            System.out.println("No positive sequence detected.") ;

        return;
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[] = { 1, 2, -3, 2, 3, 4, -6,
                      1, 2, 3, 4, 5, -8, 5, 6 };
        int n = arr.length;
        getLongestSeq(arr, n);

    }
}

// This article is contributed by vt_m.
```

## 蟒蛇 3

```
# Python code to find longest running
# sequence of positive integers.

def getLongestSeq(a, n):
    maxIdx = 0
    maxLen = 0
    currLen = 0
    currIdx = 0
    for k in range(n):
        if a[k] > 0:
            currLen +=1

            # New sequence, store
            # beginning index.
            if currLen == 1:
                currIdx = k
        else:
            if currLen > maxLen:
                maxLen = currLen
                maxIdx = currIdx
            currLen = 0

    if maxLen > 0:
        print('Index : ',maxIdx,',Length : ',maxLen,)
    else:
        print("No positive sequence detected.")

# Driver code
arr = [ 1, 2, -3, 2, 3, 4, -6,
        1, 2, 3, 4, 5, -8, 5, 6]
n = len(arr)
getLongestSeq(arr, n)

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find longest running
// sequence of positive integers.
using System;

class GFG {

    // Prints longest sequence of
    // positive integers in an array.
    static void getLongestSeq(int []a, int n)
    {

        // Variables to keep track of maximum
        // length and starting point of
        // maximum length. And same for current
        // length.
        int maxIdx = 0, maxLen = 0, currLen = 0,
            currIdx = 0;

        for (int k = 0; k < n; k++)
        {
            if (a[k] > 0)
            {
                currLen++;

                // New sequence, store
                // beginning index.
                if (currLen == 1)
                    currIdx = k;        
            }
            else
            {
                if (currLen > maxLen)
                {
                    maxLen = currLen;
                    maxIdx = currIdx;
                }
                currLen = 0;
            }
        }

        if (maxLen > 0)
        {
            Console.Write( "Length " + maxLen) ;
            Console.WriteLine( ",starting index "
                                      + maxIdx );
        }
        else
            Console.WriteLine("No positive sequence"
                                   + " detected.") ;

        return;
    }

    // driver code
    public static void Main()
    {
        int []arr = { 1, 2, -3, 2, 3, 4, -6,
                    1, 2, 3, 4, 5, -8, 5, 6 };
        int n = arr.Length;
        getLongestSeq(arr, n);

    }

}
// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find longest running
// sequence of positive integers.

// Prints longest sequence of positive
// integers in an array.
function getLongestSeq($a, $n)
{

    // Variables to keep track
    // of maximum length and
    // starting point of maximum
    // length. And same for
    // current length.
    $maxIdx = 0;
    $maxLen = 0;
    $currLen = 0;
    $currIdx = 0;

    for ($k = 0; $k < $n; $k++) {
        if ($a[$k] > 0) {
            $currLen++;

            // New sequence, store
            // beginning index.
            if ($currLen == 1)
                $currIdx = $k;        
        }
        else {
            if ($currLen > $maxLen) {
                $maxLen = $currLen;
                $maxIdx = $currIdx;
            }
            $currLen = 0;
        }
    }

    if ($maxLen > 0)
        echo "Length " . $maxLen.
             ", starting index " .
             $maxIdx ."\n" ;
    else
        echo "No positive sequence detected."."\n";

    return;
}

    // Driver Code
    $arr = array(1, 2, -3, 2, 3, 4, -6,
                 1, 2, 3, 4, 5, -8, 5, 6);
    $n = count($arr);
    getLongestSeq($arr, $n);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>
    // Javascript program to find longest running
    // sequence of positive integers.

    // Prints longest sequence of
    // positive integers in an array.
    function getLongestSeq(a, n)
    {

        // Variables to keep track of maximum
        // length and starting point of
        // maximum length. And same for current
        // length.
        let maxIdx = 0, maxLen = 0, currLen = 0, currIdx = 0;

        for (let k = 0; k < n; k++)
        {
            if (a[k] > 0)
            {
                currLen++;

                // New sequence, store
                // beginning index.
                if (currLen == 1)
                    currIdx = k;        
            }
            else
            {
                if (currLen > maxLen)
                {
                    maxLen = currLen;
                    maxIdx = currIdx;
                }
                currLen = 0;
            }
        }

        if (maxLen > 0)
        {
            document.write( "Length " + maxLen) ;
            document.write( ", starting index "
                                      + maxIdx + "</br>");
        }
        else
            document.write("No positive sequence"
                                   + " detected.") ;

        return;
    }

    let arr = [ 1, 2, -3, 2, 3, 4, -6,
                    1, 2, 3, 4, 5, -8, 5, 6 ];
    let n = arr.length;
    getLongestSeq(arr, n);

</script>
```

输出:

```
Length 5, starting index 7
```

算法是 O(n)时间和 O(1)辅助空间。