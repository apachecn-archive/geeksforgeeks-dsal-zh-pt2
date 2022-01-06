# 在给定的约束条件下查找重复项

> 原文:[https://www . geesforgeks . org/find-duplicates-given-constraints/](https://www.geeksforgeeks.org/find-duplicates-given-constraints/)

一个排序的数组包含 6 个不同的数字，只有一个数字重复 5 次。所以数组中总共有 10 个数字。仅使用两次比较来查找重复的数字。
**例:**

```
Input: arr[] = {1, 1, 1, 1, 1, 5, 7, 10, 20, 30}
Output: 1

Input: arr[] = {1, 2, 3, 3, 3, 3, 3, 5, 9, 10}
Output: 3
```

问于**雅虎**T2】

一个重要观察是，arr[4]或 arr[5]肯定是重复元素的出现。下面是基于这一观察的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find duplicate element under
// given constraints.
#include<bits/stdc++.h>
using namespace std;

// This function assumes array is sorted,  has
// 10 elements,  there are totoal 6 different
// elements and one element repeats 5 times.
int findDuplicate(int a[])
{
    if (a[3] == a[4])
        return a[3];
    else if (a[4] == a[5])
        return a[4];
    else
        return a[5];
}

// Driver code
int main()
{
    int a[] = {1, 1, 1, 1, 1, 5, 7, 10, 20, 30};
    cout << findDuplicate(a);
    return 0;
}
```

## Java 语言（一种计算机语言，尤用于创建网站）

```
// Java program to find duplicate element under
// given constraints.
class Num{

// This function assumes array is sorted, has
// 10 elements, there are totoal 6 different
// elements and one element repeats 5 times.
static int findDuplicate(int a[])
{
    if (a[3] == a[4])
        return a[3];
    else if (a[4] == a[5])
        return a[4];
    else
        return a[5];
}

// Driver code
public static void main(String[] args)
{
    int a[] = {1, 1, 1, 1, 1, 5, 7, 10, 20, 30};
    System.out.println(findDuplicate(a));
}
}
//This code is contributed by
//Smitha Dinesh Semwal
```

## 蟒蛇 3

```
# Python 3 program to find duplicate
# element under given constraints.

# This function assumes array is
# sorted, has 10 elements, there are
# totoal 6 different elements and one
# element repeats 5 times.
def findDuplicate(a):

    if (a[3] == a[4]):
        return a[3]
    elif (a[4] == a[5]):
        return a[4]
    else:
        return a[5]

# Driver code
a = [1, 1, 1, 1, 1, 5, 7,
              10, 20, 30]

print(findDuplicate(a))

# This code is contributed by Smitha Dinesh Semwal
```

## C#

```
// C# program to find duplicate 
// element under given constraints.
using System;

class GFG {

// This function assumes array is
// sorted, has 10 elements, there
// are totoal 6 different elements
// and one element repeats 5 times.
static int findDuplicate(int []a)
{
    if (a[3] == a[4])
        return a[3];
    else if (a[4] == a[5])
        return a[4];
    else
        return a[5];
}

// Driver code
public static void Main()
{
    int []a = {1, 1, 1, 1, 1, 5,
               7, 10, 20, 30};
    Console.Write(findDuplicate(a));
}
}

// This code is contributed by nitin mittal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find duplicate
// element under given constraints.

// This function assumes array is
// sorted, has 10 elements, there
// are totoal 6 different elements
// and one element repeats 5 times.
function findDuplicate($a)
{
    if ($a[3] == $a[4])
        return $a[3];
    else if ($a[4] == $a[5])
        return $a[4];
    else
        return $a[5];
}

// Driver code
$a = array(1, 1, 1, 1, 1,
           5, 7, 10, 20, 30);
echo findDuplicate($a);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find duplicate element under
// given constraints.

// This function assumes array is sorted, has
// 10 elements, there are totoal 6 different
// elements and one element repeats 5 times.
function findDuplicate(a)
{
    if (a[3] == a[4])
        return a[3];
    else if (a[4] == a[5])
        return a[4];
    else
        return a[5];
}

// Driver code
    let a = [1, 1, 1, 1, 1, 5, 7, 10, 20, 30];
    document.write(findDuplicate(a));

</script>
```

**输出:**

```
1
```

**练习:**将上述问题扩展为一个有 n 个不同元素的数组，数组大小为 2*(n-1)，一个元素重复(n-1)次。
本文由**拉克什·库马尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。