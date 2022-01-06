# 数组中最频繁和最不频繁元素之间的最小距离

> 原文:[https://www . geesforgeks . org/任何最频繁和最不频繁的数组元素之间的最小距离/](https://www.geeksforgeeks.org/minimum-distance-between-any-most-frequent-and-least-frequent-element-of-an-array/)

给定一个整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**大小为 **N** ，任务是找到给定数组中任何最频繁和最不频繁元素之间的最小距离。

**示例:**

> **输入:** arr[] = {1，1，2，3，2，3，3}
> **输出:** 1
> **解释:**出现频率最低的元素是 1 和 2，出现在索引:0，1，2，4。
> 然而，最常见的元素是出现在索引处的 3:3、5、6。
> 所以最小距离为(3-2) = 1。
> 
> **输入:** arr[] = {1，3，4，4，3，4}
> **输出:** 2
> **解释:**最不频繁的元素是 1，出现在索引:0 处。
> 然而，最常见的元素是出现在索引处的 4:2、3、5。
> 所以最小距离为(2-0) = 2。

**逼近**:思路是找出数组中最少和最频繁元素的索引，找出那些索引之间的差异最小。按照以下步骤解决问题:

1.  将每个元素的频率存储在 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 中。
2.  将最少和最频繁的元素存储在单独的[集合](https://www.geeksforgeeks.org/set-in-java/)中。
3.  从数组开始遍历。如果当前元素是最不频繁的元素，则更新最不频繁元素的最后一个索引。
4.  否则，如果当前元素是最频繁的元素，则计算当前元素和最不频繁元素的最后一个索引之间的距离，并更新所需的最小距离。
5.  同样，从头到尾遍历数组，重复**第 3 步**和**第 4 步**，找出数组中任何最频繁和最不频繁元素之间的最小距离。
6.  打印最小距离。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum
// distance between any two most
// and least frequent element
void getMinimumDistance(int a[], int n)
{

    // Initialize sets to store the least
    // and the most frequent elements
    set<int> min_set;
    set<int> max_set;

    // Initialize variables to store
    // max and min frequency
    int max = 0, min = INT_MAX;

    // Initialize HashMap to store
    // frequency of each element
    map<int, int> frequency;

    // Loop through the array
    for (int i = 0; i < n; i++) {

        // Store the count of each element
        frequency[a[i]] += 1;
    }

    // Store the least and most frequent
    // elements in the respective sets
    for (int i = 0; i < n; i++) {

        // Store count of current element
        int count = frequency[a[i]];

        // If count is equal
        // to max count
        if (count == max) {

            // Store in max set
            max_set.insert(a[i]);
        }

        // If count is greater
        // then max count
        else if (count > max) {

            // Empty max set
            max_set.clear();

            // Update max count
            max = count;

            // Store in max set
            max_set.insert(a[i]);
        }

        // If count is equal
        // to min count
        if (count == min) {

            // Store in min set
            min_set.insert(a[i]);
        }

        // If count is less
        // then max count
        else if (count < min) {

            // Empty min set
            min_set.clear();

            // Update min count
            min = count;

            // Store in min set
            min_set.insert(a[i]);
        }
    }

    // Initialize a variable to
    // store the minimum distance
    int min_dist = INT_MAX;

    // Initialize a variable to
    // store the last index of
    // least frequent element
    int last_min_found = -1;

    // Traverse array
    for (int i = 0; i < n; i++) {

        // If least frequent element
        if (min_set.find(a[i]) != min_set.end())

            // Update last index of
            // least frequent element
            last_min_found = i;

        // If most frequent element
        if (max_set.find(a[i]) != max_set.end()
            && last_min_found != -1) {

            // Update minimum distance
            if ((i - last_min_found) < min_dist)
                min_dist = i - last_min_found;
        }
    }

    last_min_found = -1;

    // Traverse array from the end
    for (int i = n - 1; i >= 0; i--) {

        // If least frequent element
        if (min_set.find(a[i]) != min_set.end())

            // Update last index of
            // least frequent element
            last_min_found = i;

        // If most frequent element
        if (max_set.find(a[i]) != max_set.end()
            && last_min_found != -1) {

            // Update minimum distance
            if ((last_min_found - i) > min_dist)
                min_dist = last_min_found - i;
        }
    }

    // Print the minimum distance
    cout << (min_dist);
}

// Driver Code
int main()
{

    // Given array
    int arr[] = { 1, 1, 2, 3, 2, 3, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    getMinimumDistance(arr, N);
}

// This code is contributed by ukasp.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to find the minimum
    // distance between any two most
    // and least frequent element
    public static void
    getMinimumDistance(int a[], int n)
    {

        // Initialize sets to store the least
        // and the most frequent elements
        Set<Integer> min_set = new HashSet<>();
        Set<Integer> max_set = new HashSet<>();

        // Initialize variables to store
        // max and min frequency
        int max = 0, min = Integer.MAX_VALUE;

        // Initialize HashMap to store
        // frequency of each element
        HashMap<Integer, Integer> frequency
            = new HashMap<>();

        // Loop through the array
        for (int i = 0; i < n; i++) {

            // Store the count of each element
            frequency.put(
                a[i],
                frequency
                        .getOrDefault(a[i], 0)
                    + 1);
        }

        // Store the least and most frequent
        // elements in the respective sets
        for (int i = 0; i < n; i++) {

            // Store count of current element
            int count = frequency.get(a[i]);

            // If count is equal
            // to max count
            if (count == max) {

                // Store in max set
                max_set.add(a[i]);
            }

            // If count is greater
            // then max count
            else if (count > max) {

                // Empty max set
                max_set.clear();

                // Update max count
                max = count;

                // Store in max set
                max_set.add(a[i]);
            }

            // If count is equal
            // to min count
            if (count == min) {

                // Store in min set
                min_set.add(a[i]);
            }

            // If count is less
            // then max count
            else if (count < min) {

                // Empty min set
                min_set.clear();

                // Update min count
                min = count;

                // Store in min set
                min_set.add(a[i]);
            }
        }

        // Initialize a variable to
        // store the minimum distance
        int min_dist = Integer.MAX_VALUE;

        // Initialize a variable to
        // store the last index of
        // least frequent element
        int last_min_found = -1;

        // Traverse array
        for (int i = 0; i < n; i++) {

            // If least frequent element
            if (min_set.contains(a[i]))

                // Update last index of
                // least frequent element
                last_min_found = i;

            // If most frequent element
            if (max_set.contains(a[i])
                && last_min_found != -1) {

                // Update minimum distance
                min_dist = Math.min(min_dist,
                                    i - last_min_found);
            }
        }

        last_min_found = -1;

        // Traverse array from the end
        for (int i = n - 1; i >= 0; i--) {

            // If least frequent element
            if (min_set.contains(a[i]))

                // Update last index of
                // least frequent element
                last_min_found = i;

            // If most frequent element
            if (max_set.contains(a[i])
                && last_min_found != -1) {

                // Update minimum distance
                min_dist = Math.min(min_dist,
                                    last_min_found - i);
            }
        }

        // Print the minimum distance
        System.out.println(min_dist);
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given array
        int arr[] = { 1, 1, 2, 3, 2, 3, 3 };

        int N = arr.length;

        // Function Call
        getMinimumDistance(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to find the minimum
# distance between any two most
# and least frequent element
def getMinimumDistance(a, n):

    # Initialize sets to store the least
    # and the most frequent elements
    min_set = {}
    max_set = {}

    # Initialize variables to store
    # max and min frequency
    max, min = 0, sys.maxsize + 1

    # Initialize HashMap to store
    # frequency of each element
    frequency = {}

    # Loop through the array
    for i in range(n):

        # Store the count of each element
        frequency[a[i]] = frequency.get(a[i], 0) + 1

    # Store the least and most frequent
    # elements in the respective sets
    for i in range(n):

        # Store count of current element
        count = frequency[a[i]]

        # If count is equal
        # to max count
        if (count == max):

            # Store in max set
            max_set[a[i]] = 1

        # If count is greater
        # then max count
        elif (count > max):

            # Empty max set
            max_set.clear()

            # Update max count
            max = count

            # Store in max set
            max_set[a[i]] = 1

        # If count is equal
        # to min count
        if (count == min):

            # Store in min set
            min_set[a[i]] = 1

        # If count is less
        # then max count
        elif (count < min):

            # Empty min set
            min_set.clear()

            # Update min count
            min = count

            # Store in min set
            min_set[a[i]] = 1

    # Initialize a variable to
    # store the minimum distance
    min_dist = sys.maxsize + 1

    # Initialize a variable to
    # store the last index of
    # least frequent element
    last_min_found = -1

    # Traverse array
    for i in range(n):

        # If least frequent element
        if (a[i] in min_set):

            # Update last index of
            # least frequent element
            last_min_found = i

        # If most frequent element
        if ((a[i] in max_set) and
            last_min_found != -1):

            # Update minimum distance
            if i-last_min_found < min_dist:
                min_dist = i - last_min_found

    last_min_found = -1

    # Traverse array from the end
    for i in range(n - 1, -1, -1):

        # If least frequent element
        if (a[i] in min_set):

            # Update last index of
            # least frequent element
            last_min_found = i;

        # If most frequent element
        if ((a[i] in max_set) and
            last_min_found != -1):

            # Update minimum distance
            if min_dist > last_min_found - i:
                min_dist = last_min_found - i

    # Print the minimum distance
    print(min_dist)

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [ 1, 1, 2, 3, 2, 3, 3 ]

    N = len(arr)

    # Function Call
    getMinimumDistance(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach

using System;
using System.Collections.Generic;

public class GFG{

    // Function to find the minimum
    // distance between any two most
    // and least frequent element
    public static void
    getMinimumDistance(int[] a, int n)
    {

        // Initialize sets to store the least
        // and the most frequent elements
        HashSet<int> min_set = new HashSet<int>();
        HashSet<int> max_set = new HashSet<int>();

        // Initialize variables to store
        // max and min frequency
        int max = 0, min = Int32.MaxValue;

        // Initialize HashMap to store
        // frequency of each element
        Dictionary<int, int> frequency = 
                       new Dictionary<int, int>();

        // Loop through the array
        for (int i = 0; i < n; i++) {

            // Store the count of each element
            if(!frequency.ContainsKey(a[i]))
                frequency.Add(a[i],0);
            frequency[a[i]]++;
        }

        // Store the least and most frequent
        // elements in the respective sets
        for (int i = 0; i < n; i++) {

            // Store count of current element
            int count = frequency[a[i]];

            // If count is equal
            // to max count
            if (count == max) {

                // Store in max set
                max_set.Add(a[i]);
            }

            // If count is greater
            // then max count
            else if (count > max) {

                // Empty max set
                max_set.Clear();

                // Update max count
                max = count;

                // Store in max set
                max_set.Add(a[i]);
            }

            // If count is equal
            // to min count
            if (count == min) {

                // Store in min set
                min_set.Add(a[i]);
            }

            // If count is less
            // then max count
            else if (count < min) {

                // Empty min set
                min_set.Clear();

                // Update min count
                min = count;

                // Store in min set
                min_set.Add(a[i]);
            }
        }

        // Initialize a variable to
        // store the minimum distance
        int min_dist = Int32.MaxValue;

        // Initialize a variable to
        // store the last index of
        // least frequent element
        int last_min_found = -1;

        // Traverse array
        for (int i = 0; i < n; i++) {

            // If least frequent element
            if (min_set.Contains(a[i]))

                // Update last index of
                // least frequent element
                last_min_found = i;

            // If most frequent element
            if (max_set.Contains(a[i])
                && last_min_found != -1) {

                // Update minimum distance
                min_dist = Math.Min(min_dist,
                                    i - last_min_found);
            }
        }

        last_min_found = -1;

        // Traverse array from the end
        for (int i = n - 1; i >= 0; i--) {

            // If least frequent element
            if (min_set.Contains(a[i]))

                // Update last index of
                // least frequent element
                last_min_found = i;

            // If most frequent element
            if (max_set.Contains(a[i])
                && last_min_found != -1) {

                // Update minimum distance
                min_dist = Math.Min(min_dist,
                                    last_min_found - i);
            }
        }

        // Print the minimum distance
        Console.WriteLine(min_dist);
    }

    // Driver Code   
    static public void Main ()
    {

        // Given array
        int[] arr = { 1, 1, 2, 3, 2, 3, 3 };
        int N = arr.Length;

        // Function Call
        getMinimumDistance(arr, N);

    }
}

// This code is contributed by patel2127.
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find the minimum
// distance between any two most
// and least frequent element
function getMinimumDistance(a, n)
{

    // Initialize sets to store the least
    // and the most frequent elements
    var min_set = new Set();
    var max_set = new Set();

    // Initialize variables to store
    // max and min frequency
    var max = 0, min = 1000000000;

    // Initialize HashMap to store
    // frequency of each element
    var frequency = new Map();

    // Loop through the array
    for(var i = 0; i < n; i++)
    {

        // Store the count of each element
        if(frequency.has(a[i]))
            frequency.set(a[i],
            frequency.get(a[i]) + 1)
        else
            frequency.set(a[i], 1)
    }

    // Store the least and most frequent
    // elements in the respective sets
    for(var i = 0; i < n; i++)
    {

        // Store count of current element
        var count = frequency.get(a[i]);

        // If count is equal
        // to max count
        if (count == max)
        {

            // Store in max set
            max_set.add(a[i]);
        }

        // If count is greater
        // then max count
        else if (count > max)
        {

            // Empty max set
            max_set = new Set();

            // Update max count
            max = count;

            // Store in max set
            max_set.add(a[i]);
        }

        // If count is equal
        // to min count
        if (count == min)
        {

            // Store in min set
            min_set.add(a[i]);
        }

        // If count is less
        // then max count
        else if (count < min)
        {

            // Empty min set
            min_set = new Set();

            // Update min count
            min = count;

            // Store in min set
            min_set.add(a[i]);
        }
    }

    // Initialize a variable to
    // store the minimum distance
    var min_dist = 1000000000;

    // Initialize a variable to
    // store the last index of
    // least frequent element
    var last_min_found = -1;

    // Traverse array
    for(var i = 0; i < n; i++)
    {

        // If least frequent element
        if (min_set.has(a[i]))

            // Update last index of
            // least frequent element
            last_min_found = i;

        // If most frequent element
        if (max_set.has(a[i]) &&
            last_min_found != -1)
        {

            // Update minimum distance
            if ((i - last_min_found) < min_dist)
                min_dist = i - last_min_found;
        }
    }

    last_min_found = -1;

    // Traverse array from the end
    for(var i = n - 1; i >= 0; i--)
    {

        // If least frequent element
        if (min_set.has(a[i]))

            // Update last index of
            // least frequent element
            last_min_found = i;

        // If most frequent element
        if (max_set.has(a[i]) &&
            last_min_found != -1)
        {

            // Update minimum distance
            if ((last_min_found - i) > min_dist)
                min_dist = last_min_found - i;
        }
    }

    // Print the minimum distance
    document.write(min_dist);
}

// Driver Code

// Given array
var arr = [ 1, 1, 2, 3, 2, 3, 3 ];
var N = arr.length;

// Function Call
getMinimumDistance(arr, N);

// This code is contributed by itsok

</script>
```

**Output:** 

```
1
```

***时间复杂度:** O(N)，其中 N 为数组长度。*
***辅助空间:*** *O(N)*