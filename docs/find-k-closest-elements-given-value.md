# 找到与给定值最接近的 k 个元素

> 原文:[https://www . geesforgeks . org/find-k-最接近元素-给定值/](https://www.geeksforgeeks.org/find-k-closest-elements-given-value/)

给定一个排序的数组 arr[]和值 X，找到 arr[]中与 X 最接近的 k 个元素。

**示例:**

```
Input: K = 4, X = 35
       arr[] = {12, 16, 22, 30, 35, 39, 42, 
               45, 48, 50, 53, 55, 56}
Output: 30 39 42 45
```

请注意，如果元素出现在数组中，那么它不应该出现在输出中，只需要其他最接近的元素。

在下面的解决方案中，假设数组的所有元素都是不同的。
一个**简单的解决方案**就是对 k 个最接近的元素做线性搜索。
1)从第一个元素开始，搜索交叉点(元素小于或等于 X 的前一点和元素大于 X 的后一点)。这一步需要 O(n)个时间。
2)一旦找到交叉点，就可以比较交叉点两侧的元素，打印 k 个最接近的元素。这一步需要时间。
上述解的时间复杂度为 O(n)。

一个**优化解**是在 O(Logn + k)时间内找到 k 个元素。想法是用[二分搜索法](http://geeksquiz.com/binary-search/)找到交叉点。一旦找到交叉点的索引，我们就可以在 O(k)时间内打印 k 个最接近的元素。

## C++

```
#include<stdio.h>

/* Function to find the cross over point (the point before
which elements are smaller than or equal to x and after
which greater than x)*/
int findCrossOver(int arr[], int low, int high, int x)
{
// Base cases
if (arr[high] <= x) // x is greater than all
    return high;
if (arr[low] > x) // x is smaller than all
    return low;

// Find the middle point
int mid = (low + high)/2; /* low + (high - low)/2 */

/* If x is same as middle element, then return mid */
if (arr[mid] <= x && arr[mid+1] > x)
    return mid;

/* If x is greater than arr[mid], then either arr[mid + 1]
    is ceiling of x or ceiling lies in arr[mid+1...high] */
if(arr[mid] < x)
    return findCrossOver(arr, mid+1, high, x);

return findCrossOver(arr, low, mid - 1, x);
}

// This function prints k closest elements to x in arr[].
// n is the number of elements in arr[]
void printKclosest(int arr[], int x, int k, int n)
{
    // Find the crossover point
    int l = findCrossOver(arr, 0, n-1, x);
    int r = l+1; // Right index to search
    int count = 0; // To keep track of count of elements already printed

    // If x is present in arr[], then reduce left index
    // Assumption: all elements in arr[] are distinct
    if (arr[l] == x) l--;

    // Compare elements on left and right of crossover
    // point to find the k closest elements
    while (l >= 0 && r < n && count < k)
    {
        if (x - arr[l] < arr[r] - x)
            printf("%d ", arr[l--]);
        else
            printf("%d ", arr[r++]);
        count++;
    }

    // If there are no more elements on right side, then
    // print left elements
    while (count < k && l >= 0)
        printf("%d ", arr[l--]), count++;

    // If there are no more elements on left side, then
    // print right elements
    while (count < k && r < n)
        printf("%d ", arr[r++]), count++;
}

/* Driver program to check above functions */
int main()
{
int arr[] ={12, 16, 22, 30, 35, 39, 42,
            45, 48, 50, 53, 55, 56};
int n = sizeof(arr)/sizeof(arr[0]);
int x = 35, k = 4;
printKclosest(arr, x, 4, n);
return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k closest elements to a given value
class KClosest
{
    /* Function to find the cross over point (the point before
       which elements are smaller than or equal to x and after
       which greater than x)*/
    int findCrossOver(int arr[], int low, int high, int x)
    {
        // Base cases
        if (arr[high] <= x) // x is greater than all
            return high;
        if (arr[low] > x)  // x is smaller than all
            return low;

        // Find the middle point
        int mid = (low + high)/2;  /* low + (high - low)/2 */

        /* If x is same as middle element, then return mid */
        if (arr[mid] <= x && arr[mid+1] > x)
            return mid;

        /* If x is greater than arr[mid], then either arr[mid + 1]
          is ceiling of x or ceiling lies in arr[mid+1...high] */
        if(arr[mid] < x)
            return findCrossOver(arr, mid+1, high, x);

        return findCrossOver(arr, low, mid - 1, x);
    }

    // This function prints k closest elements to x in arr[].
    // n is the number of elements in arr[]
    void printKclosest(int arr[], int x, int k, int n)
    {
        // Find the crossover point
        int l = findCrossOver(arr, 0, n-1, x);
        int r = l+1;   // Right index to search
        int count = 0; // To keep track of count of elements
                       // already printed

        // If x is present in arr[], then reduce left index
        // Assumption: all elements in arr[] are distinct
        if (arr[l] == x) l--;

        // Compare elements on left and right of crossover
        // point to find the k closest elements
        while (l >= 0 && r < n && count < k)
        {
            if (x - arr[l] < arr[r] - x)
                System.out.print(arr[l--]+" ");
            else
                System.out.print(arr[r++]+" ");
            count++;
        }

        // If there are no more elements on right side, then
        // print left elements
        while (count < k && l >= 0)
        {
            System.out.print(arr[l--]+" ");
            count++;
        }

        // If there are no more elements on left side, then
        // print right elements
        while (count < k && r < n)
        {
            System.out.print(arr[r++]+" ");
            count++;
        }
    }

    /* Driver program to check above functions */
    public static void main(String args[])
    {
        KClosest ob = new KClosest();
        int arr[] = {12, 16, 22, 30, 35, 39, 42,
                     45, 48, 50, 53, 55, 56
                    };
        int n = arr.length;
        int x = 35, k = 4;
        ob.printKclosest(arr, x, 4, n);
    }
}
/* This code is contributed by Rajat Mishra */
```

## 蟒蛇 3

```
# Function to find the cross over point
# (the point before which elements are
# smaller than or equal to x and after
# which greater than x)
def findCrossOver(arr, low, high, x) :

    # Base cases
    if (arr[high] <= x) : # x is greater than all
        return high

    if (arr[low] > x) : # x is smaller than all
        return low

    # Find the middle point
    mid = (low + high) // 2 # low + (high - low)// 2

    # If x is same as middle element,
    # then return mid
    if (arr[mid] <= x and arr[mid + 1] > x) :
        return mid

    # If x is greater than arr[mid], then
    # either arr[mid + 1] is ceiling of x
    # or ceiling lies in arr[mid+1...high]
    if(arr[mid] < x) :
        return findCrossOver(arr, mid + 1, high, x)

    return findCrossOver(arr, low, mid - 1, x)

# This function prints k closest elements to x
# in arr[]. n is the number of elements in arr[]
def printKclosest(arr, x, k, n) :

    # Find the crossover point
    l = findCrossOver(arr, 0, n - 1, x)
    r = l + 1 # Right index to search
    count = 0 # To keep track of count of
              # elements already printed

    # If x is present in arr[], then reduce
    # left index. Assumption: all elements
    # in arr[] are distinct
    if (arr[l] == x) :
        l -= 1

    # Compare elements on left and right of crossover
    # point to find the k closest elements
    while (l >= 0 and r < n and count < k) :

        if (x - arr[l] < arr[r] - x) :
            print(arr[l], end = " ")
            l -= 1
        else :
            print(arr[r], end = " ")
            r += 1
        count += 1

    # If there are no more elements on right
    # side, then print left elements
    while (count < k and l >= 0) :
        print(arr[l], end = " ")
        l -= 1
        count += 1

    # If there are no more elements on left
    # side, then print right elements
    while (count < k and r < n) :
        print(arr[r], end = " ")
        r += 1
        count += 1

# Driver Code
if __name__ == "__main__" :

    arr =[12, 16, 22, 30, 35, 39, 42,
              45, 48, 50, 53, 55, 56]

    n = len(arr)
    x = 35
    k = 4

    printKclosest(arr, x, 4, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to find k closest elements to
// a given value
using System;

class GFG {

    /* Function to find the cross over point
    (the point before which elements are
    smaller than or equal to x and after which
    greater than x)*/
    static int findCrossOver(int []arr, int low,
                                int high, int x)
    {

        // Base cases
        // x is greater than all
        if (arr[high] <= x)
            return high;

        // x is smaller than all
        if (arr[low] > x)
            return low;

        // Find the middle point
        /* low + (high - low)/2 */
        int mid = (low + high)/2;

        /* If x is same as middle element, then
        return mid */
        if (arr[mid] <= x && arr[mid+1] > x)
            return mid;

        /* If x is greater than arr[mid], then
        either arr[mid + 1] is ceiling of x or
        ceiling lies in arr[mid+1...high] */
        if(arr[mid] < x)
            return findCrossOver(arr, mid+1,
                                      high, x);

        return findCrossOver(arr, low, mid - 1, x);
    }

    // This function prints k closest elements
    // to x in arr[]. n is the number of
    // elements in arr[]
    static void printKclosest(int []arr, int x,
                                  int k, int n)
    {

        // Find the crossover point
        int l = findCrossOver(arr, 0, n-1, x);

        // Right index to search
        int r = l + 1;

        // To keep track of count of elements
        int count = 0;

        // If x is present in arr[], then reduce
        // left index Assumption: all elements in
        // arr[] are distinct
        if (arr[l] == x) l--;

        // Compare elements on left and right of
        // crossover point to find the k closest
        // elements
        while (l >= 0 && r < n && count < k)
        {
            if (x - arr[l] < arr[r] - x)
                Console.Write(arr[l--]+" ");
            else
                Console.Write(arr[r++]+" ");
            count++;
        }

        // If there are no more elements on right
        // side, then print left elements
        while (count < k && l >= 0)
        {
            Console.Write(arr[l--]+" ");
            count++;
        }

        // If there are no more elements on left
        // side, then print right elements
        while (count < k && r < n)
        {
            Console.Write(arr[r++] + " ");
            count++;
        }
    }

    /* Driver program to check above functions */
    public static void Main()
    {
        int []arr = {12, 16, 22, 30, 35, 39, 42,
                         45, 48, 50, 53, 55, 56};
        int n = arr.Length;
        int x = 35;
        printKclosest(arr, x, 4, n);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program to Find k closest
// elements to a given value

/* Function to find the cross
   over point (the point before
   which elements are smaller
   than or equal to x and after
   which greater than x) */
function findCrossOver($arr, $low,
                       $high, $x)
{

    // Base cases

    // x is greater than all
    if ($arr[$high] <= $x)
        return $high;

    // x is smaller than all
    if ($arr[$low] > $x)
        return $low;

    // Find the middle point
    /* low + (high - low)/2 */
    $mid = ($low + $high)/2;

    /* If x is same as middle
       element, then return mid */
    if ($arr[$mid] <= $x and
        $arr[$mid + 1] > $x)
        return $mid;

    /* If x is greater than arr[mid],
       then either arr[mid + 1] is
       ceiling of x or ceiling lies
       in arr[mid+1...high] */
    if($arr[$mid] < $x)
        return findCrossOver($arr, $mid + 1,
                                 $high, $x);

    return findCrossOver($arr, $low,
                      $mid - 1, $x);
}

// This function prints k
// closest elements to x in arr[].
// n is the number of elements
// in arr[]
function printKclosest($arr, $x, $k, $n)
{

    // Find the crossover point
    $l = findCrossOver($arr, 0, $n - 1, $x);

    // Right index to search
    $r = $l + 1;

    // To keep track of count of
    // elements already printed
    $count = 0;

    // If x is present in arr[],
    // then reduce left index
    // Assumption: all elements
    // in arr[] are distinct
    if ($arr[$l] == $x) $l--;

    // Compare elements on left
    // and right of crossover
    // point to find the k
    // closest elements
    while ($l >= 0 and $r < $n
              and $count < $k)
    {
        if ($x - $arr[$l] < $arr[$r] - $x)
            echo $arr[$l--]," ";
        else
            echo $arr[$r++]," ";
        $count++;
    }

    // If there are no more
    // elements on right side,
    // then print left elements
    while ($count < $k and $l >= 0)
        echo $arr[$l--]," "; $count++;

    // If there are no more
    // elements on left side,
    // then print right elements
    while ($count < $k and $r < $n)
        echo $arr[$r++]; $count++;
}

// Driver Code
$arr =array(12, 16, 22, 30, 35, 39, 42,
                45, 48, 50, 53, 55, 56);
$n = count($arr);
$x = 35; $k = 4;

printKclosest($arr, $x, 4, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// JavaScript program to find k
// closest elements to a given value

// Function to find the cross over point
// (the point before which elements are
// smaller than or equal to x and after
// which greater than x)
function findCrossOver(arr, low, high, x)
{

    // Base cases
    if (arr[high] <= x)  // x is greater than all
        return high

    if (arr[low] > x)  // x is smaller than all
        return low

    // Find the middle point
    var mid = (low + high) // 2 // low + (high - low)// 2

    // If x is same as middle element,
    // then return mid
    if (arr[mid] <= x && arr[mid + 1] > x)
        return mid

    // If x is greater than arr[mid], then
    // either arr[mid + 1] is ceiling of x
    // or ceiling lies in arr[mid+1...high]
    if (arr[mid] < x)
        return findCrossOver(arr, mid + 1, high, x)

    return findCrossOver(arr, low, mid - 1, x)

}

// This function prints k closest elements to x
// in arr[]. n is the number of elements in arr[]
function printKclosest(arr, x, k, n)
{

    // Find the crossover point
    var l = findCrossOver(arr, 0, n - 1, x)
    var r = l + 1 // Right index to search
    var count = 0 // To keep track of count of
                  // elements already printed

    // If x is present in arr[], then reduce
    // left index. Assumption: all elements
    // in arr[] are distinct
    if (arr[l] == x)
        l -= 1

    // Compare elements on left and right of crossover
    // point to find the k closest elements
    while (l >= 0 && r < n && count < k)
    {

        if (x - arr[l] < arr[r] - x)
        {
            document.write(arr[l] + " ")
            l -= 1
        }
        else
        {
            document.write(arr[r] + " ")
            r += 1
        }
        count += 1
    }

    // If there are no more elements on right
    // side, then print left elements
    while (count < k && l >= 0)
    {
        print(arr[l])
        l -= 1
        count += 1
    }

    // If there are no more elements on left
    // side, then print right elements
    while (count < k && r < n)
    {
        print(arr[r])
        r += 1
        count += 1
    }
}

// Driver Code
var arr = [ 12, 16, 22, 30, 35, 39, 42,
            45, 48, 50, 53, 55, 56 ]

var n = arr.length
var x = 35
var k = 4

printKclosest(arr, x, 4, n)

// This code is contributed by AnkThon

</script>
```

**输出:**

```
39 30 42 45
```

该方法的时间复杂度为 O(Logn + k)。
**练习:**扩展优化解决方案，使其也适用于副本，即适用于元素不必不同的数组。
本文由**拉胡尔·贾恩**供稿。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息