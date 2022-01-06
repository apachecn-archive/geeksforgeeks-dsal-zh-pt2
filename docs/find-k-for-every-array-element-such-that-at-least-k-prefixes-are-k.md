# 为每个数组元素寻找 K，使得至少 K 个前缀≥ K

> 原文:[https://www . geesforgeks . org/find-k-for-ever-array-element-so-至少-k-前缀是-k/](https://www.geeksforgeeks.org/find-k-for-every-array-element-such-that-at-least-k-prefixes-are-k/)

给定一个由非负整数 **N** 组成的数组**arr【】**，任务是为每个索引找到一个整数 **K** ，使得数组中至少有 K 个整数，直到该索引大于或等于 K

**注意:**考虑基于 1 的索引

**示例:**

> **输入:** arr[] = {3，0，6，1，5}
> **输出:** K = {1，1，2，2，3}
> **解释:**
> 在索引 1 处，数组中有 1 个大于或等于 1 的数字，即 3。所以直到索引 1 的元素的 K 值是 1。
> 在索引 2 处，数组中有 1 个大于或等于 1 的数字，即 3。所以直到索引 2 的元素的 K 值是 1。
> 在索引 3 处，数组中有 2 个大于或等于 2 的数字，即 3 和 6。所以直到索引 3 的元素的 K 值是 2。
> 在索引 4 处，数组中有 2 个大于或等于 2 的数字，即 3 和 6。所以直到索引 4 的元素的 K 值是 2。
> 在索引 5 处，数组中有 3 个大于或等于 3 的数字，即 3、6 和 5。所以直到索引 5 的元素的 K 值是 3。
> 
> **输入:** arr[] = {9，10，7，5，0，10，2，0}
> **输出:** K = {1，2，3，4，4，5，5，5}

**天真方法:**
最简单的方法是找到范围**【0，I】**内数组所有元素的 **K** 的值，其中 **i** 是数组的索引**arr【】**，使用文章[中使用的高效方法链接在此给出](https://www.geeksforgeeks.org/maximum-value-k-such-that-array-has-at-least-k-elements-that-are-k/)。

***时间复杂度:**O(N<sup>2</sup>)*
***空间复杂度:** O(N)*

**高效方法:**
想法是使用[多集(红黑树)](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)。多集以排序顺序存储值，这有助于检查多集中的当前最小值是否大于或等于其大小。如果是，那么整数 K 的值将是多集的大小。

以下是实施步骤:

1.  从索引 0 到 N-1 遍历数组。
2.  对于每个索引，将元素插入多集，并检查多集中的最小值是否小于多集的大小。
3.  如果为真，则擦除起始元素并打印多集的大小。
4.  如果为 false，则只需打印多集的大小。
5.  多集的大小是每个索引 I 所需的 K 值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the K-value
// for every index in the array
int print_h_index(int arr[], int N)
{
    // Multiset to store the array
    // in the form of red-black tree
    multiset<int> ms;

    // Iterating over the array
    for (int i = 0; i < N; i++) {

        // Inserting the current
        // value in the multiset
        ms.insert(arr[i]);

        // Condition to check if
        // the smallest value
        // in the set is less than
        // it's size
        if (*ms.begin()
            < ms.size()) {

            // Erase the smallest
            // value
            ms.erase(ms.begin());
        }

        // h-index value will be
        // the size of the multiset
        cout << ms.size() << " ";
    }
}

// Driver Code
int main()
{

    // array
    int arr[] = { 9, 10, 7, 5, 0,
                10, 2, 0 };

    // Size of the array
    int N = sizeof(arr)
            / sizeof(arr[0]);

    // function call
    print_h_index(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to find the K-value
// for every index in the array
static void print_h_index(int arr[], int N)
{

    // Multiset to store the array
    // in the form of red-black tree
    List<Integer> ms = new ArrayList<Integer>();

    // Iterating over the array
    for(int i = 0; i < N; i++)
    {

        // Inserting the current
        // value in the multiset
        ms.add(arr[i]);

        // Condition to check if
        // the smallest value
        // in the set is less than
        // it's size
        int t = Collections.min(ms);
        if (t < ms.size())
        {

            // Erase the smallest
            // value
            ms.remove(ms.indexOf(t));
        }

        // h-index value will be
        // the size of the multiset
        System.out.print(ms.size() + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    // Array
    int arr[] = { 9, 10, 7, 5, 0,
                10, 2, 0 };

    // Size of the array
    int N = arr.length;

    // Function call
    print_h_index(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the K-value
# for every index in the array
def print_h_index(arr, N):

    # Multiset to store the array
    # in the form of red-black tree
    ms = []

    # Iterating over the array
    for i in range(N):

        # Inserting the current
        # value in the multiset
        ms.append(arr[i])
        ms.sort()

        # Condition to check if
        # the smallest value
        # in the set is less than
        # it's size
        if (ms[0] < len(ms)):

            # Erase the smallest
            # value
            ms.pop(0)

        # h-index value will be
        # the size of the multiset
        print(len(ms), end = ' ')

# Driver Code
if __name__=='__main__':

    # Array
    arr = [ 9, 10, 7, 5, 0, 10, 2, 0 ]

    # Size of the array
    N = len(arr)

    # Function call
    print_h_index(arr, N)

# This code is contributed by pratham76
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Function to find the K-value
// for every index in the array
static void print_h_index(int []arr, int N)
{

    // Multiset to store the array
    // in the form of red-black tree
    ArrayList ms = new ArrayList();

    // Iterating over the array
    for(int i = 0; i < N; i++)
    {

        // Inserting the current
        // value in the multiset
        ms.Add(arr[i]);

        // Condition to check if
        // the smallest value
        // in the set is less than
        // it's size
        int t = int.MaxValue;
        foreach(int x in ms)
        {
            if(x < t)
            {
                t = x;
            }
        }

        if (t < ms.Count)
        {

            // Erase the smallest
            // value
            ms.Remove(t);
        }

        // h-index value will be
        // the size of the multiset
        Console.Write(ms.Count + " ");
    }
}

// Driver code
public static void Main(string[] args)
{

    // Array
    int []arr = { 9, 10, 7, 5, 0,
                  10, 2, 0 };

    // Size of the array
    int N = arr.Length;

    // Function call
    print_h_index(arr, N);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the K-value
// for every index in the array
function print_h_index(arr, N)
{
    // Multiset to store the array
    // in the form of red-black tree
    var ms = []; 

    // Iterating over the array
    for (var i = 0; i < N; i++) {

        // Inserting the current
        // value in the multiset
        ms.push(arr[i]);
        ms.sort((a,b)=> a-b)
        // Condition to check if
        // the smallest value
        // in the set is less than
        // it's size
        if (ms[0]
            < ms.length) {

            // Erase the smallest
            // value
            ms.shift();
        }

        // h-index value will be
        // the size of the multiset
        document.write( ms.length + " ");
    }
}

// Driver Code
// array
var arr = [9, 10, 7, 5, 0,
            10, 2, 0 ];
// Size of the array
var N = arr.length;
// function call
print_h_index(arr, N);

</script>
```

**Output:** 

```
1 2 3 4 4 5 5 5
```

***时间复杂度:** O(N * log(N))*
***辅助空间复杂度:** O(N)*