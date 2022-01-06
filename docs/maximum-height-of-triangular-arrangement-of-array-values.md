# 数组值三角形排列的最大高度

> 原文:[https://www . geeksforgeeks . org/最大三角形排列高度值/](https://www.geeksforgeeks.org/maximum-height-of-triangular-arrangement-of-array-values/)

给定一个数组，我们需要从数组值中找到我们能形成的三角形的最大高度，这样每第(i+1)级包含更多的元素，其和大于前一级。
**例:**

```
Input : a = { 40, 100, 20, 30 }
Output : 2
Explanation : We can have 100 and 20 at the bottom level and either 40 or 30 at the upper level of the pyramid

Input : a = { 20, 20, 10, 10, 5, 2 }
Output : 3
```

首先，乍看之下，我们可能需要查看数组值。但事实并非如此。这是这个问题的棘手之处。这里我们不必关心数组的值，因为我们可以在满足这些条件的三角值中排列数组的任何元素。即使像 array = { 3，，3，3，3，3}这样所有元素都相等，我们也可以有解。我们可以在底部放置两个 3，在顶部放置一个 3，或者在底部放置三个 3，在顶部放置两个 3。你可以采取任何你自己的例子，你总是会找到一个解决方案，安排他们在一个配置。所以，如果我们的最大高度是 2，那么我们应该至少有 2 个元素在底部，一个元素在顶部，这意味着我们应该至少有 3 个元素(2*(2+1)/2)。同样，对于 3 作为高度，我们应该在数组中至少有 6 个元素。
因此，我们最终的解决方案只是基于这样的逻辑:如果我们的金字塔有最大高度 **h** *的可能，那么* **(h*(h+1))/2** *元素必须出现在数组中。*
以下是上述方法的实施:

## C++

```
// C++ program to find the maximum height
// of Pyramidal Arrangement of array values
#include <bits/stdc++.h>
using namespace std;

int MaximumHeight(int a[], int n)
{
    int result = 1;
    for (int i = 1; i <= n; ++i) {

        // Just checking whether ith level
        // is possible or not if possible
        // then we must have atleast
        // (i*(i+1))/2 elements in the
        // array
        long long y = (i * (i + 1)) / 2;

        // updating the result value
        // each time
        if (y < n)
            result = i;

        // otherwise we have exceeded n value
        else
            break;
    }
    return result;
}

int main()
{
    int arr[] = { 40, 100, 20, 30 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << MaximumHeight(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find 
// the maximum height of
// Pyramidal Arrangement
// of array values
import java.io.*;

class GFG
{
static int MaximumHeight(int []a,
                         int n)
{

    int result = 1;
    for (int i = 1; i <= n; ++i)
    {

        // Just checking whether
        // ith level is possible
        // or not if possible then
        // we must have atleast
        // (i*(i+1))/2 elements
        // in the array
        int y = (i * (i + 1)) / 2;

        // updating the result
        // value each time
        if (y < n)
            result = i;

        // otherwise we have
        // exceeded n value
        else
            break;
    }
    return result;
}

// Driver Code
public static void main (String[] args)
{
    int []arr = { 40, 100, 20, 30 };
    int n = arr.length;
    System.out.println(MaximumHeight(arr, n));
}
}

// This code is contributed by ajit
```

## 蟒蛇 3

```
# Python program to find the
# maximum height of Pyramidal
# Arrangement of array values

def MaximumHeight(a, n):
    result = 1

    for i in range(1, n):

        # Just checking whether ith level
        # is possible or not if possible
        # then we must have atleast
        # (i*(i+1))/2 elements in the array
        y = (i * (i + 1)) / 2

        # updating the result
        # value each time
        if(y < n):
            result = i

        # otherwise we have
        # exceeded n value
        else:
            break

    return result

# Driver Code
arr = [40, 100, 20, 30]
n = len(arr)
print(MaximumHeight(arr, n))

# This code is contributed by
# Sanjit_Prasad
```

## C#

```
// C# program to find
// the maximum height of
// Pyramidal Arrangement
// of array values
using System;

class GFG
{
static int MaximumHeight(int []a,
                         int n)
{
    int result = 1;
    for (int i = 1; i <= n; ++i)
    {

        // Just checking whether
        // ith level is possible
        // or not if possible then
        // we must have atleast
        // (i*(i+1))/2 elements
        // in the array
        int y = (i * (i + 1)) / 2;

        // updating the result
        // value each time
        if (y < n)
            result = i;

        // otherwise we have
        // exceeded n value
        else
            break;
    }
    return result;
}

// Driver Code
static public void Main ()
{
    int []arr = {40, 100, 20, 30};
    int n = arr.Length;
    Console.WriteLine(MaximumHeight(arr, n));
}
}

// This code is contributed
// by m_kit
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find the maximum height
// of Pyramidal Arrangement of array values

function MaximumHeight($a, $n)
{
    $result = 1;
    for ($i = 1; $i <= $n; ++$i)
    {

        // Just checking whether ith level
        // is possible or not if possible
        // then we must have atleast
        // (i*(i+1))/2 elements in the
        // array
        $y = ($i * ($i + 1)) / 2;

        // updating the result value
        // each time
        if ($y < $n)
            $result = $i;

        // otherwise we have
        // exceeded n value
        else
            break;
    }
    return $result;
}

    // Driver Code
    $arr = array(40, 100, 20, 30);
    $n = count($arr);
    echo MaximumHeight($arr, $n);

// This code is contributed by anuj_67.
?>
```

## java 描述语言

```
<script>
// Javascript program to find 
// the maximum height of
// Pyramidal Arrangement
// of array values
    function MaximumHeight( a ,n)
    {

        let result = 1;
        for ( i = 1; i <= n; ++i) {

            // Just checking whether
            // ith level is possible
            // or not if possible then
            // we must have atleast
            // (i*(i+1))/2 elements
            // in the array
            let y = (i * (i + 1)) / 2;

            // updating the result
            // value each time
            if (y < n)
                result = i;

            // otherwise we have
            // exceeded n value
            else
                break;
        }
        return result;
    }

    // Driver Code
    let arr = [ 40, 100, 20, 30 ];
    let n = arr.length;
    document.write(MaximumHeight(arr, n));

// This code is contributed by Rajput-Ji
</script>
```

**Output:** 

```
2
```