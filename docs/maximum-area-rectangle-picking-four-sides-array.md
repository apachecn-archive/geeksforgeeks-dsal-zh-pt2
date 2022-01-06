# 从数组中选取四条边得到的最大面积矩形

> 原文:[https://www . geesforgeks . org/最大面积-矩形-拾取-四边-数组/](https://www.geeksforgeeks.org/maximum-area-rectangle-picking-four-sides-array/)

给定代表长度的 n 个正整数的数组。找出最大可能的区域，其四条边是从给定的数组中选取的。请注意，只有当给定数组中有两对相等的值时，才能形成矩形。

**示例:**

```
Input : arr[] = {2, 1, 2, 5, 4, 4}
Output : 8
Explanation : Dimension will be 4 * 2

Input : arr[] = {2, 1, 3, 5, 4, 4}
Output : 0
Explanation : No rectangle possible
```

**方法 1(排序)**
任务基本缩减为寻找数组中两对相等的值。如果有两对以上，则选择具有最大值的两对。一个简单的解决方案是执行以下操作。
1)给定数组排序。
2)从最大值到最小值遍历数组，返回两对最大值。

## C++

```
// CPP program for finding maximum area possible
// of a rectangle
#include <bits/stdc++.h>
using namespace std;

// function for finding max area
int findArea(int arr[], int n)
{
    // sort array in non-increasing order
    sort(arr, arr + n, greater<int>());

    // Initialize two sides of rectangle
    int dimension[2] = { 0, 0 };

    // traverse through array
    for (int i = 0, j = 0; i < n - 1 && j < 2; i++)

        // if any element occurs twice
        // store that as dimension
        if (arr[i] == arr[i + 1])
            dimension[j++] = arr[i++];

    // return the product of dimensions
    return (dimension[0] * dimension[1]);
}

// driver function
int main()
{
    int arr[] = { 4, 2, 1, 4, 6, 6, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findArea(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding maximum area
// possible of a rectangle
import java.util.Arrays;
import java.util.Collections;

public class GFG
{    
    // function for finding max area
    static int findArea(Integer arr[], int n)
    {
        // sort array in non-increasing order
        Arrays.sort(arr, Collections.reverseOrder());

        // Initialize two sides of rectangle
        int[] dimension = { 0, 0 };

        // traverse through array
        for (int i = 0, j = 0; i < n - 1 && j < 2;
                                           i++)

            // if any element occurs twice
            // store that as dimension
            if (arr[i] == arr[i + 1])
                dimension[j++] = arr[i++];

        // return the product of dimensions
        return (dimension[0] * dimension[1]);
    }

    // driver function
    public static void main(String args[])
    {
        Integer arr[] = { 4, 2, 1, 4, 6, 6, 2, 5 };
        int n = arr.length;
        System.out.println(findArea(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program for finding
# maximum area possible of
# a rectangle

# function for finding
# max area
def findArea(arr, n):

    # sort array in
    # non-increasing order
    arr.sort(reverse = True)

    # Initialize two
    # sides of rectangle
    dimension = [0, 0]

    # traverse through array
    i = 0
    j = 0
    while(i < n - 1 and j < 2):

        # if any element occurs twice
        # store that as dimension
        if (arr[i] == arr[i + 1]):
            dimension[j] = arr[i]
            j += 1
            i += 1
        i += 1

    # return the product
    # of dimensions
    return (dimension[0] *
            dimension[1])

# Driver code
arr = [4, 2, 1, 4, 6, 6, 2, 5]
n = len(arr)
print(findArea(arr, n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program for finding maximum area
// possible of a rectangle
using System;
using System.Collections;

class GFG
{
// function for finding max area
static int findArea(int []arr, int n)
{
    // sort array in non-increasing order
    Array.Sort(arr);
    Array.Reverse(arr);

    // Initialize two sides of rectangle
    int[] dimension = { 0, 0 };

    // traverse through array
    for (int i = 0, j = 0;
             i < n - 1 && j < 2; i++)

        // if any element occurs twice
        // store that as dimension
        if (arr[i] == arr[i + 1])
            dimension[j++] = arr[i++];

    // return the product of dimensions
    return (dimension[0] * dimension[1]);
}

// Driver Code
public static void Main(String []args)
{
    int []arr = { 4, 2, 1, 4, 6, 6, 2, 5 };
    int n = arr.Length;
    Console.Write(findArea(arr, n));
}
}

// This code is contributed
// by PrinciRaj1992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program for finding maximum area possible
// of a rectangle

// function for finding max area
function findArea($arr, $n)
{

    // sort array in non-
    // increasing order
    rsort($arr);

    // Initialize two sides
    // of rectangle
    $dimension = array( 0, 0 );

    // traverse through array
    for( $i = 0, $j = 0; $i < $n - 1 &&
                           $j < 2; $i++)

        // if any element occurs twice
        // store that as dimension
        if ($arr[$i] == $arr[$i + 1])
            $dimension[$j++] = $arr[$i++];

    // return the product
    // of dimensions
    return ($dimension[0] *
            $dimension[1]);
}

    // Driver Code
    $arr = array(4, 2, 1, 4, 6, 6, 2, 5);
    $n =count($arr);
    echo findArea($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>

// Javascript program for finding maximum area possible
// of a rectangle

// function for finding max area
function findArea(arr, n)
{
    // sort array in non-increasing order
    arr.sort((a,b)=>{return b-a;})

    // Initialize two sides of rectangle
    var dimension = [0,0];

    // traverse through array
    for (var i = 0, j = 0; i < n - 1 && j < 2; i++)

        // if any element occurs twice
        // store that as dimension
        if (arr[i] == arr[i + 1])
            dimension[j++] = arr[i++];

    // return the product of dimensions
    return (dimension[0] * dimension[1]);
}

// driver function
var arr = [ 4, 2, 1, 4, 6, 6, 2, 5 ];
var n = arr.length;
document.write( findArea(arr, n));

</script>
```

