# 使所有数组元素相等所需的最小运算

> 原文:[https://www . geeksforgeeks . org/minimum-operations-要求使所有数组元素相等/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-all-the-array-elements-equal/)

给定一个由整数 **n** 和整数 **k** 组成的数组 **arr[]** 。任务是计算使所有数组元素相等所需的给定操作的最小次数。在一次操作中，数组的第 **k <sup>个</sup>** 元素被追加到数组的末尾，数组的第一个元素被删除(数组的大小保持不变)。如果该操作不能使数组元素相等，则打印 **-1** ，否则打印所需的最小操作数。
**示例:**

> **输入:** arr[] = {2，1，1，1，1}，k = 3
> **输出:** 1
> 应用运算第 1 次
> 数组中的第 3 个元素是 1 我们将其追加到数组的末尾，得到 arr[] = {2，1，1，1，1，1，1}
> 然后删除第 1 个元素，得到 arr[] = {1，1，1，1，1}
> **输入:** arr[] = {1，1

**方法:**每次操作时，首先将 **k <sup>第</sup>T5】个元素复制到最后，然后复制初始序列中的 **(k + 1) <sup>第</sup>** 个元素，然后再复制 **(k + 2) <sup>第</sup>** 个元素，依此类推。因此，当且仅当从第 **k <sup>个</sup>** 元素开始的数组中的所有元素相等时，所有元素将变得相等。现在也很明显，它所需要的操作数等于最后一个不等于初始序列
的 **n <sup>第</sup>个**元素的数的索引。下面是上述方法的实现:** 

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>

using namespace std;

    // Function to return the minimum number of
    // given operation required to make all the
    // array elements equal
    void minOperation(int n, int k, int a[])
    {

        // Check if all the elements
        // from kth index to last are equal
        for (int i = k; i < n; i++)
        {
            if(a[i] != a[k - 1])
                cout << (-1)<<endl;
        }

        // Finding the 1st element which is
        // not equal to the kth element
        for (int i = k - 2; i > -1; i--)
        {
            if(a[i] != a[k - 1])
                cout << (i + 1) << endl;
        }
    }

    // Driver code
    int main ()
    {
        int n = 5;
        int k = 3;
        int a[] = {2, 1, 1, 1, 1};

        minOperation(n, k, a);
    }

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;

class GFG
{

    // Function to return the minimum number of
    // given operation required to make all the
    // array elements equal
    static void minOperation(int n, int k, int a[])
    {

        // Check if all the elements
        // from kth index to last are equal
        for (int i = k; i < n; i++)
        {
            if(a[i] != a[k - 1])
                System.out.println(-1);
        }

        // Finding the 1st element which is
        // not equal to the kth element
        for (int i = k - 2; i > -1; i--)
        {
            if(a[i] != a[k - 1])
                System.out.println(i + 1);
        }
    }

    // Driver code
    public static void main (String[] args)
    {

        int n = 5;
        int k = 3;
        int a[] = {2, 1, 1, 1, 1};

        minOperation(n, k, a);
    }
}

// This code is contributed by ajit.
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to return the minimum number of given operation
# required to make all the array elements equal
def minOperation(n, k, a):

    # Check if all the elements
    # from kth index to last are equal
    for i in range(k, n):
        if(a[i] != a[k - 1]):
            return -1

    # Finding the 1st element
    # which is not equal to the kth element
    for i in range(k-2, -1, -1):
        if(a[i] != a[k-1]):
            return i + 1

# Driver code
n = 5
k = 3
a = [2, 1, 1, 1, 1]
print(minOperation(n, k, a))
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

    // Function to return the minimum number of
    // given operation required to make all the
    // array elements equal
    static void minOperation(int n, int k, int []a)
    {

        // Check if all the elements
        // from kth index to last are equal
        for (int i = k; i < n; i++)
        {
            if(a[i] != a[k - 1])
                Console.WriteLine(-1);

        }

        // Finding the 1st element which is
        // not equal to the kth element
        for (int i = k - 2; i > -1; i--)
        {
            if(a[i] != a[k - 1])
                Console.WriteLine(i + 1);
        }
    }

    // Driver code
    static public void Main ()
    {
        int n = 5;
        int k = 3;
        int []a = {2, 1, 1, 1, 1};

        minOperation(n, k, a);
    }
}

// This code is contributed by Ryuga
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php implementation of the approach

// Function to return the minimum number of
// given operation required to make all the
// array elements equal
function minOperation($n, $k, &$a)
{

    // Check if all the elements
    // from kth index to last are equal
    for ($i = $k; $i < $n; $i++)
    {
        if($a[$i] != $a[$k - 1])
            return -1;
    }

    // Finding the 1st element which is
    // not equal to the kth element
    for ($i = $k - 2; $i > -1; $i--)
    {
        if($a[$i] != $a[$k - 1])
            return ($i + 1);
    }
}

// Driver code
$n = 5;
$k = 3;
$a = array(2, 1, 1, 1, 1);
echo(minOperation($n, $k, $a));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// javascript implementation of the above approach

    // Function to return the minimum number of
    // given operation required to make all the
    // array elements equal
    function minOperation(n, k, a)
    {

        // Check if all the elements
        // from kth index to last are equal
        for (i = k; i < n; i++)
        {
            if (a[i] != a[k - 1])
                document.write(-1);
        }

        // Finding the 1st element which is
        // not equal to the kth element
        for (i = k - 2; i > -1; i--)
        {
            if (a[i] != a[k - 1])
                document.write(i + 1);
        }
    }

    // Driver code
        var n = 5;
        var k = 3;
        var a = [ 2, 1, 1, 1, 1 ];

        minOperation(n, k, a);

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
1
```