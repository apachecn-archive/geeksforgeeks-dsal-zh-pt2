# 通过移除更大的对来制造阵列尺寸 1 的最小成本

> 原文:[https://www . geesforgeks . org/最低成本-制作阵列-大小-1-移除-较大对/](https://www.geeksforgeeks.org/minimum-cost-make-array-size-1-removing-larger-pairs/)

给定 n 个整数的数组。我们需要将数组的大小减少到 1。我们可以选择一对整数，去掉这两个中较大的一个。这会将数组大小减少 1。该操作的成本等于较小操作的价值。找出将数组转换为单个元素所需的最小操作成本总和。
**例:**

```
Input: 4 3 2 
Output: 4
Explanation: 
Choose (4, 2) so 4 is removed, new array 
= {2, 3}. Now choose (2, 3) so 3 is removed. 
So total cost = 2 + 2 = 4

Input: 3 4
Output: 3
Explanation: choose 3, 4, so cost is 3\. 
```

想法是总是选择最小值作为配对的一部分，并移除较大的值。这最大限度地降低了将阵列缩小到 1 号的成本。
以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// CPP program to find minimum cost to
// reduce array size to 1,
#include <bits/stdc++.h>
using namespace std;

// function to calculate the minimum cost
int cost(int a[], int n)
{
    // Minimum cost is n-1 multiplied with
    // minimum element.
    return (n - 1) * (*min_element(a, a + n));
}

// driver program to test the above function.
int main()
{
    int a[] = { 4, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << cost(a, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum cost
// to reduce array size to 1,
import java.lang.*;

public class GFG {

    // function to calculate the
    // minimum cost
    static int cost(int []a, int n)
    {
        int min = a[0];

        // find the minimum using
        // for loop
        for(int i = 1; i< a.length; i++)
        {
            if (a[i] < min)
                min = a[i];
        }

        // Minimum cost is n-1 multiplied
        // with minimum element.
        return (n - 1) * min;
    }

    // driver program to test the
    // above function.
    static public void main (String[] args)
    {

        int []a = { 4, 3, 2 };
        int n = a.length;

        System.out.println(cost(a, n));
    }
}

// This code is contributed by parashar.
```

## 蟒蛇 3

```
# Python program to find minimum
# cost to reduce array size to 1

# function to calculate the
# minimum cost
def cost(a, n):

    # Minimum cost is n-1 multiplied
    # with minimum element.
    return ( (n - 1) * min(a) )

# driver code
a = [ 4, 3, 2 ]
n = len(a)
print(cost(a, n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// C# program to find minimum cost to
// reduce array size to 1,
using System;
using System.Linq;

public class GFG {

    // function to calculate the minimum cost
    static int cost(int []a, int n)
    {

        // Minimum cost is n-1 multiplied with
        // minimum element.
        return (n - 1) * a.Min();
    }

    // driver program to test the above function.
    static public void Main (){

        int []a = { 4, 3, 2 };
        int n = a.Length;

        Console.WriteLine(cost(a, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find minimum cost to
// reduce array size to 1,

// function to calculate
// the minimum cost
function cost($a, $n)
{

    // Minimum cost is n-1
    // multiplied with
    // minimum element.
    return ($n - 1) * (min($a));
}

    // Driver Code
    $a = array(4, 3, 2);
    $n = count($a);
    echo cost($a, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find minimum cost
// to reduce array size to 1,

    // function to calculate the
    // minimum cost
    function cost(a, n)
    {
        let min = a[0];

        // find the minimum using
        // for loop
        for(let i = 1; i< a.length; i++)
        {
            if (a[i] < min)
                min = a[i];
        }

        // Minimum cost is n-1 multiplied
        // with minimum element.
        return (n - 1) * min;
    }

// Driver code   

        let a = [ 4, 3, 2 ];
        let n = a.length;

        document.write(cost(a, n));

</script>
```

**输出:**

```
4
```

**时间复杂度** : O(n)
本文由 [**奋斗者**](https://www.facebook.com/raja.vikramaditya.7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。