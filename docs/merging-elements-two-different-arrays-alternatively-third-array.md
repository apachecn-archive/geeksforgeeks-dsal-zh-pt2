# 在第三个数组中交替合并两个不同数组的元素

> 原文:[https://www . geesforgeks . org/merging-elements-两个不同的数组-交替-第三个数组/](https://www.geeksforgeeks.org/merging-elements-two-different-arrays-alternatively-third-array/)

给定两个数组 arr1[]和 arr2[]，我们需要组合两个数组，使得组合的数组具有两者的交替元素。如果一个数组有额外的元素，那么这些元素将被追加到组合数组的末尾。

```
Input : arr1[] = {1, 2, 3, 4, 5, 6}
        arr2[] = {11, 22, 33, 44}
Output: {1, 11, 2, 22, 3, 33, 4, 44, 5, 6}

Input : arr1[] = {1, 2, 3, 4, 5, 6, 7, 8}
        arr2[] = {11, 22, 33, 44}
Output: {1, 11, 2, 22, 3, 33, 4, 44, 5, 6, 7, 8}
```

我们遍历两个给定的数组，并逐一将它们的元素放入组合数组中。在一个数组用完之后，我们放入另一个数组的剩余元素。

## C++

```
// C++ program to merge two sorted arrays/
#include<iostream>
using namespace std;

// Alternatively merge arr1[0..n1-1] and arr2[0..n2-1]
// into arr3[0..n1+n2-1]
void alternateMerge(int arr1[], int arr2[], int n1,
                    int n2, int arr3[])
{
    int i = 0, j = 0, k = 0;

    // Traverse both array
    while (i<n1 && j <n2)
    {
        arr3[k++] = arr1[i++];
        arr3[k++] = arr2[j++];
    }

    // Store remaining elements of first array
    while (i < n1)
        arr3[k++] = arr1[i++];

    // Store remaining elements of second array
    while (j < n2)
        arr3[k++] = arr2[j++];
}

// Driver code
int main()
{
    int arr1[] = {1, 3, 5, 7, 9, 11};
    int n1 = sizeof(arr1) / sizeof(arr1[0]);

    int arr2[] = {2, 4, 6, 8};
    int n2 = sizeof(arr2) / sizeof(arr2[0]);

    int arr3[n1+n2];
    alternateMerge(arr1, arr2, n1, n2, arr3);

    cout << "Array after merging" <<endl;
    for (int i=0; i < n1+n2; i++)
        cout << arr3[i] << " ";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to merge two sorted arrays
import java.io.*;

class GFG {

    // Alternatively merge arr1[0..n1-1] and
    // arr2[0..n2-1] into arr3[0..n1+n2-1]
    static void alternateMerge(int arr1[], int arr2[],
                               int n1, int n2, int arr3[])
    {
        int i = 0, j = 0, k = 0;

        // Traverse both array
        while (i < n1 && j < n2)
        {
            arr3[k++] = arr1[i++];
            arr3[k++] = arr2[j++];
        }

        // Store remaining elements of first array
        while (i < n1)
            arr3[k++] = arr1[i++];

        // Store remaining elements of second array
        while (j < n2)
            arr3[k++] = arr2[j++];
    }

    // Driver code
    public static void main(String args[])
    {
        int arr1[] = {1, 3, 5, 7, 9, 11};
        int n1 = arr1.length;

        int arr2[] = {2, 4, 6, 8};
        int n2 = arr2.length;

        int arr3[] = new int[n1+n2];
        alternateMerge(arr1, arr2, n1, n2, arr3);

        System.out.println("Array after merging");
        for (int i = 0; i < n1 + n2; i++)
            System.out.print( arr3[i] + " ");
    }
}

// This code is contributed
// by Nikita Tiwari.
```

## 蟒蛇 3

```
# Python3 program to merge two sorted arrays/

# Alternatively merge arr1[0..n1-1] and
# arr2[0..n2-1] into arr3[0..n1 + n2-1]
def alternateMerge(arr1, arr2, n1, n2, arr3) :
    i = 0; j = 0; k = 0

    # Traverse both array
    while (i < n1 and j < n2) :
        arr3[k] = arr1[i]
        i += 1
        k += 1

        arr3[k] = arr2[j]
        j += 1
        k += 1

    # Store remaining elements of first array
    while (i < n1) :
        arr3[k] = arr1[i]
        i += 1
        k += 1

    # Store remaining elements of second array
    while (j < n2) :
        arr3[k] = arr2[j]
        k += 1
        j += 1

# Driver code
arr1 = [1, 3, 5, 7, 9, 11]
n1 = len(arr1)

arr2 = [2, 4, 6, 8]
n2 = len(arr2)

arr3= [0] *(n1 + n2)
alternateMerge(arr1, arr2, n1, n2, arr3)

print("Array after merging")
for i in range(0, (n1 + n2)) :
    print(arr3[i] , end = " ")

# This code is contributed by Nikita Tiwari.
```

## C#

```
// C# program to merge two sorted arrays
using System;

class GFG {

    // Alternatively merge arr1[0..n1-1]
    // and arr2[0..n2-1] into arr3[0..n1+n2-1]
    static void alternateMerge(int []arr1, int []arr2,
                           int n1, int n2, int []arr3)
    {
        int i = 0, j = 0, k = 0;

        // Traverse both array
        while (i < n1 && j < n2)
        {
            arr3[k++] = arr1[i++];
            arr3[k++] = arr2[j++];
        }

        // Store remaining elements of first array
        while (i < n1)
            arr3[k++] = arr1[i++];

        // Store remaining elements of second array
        while (j < n2)
            arr3[k++] = arr2[j++];
    }

    // Driver code
    public static void Main()
    {
        int []arr1 = new int[]{1, 3, 5, 7, 9, 11};
        int n1 = arr1.Length;

        int []arr2 = new int[]{2, 4, 6, 8};
        int n2 = arr2.Length;

        int []arr3= new int[n1 + n2];
        alternateMerge(arr1, arr2, n1, n2, arr3);

        Console.WriteLine("Array after merging");
        for (int i = 0; i < n1+n2; i++)
            Console.Write(arr3[i] + " ");
    }
}

// This code is contributed by Sam007.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to merge two
// sorted arrays

// Alternatively merge arr1[0..n1-1]
// and arr2[0..n2-1] into
// arr3[0..n1+n2-1]
function alternateMerge($arr1, $arr2,
                        $n1, $n2)
{
    $i = 0;
    $j = 0;
    $k = 0;
    $arr3 = array();

    // Traverse both array
    while ($i < $n1 && $j < $n2)
    {
        $arr3[$k++] = $arr1[$i++];
        $arr3[$k++] = $arr2[$j++];
    }

    // Store remaining elements
    // of first array
    while ($i < $n1)
        $arr3[$k++] = $arr1[$i++];

    // Store remaining elements
    // of second array
    while($j < $n2)
        $arr3[$k++] = $arr2[$j++];

    echo "Array after merging"."\n";
    for ($i = 0; $i < ($n1 + $n2); $i++)
        echo $arr3[$i] ." ";

}

    // Driver Code
    $arr1 = array(1, 3, 5, 7, 9, 11);
    $n1 = count($arr1);

    $arr2 = array(2, 4, 6, 8);
    $n2 = count($arr2);
    alternateMerge($arr1, $arr2, $n1, $n2);

// This code is contributed by Sam007
?>
```

## java 描述语言

```
<script>

// Javascript program to merge two sorted arrays/

// Alternatively merge arr1[0..n1-1] and arr2[0..n2-1]
// into arr3[0..n1+n2-1]
function alternateMerge(arr1, arr2, n1,
                    n2, arr3)
{
    let i = 0, j = 0, k = 0;

    // Traverse both array
    while (i<n1 && j <n2)
    {
        arr3[k++] = arr1[i++];
        arr3[k++] = arr2[j++];
    }

    // Store remaining elements of first array
    while (i < n1)
        arr3[k++] = arr1[i++];

    // Store remaining elements of second array
    while (j < n2)
        arr3[k++] = arr2[j++];
}

// Driver code

    let arr1 = [1, 3, 5, 7, 9, 11];
    let n1 = arr1.length;

    let arr2 = [2, 4, 6, 8];
    let n2 = arr2.length;

    let arr3 = new Array(n1+n2);
    alternateMerge(arr1, arr2, n1, n2, arr3);

    document.write("Array after merging" + "<br>");
    for (let i=0; i < n1+n2; i++)
        document.write(arr3[i] + " ");

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Array after merging
1 2 3 4 5 6 7 8 9 11 
```

时间复杂度:O(n1 + n2)