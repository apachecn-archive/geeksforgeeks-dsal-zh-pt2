# 计算三胞胎，使 A[i] < B[j] < C[k]

> 原文:[https://www . geesforgeks . org/count-the-triples-so-ai-bj-CK/](https://www.geeksforgeeks.org/count-the-triplets-such-that-ai-bj-ck/)

给定三个数组 **A[]** 、 **B[]** 和**C[]****N**整数。任务是找到三胞胎 **(A[i]，B[j]，C[k])** 的计数，使得 **A[i] < B[j] < C[k]** 。

> **输入:** A[] = {1，5}，B[] = {2，4}，C[] = {3，6}
> **输出:** 3
> 三元组为(1，2，3)、(1，4，6)和(1，2，6)
> T7】输入: A[] = {1，1，1}，B[] = {2，2，2}，C[] = {3，3，3}
> **输出:**

****方法:**对所有给定的数组进行排序。现在在数组 **B[]** 中固定一个元素说 **X** ，对于每个 **X** ，答案将是数组 **A[]** 中小于 **X** 的元素个数与数组 **C[]** 中大于 **X** 的元素个数的乘积。我们可以使用修改后的[二分搜索法](https://www.geeksforgeeks.org/binary-search/)计算这两个计数。
以下是上述方法的实施:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of elements in arr[] which are
// less than the given key
int countLessThan(int arr[], int n, int key)
{
    int l = 0, r = n - 1;
    int index = -1;

    // Modified binary search
    while (l <= r) {
        int m = (l + r) / 2;

        if (arr[m] < key) {
            l = m + 1;
            index = m;
        }
        else {
            r = m - 1;
        }
    }

    return (index + 1);
}

// Function to return the count
// of elements in arr[] which are
// greater than the given key
int countGreaterThan(int arr[], int n, int key)
{
    int l = 0, r = n - 1;
    int index = -1;

    // Modified binary search
    while (l <= r) {
        int m = (l + r) / 2;

        if (arr[m] <= key) {
            l = m + 1;
        }
        else {
            r = m - 1;
            index = m;
        }
    }

    if (index == -1)
        return 0;
    return (n - index);
}

// Function to return the count
// of the required triplets
int countTriplets(int n, int* a, int* b, int* c)
{
    // Sort all three arrays
    sort(a, a + n);
    sort(b, b + n);
    sort(c, c + n);

    int count = 0;

    // Iterate for all the elements of array B
    for (int i = 0; i < n; ++i) {
        int current = b[i];
        int a_index = -1, c_index = -1;

        // Count of elements in A[]
        // which are less than the
        // chosen element from B[]
        int low = countLessThan(a, n, current);

        // Count of elements in C[]
        // which are greater than the
        // chosen element from B[]
        int high = countGreaterThan(c, n, current);

        // Update the count
        count += (low * high);
    }

    return count;
}

// Driver code
int main()
{
    int a[] = { 1, 5 };
    int b[] = { 2, 4 };
    int c[] = { 3, 6 };
    int size = sizeof(a) / sizeof(a[0]);

    cout << countTriplets(size, a, b, c);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count
    // of elements in arr[] which are
    // less than the given key
    static int countLessThan(int arr[], int n, int key)
    {
        int l = 0, r = n - 1;
        int index = -1;

        // Modified binary search
        while (l <= r)
        {
            int m = (l + r) / 2;

            if (arr[m] < key)
            {
                l = m + 1;
                index = m;
            }
            else
            {
                r = m - 1;
            }
        }

        return (index + 1);
    }

    // Function to return the count
    // of elements in arr[] which are
    // greater than the given key
    static int countGreaterThan(int arr[], int n, int key)
    {
        int l = 0, r = n - 1;
        int index = -1;

        // Modified binary search
        while (l <= r)
        {
            int m = (l + r) / 2;

            if (arr[m] <= key)
            {
                l = m + 1;
            }
            else
            {
                r = m - 1;
                index = m;
            }
        }

        if (index == -1)
            return 0;
        return (n - index);
    }

    // Function to return the count
    // of the required triplets
    static int countTriplets(int n, int a[], int b[], int c[])
    {
        // Sort all three arrays
        Arrays.sort(a) ;
        Arrays.sort(b);
        Arrays.sort(c);

        int count = 0;

        // Iterate for all the elements of array B
        for (int i = 0; i < n; ++i)
        {
            int current = b[i];

            // Count of elements in A[]
            // which are less than the
            // chosen element from B[]
            int low = countLessThan(a, n, current);

            // Count of elements in C[]
            // which are greater than the
            // chosen element from B[]
            int high = countGreaterThan(c, n, current);

            // Update the count
            count += (low * high);
        }

        return count;
    }

    // Driver code
    public static void main(String args[])
    {
        int a[] = { 1, 5 };
        int b[] = { 2, 4 };
        int c[] = { 3, 6 };
        int size = a.length;

        System.out.println(countTriplets(size, a, b, c));

    }
}
// This code is contributed by Arnab Kundu
```

## **蟒蛇 3**

```
# Python 3 implementation of the approach

# Function to return the count
# of elements in arr[] which are
# less than the given key
def countLessThan(arr, n, key):
    l = 0
    r = n - 1
    index = -1

    # Modified binary search
    while (l <= r):
        m = (l + r) // 2

        if (arr[m] < key) :
            l = m + 1
            index = m

        else :
            r = m - 1

    return (index + 1)

# Function to return the count
# of elements in arr[] which are
# greater than the given key
def countGreaterThan(arr, n, key):

    l = 0
    r = n - 1
    index = -1

    # Modified binary search
    while (l <= r) :
        m = (l + r) // 2

        if (arr[m] <= key) :
            l = m + 1
        else :
            r = m - 1
            index = m

    if (index == -1):
        return 0
    return (n - index)

# Function to return the count
# of the required triplets
def countTriplets(n, a, b, c):

    # Sort all three arrays
    a.sort
    b.sort()
    c.sort()

    count = 0

    # Iterate for all the elements of array B
    for i in range(n):
        current = b[i]
        a_index = -1
        c_index = -1

        # Count of elements in A[]
        # which are less than the
        # chosen element from B[]
        low = countLessThan(a, n, current)

        # Count of elements in C[]
        # which are greater than the
        # chosen element from B[]
        high = countGreaterThan(c, n, current)

        # Update the count
        count += (low * high)

    return count

# Driver code
if __name__ == "__main__":

    a = [ 1, 5 ]
    b = [ 2, 4 ]
    c = [ 3, 6 ]
    size = len(a)

    print( countTriplets(size, a, b, c))

# This code is contributed by ChitraNayal
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count
    // of elements in arr[] which are
    // less than the given key
    static int countLessThan(int []arr, int n, int key)
    {
        int l = 0, r = n - 1;
        int index = -1;

        // Modified binary search
        while (l <= r)
        {
            int m = (l + r) / 2;

            if (arr[m] < key)
            {
                l = m + 1;
                index = m;
            }
            else
            {
                r = m - 1;
            }
        }

        return (index + 1);
    }

    // Function to return the count
    // of elements in arr[] which are
    // greater than the given key
    static int countGreaterThan(int []arr, int n, int key)
    {
        int l = 0, r = n - 1;
        int index = -1;

        // Modified binary search
        while (l <= r)
        {
            int m = (l + r) / 2;

            if (arr[m] <= key)
            {
                l = m + 1;
            }
            else
            {
                r = m - 1;
                index = m;
            }
        }

        if (index == -1)
            return 0;
        return (n - index);
    }

    // Function to return the count
    // of the required triplets
    static int countTriplets(int n, int []a, int []b, int []c)
    {
        // Sort all three arrays
        Array.Sort(a) ;
        Array.Sort(b);
        Array.Sort(c);

        int count = 0;

        // Iterate for all the elements of array B
        for (int i = 0; i < n; ++i)
        {
            int current = b[i];

            // Count of elements in A[]
            // which are less than the
            // chosen element from B[]
            int low = countLessThan(a, n, current);

            // Count of elements in C[]
            // which are greater than the
            // chosen element from B[]
            int high = countGreaterThan(c, n, current);

            // Update the count
            count += (low * high);
        }

        return count;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 1, 5 };
        int []b = { 2, 4 };
        int []c = { 3, 6 };
        int size = a.Length;

        Console.WriteLine(countTriplets(size, a, b, c));

    }
}

