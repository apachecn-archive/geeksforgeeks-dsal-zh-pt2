# 使异或最大化需要移除的元素的最小数量

> 原文:[https://www . geeksforgeeks . org/最小待移除元素数最大异或/](https://www.geeksforgeeks.org/minimum-number-of-elements-to-be-removed-to-make-xor-maximum/)

给定一个数字![N     ](img/38c509a53b4dd294712940cf7ecf6566.png "Rendered by QuickLaTeX.com")，其中![1\leq N\leq 10^{18}     ](img/e7975947838056438df920364cf90221.png "Rendered by QuickLaTeX.com")。任务是在![1     ](img/8cac2ba3fb6ce3c0fce5effb616c3c32.png "Rendered by QuickLaTeX.com")到![N     ](img/38c509a53b4dd294712940cf7ecf6566.png "Rendered by QuickLaTeX.com")之间找到要删除的元素的最小数量，使得从剩余元素获得的异或最大。
**例** :

```
Input: N = 5
Output: 2

Input: 1000000000000000
Output: 1
```

**方法:**考虑以下情况:

> **情况 1:** 当![n=1     ](img/14eb4a3ce7729e1e4ccc00f29c1e0f46.png "Rendered by QuickLaTeX.com")或![n=2     ](img/470573eb16c929d5bead66cd52ecec9b.png "Rendered by QuickLaTeX.com")时，则回答为 **0** 。不需要移除任何元素。
> **情况 2:** 现在我们要找一个是 **2** 的幂，大于等于![n     ](img/fa0f9698e6e59ce8e3e999505a99dbbe.png "Rendered by QuickLaTeX.com")的数。
> 这个号码就叫![a     ](img/dad1f7e479eb136e5f42993179fc50ca.png "Rendered by QuickLaTeX.com")吧。
> 所以，如果![n=a     ](img/248f43eeea58706688f6f4acc3347c20.png "Rendered by QuickLaTeX.com")或者![n=a-1     ](img/2ab1956a0cb121f66d723d13afaa216a.png "Rendered by QuickLaTeX.com")那么我们就去掉![a-1     ](img/f0584078718ec30b90c641aebe58d962.png "Rendered by QuickLaTeX.com")。因此答案是 **1** 。
> 否则如果![n=a-2     ](img/1c4f703633fee4fa598634bc94b09925.png "Rendered by QuickLaTeX.com")，那么答案是 **0** 。不需要移除任何元素。
> **案例三:**否则，如果![n     ](img/fa0f9698e6e59ce8e3e999505a99dbbe.png "Rendered by QuickLaTeX.com")为![even     ](img/96a41764b35b53259b48a5bb07f7f541.png "Rendered by QuickLaTeX.com")，那么答案为 **1** 。
> 否则如果![n     ](img/fa0f9698e6e59ce8e3e999505a99dbbe.png "Rendered by QuickLaTeX.com")是![odd     ](img/83bbfcc9426472db7edaec57028d64d0.png "Rendered by QuickLaTeX.com")，那么答案就是 **2** 。

以下是上述方法的实现:

## C++

```
// C++ implementation to find minimum number of
// elements to remove to get maximum XOR value
#include <bits/stdc++.h>
using namespace std;

unsigned int nextPowerOf2(unsigned int n)
{
    unsigned count = 0;

    // First n in the below condition
    // is for the case where n is 0
    if (n && !(n & (n - 1)))
        return n;

    while (n != 0) {
        n >>= 1;
        count += 1;
    }

    return 1 << count;
}

// Function to find minimum number of
// elements to be removed.
int removeElement(unsigned int n)
{

    if (n == 1 || n == 2)
        return 0;

    unsigned int a = nextPowerOf2(n);

    if (n == a || n == a - 1)
        return 1;

    else if (n == a - 2)
        return 0;

    else if (n % 2 == 0)
        return 1;

    else
        return 2;
}

// Driver code
int main()
{
    unsigned int n = 5;

    // print minimum number of elements
    // to be removed
    cout << removeElement(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation to find minimum number of
//elements to remove to get maximum XOR value
public class GFG {

    static int nextPowerOf2(int n)
    {
     int count = 0;

     // First n in the below condition
     // is for the case where n is 0
     if (n!=0 && (n& (n - 1))==0)
         return n;

     while (n != 0) {
         n >>= 1;
         count += 1;
     }

     return 1 << count;
    }

    //Function to find minimum number of
    //elements to be removed.
    static int removeElement(int n)
    {

     if (n == 1 || n == 2)
         return 0;

     int a = nextPowerOf2(n);

     if (n == a || n == a - 1)
         return 1;

     else if (n == a - 2)
         return 0;

     else if (n % 2 == 0)
         return 1;

     else
         return 2;
    }

    //Driver code
    public static void main(String[] args) {

         int n = 5;

         // print minimum number of elements
         // to be removed
         System.out.println(removeElement(n));
    }
}
```

## 蟒蛇 3

```
# Python 3 to find minimum number
# of elements to remove to get
# maximum XOR value

def nextPowerOf2(n) :
    count = 0

    # First n in the below condition
    # is for the case where n is 0
    if (n and not(n and (n - 1))) :
        return n

    while n != 0 :
        n >>= 1
        count += 1

    return 1 << count

# Function to find minimum number
# of elements to be removed.
def removeElement(n) :

    if n == 1 or n == 2 :
        return 0

    a = nextPowerOf2(n)

    if n == a or n == a - 1 :
        return 1

    elif n == a - 2 :
        return 0

    elif n % 2 == 0 :
        return 1

    else :
        return 2

# Driver Code
if __name__ == "__main__" :

    n = 5

    # print minimum number of
    # elements to be removed
    print(removeElement(n))

# This code is contributed
# by ANKITRAI1
```

## C#

```
//C# implementation to find minimum number of
//elements to remove to get maximum XOR value

using System;
public class GFG {

    static int nextPowerOf2(int n)
    {
     int count = 0;

     // First n in the below condition
     // is for the case where n is 0
     if (n!=0 && (n& (n - 1))==0)
         return n;

     while (n != 0) {
         n >>= 1;
         count += 1;
     }

     return 1 << count;
    }

    //Function to find minimum number of
    //elements to be removed.
    static int removeElement(int n)
    {

     if (n == 1 || n == 2)
         return 0;

     int a = nextPowerOf2(n);

     if (n == a || n == a - 1)
         return 1;

     else if (n == a - 2)
         return 0;

     else if (n % 2 == 0)
         return 1;

     else
         return 2;
    }

    //Driver code
    public static void Main() {

         int n = 5;

         // print minimum number of elements
         // to be removed
         Console.Write(removeElement(n));
    }
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find
// minimum number of elements
// to remove to get maximum
// XOR value

function nextPowerOf2($n)
{
    $count = 0;

    // First n in the below condition
    // is for the case where n is 0
    if ($n && !($n & ($n - 1)))
        return $n;

    while ($n != 0)
    {
        $n >>= 1;
        $count += 1;
    }

    return 1 << $count;
}

// Function to find minimum number
// of elements to be removed.
function removeElement($n)
{

    if ($n == 1 || $n == 2)
        return 0;

    $a = nextPowerOf2($n);

    if ($n == $a || $n == $a - 1)
        return 1;

    else if ($n == $a - 2)
        return 0;

    else if ($n % 2 == 0)
        return 1;

    else
        return 2;
}

// Driver code
$n = 5;

// print minimum number of
// elements to be removed
echo removeElement($n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation to
// find minimum number of
// elements to remove to get
// maximum XOR value

function nextPowerOf2(n)
{
    let count = 0;

    // First n in the below condition
    // is for the case where n is 0
    if (n && !(n & (n - 1)))
        return n;

    while (n != 0) {
        n >>= 1;
        count += 1;
    }

    return 1 << count;
}

// Function to find minimum number of
// elements to be removed.
function removeElement(n)
{

    if (n == 1 || n == 2)
        return 0;

    let a = nextPowerOf2(n);

    if (n == a || n == a - 1)
        return 1;

    else if (n == a - 2)
        return 0;

    else if (n % 2 == 0)
        return 1;

    else
        return 2;
}

// Driver code
    let n = 5;

    // print minimum number of elements
    // to be removed
    document.write(removeElement(n));

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(logn)