# 找到一个数组中每隔一个元素出现两次的元素

> 原文:[https://www . geeksforgeeks . org/find-element-出现-array-ever-element-出现-两次/](https://www.geeksforgeeks.org/find-element-appears-array-every-element-appears-twice/)

给定一个整数数组。所有数字都出现两次，只有一个数字出现一次。在 O(n)时间&常数额外空间中找到数字。

**示例:**

```
Input:  ar[] = {7, 3, 5, 4, 5, 3, 4}
Output: 7 
```

一种解决方案是检查每个元素是否出现一次。一旦找到具有单个匹配项的元素，就返回它。该解的时间复杂度为 O(n <sup>2</sup> )。

更好的解决方案是使用哈希。
1)遍历所有元素，并将其放入哈希表中。元素用作键，出现次数用作哈希表中的值。
2)再次遍历数组，打印哈希表中计数为 1 的元素。
此解决方案在 O(n)时间内有效，但需要额外的空间。
最好的解决办法是用 XOR。所有数组元素的异或运算给出了一次出现的数字。这个想法基于以下两个事实。
一个数与自身的异或是 0。
b)一个数与 0 的异或就是数本身。

```
Let us consider the above example.  
Let ^ be xor operator as in C and C++.

res = 7 ^ 3 ^ 5 ^ 4 ^ 5 ^ 3 ^ 4

Since XOR is associative and commutative, above 
expression can be written as:
res = 7 ^ (3 ^ 3) ^ (4 ^ 4) ^ (5 ^ 5)  
    = 7 ^ 0 ^ 0 ^ 0
    = 7 ^ 0
    = 7 
```

下面是上述算法的实现。

## C++

```
// C++ program to find the array
// element that appears only once
#include <iostream>
using namespace std;

int findSingle(int ar[], int ar_size)
    {
        // Do XOR of all elements and return
        int res = ar[0];
        for (int i = 1; i < ar_size; i++)
            res = res ^ ar[i];

        return res;
    }

// Driver code
int main()
    {
        int ar[] = {2, 3, 5, 4, 5, 3, 4};
        int n = sizeof(ar) / sizeof(ar[0]);
        cout << "Element occurring once is "
             << findSingle(ar, n);
        return 0;
    }
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the array
// element that appears only once
class MaxSum
{
    // Return the maximum Sum of difference
    // between consecutive elements.
    static int findSingle(int ar[], int ar_size)
    {
        // Do XOR of all elements and return
        int res = ar[0];
        for (int i = 1; i < ar_size; i++)
            res = res ^ ar[i];

        return res;
    }

    // Driver code
    public static void main (String[] args)
    {
        int ar[] = {2, 3, 5, 4, 5, 3, 4};
        int n = ar.length;
        System.out.println("Element occurring once is " +
                            findSingle(ar, n) + " ");
    }
}
// This code is contributed by Prakriti Gupta
```

## 蟒蛇 3

```
# function to find the once
# appearing element in array
def findSingle( ar, n):

    res = ar[0]

    # Do XOR of all elements and return
    for i in range(1,n):
        res = res ^ ar[i]

    return res

# Driver code
ar = [2, 3, 5, 4, 5, 3, 4]
print "Element occurring once is", findSingle(ar, len(ar))

# This code is contributed by __Devesh Agrawal__
```

## C#

```
// C# program to find the array
// element that appears only once
using System;

class GFG
{
    // Return the maximum Sum of difference
    // between consecutive elements.
    static int findSingle(int []ar, int ar_size)
    {
        // Do XOR of all elements and return
        int res = ar[0];
        for (int i = 1; i < ar_size; i++)
            res = res ^ ar[i];

        return res;
    }

    // Driver code
    public static void Main ()
    {
        int []ar = {2, 3, 5, 4, 5, 3, 4};
        int n = ar.Length;
        Console.Write("Element occurring once is " +
                            findSingle(ar, n) + " ");
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the array
// element that appears only once

function findSingle($ar, $ar_size)
    {

        // Do XOR of all
        // elements and return
        $res = $ar[0];
        for ($i = 1; $i < $ar_size; $i++)
            $res = $res ^ $ar[$i];

        return $res;
    }

    // Driver code
    $ar = array(2, 3, 5, 4, 5, 3, 4);
    $n = count($ar);
    echo "Element occurring once is "
         , findSingle($ar, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find the array
// element that appears only once

function findSingle(ar, ar_size)
    {
        // Do XOR of all elements and return
        let res = ar[0];
        for (let i = 1; i < ar_size; i++)
            res = res ^ ar[i];

        return res;
    }

// Driver code 
        let ar = [2, 3, 5, 4, 5, 3, 4];
        let n = ar.length;
        document.write("Element occurring once is "
            + findSingle(ar, n));

// This code is contributed by Surbhi Tyagi

</script>
```

