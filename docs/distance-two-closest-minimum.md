# 两个最近的最小值之间的距离

> 原文:[https://www.geeksforgeeks.org/distance-two-closest-minimum/](https://www.geeksforgeeks.org/distance-two-closest-minimum/)

给定 n 个整数的数组。求数组中任意两个最小整数之间的最小距离。
**例:**

```
Input : arr[] = {5, 1, 2, 3, 4, 1, 2, 1}
Output : 2
Explanation: The minimum element 1 occurs at 
             indexes: 1, 5 and 7\. So the minimum
             distance is 7-5 = 2.

Input : arr[] = {1, 2, 1}
Output : 2
```

**蛮力法**:最简单的方法就是求最小元素的所有对指标，计算最小距离。
时间复杂度:O(n^2)，其中 n 是数组中元素的总数。
**有效方法**:一个有效的方法是观察索引 j 和 I 之间的距离总是小于索引 k 和 I 之间的距离，其中，k 大于 j。也就是说，我们只需要检查连续的最小元素对之间的距离，而不是所有对之间的距离。下面是分步算法:

*   找到数组中的最小元素
*   查找数组中所有出现的最小元素，并将索引插入到新的数组、列表或向量中。
*   检查索引列表的大小是否大于 1，即最小元素至少出现两次。如果不是，返回-1。
*   遍历索引列表，计算任意两个连续索引之间的最小差异。

以下是上述思路的实现:

## C++

```
// CPP program to find Distance between
// two closest minimum
#include <iostream>
#include <limits.h>
#include <vector>

using namespace std;

// function to find Distance between
// two closest minimum
int findClosestMin(int arr[], int n)
{
    int min = INT_MAX;

    // find the min element in the array
    for (int i = 0; i < n; i++)
        if (arr[i] < min)
            min = arr[i];

    // vector to store indexes of occurrences
    // of minimum element in the array
    vector<int> indexes;

    // store indexes of occurrences
    // of minimum element in the array
    for (int i = 0; i < n; i++)
        if (arr[i] == min)
            indexes.push_back(i);

    // if minimum element doesnot occurs atleast
    // two times, return -1.
    if (indexes.size() < 2)
        return -1;

    int min_dist = INT_MAX;

    // calculate minimum difference between
    // any two consecutive indexes
    for (int i = 1; i < indexes.size(); i++)
        if ((indexes[i] - indexes[i - 1]) < min_dist)
            min_dist = (indexes[i] - indexes[i - 1]);

    return min_dist;
}

// Driver code
int main()
{
    int arr[] = { 5, 1, 2, 3, 4, 1, 2, 1 };
    int size = sizeof(arr) / sizeof(arr[0]);
    cout << findClosestMin(arr, size);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Distance between
// two closest minimum
import java.util.Vector;

class GFG {

// function to find Distance between
// two closest minimum
    static int findClosestMin(int arr[], int n) {
        int min = Integer.MAX_VALUE;

        // find the min element in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }

        // vector to store indexes of occurrences
        // of minimum element in the array
        Vector<Integer> indexes = new Vector<>();

        // store indexes of occurrences
        // of minimum element in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] == min) {
                indexes.add(i);
            }
        }

        // if minimum element doesnot occurs atleast
        // two times, return -1.
        if (indexes.size() < 2) {
            return -1;
        }

        int min_dist = Integer.MAX_VALUE;

        // calculate minimum difference between
        // any two consecutive indexes
        for (int i = 1; i < indexes.size(); i++) {
            if ((indexes.get(i) - indexes.get(i - 1)) < min_dist) {
                min_dist = (indexes.get(i) - indexes.get(i - 1));
            }
        }

        return min_dist;
    }

// Driver code
    public static void main(String args[]) {
        int arr[] = {5, 1, 2, 3, 4, 1, 2, 1};
        int size = arr.length;
        System.out.println(findClosestMin(arr, size));
    }
}

// This code is contributed by PrinciRaj19992
```

## 蟒蛇 3

```
# Python3 program to find Distance
# between two closest minimum
import sys

# function to find Distance between
# two closest minimum
def findClosestMin(arr, n):

    #assigning maximum value in python
    min = sys.maxsize

    for i in range(0, n):
        if (arr[i] < min):
            min = arr[i]

    # list in python to store indexes
    # of occurrences of minimum element
    # in the array
    indexes = []

    # store indexes of occurrences
    # of minimum element in the array
    for i in range(0, n):
        if (arr[i] == min):
            indexes.append(i)

    # if minimum element doesnot occurs
    #  atleast two times, return -1.
    if (len(indexes) < 2):
        return -1

    min_dist = sys.maxsize

    # calculate minimum difference between
    # any two consecutive indexes
    for i in range(1, len(indexes)):
        if ((indexes[i] - indexes[i - 1]) < min_dist):
            min_dist = (indexes[i] - indexes[i - 1]);

    return min_dist;

# Driver code
arr = [ 5, 1, 2, 3, 4, 1, 2, 1 ]
ans = findClosestMin(arr, 8)
print (ans)

# This code is contributed by saloni1297.
```

## C#

```

// C# program to find Distance between
// two closest minimum
using System;
using System.Collections.Generic;
public class GFG {

// function to find Distance between
// two closest minimum
    static int findClosestMin(int []arr, int n) {
        int min = int.MaxValue;

        // find the min element in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }

        // vector to store indexes of occurrences
        // of minimum element in the array
        List<int> indexes = new List<int>();

        // store indexes of occurrences
        // of minimum element in the array
        for (int i = 0; i < n; i++) {
            if (arr[i] == min) {
                indexes.Add(i);
            }
        }

        // if minimum element doesnot occurs atleast
        // two times, return -1.
        if (indexes.Count < 2) {
            return -1;
        }
        int min_dist = int.MaxValue;

        // calculate minimum difference between
        // any two consecutive indexes
        for (int i = 1; i < indexes.Count; i++) {
            if ((indexes[i] - indexes[i-1]) < min_dist) {
                min_dist = (indexes[i] - indexes[i-1]);
            }
        }

        return min_dist;
    }

// Driver code
    public static void Main() {
        int []arr = {5, 1, 2, 3, 4, 1, 2, 1};
        int size = arr.Length;
        Console.WriteLine(findClosestMin(arr, size));
    }
}

// This code is contributed by PrinciRaj19992
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// Php program to find Distance between
// two closest minimum

// function to find Distance between
// two closest minimum
function findClosestMin($arr, $n)
{
    $min = PHP_INT_MAX;

    # find the min element in the array
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] < $min)
            $min = $arr[$i];

    // vector to store indexes of occurrences
    // of minimum element in the array
    $indexes = array() ;

    // store indexes of occurrences
    // of minimum element in the array
    for ($i = 0; $i < $n; $i++)
        if ($arr[$i] == $min)
            array_push($indexes, $i);

    // if minimum element doesnot occurs atleast
    // two times, return -1.
    if (sizeof($indexes) < 2)
        return -1;

    $min_dist = PHP_INT_MAX;

    // calculate minimum difference between
    // any two consecutive indexes
    for ($i = 1; $i < sizeof($indexes); $i++)
        if (($indexes[$i] -
             $indexes[$i - 1]) < $min_dist)
            $min_dist = ($indexes[$i] -
                         $indexes[$i - 1]);

    return $min_dist;
}

// Driver code
$arr = array( 5, 1, 2, 3, 4, 1, 2, 1 );
$size = sizeof($arr);
echo findClosestMin($arr, $size);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
    // Javascript program to find Distance between two closest minimum

    // function to find Distance between
    // two closest minimum
    function findClosestMin(arr, n) {
        let min = Number.MAX_VALUE;

        // find the min element in the array
        for (let i = 0; i < n; i++) {
            if (arr[i] < min) {
                min = arr[i];
            }
        }

        // vector to store indexes of occurrences
        // of minimum element in the array
        let indexes = [];

        // store indexes of occurrences
        // of minimum element in the array
        for (let i = 0; i < n; i++) {
            if (arr[i] == min) {
                indexes.push(i);
            }
        }

        // if minimum element doesnot occurs atleast
        // two times, return -1.
        if (indexes.length < 2) {
            return -1;
        }
        let min_dist = Number.MAX_VALUE;

        // calculate minimum difference between
        // any two consecutive indexes
        for (let i = 1; i < indexes.length; i++) {
            if ((indexes[i] - indexes[i-1]) < min_dist) {
                min_dist = (indexes[i] - indexes[i-1]);
            }
        }

        return min_dist;
    }

    let arr = [5, 1, 2, 3, 4, 1, 2, 1];
    let size = arr.length;
    document.write(findClosestMin(arr, size));

    // This code is contributed by suresh07.
</script>
```

**输出:**

```
2
```

**时间复杂度**:O(n)
T3】辅助空间 : O(n)