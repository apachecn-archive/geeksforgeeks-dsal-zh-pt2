# 字典最小交替数组

> 原文:[https://www . geeksforgeeks . org/词典-最小-替代-数组/](https://www.geeksforgeeks.org/lexicographical-smallest-alternate-array/)

给定一个由不同元素组成的数组 **arr[]** ，任务是重新排列该数组，使其在字典上最小，并且具有形式**arr[0]>arr[1]<arr[2]>arr[3]<……**
T5】示例:

> **输入:** arr[] = {3，2，1，4，5 }
> T3】输出:2 1 4 3 5
> T6】输入: arr[] = {10，22 }
> T9】输出: 22 10

**方法:**为了得到字典上最小的数组，我们可以选择最小元素作为第一个元素，但这不会满足第一个元素必须严格大于第二个元素的条件。
现在，第二个最好的选择是从数组中选择第二个最小值，并且唯一小于它的元素是最小的元素，它将是数组的第二个元素。
对剩余的数组元素应用相同的过程，选择剩余元素的第二个最小值，然后选择每两个连续位置的最小值，这可以通过首先对给定数组进行[排序](https://www.geeksforgeeks.org/sorting-algorithms/)然后每两个连续元素进行交换来获得。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the
// contents of an array
void printArr(int arr[], int n)
{
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
}

// Function to find the lexicographically
// smallest alternating array
void smallestArr(int arr[], int n)
{

    // Sort the array
    sort(arr, arr + n);

    // Swap every two consecutive elements
    for (int i = 0; i + 1 < n; i = i + 2) {
        swap(arr[i], arr[i + 1]);
    }

    // Print the re-arranged array
    printArr(arr, n);
}

// Driver code
int main()
{
    int arr[] = { 3, 2, 1, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    smallestArr(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

    // Function to print the
    // contents of an array
    static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            System.out.print(arr[i] + " ");
    }

    // Function to find the lexicographically
    // smallest alternating array
    static void smallestArr(int[] arr, int n)
    {

        // Sort the array
        Arrays.sort(arr);

        // Swap every two consecutive elements
        for (int i = 0; i + 1 < n; i = i + 2)
        {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        // Print the re-arranged array
        printArr(arr, n);
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] arr = { 3, 2, 1, 4, 5 };
        int n = arr.length;
        smallestArr(arr, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the
# contents of an array
def printArr(arr, n):
    for i in range(n):
        print(arr[i], end = " ");

# Function to find the lexicographically
# smallest alternating array
def smallestArr(arr, n):

    # Sort the array
    arr.sort();

    # Swap every two consecutive elements
    for i in range(0, n - 1, 2):

        temp = arr[i];
        arr[i] = arr[i + 1];
        arr[i + 1] = temp;

    # Print the re-arranged array
    printArr(arr, n);

# Driver code
if __name__ == '__main__':

    arr = [ 3, 2, 1, 4, 5 ];
    n = len(arr);
    smallestArr(arr, n);

# This code contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the
    // contents of an array
    static void printArr(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Function to find the lexicographically
    // smallest alternating array
    static void smallestArr(int[] arr, int n)
    {

        // Sort the array
        Array.Sort(arr);

        // Swap every two consecutive elements
        for (int i = 0; i + 1 < n; i = i + 2)
        {
            int temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        // Print the re-arranged array
        printArr(arr, n);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 2, 1, 4, 5 };
        int n = arr.Length;
        smallestArr(arr, n);
    }
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the
// contents of an array
function printArr($arr, $n)
{
    for ($i = 0; $i < $n; $i++)
    {
        echo $arr[$i];
        echo " ";
    }
}

// Function to find the lexicographically
// smallest alternating array
function smallestArr($arr, $n)
{

    // Sort the array
    sort($arr);

    // Swap every two consecutive elements
    for ($i = 0; $i + 1 < $n; $i = $i + 2)
    {
        $temp = $arr[$i];
        $arr[$i] = $arr[$i + 1];
        $arr[$i + 1] = $temp;
    }

    // Print the re-arranged array
    printArr($arr, $n);
}

// Driver code
$arr = array( 3, 2, 1, 4, 5 );
$n = count($arr);

smallestArr($arr, $n);

// This code is contributed by Naman_Garg.
?>
```

## java 描述语言

```
// javascript implementation of the approach

    // Function to print the
    // contents of an array
    function printArr(arr, n)
    {
        for (var i = 0; i < n; i++)
            document.write(arr[i] + " ");
    }

    // Function to find the lexicographically
    // smallest alternating array

    function smallestArr( arr,  n)
    {

        // Sort the array       
        arr.sort();

        // Swap every two consecutive elements
        for (var i = 0; i + 1 < n; i = i + 2)
        {
            var temp = arr[i];
            arr[i] = arr[i + 1];
            arr[i + 1] = temp;
        }

        // Print the re-arranged array
        printArr(arr, n);
    }

    // Driver code
        var arr = [ 3, 2, 1, 4, 5 ] ;
        var n = arr.length;
        smallestArr(arr, n);

// This code is contributed by bunnyram19.
```

**Output:** 

```
2 1 4 3 5
```