**输出:**

```
24
```

时间复杂度:O(n Log n)

**方法 2 (Hashing)**
想法是将所有第一次出现的元素插入一个 hash 集中。对于第二次出现，记录最大两个值。

## C++

```
// CPP program for finding maximum area possible
// of a rectangle
#include <bits/stdc++.h>
using namespace std;

// function for finding max area
int findArea(int arr[], int n)
{
    unordered_set<int> s;

    // traverse through array
    int first = 0, second = 0;
    for (int i = 0; i < n; i++) {

        // If this is first occurrence of arr[i],
        // simply insert and continue
        if (s.find(arr[i]) == s.end()) {
            s.insert(arr[i]);
            continue;
        }

        // If this is second (or more) occurrence,
        // update first and second maximum values.
        if (arr[i] > first) {
            second = first;
            first = arr[i];
        } else if (arr[i] > second)
            second = arr[i];
    }

    // return the product of dimensions
    return (first * second);
}

// driver function
int main()
{
    int arr[] = { 4, 2, 1, 4, 6, 6, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << findArea(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for finding maximum
// area possible of a rectangle
import java.util.HashSet;
import java.util.Set;

public class GFG
{    
    // function for finding max area
    static int findArea(int arr[], int n)
    {
        //unordered_set<int> s;

        Set<Integer> s = new HashSet<>();

        // traverse through array
        int first = 0, second = 0;
        for (int i = 0; i < n; i++) {

            // If this is first occurrence of
            // arr[i], simply insert and continue
            if (!s.contains(arr[i])) {
                s.add(arr[i]);
                continue;
            }

            // If this is second (or more)
            // occurrence, update first and
            // second maximum values.
            if (arr[i] > first) {
                second = first;
                first = arr[i];
            } else if (arr[i] > second)
                second = arr[i];
        }

        // return the product of dimensions
        return (first * second);
    }

    // driver function
    public static void main(String args[])
    {
        int arr[] = { 4, 2, 1, 4, 6, 6, 2, 5 };
        int n = arr.length;
        System.out.println(findArea(arr, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python 3 program for finding maximum
# area possible of a rectangle

# function for finding max area
def findArea(arr, n):

    s = []

    # traverse through array
    first = 0
    second = 0
    for i in range(n) :

        # If this is first occurrence of
        # arr[i], simply insert and continue
        if arr[i] not in s:
            s.append(arr[i])
            continue

        # If this is second (or more) occurrence,
        # update first and second maximum values.
        if (arr[i] > first) :
            second = first
            first = arr[i]
        elif (arr[i] > second):
            second = arr[i]

    # return the product of dimensions
    return (first * second)

# Driver Code
if __name__ == "__main__":

    arr = [ 4, 2, 1, 4, 6, 6, 2, 5 ]
    n = len(arr)
    print(findArea(arr, n))

# This code is contributed by ita_c
```

## C#

```
using System;
using System.Collections.Generic;

// c# program for finding maximum 
// area possible of a rectangle

public class GFG
{
    // function for finding max area
    public static int findArea(int[] arr, int n)
    {
        //unordered_set<int> s;

        ISet<int> s = new HashSet<int>();

        // traverse through array
        int first = 0, second = 0;
        for (int i = 0; i < n; i++)
        {

            // If this is first occurrence of 
            // arr[i], simply insert and continue
            if (!s.Contains(arr[i]))
            {
                s.Add(arr[i]);
                continue;
            }

            // If this is second (or more) 
            // occurrence, update first and 
            // second maximum values.
            if (arr[i] > first)
            {
                second = first;
                first = arr[i];
            }
            else if (arr[i] > second)
            {
                second = arr[i];
            }
        }

        // return the product of dimensions
        return (first * second);
    }

    // driver function
    public static void Main(string[] args)
    {
        int[] arr = new int[] {4, 2, 1, 4, 6, 6, 2, 5};
        int n = arr.Length;
        Console.WriteLine(findArea(arr, n));
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// Javascript program for finding maximum
// area possible of a rectangle

// Function for finding max area
function findArea(arr, n)
{
    let s = new Set();

    // Traverse through array
    let first = 0, second = 0;
    for(let i = 0; i < n; i++)
    {

        // If this is first occurrence of
        // arr[i], simply insert and continue
        if (!s.has(arr[i]))
        {
            s.add(arr[i]);
            continue;
        }

        // If this is second (or more)
        // occurrence, update first and
        // second maximum values.
        if (arr[i] > first)
        {
            second = first;
            first = arr[i];
        }
        else if (arr[i] > second)
            second = arr[i];
    }

    // Return the product of dimensions
    return (first * second);
}

// Driver Code
let arr = [ 4, 2, 1, 4, 6, 6, 2, 5 ];
let n = arr.length;

document.write(findArea(arr, n));

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
24
```

**时间复杂度:** O(n)

本文由[**Shivam Pradhan(anuj _ charm)**](https://www.linkedin.com/in/imanuj)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。