# 找出一个数组中某个数字的出现频率

> 原文:[https://www.geeksforgeeks.org/find-frequency-number-array/](https://www.geeksforgeeks.org/find-frequency-number-array/)

给定一个数组、一个[]和一个元素 x，找出 x 在[]中出现的次数。
示例:

```
Input  : a[] = {0, 5, 5, 5, 4}
           x = 5
Output : 3

Input  : a[] = {1, 2, 3}
          x = 4
Output : 0
```

**如果数组没有排序**

想法很简单，我们初始化计数为 0。我们以线性方式遍历数组。对于每个与 x 匹配的元素，我们增加计数。最后，我们返回计数。
以下是实施办法。

## C++

```
// CPP program to count occurrences of an
// element in an unsorted array
#include<iostream>
using namespace std;

int frequency(int a[], int n, int x)
{
    int count = 0;
    for (int i=0; i < n; i++)
       if (a[i] == x)
          count++;
    return count;
}

// Driver program
int main() {
    int a[] = {0, 5, 5, 5, 4};
    int x = 5;
    int n = sizeof(a)/sizeof(a[0]);
    cout << frequency(a, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count
// occurrences of an
// element in an unsorted
// array

import java.io.*;

class GFG {

    static int frequency(int a[],
    int n, int x)
    {
        int count = 0;
        for (int i=0; i < n; i++)
        if (a[i] == x)
            count++;
        return count;
    }

    // Driver program
    public static void main (String[]
    args) {

        int a[] = {0, 5, 5, 5, 4};
        int x = 5;
        int n = a.length;

        System.out.println(frequency(a, n, x));
    }
}

// This code is contributed
// by Ansu Kumari
```

## 蟒蛇 3

```
# Python program to count
# occurrences of an
# element in an unsorted
# array
def frequency(a, x):
    count = 0

    for i in a:
        if i == x: count += 1
    return count

# Driver program
a = [0, 5, 5, 5, 4]
x = 5
print(frequency(a, x))

# This code is contributed by Ansu Kumari
```

## C#

```
// C# program to count
// occurrences of an
// element in an unsorted
// array
using System;

class GFG {

    static int frequency(int []a,
    int n, int x)
    {
        int count = 0;
        for (int i=0; i < n; i++)
        if (a[i] == x)
            count++;
        return count;
    }

    // Driver program
    static public void Main (){

        int []a = {0, 5, 5, 5, 4};
        int x = 5;
        int n = a.Length;

        Console.Write(frequency(a, n, x));
    }
}

// This code is contributed
// by Anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count occurrences of an
// element in an unsorted array

function frequency($a, $n, $x)
{
    $count = 0;
    for ($i = 0; $i < $n; $i++)
    if ($a[$i] == $x)
        $count++;
    return $count;
}

    // Driver Code
    $a = array (0, 5, 5, 5, 4);
    $x = 5;
    $n = sizeof($a);
    echo frequency($a, $n, $x);

// This code is contributed by ajit
?>
```

## java 描述语言

```
<script>
    // C# program to count occurrences of an element in an unsorted array

    function frequency(a, n, x)
    {
        let count = 0;
        for (let i=0; i < n; i++)
        if (a[i] == x)
            count++;
        return count;
    }

    let a = [0, 5, 5, 5, 4];
    let x = 5;
    let n = a.length;

    document.write(frequency(a, n, x));

</script>
```

**输出:**

```
3
```

时间复杂度:O(n)
辅助空间:O(1)

**如果数组已排序**

我们可以对已排序和未排序的应用方法。但是对于排序后的数组，我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)对其进行优化，使其在 O(Log n)时间内工作。详情请参考以下文章。[计算排序数组中出现的次数(或频率)](https://www.geeksforgeeks.org/count-number-of-occurrences-or-frequency-in-a-sorted-array/)。

**如果单个数组上有多个查询**

我们可以使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来存储所有元素的频率。然后我们可以在 O(1)时间内回答所有的查询。详情请参考[未排序数组中每个元素的频率](https://www.geeksforgeeks.org/frequency-element-unsorted-array/)。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to answer queries for frequencies
// in O(1) time.
#include <bits/stdc++.h>
using namespace std;

unordered_map<int, int> hm;

void countFreq(int a[], int n)
{
    // Insert elements and their
    // frequencies in hash map.
    for (int i=0; i<n; i++)
        hm[a[i]]++;
}

// Return frequency of x (Assumes that
// countFreq() is called before)
int query(int x)
{
    return hm[x];
}

// Driver program
int main()
{
    int a[] = {1, 3, 2, 4, 2, 1};
    int n = sizeof(a)/sizeof(a[0]);
    countFreq(a, n);
    cout << query(2) << endl;
    cout << query(3) << endl;
    cout << query(5) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer
// queries for frequencies
// in O(1) time.

import java.io.*;
import java.util.*;

class GFG {

   static HashMap <Integer, Integer> hm = new HashMap<Integer, Integer>();

   static void countFreq(int a[], int n)
   {
        // Insert elements and their
        // frequencies in hash map.
        for (int i=0; i<n; i++)
            if (hm.containsKey(a[i]) )
                hm.put(a[i], hm.get(a[i]) + 1);
            else hm.put(a[i] , 1);
    }

    // Return frequency of x (Assumes that
    // countFreq() is called before)
    static int query(int x)
    {
        if (hm.containsKey(x))
            return hm.get(x);
        return 0;
    }

    // Driver program
    public static void main (String[] args) {
        int a[] = {1, 3, 2, 4, 2, 1};
        int n = a.length;
        countFreq(a, n);
        System.out.println(query(2));
        System.out.println(query(3));
        System.out.println(query(5));
    }
    }

// This code is contributed by Ansu Kumari
```

## 蟒蛇 3

```
# Python program to
# answer queries for
# frequencies
# in O(1) time.

hm = {}

def countFreq(a):
    global hm

    # Insert elements and their
    # frequencies in hash map.

    for i in a:
        if i in hm: hm[i] += 1
        else: hm[i] = 1

# Return frequency
# of x (Assumes that
# countFreq() is
# called before)
def query(x):
    if x in hm:
        return hm[x]
    return 0

# Driver program
a = [1, 3, 2, 4, 2, 1]
countFreq(a)
print(query(2))
print(query(3))
print(query(5))

# This code is contributed
# by Ansu Kumari
```

## C#

```
// C# program to answer
// queries for frequencies
// in O(1) time.
using System;
using System.Collections.Generic;
class GFG
{

static Dictionary <int, int> hm = new Dictionary<int, int>();

static void countFreq(int []a, int n)
{
    // Insert elements and their
    // frequencies in hash map.
    for (int i = 0; i < n; i++)
        if (hm.ContainsKey(a[i]) )
            hm[a[i]] = hm[a[i]] + 1;
        else hm.Add(a[i], 1);
}

// Return frequency of x (Assumes that
// countFreq() is called before)
static int query(int x)
{
    if (hm.ContainsKey(x))
        return hm[x];
    return 0;
}

// Driver code
public static void Main(String[] args)
{
    int []a = {1, 3, 2, 4, 2, 1};
    int n = a.Length;
    countFreq(a, n);
    Console.WriteLine(query(2));
    Console.WriteLine(query(3));
    Console.WriteLine(query(5));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to answer
// queries for frequencies
// in O(1) time.

var hm = new Map();

function countFreq(a, n)
{
    // Insert elements and their
    // frequencies in hash map.
    for (var i=0; i<n; i++)
    {
        if(hm.has(a[i]))
        {
            hm.set(a[i], hm.get(a[i])+1);
        }
        else
        {
            hm.set(a[i], 1);
        }
    }
}

// Return frequency of x (Assumes that
// countFreq() is called before)
function query(x)
{
    if(hm.has(x))
    {
        return hm.get(x);
    }
    return 0;
}

// Driver program
var a = [1, 3, 2, 4, 2, 1];
var n = a.length;
countFreq(a, n);
document.write( query(2) + "<br>");
document.write( query(3) + "<br>");
document.write( query(5) + "<br>");

</script>
```

**输出:**

```
2
1
0
```

本文由 [**桑吉塔·德伊**](https://auth.geeksforgeeks.org/profile.php?user=Sangita Dey) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。