**输出:**

```
Element occurring once is 2
```

该解决方案的时间复杂度为 O(n)，需要 O(1)个额外空间。

**另一种方法:**
这不是一种有效的方法，而只是获得预期结果的另一种方法。如果我们将每个数字加一次，然后将总和乘以 2，我们将得到数组中每个元素总和的两倍。然后我们将从 twice_sum 中减去整个数组的和，得到所需的数字(在数组中出现一次)。
数组[] : [a，a，b，b，c，c，d]
数学方程= 2 *(a+b+ c+d)–(a+a+b+ b+ c+c+d)

更简单的话:**2 *(sum _ of _ array _ 不带 _ duplicates)–(sum _ of _ array)**

```
let arr[] = {7, 3, 5, 4, 5, 3, 4}
Required no = 2*(sum_of_array_without_duplicates) - (sum_of_array)
            = 2*(7 + 3 + 5 + 4) - (7 + 3 + 5 + 4 + 5 + 3 + 4) 
            = 2*     19         -      31 
            = 38 - 31
            = 7 (required answer)
```

因为我们知道集合不包含任何重复的元素，我们将在这里使用 [*集合*](https://www.geeksforgeeks.org/sets-in-python/) 。

下面是上述方法的实现:

## C++

```
// C++ program to find
// element that appears once
#include <bits/stdc++.h>

using namespace std;

// function which find number
int singleNumber(int nums[],int n)
{
    map<int,int> m;
    long sum1 = 0,sum2 = 0;

    for(int i = 0; i < n; i++)
    {
        if(m[nums[i]] == 0)
        {
            sum1 += nums[i];
            m[nums[i]]++;
        }
        sum2 += nums[i];
    }

    // applying the formula.
    return 2 * (sum1) - sum2;
}

// Driver code
int main()
{
    int a[] = {2, 3, 5, 4, 5, 3, 4};
    int n = 7;
    cout << singleNumber(a,n) << "\n";

    int b[] = {15, 18, 16, 18, 16, 15, 89};

    cout << singleNumber(b,n);
    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// element that appears once
import java.io.*;
import java.util.*;

class GFG
{

    // function which find number
    static int singleNumber(int[] nums, int n)
    {
        HashMap<Integer, Integer> m = new HashMap<>();
        long sum1 = 0, sum2 = 0;
        for (int i = 0; i < n; i++)
        {
            if (!m.containsKey(nums[i]))
            {
                sum1 += nums[i];
                m.put(nums[i], 1);
            }
            sum2 += nums[i];
        }

        // applying the formula.
        return (int)(2 * (sum1) - sum2);
    }

    // Driver code
    public static void main(String args[])
    {
        int[] a = {2, 3, 5, 4, 5, 3, 4};
        int n = 7;
        System.out.println(singleNumber(a,n));

        int[] b = {15, 18, 16, 18, 16, 15, 89};
        System.out.println(singleNumber(b,n));
    }
}

// This code is contributed by rachana soma
```

## 蟒蛇 3

```
# Python3 program to find
# element that appears once

# function which find number
def singleNumber(nums):

# applying the formula.
    return 2 * sum(set(nums)) - sum(nums)

# driver code
a = [2, 3, 5, 4, 5, 3, 4]
print (int(singleNumber(a)))

a = [15, 18, 16, 18, 16, 15, 89]
print (int(singleNumber(a)))

# This code is contributed by "Abhishek Sharma 44"
```

## C#

```
// C# program to find
// element that appears once
using System;
using System.Collections.Generic;

class GFG
{

    // function which find number
    static int singleNumber(int[] nums, int n)
    {
        Dictionary<int,int> m = new Dictionary<int,int>();
        long sum1 = 0, sum2 = 0;
        for (int i = 0; i < n; i++)
        {
            if (!m.ContainsKey(nums[i]))
            {
                sum1 += nums[i];
                m.Add(nums[i], 1);
            }
            sum2 += nums[i];
        }

        // applying the formula.
        return (int)(2 * (sum1) - sum2);
    }

    // Driver code
    public static void Main(String []args)
    {
        int[] a = {2, 3, 5, 4, 5, 3, 4};
        int n = 7;
        Console.WriteLine(singleNumber(a,n));

        int[] b = {15, 18, 16, 18, 16, 15, 89};
        Console.WriteLine(singleNumber(b,n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// Javascript program to find
// element that appears once

    // function which find number
    function singleNumber(nums,n)
    {
        let m = new Map();
        let sum1 = 0, sum2 = 0;
        for (let i = 0; i < n; i++)
        {
            if (!m.has(nums[i]))
            {
                sum1 += nums[i];
                m.set(nums[i], 1);
            }
            sum2 += nums[i];
        }

        // applying the formula.
        return (2 * (sum1) - sum2);
    }

    // Driver code
    let a=[2, 3, 5, 4, 5, 3, 4];
    let n = 7;
    document.write(singleNumber(a,n)+"<br>");

    let b=[15, 18, 16, 18, 16, 15, 89];
    document.write(singleNumber(b,n));

    // This code is contributed by unknown2108

</script>
```

**输出:**

```
2
89
```

**另一种方法:**

这是在重复元素列表中查找单个元素的有效方法。在这种方法中，我们使用二分搜索法算法来找到重复元素列表中的单个元素。在此之前，我们需要确定数组是否排序。第一步是对数组进行排序，因为如果数组没有排序，二分搜索法算法就不起作用。

现在让我们来看看二分搜索法的实施方案:

有两个由数组中唯一一个元素创建的半部分，即左半部分和右半部分。现在，如果左半部分存在重复，那么左半部分的重复元素的第一个实例是偶数索引，第二个实例是奇数索引。左半部分的相反发生在右半部分(第一个实例是奇数索引，第二个实例是偶数索引)。现在应用二分搜索法算法:

1)解决方法是取数组的两个索引(低和高)，其中**低**指向数组索引 0，**高**指向数组索引(数组大小-2)。我们从(低+高)/2 的值中取出中间指数。

