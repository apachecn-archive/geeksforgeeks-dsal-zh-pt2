# 字符串的字典顺序

> 原文:[https://www . geeksforgeeks . org/词典-字符串排名/](https://www.geeksforgeeks.org/lexicographic-rank-of-a-string/)

给定一个字符串，在按字典顺序排列的所有排列中找到它的等级。比如“abc”的排名是 1，“acb”的排名是 2，“cba”的排名是 6。

**示例:**

```
Input : str[] = "acb"
Output : Rank = 2

Input : str[] = "string"
Output : Rank = 598

Input : str[] = "cba"
Output : Rank = 6
```

为了简单起见，让我们假设字符串不包含任何重复的字符。

一个简单的解决方案是将等级初始化为 1，[按照字典顺序](https://www.geeksforgeeks.org/lexicographic-permutations-of-string/)生成所有排列。生成排列后，检查生成的排列是否与给定的字符串相同，如果相同，则返回秩，如果不相同，则将秩增加 1。在最坏的情况下，该解决方案的时间复杂度将是指数级的。以下是一个有效的解决方案。

让给定的字符串为“string”。在输入字符串中，“S”是第一个字符。总共有 6 个字符，其中 4 个小于“S”。所以可以有 4 * 5！第一个字符小于“S”的较小字符串，如下面的
R X X X X X X
I X X X X X X
N X X X X X
G X X X X
现在让我们修正“S”，找到以“S”开头的较小字符串。

对 T 重复同样的过程，排名是 4*5！+ 4*4!+…

现在固定 T，对 R 重复同样的过程，排名是 4*5！+ 4*4!+ 3*3!+…

现在固定 R，对 I 重复同样的过程，排名是 4*5！+ 4*4!+ 3*3!+ 1*2!+…

现在修复我，对 N 重复同样的过程，排名是 4*5！+ 4*4!+ 3*3!+ 1*2!+ 1*1!+…

现在固定 N，对 G 重复同样的过程，排名是 4*5！+ 4*4!+ 3*3!+ 1*2!+ 1*1!+ 0*0!

排名= 4*5！+ 4*4!+ 3*3!+ 1*2!+ 1*1!+ 0*0!= 597

请注意，上面的计算找到了较小字符串的计数。因此，给定字符串的秩是较小字符串的计数加 1。最终排名= 1 + 597 = 598

下面是上述方法的实现:

## C++

```
// C++ program to find lexicographic rank
// of a string
#include <bits/stdc++.h>
#include <string.h>

using namespace std;
// A utility function to find factorial of n
int fact(int n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// A utility function to count smaller characters on right
// of arr[low]
int findSmallerInRight(char* str, int low, int high)
{
    int countRight = 0, i;

    for (i = low + 1; i <= high; ++i)
        if (str[i] < str[low])
            ++countRight;

    return countRight;
}

// A function to find rank of a string in all permutations
// of characters
int findRank(char* str)
{
    int len = strlen(str);
    int mul = fact(len);
    int rank = 1;
    int countRight;

    int i;
    for (i = 0; i < len; ++i) {
        mul /= len - i;

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        countRight = findSmallerInRight(str, i, len - 1);

        rank += countRight * mul;
    }

    return rank;
}

// Driver program to test above function
int main()
{
    char str[] = "string";
    cout << findRank(str);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## C

```
// C program to find lexicographic rank
// of a string
#include <stdio.h>
#include <string.h>

// A utility function to find factorial of n
int fact(int n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// A utility function to count smaller characters on right
// of arr[low]
int findSmallerInRight(char* str, int low, int high)
{
    int countRight = 0, i;

    for (i = low + 1; i <= high; ++i)
        if (str[i] < str[low])
            ++countRight;

    return countRight;
}

// A function to find rank of a string in all permutations
// of characters
int findRank(char* str)
{
    int len = strlen(str);
    int mul = fact(len);
    int rank = 1;
    int countRight;

    int i;
    for (i = 0; i < len; ++i) {
        mul /= len - i;

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        countRight = findSmallerInRight(str, i, len - 1);

        rank += countRight * mul;
    }

    return rank;
}

// Driver program to test above function
int main()
{
    char str[] = "string";
    printf("%d", findRank(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find lexicographic rank
// of a string
import java.io.*;
import java.util.*;

class GFG {

    // A utility function to find factorial of n
    static int fact(int n)
    {
        return (n <= 1) ? 1 : n * fact(n - 1);
    }

    // A utility function to count smaller
    // characters on right of arr[low]
    static int findSmallerInRight(String str, int low,
                                  int high)
    {
        int countRight = 0, i;

        for (i = low + 1; i <= high; ++i)
            if (str.charAt(i) < str.charAt(low))
                ++countRight;

        return countRight;
    }

    // A function to find rank of a string in
    // all permutations of characters
    static int findRank(String str)
    {
        int len = str.length();
        int mul = fact(len);
        int rank = 1;
        int countRight;

        for (int i = 0; i < len; ++i) {
            mul /= len - i;

            // count number of chars smaller
            // than str[i] from str[i+1] to
            // str[len-1]
            countRight = findSmallerInRight(str, i, len - 1);

            rank += countRight * mul;
        }

        return rank;
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        String str = "string";
        System.out.println(findRank(str));
    }
}

// This code is contributed by Nikita Tiwari.
```

## 计算机编程语言

```
# Python program to find lexicographic
# rank of a string

# A utility function to find factorial
# of n
def fact(n) :
    f = 1
    while n >= 1 :
        f = f * n
        n = n - 1
    return f

# A utility function to count smaller
# characters on right of arr[low]
def findSmallerInRight(st, low, high) :

    countRight = 0
    i = low + 1
    while i <= high :
        if st[i] < st[low] :
            countRight = countRight + 1
        i = i + 1

    return countRight

# A function to find rank of a string
# in all permutations of characters
def findRank (st) :
    ln = len(st)
    mul = fact(ln)
    rank = 1
    i = 0

    while i < ln :

        mul = mul / (ln - i)

        # count number of chars smaller
        # than str[i] from str[i + 1] to
        # str[len-1]
        countRight = findSmallerInRight(st, i, ln-1)

        rank = rank + countRight * mul
        i = i + 1

    return rank

# Driver program to test above function
st = "string"
print (findRank(st))

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find lexicographic rank
// of a string
using System;

class GFG {

    // A utility function to find factorial of n
    static int fact(int n)
    {
        return (n <= 1) ? 1 : n * fact(n - 1);
    }

    // A utility function to count smaller
    // characters on right of arr[low]
    static int findSmallerInRight(string str,
                                  int low, int high)
    {
        int countRight = 0, i;

        for (i = low + 1; i <= high; ++i)
            if (str[i] < str[low])
                ++countRight;

        return countRight;
    }

    // A function to find rank of a string in
    // all permutations of characters
    static int findRank(string str)
    {
        int len = str.Length;
        int mul = fact(len);
        int rank = 1;
        int countRight;

        for (int i = 0; i < len; ++i) {
            mul /= len - i;

            // count number of chars smaller
            // than str[i] from str[i+1] to
            // str[len-1]
            countRight = findSmallerInRight(str,
                                            i, len - 1);

            rank += countRight * mul;
        }

        return rank;
    }

    // Driver program to test above function
    public static void Main()
    {
        string str = "string";
        Console.Write(findRank(str));
    }
}

// This code is contributed nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A utility function to find factorial of n
function fact($n)
{
    return ($n <= 1) ? 1 :$n * fact($n - 1);
}

// A utility function to count smaller
// characters on right of arr[low]
function findSmallerInRight($str, $low, $high)
{
    $countRight = 0;

    for ($i = $low + 1; $i <= $high; ++$i)
        if ($str[$i] < $str[$low])
            ++$countRight;

    return $countRight;
}

// A function to find rank of a string
// in all permutations of characters
function findRank ($str)
{
    $len = strlen($str);
    $mul = fact($len);
    $rank = 1;

    for ($i = 0; $i < $len; ++$i)
    {
        $mul /= $len - $i;

        // count number of chars smaller than
        // str[i] from str[i+1] to str[len-1]
        $countRight = findSmallerInRight($str, $i,
                                         $len - 1);

        $rank += $countRight * $mul ;
    }

    return $rank;
}

// Driver Code
$str = "string";
echo findRank($str);

// This code is contributed by ChitraNayal
?>
```

## java 描述语言

```
<script>

// JavaScript program to find lexicographic rank

// A utility function to find factorial of n
function fact(n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// A utility function to count smaller
// characters on right of arr[low]
function findSmallerInRight(str, low, high)
{
    let countRight = 0;
    let i;

    for(i = low + 1; i <= high; ++i)
        if (str[i] < str[low])
            ++countRight;

    return countRight;
}

// A function to find rank of a string
// in all permutations of characters
function findRank(str)
{
    let len = (str).length;
    let mul = fact(len);
    let rank = 1;
    let countRight;
    let i;

    for(i = 0; i < len; ++i)
    {
        mul /= len - i;

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        countRight = findSmallerInRight(str, i, len - 1);

        rank += countRight * mul;
    }
    return rank;
}

// Driver code
let str = "string";
document.write(findRank(str));

// This code is contributed by rohan07

</script>
```

**输出:**

```
598
```

上述解决方案的时间复杂度是 O(n^2).我们可以通过创建一个大小为 256 的辅助数组来将时间复杂度降低到 O(n)。请参见以下代码。

## C++

```
// A O(n) solution for finding rank of string
#include <bits/stdc++.h>
using namespace std;
#define MAX_CHAR 256

// A utility function to find factorial of n
int fact(int n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// Construct a count array where value at every index
// contains count of smaller characters in whole string
void populateAndIncreaseCount(int* count, char* str)
{
    int i;

    for (i = 0; str[i]; ++i)
        ++count[str[i]];

    for (i = 1; i < MAX_CHAR; ++i)
        count[i] += count[i - 1];
}

// Removes a character ch from count[] array
// constructed by populateAndIncreaseCount()
void updatecount(int* count, char ch)
{
    int i;
    for (i = ch; i < MAX_CHAR; ++i)
        --count[i];
}

// A function to find rank of a string in all permutations
// of characters
int findRank(char* str)
{
    int len = strlen(str);
    int mul = fact(len);
    int rank = 1, i;

    // all elements of count[] are initialized with 0
    int count[MAX_CHAR] = { 0 };

    // Populate the count array such that count[i]
    // contains count of characters which are present
    // in str and are smaller than i
    populateAndIncreaseCount(count, str);

    for (i = 0; i < len; ++i) {
        mul /= len - i;

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        rank += count[str[i] - 1] * mul;

        // Reduce count of characters greater than str[i]
        updatecount(count, str[i]);
    }

    return rank;
}

// Driver program to test above function
int main()
{
    char str[] = "string";
    cout << findRank(str);
    return 0;
}

// This is code is contributed by rathbhupendra
```

## C

```
// A O(n) solution for finding rank of string
#include <stdio.h>
#include <string.h>
#define MAX_CHAR 256

// A utility function to find factorial of n
int fact(int n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// Construct a count array where value at every index
// contains count of smaller characters in whole string
void populateAndIncreaseCount(int* count, char* str)
{
    int i;

    for (i = 0; str[i]; ++i)
        ++count[str[i]];

    for (i = 1; i < MAX_CHAR; ++i)
        count[i] += count[i - 1];
}

// Removes a character ch from count[] array
// constructed by populateAndIncreaseCount()
void updatecount(int* count, char ch)
{
    int i;
    for (i = ch; i < MAX_CHAR; ++i)
        --count[i];
}

// A function to find rank of a string in all permutations
// of characters
int findRank(char* str)
{
    int len = strlen(str);
    int mul = fact(len);
    int rank = 1, i;

    // all elements of count[] are initialized with 0
    int count[MAX_CHAR] = { 0 };

    // Populate the count array such that count[i]
    // contains count of characters which are present
    // in str and are smaller than i
    populateAndIncreaseCount(count, str);

    for (i = 0; i < len; ++i) {
        mul /= len - i;

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        rank += count[str[i] - 1] * mul;

        // Reduce count of characters greater than str[i]
        updatecount(count, str[i]);
    }

    return rank;
}

// Driver program to test above function
int main()
{
    char str[] = "string";
    printf("%d", findRank(str));
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A O(n) solution for finding rank of string

class GFG {

    static int MAX_CHAR = 256;

    // A utility function to find factorial of n
    static int fact(int n)
    {
        return (n <= 1) ? 1 : n * fact(n - 1);
    }

    // Construct a count array where value at every index
    // contains count of smaller characters in whole string
    static void populateAndIncreaseCount(int[] count, char[] str)
    {
        int i;

        for (i = 0; i < str.length; ++i)
            ++count[str[i]];

        for (i = 1; i < MAX_CHAR; ++i)
            count[i] += count[i - 1];
    }

    // Removes a character ch from count[] array
    // constructed by populateAndIncreaseCount()
    static void updatecount(int[] count, char ch)
    {
        int i;
        for (i = ch; i < MAX_CHAR; ++i)
            --count[i];
    }

    // A function to find rank of a string in all permutations
    // of characters
    static int findRank(char[] str)
    {
        int len = str.length;
        int mul = fact(len);
        int rank = 1, i;

        // all elements of count[] are initialized with 0
        int count[] = new int[MAX_CHAR];

        // Populate the count array such that count[i]
        // contains count of characters which are present
        // in str and are smaller than i
        populateAndIncreaseCount(count, str);

        for (i = 0; i < len; ++i) {
            mul /= len - i;

            // count number of chars smaller than str[i]
            // from str[i+1] to str[len-1]
            rank += count[str[i] - 1] * mul;

            // Reduce count of characters greater than str[i]
            updatecount(count, str[i]);
        }

        return rank;
    }

    // Driver code
    public static void main(String args[])
    {
        char str[] = "string".toCharArray();
        System.out.println(findRank(str));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A O(n) solution for finding rank of string
MAX_CHAR=256;

# all elements of count[] are initialized with 0
count=[0]*(MAX_CHAR + 1);

# A utility function to find factorial of n
def fact(n):
    return 1 if(n <= 1) else (n * fact(n - 1));

# Construct a count array where value at every index
# contains count of smaller characters in whole string
def populateAndIncreaseCount(str):
    for i in range(len(str)):
        count[ord(str[i])]+=1;

    for i in range(1,MAX_CHAR):
        count[i] += count[i - 1];

# Removes a character ch from count[] array
# constructed by populateAndIncreaseCount()
def updatecount(ch):

    for i in range(ord(ch),MAX_CHAR):
        count[i]-=1;

# A function to find rank of a string in all permutations
# of characters
def findRank(str):
    len1 = len(str);
    mul = fact(len1);
    rank = 1;

    # Populate the count array such that count[i]
    # contains count of characters which are present
    # in str and are smaller than i
    populateAndIncreaseCount(str);

    for i in range(len1):
        mul = mul//(len1 - i);

        # count number of chars smaller than str[i]
        # from str[i+1] to str[len-1]
        rank += count[ord(str[i]) - 1] * mul;

        # Reduce count of characters greater than str[i]
        updatecount(str[i]);

    return rank;

# Driver code
str = "string";
print(findRank(str));

# This is code is contributed by chandan_jnu
```

## C#

```
// A O(n) solution for finding rank of string
using System;

class GFG {

    static int MAX_CHAR = 256;

    // A utility function to find factorial of n
    static int fact(int n)
    {
        return (n <= 1) ? 1 : n * fact(n - 1);
    }

    // Construct a count array where value at every index
    // contains count of smaller characters in whole string
    static void populateAndIncreaseCount(int[] count, char[] str)
    {
        int i;

        for (i = 0; i < str.Length; ++i)
            ++count[str[i]];

        for (i = 1; i < MAX_CHAR; ++i)
            count[i] += count[i - 1];
    }

    // Removes a character ch from count[] array
    // constructed by populateAndIncreaseCount()
    static void updatecount(int[] count, char ch)
    {
        int i;
        for (i = ch; i < MAX_CHAR; ++i)
            --count[i];
    }

    // A function to find rank of a string in all permutations
    // of characters
    static int findRank(char[] str)
    {
        int len = str.Length;
        int mul = fact(len);
        int rank = 1, i;

        // all elements of count[] are initialized with 0
        int[] count = new int[MAX_CHAR];

        // Populate the count array such that count[i]
        // contains count of characters which are present
        // in str and are smaller than i
        populateAndIncreaseCount(count, str);

        for (i = 0; i < len; ++i) {
            mul /= len - i;

            // count number of chars smaller than str[i]
            // from str[i+1] to str[len-1]
            rank += count[str[i] - 1] * mul;

            // Reduce count of characters greater than str[i]
            updatecount(count, str[i]);
        }

        return rank;
    }

    // Driver code
    public static void Main(String[] args)
    {
        char[] str = "string".ToCharArray();
        Console.WriteLine(findRank(str));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A O(n) solution for finding rank of string
$MAX_CHAR=256;

// A utility function to find factorial of n
function fact($n)
{
    return ($n <= 1) ? 1 : $n * fact($n - 1);
}

// Construct a count array where value at every index
// contains count of smaller characters in whole string
function populateAndIncreaseCount(&$count, $str)
{
global $MAX_CHAR;
    for ($i = 0; $i < strlen($str); ++$i)
        ++$count[ord($str[$i])];

    for ($i = 1; $i < $MAX_CHAR; ++$i)
        $count[$i] += $count[$i - 1];
}

// Removes a character ch from count[] array
// constructed by populateAndIncreaseCount()
function updatecount(&$count, $ch)
{
    global $MAX_CHAR;
    for ($i = ord($ch); $i < $MAX_CHAR; ++$i)
        --$count[$i];
}

// A function to find rank of a string in all permutations
// of characters
function findRank($str)
{
    global $MAX_CHAR;
    $len = strlen($str);
    $mul = fact($len);
    $rank = 1;

    // all elements of count[] are initialized with 0
    $count=array_fill(0, $MAX_CHAR + 1, 0);

    // Populate the count array such that count[i]
    // contains count of characters which are present
    // in str and are smaller than i
    populateAndIncreaseCount($count, $str);

    for ($i = 0; $i < $len; ++$i)
    {
        $mul = (int)($mul/($len - $i));

        // count number of chars smaller than str[i]
        // from str[i+1] to str[len-1]
        $rank += $count[ord($str[$i]) - 1] * $mul;

        // Reduce count of characters greater than str[i]
        updatecount($count, $str[$i]);
    }

    return $rank;
}

    // Driver code
    $str = "string";
    echo findRank($str);

// This is code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>
// A O(n) solution for finding rank of string
let MAX_CHAR = 256;

 // A utility function to find factorial of n
function fact(n)
{
    return (n <= 1) ? 1 : n * fact(n - 1);
}

// Construct a count array where value at every index
    // contains count of smaller characters in whole string
function populateAndIncreaseCount(count,str)
{
    let i;

        for (i = 0; i < str.length; ++i)
            ++count[str[i].charCodeAt(0)];

        for (i = 1; i < MAX_CHAR; ++i)
            count[i] += count[i - 1];
}

// Removes a character ch from count[] array
    // constructed by populateAndIncreaseCount()
function updatecount(count,ch)
{
    let i;
        for (i = ch.charCodeAt(0); i < MAX_CHAR; ++i)
            --count[i];
}

// A function to find rank of a string in all permutations
    // of characters
function findRank(str)
{
    let len = str.length;
        let mul = fact(len);
        let rank = 1, i;

        // all elements of count[] are initialized with 0
        let count = new Array(MAX_CHAR);
         for(let i = 0; i < count.length; i++)
        {
            count[i] = 0;
        }

        // Populate the count array such that count[i]
        // contains count of characters which are present
        // in str and are smaller than i
        populateAndIncreaseCount(count, str);

        for (i = 0; i < len; ++i) {
            mul = Math.floor(mul/(len - i));

            // count number of chars smaller than str[i]
            // from str[i+1] to str[len-1]
            rank += count[str[i].charCodeAt(0) - 1] * mul;

            // Reduce count of characters greater than str[i]
            updatecount(count, str[i]);
        }

        return rank;
}

// Driver code
let str= "string".split("");
document.write(findRank(str));

// This code is contributed by rag2127
</script>
```

**输出:**

```
598
```

上述程序不适用于重复字符。为了使它们适用于重复的字符，找到所有较小的字符(这次也包括相等的字符)，做与上面相同的操作，但是，这次将由 p！其中 p 是重复字符出现的次数。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。