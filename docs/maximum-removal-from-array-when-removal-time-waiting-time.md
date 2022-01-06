# 移除时间> =等待时间

时从阵列中移除的最大值

> 原文:[https://www . geesforgeks . org/最大-从阵列中移除-移除时-等待时间/](https://www.geeksforgeeks.org/maximum-removal-from-array-when-removal-time-waiting-time/)

假设一个数组中有 N 个元素。任务是从左到右移除数组中的元素。然而，从数组中移除一个元素需要一些时间(让我们称之为**移除时间**)。移除元素的时间等于该元素的的值(以秒为单位)。
一个元素只有在移除它所需的时间(移除时间)大于或等于它在数组中等待的时间时才能被移除。

**注意**:在开始移除元素之前，允许改变数组中元素的顺序。您的任务是找到可以从数组中移除的元素的最大数量。

**示例:**

> **输入** : arr[] = {6，5，11，3}
> **输出** : 3
> **解释**:让我们按照以下方式对元素重新排序:
> 3，5，6，11
> -第一个元素需要 3 秒钟才能被移除。因为它是第一个元素，所以可以在 3 秒钟内移除。
> -第二个元素在数组中等待 3 秒。这个元素需要 5 秒钟才能被移除，这比它的等待时间还长，因此它可以被移除。
> -第三个元素在数组中等待 8 秒。这个元素需要 6 秒钟才能被移除，这比它的等待时间要短，因此它不能被移除并且被跳过。
> -第四个元素也在数组中等待 8 秒。这个元素需要 11 秒钟才能被移除，这比它的等待时间还长，因此它可以被移除。
> -因此，最多可以移除 3 个元素。
> 
> **输入** : arr[] = {5，4，1，10}
> **输出** : 4
> **解释**:我们按照以下方式对元素重新排序:
> 1，4，5，10
> 可以观察到，由于每个元素的移除时间大于或等于它们的等待时间，所以它们都可以被移除。

其思想是将所有元素按照移除时间的**升序**排列。从左侧开始迭代，保持移除时间的**累计和**(这将作为下一个元素的**等待时间**)。检查每个元素的移除时间是否大于或等于累计时间(等待时间)。如果小于，则不能移除。如果它等于或大于，则可以删除它，并将其删除时间加到累计总和中。一直进行到数组的末尾。

下面是上述方法的实现:

## C++

```
// C++ code to find the maximum number of
// elements that can be removed
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum number of
// elements that can be removed
int maxRemoval(int arr[], int n)
{
    // it will contain frequency of
    // elements that can be removed
    int count = 0;

    // maintain cumulative sum of removal time
    int cumulative_sum = 0;

    // arrange elements in ascending order
    // of their removal time
    sort(arr, arr + n);

    for (int i = 0; i < n; i++) {
        if (arr[i] >= cumulative_sum) {
            count++;
            cumulative_sum += arr[i];
        }
    }

    return count;
}

// Driver code
int main()
{
    int arr[] = { 10, 5, 3, 7, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << maxRemoval(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the maximum number of
// elements that can be removed
import java.io.*;
import java.util.*;

class GFG {

// Function to find maximum number of
// elements that can be removed
static int maxRemoval(int arr[], int n)
{
    // it will contain frequency of
    // elements that can be removed
    int count = 0;

    // maintain cumulative sum of removal time
    int cumulative_sum = 0;

    // arrange elements in ascending order
    // of their removal time
    Arrays.sort(arr);

    for (int i = 0; i < n; i++) {
        if (arr[i] >= cumulative_sum) {
            count++;
            cumulative_sum += arr[i];
        }
    }

    return count;
}

// Driver code

    public static void main (String[] args) {
        int arr[] = { 10, 5, 3, 7, 2 };
    int n = arr.length;
    System.out.println(maxRemoval(arr, n));
    }
}
// This code is contributed
// by inder_verma..
```

## 蟒蛇 3

```
# Python3 code to find the maximum number
# of elements that can be removed

# Function to find maximum number of
# elements that can be removed
def maxRemoval(arr, n):

    # It will contain frequency of
    # elements that can be removed
    count = 0

    # maintain cumulative sum of
    # removal time
    cumulative_sum = 0

    # arrange elements in ascending
    # order of their removal time
    arr.sort()

    for i in range(n):
        if arr[i] >= cumulative_sum:
            count += 1
            cumulative_sum += arr[i]

    return count

# Driver code
if __name__ == "__main__":

    arr = [10, 5, 3, 7, 2]
    n = len(arr)

    print(maxRemoval(arr, n))

# This code is contributed by
# Rituraj Jain
```

## C#

```
// C# code to find the maximum number
// of elements that can be removed
using System;

class GFG
{

// Function to find maximum number
// of elements that can be removed
static int maxRemoval(int[] arr, int n)
{
    // it will contain frequency of
    // elements that can be removed
    int count = 0;

    // maintain cumulative sum
    // of removal time
    int cumulative_sum = 0;

    // arrange elements in ascending
    // order of their removal time
    Array.Sort(arr);

    for (int i = 0; i < n; i++)
    {
        if (arr[i] >= cumulative_sum)
        {
            count++;
            cumulative_sum += arr[i];
        }
    }

    return count;
}

// Driver code
public static void Main ()
{
    int[] arr = { 10, 5, 3, 7, 2 };
    int n = arr.Length;
    Console.Write(maxRemoval(arr, n));
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the maximum
// number of elements that can
// be removed

// Function to find maximum number
// of elements that can be removed
function maxRemoval(&$arr, $n)
{
    // it will contain frequency of
    // elements that can be removed
    $count = 0;

    // maintain cumulative
    // sum of removal time
    $cumulative_sum = 0;

    // arrange elements in ascending
    // order of their removal time
    sort($arr);

    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] >= $cumulative_sum)
        {
            $count++;
            $cumulative_sum += $arr[$i];
        }
    }

    return $count;
}

// Driver code
$arr = array(10, 5, 3, 7, 2 );
$n = sizeof($arr);

echo (maxRemoval($arr, $n));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>

// Javascript code to find the maximum number of
// elements that can be removed

// Function to find maximum number of
// elements that can be removed
function maxRemoval(arr, n)
{
    // it will contain frequency of
    // elements that can be removed
    var count = 0;

    // maintain cumulative sum of removal time
    var cumulative_sum = 0;

    // arrange elements in ascending order
    // of their removal time
    arr.sort((a,b)=> a-b);

    for (var i = 0; i < n; i++) {
        if (arr[i] >= cumulative_sum) {
            count++;
            cumulative_sum += arr[i];
        }
    }

    return count;
}

// Driver code
var arr = [ 10, 5, 3, 7, 2 ];
var n = arr.length;
document.write( maxRemoval(arr, n));

</script>
```

**Output:** 

```
4
```