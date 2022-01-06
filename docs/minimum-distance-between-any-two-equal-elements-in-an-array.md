# 数组中任意两个相等元素之间的最小距离

> 原文:[https://www . geesforgeks . org/任意两个相等数组元素之间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-any-two-equal-elements-in-an-array/)

给定一个数组 **arr** ，任务是找到数组中任意两个相同元素之间的最小距离。如果没有找到这样的元素，返回-1。

**示例:**

> **输入:** arr = {1，2，3，2，1}
> **输出:** 2
> **解释:**
> 这个数组中有两个匹配的值对:1 和 2。
> 两个 1 之间的最小距离= 4
> 两个 2 之间的最小距离= 2
> 因此，数组中任意两个相等元素之间的最小距离= 2
> 
> **输入:** arr = {3，5，4，6，5，3}
> **输出:** 3
> **解释:**
> 这个数组中有两对匹配的值:3 和 5。
> 两个 3 之间的最小距离= 5
> 两个 5 之间的最小距离= 3
> 因此，数组中任意两个相等元素之间的最小距离= 3

**天真方法:**最简单的方法是使用两个[嵌套的循环](https://www.geeksforgeeks.org/java-nested-loops-with-examples/)来形成每个组合。如果元素相等，求最小距离。
***时间复杂度:** O(N <sup>2</sup> )*

**有效方法:**解决这个问题的有效方法是使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)将**数组元素存储为关键字，将它们的索引存储为值**。

下面是分步算法:

1.  [逐个遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)。
2.  [检查该元素是否在地图中](https://www.geeksforgeeks.org/check-key-present-cpp-map-unordered_map/)。
    *   如果地图不包含此元素，将其作为**(元素，当前索引)对**插入。
    *   如果数组元素存在于映射中，则从映射中获取该元素的前一个索引。
3.  找出前一个索引和当前索引之间的差异
4.  比较每个差异和[找到最小](https://www.geeksforgeeks.org/find-the-minimum-distance-between-two-numbers/)距离。
5.  如果没有找到这样的元素，返回-1。

下面是上述方法的实现。

## C++

```
// C++ program to find the minimum distance
// between two occurrences of the same element
#include<bits/stdc++.h>
using namespace std;

// Function to find the minimum
// distance between the same elements
int minimumDistance(int a[], int n)
{

    // Create a HashMap to
    // store (key, values) pair.
    map<int,int> hmap;

    int minDistance = INT_MAX;

    // Initialize previousIndex
    // and currentIndex as 0
    int previousIndex = 0, currentIndex = 0;

    // Traverse the array and
    // find the minimum distance
    // between the same elements with map

    for (int i = 0; i < n; i++) {

        if (hmap.find(a[i])!=hmap.end()) {
            currentIndex = i;

            // Fetch the previous index from map.
            previousIndex = hmap[a[i]];

            // Find the minimum distance.
            minDistance = min((currentIndex -
                        previousIndex),minDistance);
        }

        // Update the map.
        hmap[a[i]] = i;
    }

    // return minimum distance,
    // if no such elements found, return -1
    return (minDistance == INT_MAX ? -1 : minDistance);
}

// Driver code
int main()
{

    // Test Case 1:
    int a1[] = { 1, 2, 3, 2, 1 };
    int n = sizeof(a1)/sizeof(a1[0]);

    cout << minimumDistance(a1, n) << endl;

    // Test Case 2:
    int a2[] = { 3, 5, 4, 6, 5, 3 };
    n = sizeof(a2)/sizeof(a2[0]);
    cout << minimumDistance(a2, n) << endl;

    // Test Case 3:
    int a3[] = { 1, 2, 1, 4, 1 };
    n = sizeof(a3)/sizeof(a3[0]);

    cout << minimumDistance(a3, n) << endl;
}

// This code is contributed by Sanjit_Prasad
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the minimum distance
// between two occurrences of the same element

import java.util.*;
import java.math.*;

class GFG {

    // Function to find the minimum
    // distance between the same elements
    static int minimumDistance(int[] a)
    {

        // Create a HashMap to
        // store (key, values) pair.
        HashMap<Integer, Integer> hmap
            = new HashMap<>();
        int minDistance = Integer.MAX_VALUE;

        // Initialize previousIndex
        // and currentIndex as 0
        int previousIndex = 0, currentIndex = 0;

        // Traverse the array and
        // find the minimum distance
        // between the same elements with map
        for (int i = 0; i < a.length; i++) {

            if (hmap.containsKey(a[i])) {
                currentIndex = i;

                // Fetch the previous index from map.
                previousIndex = hmap.get(a[i]);

                // Find the minimum distance.
                minDistance
                    = Math.min(
                        (currentIndex - previousIndex),
                        minDistance);
            }

            // Update the map.
            hmap.put(a[i], i);
        }

        // return minimum distance,
        // if no such elements found, return -1
        return (
            minDistance == Integer.MAX_VALUE
                ? -1
                : minDistance);
    }

    // Driver code
    public static void main(String args[])
    {

        // Test Case 1:
        int a1[] = { 1, 2, 3, 2, 1 };
        System.out.println(minimumDistance(a1));

        // Test Case 2:
        int a2[] = { 3, 5, 4, 6, 5, 3 };
        System.out.println(minimumDistance(a2));

        // Test Case 3:
        int a3[] = { 1, 2, 1, 4, 1 };
        System.out.println(minimumDistance(a3));
    }
}
```

## 蟒蛇 3

```
# Python3 program to find the minimum distance
# between two occurrences of the same element

# Function to find the minimum
# distance between the same elements
def minimumDistance(a):

    # Create a HashMap to
    # store (key, values) pair.
    hmap = dict()
    minDistance = 10**9

    # Initialize previousIndex
    # and currentIndex as 0
    previousIndex = 0
    currentIndex = 0

    # Traverse the array and
    # find the minimum distance
    # between the same elements with map
    for i in range(len(a)):

        if a[i] in hmap:
            currentIndex = i

            # Fetch the previous index from map.
            previousIndex = hmap[a[i]]

            # Find the minimum distance.
            minDistance = min((currentIndex -
                        previousIndex), minDistance)

        # Update the map.
        hmap[a[i]] = i

    # return minimum distance,
    # if no such elements found, return -1
    if minDistance == 10**9:
        return -1
    return minDistance

# Driver code
if __name__ == '__main__':

    # Test Case 1:
    a1 = [1, 2, 3, 2, 1 ]
    print(minimumDistance(a1))

    # Test Case 2:
    a2 = [3, 5, 4, 6, 5,3]
    print(minimumDistance(a2))

    # Test Case 3:
    a3 = [1, 2, 1, 4, 1 ]
    print(minimumDistance(a3))

# This code is contributed by mohit kumar 29   
```

## C#

```
// C# program to find the minimum distance
// between two occurrences of the same element
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// distance between the same elements
static int minimumDistance(int[] a)
{

    // Create a HashMap to
    // store (key, values) pair.
    Dictionary<int,
               int> hmap = new Dictionary<int,
                                          int>();
    int minDistance = Int32.MaxValue;

    // Initialize previousIndex
    // and currentIndex as 0
    int previousIndex = 0, currentIndex = 0;

    // Traverse the array and
    // find the minimum distance
    // between the same elements with map
    for(int i = 0; i < a.Length; i++)
    {
        if (hmap.ContainsKey(a[i]))
        {
            currentIndex = i;

            // Fetch the previous index from map.
            previousIndex = hmap[a[i]];

            // Find the minimum distance.
            minDistance = Math.Min((currentIndex -
                                    previousIndex),
                                    minDistance);
        }

        // Update the map.
        if (!hmap.ContainsKey(a[i]))
            hmap.Add(a[i], i);
        else
            hmap[a[i]] = i;
    }

    // Return minimum distance,
    // if no such elements found, return -1
    return(minDistance == Int32.MaxValue ?
                    -1 : minDistance);
}

// Driver code
static public void Main()
{

    // Test Case 1:
    int[] a1 = { 1, 2, 3, 2, 1 };
    Console.WriteLine(minimumDistance(a1));

    // Test Case 2:
    int[] a2 = { 3, 5, 4, 6, 5, 3 };
    Console.WriteLine(minimumDistance(a2));

    // Test Case 3:
    int[] a3 = { 1, 2, 1, 4, 1 };
    Console.WriteLine(minimumDistance(a3));
}
}

// This code is contributed by unknown2108
```

## java 描述语言

```
<script>

// Javascript program to find the minimum distance
// between two occurrences of the same element

// Function to find the minimum
// distance between the same elements
function minimumDistance(a, n)
{

    // Create a HashMap to
    // store (key, values) pair.
    var hmap = new Map();

    var minDistance = 1000000000;

    // Initialize previousIndex
    // and currentIndex as 0
    var previousIndex = 0, currentIndex = 0;

    // Traverse the array and
    // find the minimum distance
    // between the same elements with map

    for (var i = 0; i < n; i++) {

        if (hmap.has(a[i])) {
            currentIndex = i;

            // Fetch the previous index from map.
            previousIndex = hmap.get(a[i]);

            // Find the minimum distance.
            minDistance = Math.min((currentIndex -
                        previousIndex),minDistance);
        }

        // Update the map.
        hmap.set(a[i], i);
    }

    // return minimum distance,
    // if no such elements found, return -1
    return (minDistance == 1000000000 ? -1 : minDistance);
}

// Driver code
// Test Case 1:
var a1 = [1, 2, 3, 2, 1];
var n = a1.length;
document.write( minimumDistance(a1, n) + "<br>");

// Test Case 2:
var a2 = [3, 5, 4, 6, 5, 3];
n = a2.length;
document.write( minimumDistance(a2, n) + "<br>");

// Test Case 3:
var a3 = [1, 2, 1, 4, 1];
n = a3.length;
document.write( minimumDistance(a3, n));

// This code is contributed by famously.
</script>
```

**Output:** 

```
2
3
2
```

***时间复杂度:**O(N)*T4】