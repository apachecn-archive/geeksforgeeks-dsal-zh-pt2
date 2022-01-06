# 将数组前缀乘以-1

最大化数组的和

> 原文:[https://www . geeksforgeeks . org/通过将数组前缀乘以 1 来最大化数组总和/](https://www.geeksforgeeks.org/maximize-the-sum-of-array-by-multiplying-prefix-of-array-with-1/)

给定一个元素数组“arr”，任务是在执行以下操作后最大化该数组的元素总和:
您可以取“arr”的任何前缀，并将前缀的每个元素乘以“-1”。
在第一行中，打印最大化总和，然后在下一行中，打印选择前缀序列的索引。
**例:**

```
Input: arr = {1, -2, -3, 4}
Output: 10
2 1 3 2
Flip the prefix till 2nd element then the sequence is -1  2 -3  4
Flip the prefix till 1st element then the sequence is  1  2 -3  4
Flip the prefix till 3rd element then the sequence is -1 -2  3  4
Flip the prefix till 2nd element then the sequence is  1  2  3  4
And, the final maximised sum is 10

Input: arr = {1, 2, 3, 4}
Output: 10
As, all the elements are already positive.
```

**方法:**最大和总是![\small \sum \left | A_i \right |    ](img/67a11a1ddd6fe8329a44e2d8e4885216.png "Rendered by QuickLaTeX.com")，因为给定的操作可以将数组的所有数字从负数变为正数。

*   从左到右遍历数组，如果索引“I”处的元素为负，则选择“I”作为前缀数组的结束索引，并将每个元素乘以“-1”。
*   由于上一步的操作，数组中索引“I”之前的所有元素都必须是负数。因此，取以索引“i-1”结尾的前缀数组，再次应用相同的操作，将所有元素都改为正数。
*   重复以上步骤，直到遍历完整个数组，并打印所有元素的总和以及最后所选前缀数组的所有结束索引。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

void maxSum(int *a, int n)
{

    vector<int> l;

    // To store sum
    int s = 0;

    // To store ending indices
    // of the chosen prefix array vect
    for (int i = 0; i < n; i++)
    {

        // Adding the absolute
        // value of a[i]
        s += abs(a[i]);
        if (a[i] >= 0)
            continue;

        // If i == 0 then there is no index
        // to be flipped in (i-1) position
        if (i == 0)
            l.push_back(i + 1);
        else
        {
            l.push_back(i + 1);
            l.push_back(i);
        }

    }

    // print the maximized sum
    cout << s << endl;

    // print the ending indices
    // of the chosen prefix arrays
    for (int i = 0; i < l.size(); i++)
    cout << l[i] << " ";

}

// Driver Code   
int main()
{
    int n = 4;
    int a[] = {1, -2, -3, 4};
    maxSum(a, n);
}

// This code is contributed by
// Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static void maxSum(int []a, int n)
{
    Vector<Integer> l = new Vector<Integer>();

    // To store sum
    int s = 0;

    // To store ending indices
    // of the chosen prefix array vect
    for (int i = 0; i < n; i++)
    {

        // Adding the absolute
        // value of a[i]
        s += Math.abs(a[i]);
        if (a[i] >= 0)
            continue;

        // If i == 0 then there is no index
        // to be flipped in (i-1) position
        if (i == 0)
            l.add(i + 1);
        else
        {
            l.add(i + 1);
            l.add(i);
        }
    }

    // print the maximised sum
    System.out.println(s);

    // print the ending indices
    // of the chosen prefix arrays
    for (int i = 0; i < l.size(); i++)
    System.out.print(l.get(i) + " ");
}

// Driver Code
public static void main(String[] args)
{
    int n = 4;
    int a[] = {1, -2, -3, 4};
    maxSum(a, n);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python implementation of the approach
def maxSum(arr, n):
    # To store sum
    s = 0

    # To store ending indices
    # of the chosen prefix arrays
    l = []
    for i in range(len(a)):

        # Adding the absolute
        # value of a[i]
        s += abs(a[i])
        if (a[i] >= 0):
            continue

        # If i == 0 then there is
        # no index to be flipped
        # in (i-1) position
        if (i == 0):
            l.append(i + 1)
        else:
            l.append(i + 1)
            l.append(i)

    # print the
    # maximised sum
    print(s)

    # print the ending indices
    # of the chosen prefix arrays
    print(*l)

n = 4
a = [1, -2, -3, 4]
maxSum(a, n)
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static void maxSum(int []a, int n)
{
    List<int> l = new List<int>();

    // To store sum
    int s = 0;

    // To store ending indices
    // of the chosen prefix array vect
    for (int i = 0; i < n; i++)
    {

        // Adding the absolute
        // value of a[i]
        s += Math.Abs(a[i]);
        if (a[i] >= 0)
            continue;

        // If i == 0 then there is no index
        // to be flipped in (i-1) position
        if (i == 0)
            l.Add(i + 1);
        else
        {
            l.Add(i + 1);
            l.Add(i);
        }
    }

    // print the maximised sum
    Console.WriteLine(s);

    // print the ending indices
    // of the chosen prefix arrays
    for (int i = 0; i < l.Count; i++)
    Console.Write(l[i] + " ");
}

// Driver Code
public static void Main(String[] args)
{
    int n = 4;
    int []a = {1, -2, -3, 4};
    maxSum(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach
function maxSum($a, $n)
{
    // To store sum
    $s = 0;

    // To store ending indices
    // of the chosen prefix arrays
    $l = array();
    for ($i = 0; $i < count($a); $i++)
    {

        // Adding the absolute
        // value of a[i]
        $s += abs($a[$i]);
        if ($a[$i] >= 0)
            continue;

        // If i == 0 then there is
        // no index to be flipped
        // in (i-1) position
        if ($i == 0)
            array_push($l, $i + 1);
        else
        {
            array_push($l, $i + 1);
            array_push($l, $i);
        }
    }

    // print the
    // maximised sum
    echo $s . "\n";

    // print the ending indices
    // of the chosen prefix arrays
    for($i = 0; $i < count($l); $i++)
    echo $l[$i] . " ";
}

// Driver Code
$n = 4;
$a = array(1, -2, -3, 4);
maxSum($a, $n);

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

    function maxSum(a, n)
{
    let l = [];

    // To store sum
    let s = 0;

    // To store ending indices
    // of the chosen prefix array vect
    for (let i = 0; i < n; i++)
    {

        // Adding the absolute
        // value of a[i]
        s += Math.abs(a[i]);
        if (a[i] >= 0)
            continue;

        // If i == 0 then there is no index
        // to be flipped in (i-1) position
        if (i == 0)
            l.push(i + 1);
        else
        {
            l.push(i + 1);
            l.push(i);
        }
    }

    // print the maximised sum
    document.write(s + "<br/>");

    // print the ending indices
    // of the chosen prefix arrays
    for (let i = 0; i < l.length; i++)
    document.write(l[i] + " ");
}

// driver code

    let n = 4;
    let a = [1, -2, -3, 4];
    maxSum(a, n);

</script>
```

**Output:** 

```
10
2 1 3 2
```