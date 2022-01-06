# 求“k”，使其与每个数组元素的模相同

> 原文:[https://www . geeksforgeeks . org/find-k-module-array-element/](https://www.geeksforgeeks.org/finding-k-modulus-array-element/)

给定 n 个整数的数组。我们需要找到所有这样的“k”

```
arr[0] % k = arr[1] % k = ....... = arr[n-1] % k 
```

**例:**

```
Input  : arr[] = {6, 38, 34}
Output : 1 2 4
        6%1 = 38%1 = 34%1 = 0
        6%2 = 38%2 = 34%2 = 0
        6%4 = 38%4 = 34%2 = 2

Input  : arr[] = {3, 2}
Output : 1
```

假设数组只包含两个元素 a 和 b (b>a)。所以我们可以写出 **b = a + d** ，其中 d 是正整数，而‘k’是一个数，这样 b%k = a%k。

```
(a + d)%k = a%k
a%k + d%k = a%k 
d%k = 0
```

现在我们从上面的计算中得到了‘k’应该是两个数差的除数。
现在当我们有一个整数数组时我们要做什么

1.  找出数组的最大和最小元素之间的差异
2.  找出所有的除数。
3.  步骤 3:对于每个除数，检查 arr[I]%除数(d)是否相同。如果是一样的，就打印出来。

## C++

```
// C++ implementation of finding all k
// such that arr[i]%k is same for each i
#include<bits/stdc++.h>
using namespace std;

// Prints all k such that arr[i]%k is same for all i
void printEqualModNumbers (int arr[], int n)
{
    // sort the numbers
    sort(arr, arr + n);

    // max difference will be the difference between
    // first and last element of sorted array
    int d = arr[n-1] - arr[0];

    // Case when all the array elements are same
    if(d==0){
        cout<<"Infinite solution";
        return;
    }

    // Find all divisors of d and store in
    // a vector v[]
    vector <int> v;
    for (int i=1; i*i<=d; i++)
    {
        if (d%i == 0)
        {
            v.push_back(i);
            if (i != d/i)
                v.push_back(d/i);
        }
    }

    // check for each v[i] if its modulus with
    // each array element is same or not
    for (int i=0; i<v.size(); i++)
    {
        int temp = arr[0]%v[i];

        // checking for each array element if
        // its modulus with k is equal to k or not
        int j;
        for (j=1; j<n; j++)
            if (arr[j] % v[i] != temp)
                break;

        // if check is true print v[i]
        if (j == n)
            cout << v[i] <<" ";
    }
}

// Driver function
int main()
{
    int arr[] = {38, 6, 34};
    int n = sizeof(arr)/sizeof(arr[0]);
    printEqualModNumbers(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//  Java implementation of finding all k
// such that arr[i]%k is same for each i

import java.util.Arrays;
import java.util.Vector;

class Test
{
    // Prints all k such that arr[i]%k is same for all i
    static void printEqualModNumbers (int arr[], int n)
    {
        // sort the numbers
        Arrays.sort(arr);

        // max difference will be the difference between
        // first and last element of sorted array
        int d = arr[n-1] - arr[0];
        // Case when all the array elements are same
        if(d==0){
            System.out.println("Infinite solution");
            return;
        }
        // Find all divisors of d and store in
        // a vector v[]
        Vector<Integer> v = new Vector<>();
        for (int i=1; i*i<=d; i++)
        {
            if (d%i == 0)
            {
                v.add(i);
                if (i != d/i)
                    v.add(d/i);
            }
        }

        // check for each v[i] if its modulus with
        // each array element is same or not
        for (int i=0; i<v.size(); i++)
        {
            int temp = arr[0]%v.get(i);

            // checking for each array element if
            // its modulus with k is equal to k or not
            int j;
            for (j=1; j<n; j++)
                if (arr[j] % v.get(i) != temp)
                    break;

            // if check is true print v[i]
            if (j == n)
                System.out.print(v.get(i) + " ");
        }
    }

    // Driver method
    public static void main(String args[])
    {
        int arr[] = {38, 6, 34};

        printEqualModNumbers(arr, arr.length);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of finding all k
# such that arr[i]%k is same for each i

# Prints all k such that arr[i]%k is
# same for all i
def printEqualModNumbers(arr, n):

    # sort the numbers
    arr.sort();

    # max difference will be the difference
    # between first and last element of
    # sorted array
    d = arr[n - 1] - arr[0];
    // Case when all the array elements are same
    if(d==0):
        print("Infinite solution")
        return

    # Find all divisors of d and store
    # in a vector v[]
    v = [];
    i = 1;
    while (i * i <= d):
        if (d % i == 0):
                v.append(i);
                if (i != d / i):
                    v.append(d / i);
        i += 1;

    # check for each v[i] if its modulus with
    # each array element is same or not
    for i in range(len(v)):
        temp = arr[0] % v[i];

        # checking for each array element if
        # its modulus with k is equal to k or not
        j = 1;
        while (j < n):
            if (arr[j] % v[i] != temp):
                break;
            j += 1;

        # if check is true print v[i]
        if (j == n):
            print(v[i], end = " ");

# Driver Code
arr = [38, 6, 34];
printEqualModNumbers(arr, len(arr));

# This code is contributed by mits
```

## C#

```
// C# implementation of finding all k
// such that arr[i]%k is same for each i
using System;
using System.Collections;
class Test
{
    // Prints all k such that arr[i]%k is same for all i
    static void printEqualModNumbers (int []arr, int n)
    {
        // sort the numbers
        Array.Sort(arr);

        // max difference will be the difference between
        // first and last element of sorted array
        int d = arr[n-1] - arr[0];
        // Case when all the array elements are same
        if(d==0){
            Console.write("Infinite solution");
            return;
        }
        // Find all divisors of d and store in
        // a vector v[]
        ArrayList v = new ArrayList();
        for (int i=1; i*i<=d; i++)
        {
            if (d%i == 0)
            {
                v.Add(i);
                if (i != d/i)
                    v.Add(d/i);
            }
        }

        // check for each v[i] if its modulus with
        // each array element is same or not
        for (int i=0; i<v.Count; i++)
        {
            int temp = arr[0]%(int)v[i];

            // checking for each array element if
            // its modulus with k is equal to k or not
            int j;
            for (j=1; j<n; j++)
                if (arr[j] % (int)v[i] != temp)
                    break;

            // if check is true print v[i]
            if (j == n)
                Console.Write(v[i] + " ");
        }
    }

    // Driver method
    public static void Main()
    {
        int []arr = {38, 6, 34};

        printEqualModNumbers(arr, arr.Length);
    }
}
// This code is contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of finding all k
// such that arr[i]%k is same for each i

    // Prints all k such that arr[i]%k is same for all i
    function printEqualModNumbers ($arr, $n)
    {
        // sort the numbers
        sort($arr);

        // max difference will be the difference between
        // first and last element of sorted array
        $d = $arr[$n-1] - $arr[0];
        // Case when all the array elements are same
        if(d==0){
            print("Infinite solution");
            return;
        }
        // Find all divisors of d and store in
        // a vector v[]
        $v = array();
        for ($i=1; $i*$i<=$d; $i++)
        {
            if ($d%$i == 0)
            {
                array_push($v,$i);
                if ($i != $d/$i)
                    array_push($v,$d/$i);
            }
        }

        // check for each v[i] if its modulus with
        // each array element is same or not
        for ($i=0; $i<count($v); $i++)
        {
            $temp = $arr[0]%$v[$i];

            // checking for each array element if
            // its modulus with k is equal to k or not
            $j=1;
            for (; $j<$n; $j++)
                if ($arr[$j] % $v[$i] != $temp)
                    break;

            // if check is true print v[i]
            if ($j == $n)
                print($v[$i]." ");
        }
    }

    // Driver method

        $arr = array(38, 6, 34);

        printEqualModNumbers($arr, count($arr));

// This code is contributed by mits
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of finding all k
// such that arr[i]%k is same for each i

    // Prints all k such that arr[i]%k is same for all i
    function printEqualModNumbers (arr, n)
    {
        // sort the numbers
        arr.sort((a, b) => a - b);

        // max difference will be the difference between
        // first and last element of sorted array
        d = arr[n-1] - arr[0];
        // Case when all the array elements are same
        if(d==0){
            document.write("Infinite solution");
            return;
        }
        // Find all divisors of d and store in
        // a vector v[]
        v = new Array();
        for (i=1; i*i<=d; i++)
        {
            if (d%i == 0)
            {
                v.push(i);
                if (i != d/i)
                    v.push(d/i);
            }
        }

        // check for each v[i] if its modulus with
        // each array element is same or not
        for (i=0; i< v.length; i++)
        {
            temp = arr[0]%v[i];

            // checking for each array element if
            // its modulus with k is equal to k or not
            j=1;
            for (; j<n; j++)
                if (arr[j] % v[i] != temp)
                    break;

            // if check is true print v[i]
            if (j == n)
                document.write(v[i] + " ");
        }
    }

    // Driver method

        let arr = new Array(38, 6, 34);

        printEqualModNumbers(arr, arr.length);

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
1 2 4 
```

本文由 **Ayush Jha** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。