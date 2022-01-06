# 查找排序数组中元素的第一个和最后一个位置

> 原文:[https://www . geeksforgeeks . org/find-排序数组中元素的首末位置/](https://www.geeksforgeeks.org/find-first-and-last-positions-of-an-element-in-a-sorted-array/)

给定一个可能有重复元素的排序数组，任务是找到给定数组中元素 x 第一次和最后一次出现的索引。

**示例:**

```
Input : arr[] = {1, 3, 5, 5, 5, 5, 67, 123, 125}    
        x = 5
Output : First Occurrence = 2
         Last Occurrence = 5

Input : arr[] = {1, 3, 5, 5, 5, 5, 7, 123, 125 }    
        x = 7
Output : First Occurrence = 6
         Last Occurrence = 6
```

天真的方法是运行 for 循环并检查数组中的给定元素。

```
1\. Run a for loop and for i = 0 to n-1
2\. Take first = -1 and last = -1 
3\. When we find element first time then we update first = i 
4\. We always update last=i whenever we find the element.
5\. We print first and last.
```

## C++

```
// C++ program to find first and last occurrence of
// an elements in given sorted array
#include <bits/stdc++.h>
using namespace std;

// Function for finding first and last occurrence
// of an elements
void findFirstAndLast(int arr[], int n, int x)
{
    int first = -1, last = -1;
    for (int i = 0; i < n; i++) {
        if (x != arr[i])
            continue;
        if (first == -1)
            first = i;
        last = i;
    }
    if (first != -1)
        cout << "First Occurrence = " << first
             << "\nLast Occurrence = " << last;
    else
        cout << "Not Found";
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 2, 2, 2, 3, 4, 7, 8, 8 };
    int n = sizeof(arr) / sizeof(int);
    int x = 8;
    findFirstAndLast(arr, n, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find first and last occurrence of
// an elements in given sorted array
import java.io.*;

class GFG {
    // Function for finding first and last occurrence
    // of an elements
    public static void findFirstAndLast(int arr[], int x)
    {
        int n = arr.length;
        int first = -1, last = -1;
        for (int i = 0; i < n; i++) {
            if (x != arr[i])
                continue;
            if (first == -1)
                first = i;
            last = i;
        }
        if (first != -1) {
            System.out.println("First Occurrence = " + first);
            System.out.println("Last Occurrence = " + last);
        }
        else
            System.out.println("Not Found");
    }

    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 2, 2, 2, 3, 4, 7, 8, 8 };
        int x = 8;
        findFirstAndLast(arr, x);
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find first and
# last occurrence of an elements in
# given sorted array

# Function for finding first and last
# occurrence of an elements
def findFirstAndLast(arr, n, x) :
    first = -1
    last = -1
    for i in range(0, n) :
        if (x != arr[i]) :
            continue
        if (first == -1) :
            first = i
        last = i

    if (first != -1) :
        print( "First Occurrence = ", first,
               " \nLast Occurrence = ", last)
    else :
        print("Not Found")

# Driver code
arr = [1, 2, 2, 2, 2, 3, 4, 7, 8, 8 ]
n = len(arr)
x = 8
findFirstAndLast(arr, n, x)

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to find first and last
// occurrence of an elements in given
// sorted array
using System;

class GFG {

    // Function for finding first and
    // last occurrence of an elements
    static void findFirstAndLast(int[] arr,
                                 int x)
    {
        int n = arr.Length;
        int first = -1, last = -1;

        for (int i = 0; i < n; i++) {
            if (x != arr[i])
                continue;
            if (first == -1)
                first = i;
            last = i;
        }
        if (first != -1) {
            Console.WriteLine("First "
                              + "Occurrence = " + first);
            Console.Write("Last "
                          + "Occurrence = " + last);
        }
        else
            Console.Write("Not Found");
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 2, 2, 2, 3,
                      4, 7, 8, 8 };
        int x = 8;
        findFirstAndLast(arr, x);
    }
}

// This code is contributed by nitin mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find first and last
// occurrence of an elements in given
// sorted array

// Function for finding first and last
// occurrence of an elements
function findFirstAndLast( $arr, $n, $x)
{
    $first = -1; $last = -1;
    for ( $i = 0; $i < $n; $i++)
    {
        if ($x != $arr[$i])
            continue;
        if ($first == -1)
            $first = $i;
        $last = $i;
    }
    if ($first != -1)
        echo "First Occurrence = ", $first,
              "\n", "\nLast Occurrence = ",
                                     $last;
    else
        echo "Not Found";
}

// Driver code
    $arr = array(1, 2, 2, 2, 2, 3, 4,
                                 7, 8, 8 );
    $n = count($arr);
    $x = 8;

    findFirstAndLast($arr, $n, $x);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find first and last occurrence of
// an elements in given sorted array

    // Function for finding first and last occurrence
    // of an elements
    function findFirstAndLast(arr,x)
    {
        let n = arr.length;
        let first = -1, last = -1;
        for (let i = 0; i < n; i++) {
            if (x != arr[i])
                continue;
            if (first == -1)
                first = i;
            last = i;
        }
        if (first != -1) {
            document.write("First Occurrence = " + first + "<br>");
            document.write("Last Occurrence = " + last + "<br>");
        }
        else
            document.write("Not Found");
    }

    let arr = [1, 2, 2, 2, 2, 3, 4, 7, 8, 8 ];
    let x = 8;
    findFirstAndLast(arr, x);

    // This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
First Occurrence = 8nLast Occurrence = 9
```