# 为数组中的每个元素找到最近的较小值

> 原文:[https://www . geesforgeks . org/find-最近-数组中每个元素的较小值/](https://www.geeksforgeeks.org/find-closest-smaller-value-for-every-element-in-array/)

给定一个整数数组，为每个元素找到最近的较小元素。如果没有更小的元素，则打印-1

**示例:**

> 输入:arr[] = {10，5，11，6，20，12}
> 输出:6，-1，10，5，12，11
> 
> 输入:arr[] = {10，5，11，10，20，12}
> 输出:5 -1 10 5 12 11

一个简单的解决方案是运行两个嵌套循环。我们一个接一个地挑选外部元素。对于每个拾取的元素，我们遍历剩余的数组并找到最近的较小元素。该方案的时间复杂度为 O(n*n)

一个**更好的解决方案**是使用排序。我们对所有元素进行排序，然后对每个元素向左遍历，直到找到一个更小的元素(请注意，一个元素可以多次出现)。

一个**高效的解决方案**是使用自平衡 BST(实现为 C++中的[集和 Java 中的](https://www.geeksforgeeks.org/set-in-cpp-stl/)[树集](https://www.geeksforgeeks.org/treeset-in-java-with-examples/))。在自平衡 BST 中，我们可以在 O(Log n)时间内完成插入和最近的较小操作。

## C++

```
// C++ program to find closest smaller value for
// every array element
#include <bits/stdc++.h>
using namespace std;

void closestSmaller(int arr[], int n)
{
    // Insert all array elements into a TreeSet
    set<int> ts;
    for (int i = 0; i < n; i++)
        ts.insert(arr[i]);

    // Find largest smaller element for every
    // array element
    for (int i = 0; i < n; i++)
    {
        auto smaller = ts.lower_bound(arr[i]);
        if (smaller == ts.begin())
            cout << -1 << " ";
        else
            cout << *(--smaller) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = {10, 5, 11, 6, 20, 12};
    int n = sizeof(arr) / sizeof(arr[0]);

    closestSmaller(arr, n);

    return 0;
}

// This code is contributed by
// sanjeev2552
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find closest smaller value for
// every array element
import java.util.*;

class TreeSetDemo {
    public static void closestSmaller(int[] arr)
    {
        // Insert all array elements into a TreeSet
        TreeSet<Integer> ts = new TreeSet<Integer>();
        for (int i = 0; i < arr.length; i++)
            ts.add(arr[i]);

        // Find largest smaller element for every
        // array element
        for (int i = 0; i < arr.length; i++) {
            Integer smaller = ts.lower(arr[i]);
            if (smaller == null)
                System.out.print(-1 + " ");
            else
                System.out.print(smaller + " ");
        }
    }

    public static void main(String[] args)
    {
        int[] arr = { 10, 5, 11, 6, 20, 12 };
        closestSmaller(arr);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find closest smaller value
# for every array element
import bisect

def closestSmaller(arr, n):

    # Insert all array elements into a TreeSet
    ts = set()

    for i in range(n):
        ts.add(arr[i])

    # Find largest smaller element for every
    # array element
    for i in range(n):
        smaller = bisect.bisect_left(list(ts), arr[i])

        if (smaller == 0):
            print(-1, end = " ")
        else:
            print((list(ts)[smaller - 1]), end = " ")
            smaller -= 1

# Driver Code
arr = [ 10, 5, 11, 6, 20, 12 ]
n = len(arr)

closestSmaller(arr, n)

# This code is contributed by rohitsingh07052
```

**Output:** 

```
6 -1 10 5 12 11
```

时间复杂度:O(n Log n)