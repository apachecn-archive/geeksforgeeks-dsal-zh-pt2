# 重复减法使所有元素相同后求最大数组和

> 原文:[https://www . geesforgeks . org/find-max-sum-making-elements-repeated-减法/](https://www.geeksforgeeks.org/find-maximum-sum-making-elements-repeated-subtraction/)

给定一个由 **n 个**元素组成的数组，找出所有元素的最大可能和，使所有元素相等。唯一允许的操作是选择任意两个元素，并用两者的绝对差替换其中较大的一个。
示例:

```
Input : 9 12 3 6 
Output : 12
Explanation :
9 12 3 6
replace a2 = 12 with a2-a4 = 12 - 6 => 6
i.e, 9 6 3 6

replace a4 = 6 with a4-a3 = 6 - 3 => 3
i.e, 9 6 3 3

replace a1 = 9 with a1-a2 = 9 - 6 => 3
i.e, 3 6 3 3

replace a2 = 6 with a2-a4 = 6 - 3 => 3
i,e. 3 3 3 3

Now, at this point we have all the elements equal, 
hence we can return our answer from here.

Input : 4 8 6 10
Output : 8
Explanation :
Resultant array formed will be:
4 8 6 10
replace a4 = 10 with a4-a1 = 10 - 4 => 6
i.e, 4 8 6 6

replace a3 = 6 with a3-a1 = 6 - 4 => 2
i.e, 4 8 2 6

replace a2 = 8 with a2-a4 = 8 - 6 => 2
i.e, 4 2 2 6

replace a4 = 6 with a4-a1 = 6 - 4 => 2
i,e. 4 2 2 2

replace a1 = 4 with a1-a2 = 4 - 2 => 2
i,e. 2 2 2 2

Now, at this point we have all the elements equal, 
hence we can return our answer from here.
```

通过分析给定的操作，即

```
    ai = ai - aj          where ai > aj
```

我们看到这类似于通过[欧几里得算法](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/)找到 GCD，如下所示:

```
   GCD(a, b) = GCD(b, a - b)
```

同样，重排的顺序也不重要，我们可以从任意两个元素开始，用两个元素的绝对差代替较大的值，并在它们之间重复，直到差为零[两个元素相同]。也就是取出任意两个数的 GCD。这样做的原因是，GCD 是关联的和可交换的。
所以想法是一次取所有元素的 GCD，用这个结果替换所有元素。

## C++

```
// Maximum possible sum of array after repeated
// subtraction operation.
#include<bits/stdc++.h>
using namespace std;

int GCD(int a, int b)
{
    if (b == 0)
        return a;
    return GCD(b, a % b);
}

int findMaxSumUtil(int arr[], int n)
{
    int finalGCD = arr[0];
    for (int i = 1; i < n; i++)
        finalGCD = GCD(arr[i], finalGCD);

    return finalGCD;
}

// This function basically calls findMaxSumUtil()
// to find GCD of all array elements, then it returns
// GCD * (Size of array)
int findMaxSum(int arr[], int n)
{
    int maxElement = findMaxSumUtil(arr, n);
    return (maxElement * n);
}

// Driver code
int main()
{
    int arr[] = {8, 20, 12, 36};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << findMaxSum(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Maximum possible sum of array after repeated
// subtraction operation.

import java.io.*;

class GFG {

    static int GCD(int a, int b)
    {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    static int findMaxSumUtil(int arr[], int n)
    {
        int finalGCD = arr[0];
        for (int i = 1; i < n; i++)
            finalGCD = GCD(arr[i], finalGCD);

        return finalGCD;
    }

    // This function basically calls
    // findMaxSumUtil() to find GCD of all
    // array elements, then it returns
    // GCD * (Size of array)
    static int findMaxSum(int arr[], int n)
    {
        int maxElement = findMaxSumUtil(arr, n);
        return (maxElement * n);
    }

    // Driver code
    public static void main (String[] args) {

        int arr[] = {8, 20, 12, 36};
        int n = arr.length;

        System.out.println(findMaxSum(arr, n));
    }
}

//This code is contributed by vt_m.
```

## 蟒蛇 3

```
# Maximum possible sum of array after
# repeated subtraction operation.

def GCD(a, b):

    if (b == 0): return a
    return GCD(b, a % b)

def findMaxSumUtil(arr, n):

    finalGCD = arr[0]
    for i in range(1, n):
        finalGCD = GCD(arr[i], finalGCD)

    return finalGCD

# This function basically calls
# findMaxSumUtil() to find GCD of
# all array elements, then it returns
# GCD * (Size of array)
def findMaxSum(arr, n):

    maxElement = findMaxSumUtil(arr, n)
    return (maxElement * n)

# Driver code
arr = [8, 20, 12, 36]
n = len(arr)
print(findMaxSum(arr, n))

# This code is contributed by Anant Agarwal.
```

## C#

```
// C# Code for Maximum possible sum of array
// after repeated subtraction operation.
using System;

class GFG {

    static int GCD(int a, int b)
    {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    static int findMaxSumUtil(int []arr, int n)
    {
        int finalGCD = arr[0];
        for (int i = 1; i < n; i++)
            finalGCD = GCD(arr[i], finalGCD);

        return finalGCD;
    }

    // This function basically calls
    // findMaxSumUtil() to find GCD of all
    // array elements, then it returns
    // GCD * (Size of array)
    static int findMaxSum(int []arr, int n)
    {
        int maxElement = findMaxSumUtil(arr, n);
        return (maxElement * n);
    }

    // Driver code
    public static void Main () {

        int []arr = {8, 20, 12, 36};
        int n = arr.Length;

        Console.WriteLine(findMaxSum(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find Maximum possible
// sum of array after repeated
// subtraction operation.

function GCD($a, $b)
{
    if ($b == 0)
        return $a;
    return GCD($b, $a % $b);
}

function findMaxSumUtil( $arr, $n)
{
    $finalGCD = $arr[0];
    for ( $i = 1; $i < $n; $i++)
        $finalGCD = GCD($arr[$i], $finalGCD);

    return $finalGCD;
}

// This function basically
// calls findMaxSumUtil()
// to find GCD of all array
// elements, then it returns
// GCD * (Size of array)
function findMaxSum( $arr, $n)
{
    $maxElement = findMaxSumUtil($arr, $n);
    return ($maxElement * $n);
}

    // Driver Code
    $arr = array(8, 20, 12, 36);
    $n = count($arr);
    echo findMaxSum($arr, $n) ;

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
    // Javascript Code for Maximum possible sum of array
    // after repeated subtraction operation.

    function GCD(a, b)
    {
        if (b == 0)
            return a;
        return GCD(b, a % b);
    }

    function findMaxSumUtil(arr, n)
    {
        let finalGCD = arr[0];
        for (let i = 1; i < n; i++)
            finalGCD = GCD(arr[i], finalGCD);

        return finalGCD;
    }

    // This function basically calls
    // findMaxSumUtil() to find GCD of all
    // array elements, then it returns
    // GCD * (Size of array)
    function findMaxSum(arr, n)
    {
        let maxElement = findMaxSumUtil(arr, n);
        return (maxElement * n);
    }

    let arr = [8, 20, 12, 36];
    let n = arr.length;

    document.write(findMaxSum(arr, n));

</script>
```

输出:

```
 16
```

本文由 [Shubham Gupta](https://www.facebook.com/Shubh1307) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。