# 字典上最小的旋转序列|集合 2

> 原文:[https://www . geeksforgeeks . org/词典-最小-旋转-序列-set-2/](https://www.geeksforgeeks.org/lexicographically-smallest-rotated-sequence-set-2/)

编写代码以在圆形数组中查找字典顺序最小值，例如，对于 BCABDADAB 数组，字典顺序最小值是 abbbcabdad
输入约束:1<n<1000
T2】示例:T4】

```
Input:  GEEKSQUIZ
Output: EEKSQUIZG

Input:  GFG
Output: FGG

Input :  CAPABCQ
Output : ABCQCAP
```

我们已经在[词典最小字符串旋转|集合 1](https://www.geeksforgeeks.org/lexicographically-minimum-string-rotation/) 中讨论了 O(n <sup>2</sup> Logn)解。这里我们需要找到最小旋转的起始索引，然后打印旋转。

```
1) Initially assume 0 to be current min 
   starting index.
2) Loop through i = 1 to n-1.
   a) For each i compare sequence starting 
      at i with current min starting index
   b) If sequence starting at i is lexicographically 
      smaller, update current min starting 
      index.
```

这里是算法
的伪代码

```
function findIndexForSmallestSequence(S, n):
    result = 0
    for i = 1:n-1
        if (sequence beginning at i < 
               sequence beginning at result)
            result = i
        end if
    end for
    return result
```

下面是上述算法的实现。

## C++

```
// C++ program to find lexicographically
// smallest sequence with rotations.
#include <iostream>
using namespace std;

// Function to compare lexicographically
// two sequence with different starting
// indexes. It returns true if sequence
// beginning with y is lexicographically
// greater.
bool compareSeq(char S[], int x, int y, int n)
{
    for (int i = 0; i < n; i++) {
        if (S[x] < S[y])
            return false;
        else if (S[x] > S[y])
            return true;
        x = (x + 1) % n;
        y = (y + 1) % n;
    }
    return true;
}

// Function to find starting index
// of lexicographically smallest sequence
int smallestSequence(char S[], int n)
{
    int index = 0;
    for (int i = 1; i < n; i++)

        // if new sequence is smaller
        if (compareSeq(S, index, i, n))

            // change index of current min
            index = i;

    return index;
}

// Function to print lexicographically
// smallest sequence
void printSmallestSequence(char S[], int n)
{
    int starting_index = smallestSequence(S, n);
    for (int i = 0; i < n; i++)
        cout << S[(starting_index + i) % n];
}

// driver code
int main()
{
    char S[] = "DCACBCAA";
    int n = 8;
    printSmallestSequence(S, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographically
// smallest sequence with rotations.
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class */
class LexoSmallest {
    // Function to compare lexicographically
    // two sequence with different starting
    // indexes. It returns true if sequence
    // beginning with y is lexicographically
    // greater.
    static boolean compareSeq(char[] S, int x, int y, int n)
    {
        for (int i = 0; i < n; i++) {
            if (S[x] < S[y])
                return false;
            else if (S[x] > S[y])
                return true;
            x = (x + 1) % n;
            y = (y + 1) % n;
        }
        return true;
    }

    // Function to find starting index
    // of lexicographically smallest sequence
    static int smallestSequence(char[] S, int n)
    {
        int index = 0;
        for (int i = 1; i < n; i++)

            // if new sequence is smaller
            if (compareSeq(S, index, i, n))

                // change index of current min
                index = i;

        return index;
    }

    // Function to print lexicographically
    // smallest sequence
    static void printSmallestSequence(String str, int n)
    {
        char[] S = str.toCharArray();
        int starting_index = smallestSequence(S, n);
        for (int i = 0; i < n; i++)
            System.out.print(S[(starting_index + i) % n]);
    }

    // driver code
    public static void main(String[] args)
    {
        String S = "DCACBCAA";
        int n = 8;
        printSmallestSequence(S, n);
    }
}
// This code is contributed by Mr Somesh Awasthi
```

## 蟒蛇 3

```
# Python 3 program to find lexicographically
# smallest sequence with rotations.

# Function to compare lexicographically
# two sequence with different starting
# indexes. It returns true if sequence
# beginning with y is lexicographically
# greater.
import copy

def printSmallestSequence(s):
    m = copy.copy(s)
    for i in range(len(s) - 1):

        if m > s[i:] + s[:i]:
            m = s[i:] + s[:i]

    return m

#Driver Code
if __name__ == '__main__':

    st = 'DCACBCAA'
    print(printSmallestSequence(st))

# This code is contributed by Koushik Reddy B
```

## C#

```
// C# program to find lexicographically
// smallest sequence with rotations.
using System;

class LexoSmallest {

    // Function to compare lexicographically
    // two sequence with different starting
    // indexes. It returns true if sequence
    // beginning with y is lexicographically
    // greater.
    static bool compareSeq(string S, int x, int y, int n)
    {
        for (int i = 0; i < n; i++) {
            if (S[x] < S[y])
                return false;
            else if (S[x] > S[y])
                return true;
            x = (x + 1) % n;
            y = (y + 1) % n;
        }
        return true;
    }

    // Function to find starting index
    // of lexicographically smallest sequence
    static int smallestSequence(string S, int n)
    {
        int index = 0;
        for (int i = 1; i < n; i++)

            // if new sequence is smaller
            if (compareSeq(S, index, i, n))

                // change index of current min
                index = i;

        return index;
    }

    // Function to print lexicographically
    // smallest sequence
    static void printSmallestSequence(string str, int n)
    {
        // char[] S=str.toCharArray();
        int starting_index = smallestSequence(str, n);
        for (int i = 0; i < n; i++)
        Console.Write(str[(starting_index + i) % n]);
    }

    // driver code
    public static void Main()
    {
        string S = "DCACBCAA";
        int n = 8;
        printSmallestSequence(S, n);
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find lexicographically
// smallest sequence with rotations.

// Function to compare lexicographically
// two sequence with different starting
// indexes. It returns true if sequence
// beginning with y is lexicographically
// greater.
function compareSeq($S, $x, $y, $n)
{
    for($i = 0; $i < $n; $i++)
    {
        if ($S[$x] < $S[$y])
            return false;
        else if ($S[$x] > $S[$y])
            return true;
        $x = ($x + 1) % $n;
        $y = ($y + 1) % $n;
    }
    return true;
}

// Function to find starting index
// of lexicographically smallest
// sequence
function smallestSequence($S, $n)
{
    $index = 0;
    for ( $i = 1; $i < $n; $i++)

        // if new sequence is smaller
        if (compareSeq($S, $index, $i, $n))

            // change index of current min
            $index = $i;

    return $index;
}

// Function to print lexicographically
// smallest sequence
function printSmallestSequence($S, $n)
{
    $starting_index = smallestSequence($S, $n);
    for ($i = 0; $i < $n; $i++)
        echo $S[($starting_index + $i) % $n];
}

    // Driver Code
    $S= "DCACBCAA";
    $n = 8;
    printSmallestSequence($S, $n);

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
// Javascript program to find lexicographically
// smallest sequence with rotations.

    // Function to compare lexicographically
    // two sequence with different starting
    // indexes. It returns true if sequence
    // beginning with y is lexicographically
    // greater.
    function compareSeq(S,x,y,n)
    {
        for (let i = 0; i < n; i++)
        {
            if (S[x] < S[y])
                return false;
            else if (S[x] > S[y])
                return true;
            x = (x + 1) % n;
            y = (y + 1) % n;
        }
        return true;
    }

    // Function to find starting index
    // of lexicographically smallest sequence
    function smallestSequence(S,n)
    {
        let index = 0;
        for (let i = 1; i < n; i++)

            // if new sequence is smaller
            if (compareSeq(S, index, i, n))

                // change index of current min
                index = i;

        return index;
    }

    // Function to print lexicographically
    // smallest sequence
    function printSmallestSequence(str,n)
    {
        let S = str.split("");
        let starting_index = smallestSequence(S, n);
        for (let i = 0; i < n; i++)
            document.write(S[(starting_index + i) % n]);
    }

    // driver code
    let S = "DCACBCAA";
    let  n = 8;
    printSmallestSequence(S, n);

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
AADCACBC
```

**时间复杂度:** O(n^2)
**辅助空间:** O(1)
本文由 [**Pratik Chhajer**](//www.pratikchhajer.me) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。