// This code is contributed by AnkitRai01
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to return the count
// of elements in arr[] which are
// less than the given key
function countLessThan(&$arr, $n, $key)
{
    $l = 0;
    $r = $n - 1;
    $index = -1;

    // Modified binary search
    while ($l <= $r)
    {
        $m = intval(($l + $r) / 2);

        if ($arr[$m] < $key)
        {
            $l = $m + 1;
            $index = $m;
        }
        else
        {
            $r = $m - 1;
        }
    }

    return ($index + 1);
}

// Function to return the count
// of elements in arr[] which are
// greater than the given key
function countGreaterThan(&$arr, $n, $key)
{
    $l = 0;
    $r = $n - 1;
    $index = -1;

    // Modified binary search
    while ($l <= $r)
    {
        $m = intval(($l + $r) / 2);

        if ($arr[$m] <= $key)
        {
            $l = $m + 1;
        }
        else
        {
            $r = $m - 1;
            $index = $m;
        }
    }

    if ($index == -1)
        return 0;
    return ($n - $index);
}

// Function to return the count
// of the required triplets
function countTriplets($n, &$a, &$b, &$c)
{
    // Sort all three arrays
    sort($a);
    sort($b);
    sort($c);

    $count = 0;

    // Iterate for all the elements of array B
    for ($i = 0; $i < $n; ++$i)
    {
        $current = $b[$i];
        $a_index = -1;
        $c_index = -1;

        // Count of elements in A[]
        // which are less than the
        // chosen element from B[]
        $low = countLessThan($a, $n, $current);

        // Count of elements in C[]
        // which are greater than the
        // chosen element from B[]
        $high = countGreaterThan($c, $n, $current);

        // Update the count
        $count += ($low * $high);
    }

    return $count;
}

