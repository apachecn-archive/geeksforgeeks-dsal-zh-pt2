# 使数组中所有元素相等所需的最小变化

> 原文:[https://www . geeksforgeeks . org/最小-更改-要求使数组中的所有元素相等/](https://www.geeksforgeeks.org/minimum-changes-required-to-make-all-element-in-an-array-equal/)

给定一个长度为 N 的数组，任务是找到使数组中所有元素相等所需的最小运算。
操作如下:

*   用数组的一个相邻元素替换数组中一个元素的值。

**示例:**

```
Input: N = 4, arr[] = {2, 3, 3, 4} 
Output: 2
Explanation:
Replace 2 and 4 by 3

Input: N = 4, arr[] = { 1, 2, 3, 4}
Output: 3
```

**方法:**
让我们假设在执行了所需的最小更改后，数组的所有元素都将变成 X。假设我们只允许用数组的相邻元素替换数组元素的值，那么 X 应该是数组的元素之一。
同样，因为我们需要尽可能最小地进行更改，所以 X 应该是数组中最大出现的元素。一旦我们找到 X 的值，我们只需要对每个不相等的元素(不是 X 的元素)进行一次更改，就可以使数组的所有元素都等于 X。

*   查找数组中最大出现元素的计数。
*   使数组的所有元素相等所需的最小变化是所有元素的
    计数–最大出现元素的计数

下面是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find minimum
// changes required to make
// all elements of the array equal
#include <bits/stdc++.h>
using namespace std;

// Function to count
// of minimum changes
// required to make all
// elements equal
int minChanges(int arr[], int n)
{

    unordered_map<int, int> umap;

    // Store the count of
    // each element as key
    // value pair in unordered map
    for (int i = 0; i < n; i++) {
        umap[arr[i]]++;
    }

    int maxFreq = 0;

    // Find the count of
    // maximum occurring element
    for (auto p : umap) {
        maxFreq = max(maxFreq, p.second);
    }

    // Return count of all
    // element minus count
    // of maximum occurring element
    return n - maxFreq;
}

// Driver code
int main()
{

    int arr[] = { 2, 3, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);

    // Function call
    cout << minChanges(arr, n) << '\n';

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum
// changes required to make
// all elements of the array equal
import java.util.*;

class GFG {

    // Function to count of minimum changes
    // required to make all elements equal
    static int minChanges(int arr[], int n)
    {

        Map<Integer, Integer> mp = new HashMap<>();

        // Store the count of each element
        // as key value pair in map
        for (int i = 0; i < n; i++) {
            if (mp.containsKey(arr[i])) {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }

            else {
                mp.put(arr[i], 1);
            }
        }

        int maxElem = 0;

        // Traverse through map and
        // find the maximum occurring element
        for (Map.Entry<Integer, Integer> entry :
             mp.entrySet()) {

            maxElem = Math.max(maxElem, entry.getValue());
        }

        // Return count of all element minus
        // count of maximum occurring element
        return n - maxElem;
    }

    // Driver code
    public static void main(String[] args)
    {

        int arr[] = { 2, 3, 3, 4 };

        int n = arr.length;

        // Function call
        System.out.println(minChanges(arr, n));
    }
}
```

## C#

```
// C# program to find minimum
// changes required to make
// all elements of the array equal

using System;
using System.Collections.Generic;

class GFG {

    // Function to count of minimum changes
    // required to make all elements equal
    static int minChanges(int[] arr, int n)
    {

        Dictionary<int, int> mp
            = new Dictionary<int, int>();

        // Store the count of each element
        // as key-value pair in Dictionary

        for (int i = 0; i < n; i++) {
            if (mp.ContainsKey(arr[i])) {
                var val = mp[arr[i]];
                mp.Remove(arr[i]);
                mp.Add(arr[i], val + 1);
            }
            else {
                mp.Add(arr[i], 1);
            }
        }

        int maxElem = 0;

        // Traverse through the Dictionary and
        // find the maximum occurring element
        foreach(KeyValuePair<int, int> entry in mp)
        {
            maxElem = Math.Max(maxElem, entry.Value);
        }

        // Return count of all element minus
        // count of maximum occurring element
        return n - maxElem;
    }

    // Driver code
    public static void Main(string[] args)
    {

        int[] arr = { 2, 3, 3, 4 };

        int n = arr.Length;

        // Function call
        Console.WriteLine(minChanges(arr, n));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find minimum
# changes required to make
# all elements of the array equal

# Function to count of minimum changes
# required to make all elements equal
def minChanges(arr, n):

    mp = dict()

    # Store the count of each element
    # as key-value pair in Dictionary

    for i in range(n):
        if arr[i] in mp.keys():
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    maxElem = 0

    # Traverse through the Dictionary and
    # find the maximum occurring element

    for x in mp:
        maxElem = max(maxElem, mp[x])

    # Return count of all element minus
    # count of maximum occurring element
    return n - maxElem

# Driver code

arr = [2, 3, 3, 4]
n = len(arr)

# Function call
print(minChanges(arr, n))
```

## java 描述语言

```
<script>

// Javascript program to find minimum
// changes required to make
// all elements of the array equal

// Function to count
// of minimum changes
// required to make all
// elements equal
function minChanges( arr, n)
{

    var umap = new Map();

    // Store the count of
    // each element as key
    // value pair in unordered map
    for (var i = 0; i < n; i++) {
        if(umap.has(arr[i]))
        {
            umap.set(arr[i], umap.get(arr[i])+1);
        }
        else
        {
            umap.set(arr[i], 1);
        }
    }

    var maxFreq = 0;

    // Find the count of
    // maximum occurring element
    umap.forEach((values,keys)=>{
        maxFreq = Math.max(maxFreq, values);
    });

    // Return count of all
    // element minus count
    // of maximum occurring element
    return n - maxFreq;
}

// Driver code
var arr = [ 2, 3, 3, 4 ];
var n = arr.length;
// Function call
document.write( minChanges(arr, n) + '<br>');

</script>
```

**Output:** 

```
2
```