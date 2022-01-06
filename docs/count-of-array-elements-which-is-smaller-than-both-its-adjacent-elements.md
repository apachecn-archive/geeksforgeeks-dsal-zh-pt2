# 小于其相邻元素的数组元素的计数

> 原文:[https://www . geeksforgeeks . org/数组元素计数-小于其相邻元素的数量/](https://www.geeksforgeeks.org/count-of-array-elements-which-is-smaller-than-both-its-adjacent-elements/)

给定一个大小为 **N** 的数组 **arr[]** ，任务是找出数组中谷点的数量。

> **谷点:**如果数组的任何元素都小于其相邻的两个元素，即![arr[i-1] > arr[i] < arr[i+1]   ](img/245714894a301b5d12f6e222214afcd9.png "Rendered by QuickLaTeX.com")，则该元素被称为谷点。

**示例:**

> **输入:** arr[] = {3，2，5}
> **输出:** 1
> **说明:**
> 只有一个谷点。那是 arr[1]。
> 
> **输入:** arr[] = {5，4，8，3，6}
> **输出:** 2
> **说明:**
> 有两个谷点。那就是 arr[1]和 arr[3]。

**方法:**想法是从 1 到![N-1   ](img/3b95f272b0cbaf5ae258973bac465b58.png "Rendered by QuickLaTeX.com")迭代数组，对于每个元素，检查该元素是否是谷点。如果是，则将谷点的计数增加 1。

```
if (arr[i-1] > arr[i] < arr[i])
     count += 1;
```

下面是上述方法的实现:

## C++

```
// C++ program to count the number
// of valley points in the array
#include<bits/stdc++.h>
using namespace std;

// Function to count the valley points
// in the given character array
int countValleys(int n, int arr[])
{
    int count = 0, temp = 0;

    // Loop to iterate over the
    // elements of the given array
    for(int i = 1; i < n - 1; i++)
    {

       // Condition to check if the given
       // element is a valley point
       if (arr[i - 1] > arr[i] &&
           arr[i] < arr[i + 1])
       {
           count++;
       }
    }
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 3, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << countValleys(n, arr);
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of valley points in the array

import java.io.*;

class GFG {

    // Function to count the valley points
    // in the given character array
    static int countValleys(int n, int arr[])
    {
        int count = 0, temp = 0;

        // Loop to iterate over the elements
        // of the given array
        for (int i = 1; i < n - 1; i++) {

            // Condition to check if the given
            // element is a valley point
            if (arr[i - 1] > arr[i]
                && arr[i] < arr[i + 1]) {
                count++;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 3, 2, 5 };
        int n = arr.length;
        System.out.println(
            countValleys(n, arr));
    }
}
```

## 蟒蛇 3

```
# Python3 program to count the number
# of valley points in the array

# Function to count the valley points
# in the given character array
def countValleys(n, arr):

    count = 0; temp = 0;

    # Loop to iterate over the
    # elements of the given array
    for i in range(1, n):

        # Condition to check if the given
        # element is a valley point
        if (arr[i - 1] > arr[i] and
            arr[i] < arr[i + 1]):

            count += 1;

    return count;

# Driver Code
arr = [ 3, 2, 5 ];
n = len(arr);

print(countValleys(n, arr));

# This code is contributed by Code_Mech
```

## C#

```
// C# program to count the number
// of valley points in the array
using System;
class GFG{

// Function to count the valley points
// in the given character array
static int countValleys(int n, int []arr)
{
    int count = 0;

    // Loop to iterate over the elements
    // of the given array
    for (int i = 1; i < n - 1; i++)
    {

        // Condition to check if the given
        // element is a valley point
        if (arr[i - 1] > arr[i] &&
            arr[i] < arr[i + 1])
        {
            count++;
        }
    }
    return count;
}

// Driver Code
public static void Main()
{
    int []arr = { 3, 2, 5 };
    int n = arr.Length;
    Console.Write(countValleys(n, arr));
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>

// Javascript program to count the number
// of valley points in the array

// Function to count the valley points
// in the given character array
function countValleys(n, arr)
{
    let count = 0, temp = 0;

    // Loop to iterate over the
    // elements of the given array
    for(let i = 1; i < n - 1; i++)
    {

       // Condition to check if the given
       // element is a valley point
       if (arr[i - 1] > arr[i] &&
           arr[i] < arr[i + 1])
       {
           count++;
       }
    }
    return count;
}

// Driver Code
let arr = [ 3, 2, 5 ];
let n = arr.length;

document.write(countValleys(n, arr));

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
1
```