// Driver code
$a = array( 1, 5 );
$b = array( 2, 4 );
$c = array( 3, 6 );
$size = sizeof($a);

echo countTriplets($size, $a, $b, $c);

// This code is contributed by ChitraNayal
?>
```

## **java 描述语言**

```
<script>

// JavaScript implementation of the approach

// Function to return the count
    // of elements in arr[] which are
    // less than the given key
function countLessThan(arr,n,key)
{
    let l = 0, r = n - 1;
        let index = -1;

        // Modified binary search
        while (l <= r)
        {
            let m = Math.floor((l + r) / 2);

            if (arr[m] < key)
            {
                l = m + 1;
                index = m;
            }
            else
            {
                r = m - 1;
            }
        }

        return (index + 1);
}

    // Function to return the count
    // of elements in arr[] which are
    // greater than the given key
function countGreaterThan(arr,n,key)
{
    let l = 0, r = n - 1;
        let index = -1;

        // Modified binary search
        while (l <= r)
        {
           let m = Math.floor((l + r) / 2);

            if (arr[m] <= key)
            {
                l = m + 1;
            }
            else
            {
                r = m - 1;
                index = m;
            }
        }

        if (index == -1)
            return 0;
        return (n - index);
}

    // Function to return the count
    // of the required triplets
function countTriplets(n,a,b,c)
{
    // Sort all three arrays
        a.sort(function(e,f){return e-f;}) ;
        b.sort(function(e,f){return e-f;}) ;
        c.sort(function(e,f){return e-f;}) ;

        let count = 0;

        // Iterate for all the elements of array B
        for (let i = 0; i < n; ++i)
        {
            let current = b[i];

            // Count of elements in A[]
            // which are less than the
            // chosen element from B[]
            let low = countLessThan(a, n, current);

            // Count of elements in C[]
            // which are greater than the
            // chosen element from B[]
            let high = countGreaterThan(c, n, current);

            // Update the count
            count += (low * high);
        }

        return count;
}

// Driver code
let a=[1, 5 ];
let b=[2, 4];
let c=[3, 6 ];
let size = a.length;
document.write(countTriplets(size, a, b, c));

// This code is contributed by avanitrachhadiya2155

</script>
```

****Output:** 

```
3
```**