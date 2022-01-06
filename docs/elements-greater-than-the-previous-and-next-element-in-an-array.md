# 大于数组中前一个和下一个元素的元素

> 原文:[https://www . geesforgeks . org/elements-大于数组中的前一个和后一个元素/](https://www.geeksforgeeks.org/elements-greater-than-the-previous-and-next-element-in-an-array/)

给定一个 N 个整数的数组。任务是打印数组中大于前一个和后一个元素的元素。
**例** :

```
Input : arr[] = {2, 3, 1, 5, 4, 9, 8, 7, 5}
Output : 3, 5, 9
In above given example 3 is greater than its 
left element 2 and right element 1\. 
Similar logic is applied to other elements 
hence our final output is 3, 5, 9.

Input : arr[] = {1, 2, 3, 2, 1}
Output : 3
```

**逼近**:由于第一个元素(arr[0])左边没有元素，最后一个元素(arr[N-1])右边也没有元素，所以这两个元素会被排除在最终答案之外。
现在，从索引 **1 到 N-2** 遍历数组，对于每个元素**arr【I】**检查**arr【I】>arr【I-1】**和**arr【I】>arr【I+1】**。
以下是上述方法的实施:

## C++

```
// C++ program to print elements greater than
// the previous and next element in an Array
#include <bits/stdc++.h>
using namespace std;

// Function to print elements greater than
// the previous and next element in an Array
void printElements(int arr[], int n)
{
    // Traverse array from index 1 to n-2
    // and check for the given condition
    for (int i = 1; i < n - 1; i++) {
        if (arr[i] > arr[i - 1] and arr[i] > arr[i + 1])
            cout << arr[i] << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 2, 3, 1, 5, 4, 9, 8, 7, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    printElements(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print elements greater than
// the previous and next element in an Array
class GfG
{

// Function to print elements greater than
// the previous and next element in an Array
static void printElements(int arr[], int n)
{
    // Traverse array from index 1 to n-2
    // and check for the given condition
    for (int i = 1; i < n - 1; i++)
    {
        if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1])
            System.out.print(arr[i] + " ");
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 1, 5, 4, 9, 8, 7, 5 };
    int n = arr.length;

    printElements(arr, n);
}
}

// This code is contributed by Prerna Saini
```

## 蟒蛇 3

```
# Python 3 program to print elements greater than
# the previous and next element in an Array

# Function to print elements greater than
# the previous and next element in an Array
def printElements(arr, n):

    # Traverse array from index 1 to n-2
    # and check for the given condition
    for i in range(1, n - 1, 1):
        if (arr[i] > arr[i - 1] and
            arr[i] > arr[i + 1]):
            print(arr[i], end = " ")

# Driver Code
if __name__ == '__main__':
    arr = [2, 3, 1, 5, 4, 9, 8, 7, 5]
    n = len(arr)

    printElements(arr, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
using System;

// c# program to print elements greater than
// the previous and next element in an Array
public class GfG
{

// Function to print elements greater than
// the previous and next element in an Array
public static void printElements(int[] arr, int n)
{
    // Traverse array from index 1 to n-2
    // and check for the given condition
    for (int i = 1; i < n - 1; i++)
    {
        if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1])
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// Driver Code
public static void Main(string[] args)
{
    int[] arr = new int[] {2, 3, 1, 5, 4, 9, 8, 7, 5};
    int n = arr.Length;

    printElements(arr, n);
}
}
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print elements greater than
// the previous and next element in an Array

// Function to print elements greater than
// the previous and next element in an Array
function printElements($arr, $n)
{
    // Traverse array from index 1 to n-2
    // and check for the given condition
    for ($i = 1; $i < $n - 1; $i++)
    {
        if ($arr[$i] > $arr[$i - 1] and
            $arr[$i] > $arr[$i + 1])
            echo $arr[$i] . " ";
    }
}

// Driver Code
$arr = array(2, 3, 1, 5, 4, 9, 8, 7, 5);
$n = sizeof($arr);

printElements($arr, $n);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to print elements greater than
// the previous and next element in an Array
function printElements(arr,  n)
{
    // Traverse array from index 1 to n-2
    // and check for the given condition
    for (var i = 1; i < n - 1; i++) {
        if (arr[i] > arr[i - 1] && arr[i] > arr[i + 1])
            document.write( arr[i] + " ");
    }
}
var arr = [ 2, 3, 1, 5, 4, 9, 8, 7, 5 ];
var n = arr.length;

printElements(arr, n);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
3 5 9
```