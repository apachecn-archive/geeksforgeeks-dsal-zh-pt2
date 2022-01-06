# 使数组中所有元素不同所需的最小运算量

> 原文:[https://www . geeksforgeeks . org/制作所有元素所需的最小操作-阵列中的不同元素/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-all-the-elements-distinct-in-an-array/)

给定一个 N 个整数的数组。如果一个数字出现多次，请从数组中选择任意一个数字 y，并将数组中的 x 替换为 x+y，这样 x+y 就不在数组中了。任务是找到使数组成为独特数组的最小操作数。
**例:**

> **输入:** a[] = {2，1，2}
> **输出:** 1
> 让 x = 2，y = 1，然后用 3 替换 2。
> 执行上述步骤使数组中的所有元素都不同。
> **输入:** a[] = {1，2，3}
> **输出:** 0

**方法:**如果一个数字出现不止一次，那么所有重复元素的总和(出现次数-1)就是答案。这背后的主要逻辑是，如果 x 被 x+y 替换，其中 y 是数组中最大的元素，那么 x 被 x+y 替换，x+y 是数组中最大的元素。使用[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储数组编号的频率。在地图中遍历，如果一个元素的频率大于 1，通过减去 1 将其添加到计数中。
以下是上述方法的实施:

## C++

```
// C++ program to find Minimum number
// of  changes to make array distinct
#include <bits/stdc++.h>
using namespace std;

// Function that returns minimum number of changes
int minimumOperations(int a[], int n)
{

    // Hash-table to store frequency
    unordered_map<int, int> mp;

    // Increase the frequency of elements
    for (int i = 0; i < n; i++)
        mp[a[i]] += 1;

    int count = 0;

    // Traverse in the map to sum up the (occurrences-1)
    // of duplicate elements
    for (auto it = mp.begin(); it != mp.end(); it++) {
        if ((*it).second > 1)
            count += (*it).second-1;
    }
    return count;
}

// Driver Code
int main()
{
    int a[] = { 2, 1, 2, 3, 3, 4, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << minimumOperations(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Minimum number
// of changes to make array distinct
import java.util.*;

class geeks
{

    // Function that returns minimum number of changes
    public static int minimumOperations(int[] a, int n)
    {

        // Hash-table to store frequency
        HashMap<Integer, Integer> mp = new HashMap<>();

        // Increase the frequency of elements
        for (int i = 0; i < n; i++)
        {
            if (mp.get(a[i]) != null)
            {
                int x = mp.get(a[i]);
                mp.put(a[i], ++x);
            }
            else
                mp.put(a[i], 1);
        }

        int count = 0;

        // Traverse in the map to sum up the (occurrences-1)
        // of duplicate elements
        for (HashMap.Entry<Integer, Integer> entry : mp.entrySet())
        {
            if (entry.getValue() > 1)
            {
                count += (entry.getValue() - 1);
            }
        }

        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] a = { 2, 1, 2, 3, 3, 4, 3 };
        int n = a.length;

        System.out.println(minimumOperations(a, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find Minimum number
# of changes to make array distinct

# Function that returns minimum
# number of changes
def minimumOperations(a, n):

    # Hash-table to store frequency
    mp = dict()

    # Increase the frequency of elements
    for i in range(n):
        if a[i] in mp.keys():
            mp[a[i]] += 1
        else:
            mp[a[i]] = 1

    count = 0

    # Traverse in the map to sum up the
    # (occurrences-1)of duplicate elements
    for it in mp:
        if (mp[it] > 1):
            count += mp[it] - 1

    return count

# Driver Code
a = [2, 1, 2, 3, 3, 4, 3 ]
n = len(a)

print(minimumOperations(a, n))

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# program to find Minimum number
// of changes to make array distinct
using System;
using System.Collections.Generic;

class geeks
{

    // Function that returns minimum number of changes
    public static int minimumOperations(int[] a, int n)
    {

        // Hash-table to store frequency
        Dictionary<int,int> mp = new Dictionary<int,int>();
        // Increase the frequency of elements
        for (int i = 0 ; i < n; i++)
        {
            if(mp.ContainsKey(a[i]))
            {
                var val = mp[a[i]];
                mp.Remove(a[i]);
                mp.Add(a[i], val + 1);
            }
            else
            {
                mp.Add(a[i], 1);
            }
        }

        int count = 0;

        // Traverse in the map to sum up the (occurrences-1)
        // of duplicate elements
        foreach(KeyValuePair<int, int> entry in mp)
        {
            if (entry.Value > 1)
            {
                count += (entry.Value - 1);
            }
        }

        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] a = { 2, 1, 2, 3, 3, 4, 3 };
        int n = a.Length;

        Console.WriteLine(minimumOperations(a, n));
    }
}

/* This code is contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>

// JavaScript program to find Minimum number
// of changes to make array distinct

    // Function that returns minimum
    // number of changes
    function minimumOperations(a,n)
    {
        // Hash-table to store frequency
        let mp = new Map();

        // Increase the frequency of elements
        for (let i = 0; i < n; i++)
        {
            if (mp.get(a[i]) != null)
            {
                let x = mp.get(a[i]);
                mp.set(a[i], ++x);
            }
            else
                mp.set(a[i], 1);
        }

        let count = 0;

        // Traverse in the map to
        // sum up the (occurrences-1)
        // of duplicate elements
        for (let [key, value] of mp.entries())
        {
            if (value > 1)
            {
                count += (value - 1);
            }
        }

        return count;
    }

    // Driver Code
    let a=[2, 1, 2, 3, 3, 4, 3];
    let n = a.length;

    document.write(minimumOperations(a, n));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)