2)现在检查中间指数值是落在左半部分还是右半部分。如果它落在左半部分，那么我们将低值更改为中间+1，如果它落在右半部分，那么我们将高指数更改为中间 1。为了检验它，我们使用了一个逻辑(**if(arr[mid]==arr[mid^1】**)。如果 mid 是偶数，那么 mid^1 将是下一个奇数指数，如果条件得到满足，那么我们可以说我们在左边的指数，否则我们可以说我们在右边的一半。但是如果 mid 是一个奇数指数，那么 mid^1 会把我们带到 mid-1，这是之前的偶数指数，等于意味着我们在右半部分，否则在左半部分。

3)这样做是因为这个实现的目的是在重复列表中找到单个元素。只有当低值大于高值时才有可能，因为此时低将指向数组中包含单个元素的索引。

4)循环结束后，我们返回索引较低的值。

## C++

```
#include <bits/stdc++.h>
using namespace std;
int singleelement(int arr[], int n)
{
    int low = 0, high = n - 2;
    int mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if (arr[mid] == arr[mid ^ 1]) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return arr[low];
}
int main()
{
    int arr[] = { 2, 3, 5, 4, 5, 3, 4 };
    int size = sizeof(arr) / sizeof(arr[0]);
    sort(arr, arr + size);
    cout << singleelement(arr, size);
    return 0;
}

// This code is contributed by Sohom Das
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.Arrays;

class GFG{

static int singleelement(int arr[], int n)
{
    int low = 0, high = n - 2;
    int mid;

    while (low <= high)
    {
        mid = (low + high) / 2;
        if (arr[mid] == arr[mid ^ 1])
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return arr[low];
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 5, 4, 5, 3, 4 };
    int size = 7;
    Arrays.sort(arr);

    System.out.println(singleelement(arr, size));
}
}

// This code is contributed by dassohom5
```

## 蟒蛇 3

```
def singleelement(arr, n):
    low = 0
    high = n - 2
    mid = 0
    while (low <= high):
        mid = (low + high) // 2
        if (arr[mid] == arr[mid ^ 1]):
            low = mid + 1
        else:
            high = mid - 1

    return arr[low]

# Driver code
arr = [2, 3, 5, 4, 5, 3, 4]
size = len(arr)
arr.sort()
print(singleelement(arr, size))

# This code is contributed by shivanisingh
```

## C#

```
using System;
using System.Collections;

class GFG{

static int singleelement(int[] arr, int n)
{
    int low = 0, high = n - 2;
    int mid;

    while (low <= high)
    {
        mid = (low + high) / 2;

        if (arr[mid] == arr[mid ^ 1])
        {
            low = mid + 1;
        }
        else
        {
            high = mid - 1;
        }
    }
    return arr[low];
}

// Driver code
public static void Main()
{
    int[] arr = { 2, 3, 5, 4, 5, 3, 4 };
    int size = 7;
    Array.Sort(arr);

    Console.WriteLine(singleelement(arr, size));
}
}

// This code is contributed by dassohom5
```

## java 描述语言

```
<script>

function singleelement(arr,n)
{
    let low = 0, high = n - 2;
    let mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if (arr[mid] == arr[mid ^ 1]) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
        }
    }
    return arr[low];
}

    let arr = [ 2, 3, 5, 4, 5, 3, 4 ];
    let size = arr.length;
    document.write(singleelement(arr, size));

</script>
```

**输出:**

```
2
```

解的时间复杂度为 O(N log(N))+O(log N)，空间复杂度为 O(1)。

本文由**拉维**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息