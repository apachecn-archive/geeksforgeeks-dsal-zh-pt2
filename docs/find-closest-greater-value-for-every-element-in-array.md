# 为数组中的每个元素找到最接近的较大值

> 原文:[https://www . geeksforgeeks . org/find-最接近-数组中每个元素的更大值/](https://www.geeksforgeeks.org/find-closest-greater-value-for-every-element-in-array/)

给定一个整数数组，找到每个元素最接近的大元素。如果没有更大的元素，则打印-1
**示例:**

> 输入:arr[] = {10，5，11，6，20，12}
> 输出:11 6 12 10 -1 20
> 输入:arr[] = {10，5，11，10，20，12}
> 输出:11 10 12 11 -1 20

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历剩余的数组并找到最近的较大元素。这个解的时间复杂度是 O(n*n)
A **更好的解**是用排序。我们对所有元素进行排序，然后对每个元素向右遍历，直到找到一个更大的元素(请注意，一个元素可以多次出现)。
一个**高效的解决方案**是使用自平衡 BST(实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/))。在自平衡 BST 中，我们可以在 O(Log n)时间内完成插入和最近的更大操作。

## C++

```
// C++ program to find closest greater value
// for every array element
#include <bits/stdc++.h>
using namespace std;

void closetGreater(int arr[], int n)
{
    // Insert all array elements into a Set
    set<int> ts;
    for (int i = 0; i < n; i++)
        ts.insert(arr[i]);

    // Find smallest greater element for
    // every array element
    for (int i = 0; i < n; i++)
    {
        auto greater = ts.upper_bound(arr[i]);

        if (greater == ts.end())
            cout << -1 << " ";
        else
            cout << *greater << " ";
    }
}

// Driver code
int main(int argc, char const *argv[])
{
    int arr[] = {10, 5, 11, 10, 20, 12};
    int n = sizeof(arr) / sizeof(arr[0]);
    closetGreater(arr, n);
    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest greater value for
// every array element
import java.util.*;

class TreeSetDemo {
    public static void closestGreater(int[] arr)
    {
        // Insert all array elements into a TreeSet
        TreeSet<Integer> ts = new TreeSet<Integer>();
        for (int i = 0; i < arr.length; i++)
            ts.add(arr[i]);

        // Find smallest greater element for every
        // array element
        for (int i = 0; i < arr.length; i++) {
            Integer greater = ts.higher(arr[i]);
            if (greater == null)
                System.out.print(-1 + " ");
            else
                System.out.print(greater + " ");
        }
    }

    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 11, 10, 20, 12};
        closestGreater(arr);
    }
}
```

## java 描述语言

```
<script>

// JavaScript program to find closest greater value
// for every array element

function closetGreater(arr, n) {
    // Insert all array elements into a Set
    let ts = new Set();
    for (let i = 0; i < n; i++)
        ts.add(arr[i]);

    // Find smallest greater element for
    // every array element
    for (let i = 0; i < n; i++) {
        let greater = upper_bound(ts, arr[i]);

        if (!greater)
            document.write(-1 + " ");
        else
            document.write(greater + " ");
    }
}

function upper_bound(s, val) {
    let temp = [...s];
    temp.sort((a, b) => a - b);
    return temp[temp.indexOf(val) + 1];
}

// Driver code

let arr = [10, 5, 11, 10, 20, 12];
let n = arr.length;
closetGreater(arr, n);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
11 10 12 11 -1 20
```

时间复杂度:O(n Log n)