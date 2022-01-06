# 具有更多频率的第一阵列的元素

> 原文:[https://www . geeksforgeeks . org/具有更多频率的第一阵列元素/](https://www.geeksforgeeks.org/elements-of-first-array-that-have-more-frequencies/)

给定两个数组(可以排序，也可以不排序)。这些数组中可能有一些共同的元素。我们需要找到出现次数在第一个数组中多于第二个数组的元素。
**例:**

```
Input : ar1[] = {1, 2, 2, 2, 3, 3, 4, 5}
        ar2[] = {2, 2, 3, 3, 3, 4}
Output : 1 2 5
1 occurs one times in first and zero times in second
2 occurs three times in first and two times in second
............................

Input : ar1[] = {1, 3, 4, 2, 3}
        ar2[] = {3, 4, 5}
Output : 3
```

想法是使用散列法。我们遍历第一个数组，并在哈希表中插入所有元素及其频率。现在，我们遍历第二个数组，并减少哈希表中常见元素的频率。现在我们再次遍历第一个数组，打印那些频率仍然大于 0 的元素。为了避免重复打印相同的元素，我们将频率设置为 0。

## C++

```
// C++ program to print all those elements of
// first array that have more frequencies than
// second array.
#include <bits/stdc++.h>
using namespace std;

// Compares two intervals according to starting times.
void moreFreq(int ar1[], int ar2[], int m, int n)
{
    // Traverse first array and store frequencies
    // of all elements
    unordered_map<int, int> mp;
    for (int i = 0; i < m; i++)
        mp[ar1[i]]++;

    // Traverse second array and reduce frequencies
    // of common elements.
    for (int i = 0; i < n; i++)
        if (mp.find(ar2[i]) != mp.end())
            mp[ar2[i]]--;

    // Now traverse first array again and print
    // all those elements whose frequencies are
    // more than 0\. To avoid repeated printing,
    // we set frequency as 0 after printing.
    for (int i = 0; i < m; i++) {
        if (mp[ar1[i]] > 0) {
            cout << ar1[i] << " ";
            mp[ar1[i]] = 0;
        }
    }
}

// Driver code
int main()
{
    int ar1[] = { 1, 2, 2, 2, 3, 3, 4, 5 };
    int ar2[] = { 2, 2, 3, 3, 3, 4 };
    int m = sizeof(ar1) / sizeof(ar1[0]);
    int n = sizeof(ar2) / sizeof(ar2[0]);
    moreFreq(ar1, ar2, m, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print all those elements of
// first array that have more frequencies than
// second array.
import java.util.*;

class GFG
{

    // Compares two intervals according to starting times.
    static void moreFreq(int ar1[], int ar2[], int m, int n)
    {
        // Traverse first array and store frequencies
        // of all elements
        Map<Integer,Integer> mp = new HashMap<>();
        for (int i = 0 ; i < m; i++)
        {
            if(mp.containsKey(ar1[i]))
            {
                mp.put(ar1[i], mp.get(ar1[i])+1);
            }
            else
            {
                mp.put(ar1[i], 1);
            }
        }

        // Traverse second array and reduce frequencies
        // of common elements.
        for (int i = 0; i < n; i++)
            if (mp.containsKey(ar2[i]))
                mp.put(ar2[i], mp.get(ar2[i])-1);

        // Now traverse first array again and print
        // all those elements whose frequencies are
        // more than 0\. To avoid repeated printing,
        // we set frequency as 0 after printing.
        for (int i = 0; i < m; i++)
        {
            if (mp.get(ar1[i]) > 0)
            {
                System.out.print(ar1[i] + " ");
                mp.put(ar1[i], 0);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int ar1[] = { 1, 2, 2, 2, 3, 3, 4, 5 };
        int ar2[] = { 2, 2, 3, 3, 3, 4 };
        int m = ar1.length;
        int n = ar2.length;
        moreFreq(ar1, ar2, m, n);
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to print all those elements of
# first array that have more frequencies than
# second array.
import math as mt

# Compares two intervals according to
# starting times.
def moreFreq(ar1, ar2, m, n):

    # Traverse first array and store
    # frequencies of all elements
    mp = dict()
    for i in range(m):
        if ar1[i] in mp.keys():
            mp[ar1[i]] += 1
        else:
            mp[ar1[i]] = 1

    # Traverse second array and reduce
    # frequencies of common elements.
    for i in range(n):
        if ar2[i] in mp.keys():
            mp[ar2[i]] -= 1

    # Now traverse first array again and print
    # all those elements whose frequencies are
    # more than 0\. To avoid repeated printing,
    # we set frequency as 0 after printing.
    for i in range(m):
        if (mp[ar1[i]] > 0):
            print(ar1[i], end = " ")
            mp[ar1[i]] = 0

# Driver code
ar1 = [ 1, 2, 2, 2, 3, 3, 4, 5 ]
ar2 = [ 2, 2, 3, 3, 3, 4 ]
m = len(ar1)
n = len(ar2)
moreFreq(ar1, ar2, m, n)

# This code is contributed
# by mohit kumar 29
```

## C#

```
// C# pprogram to print all those elements of
// first array that have more frequencies than
// second array.
using System;
using System.Collections.Generic;

class GFG
{

    // Compares two intervals according to
    // starting times.
    static void moreFreq(int []ar1, int []ar2,
                         int m, int n)
    {
        // Traverse first array and store frequencies
        // of all elements
        Dictionary<int,
                   int> mp = new Dictionary<int,
                                            int>();
        for (int i = 0 ; i < m; i++)
        {
            if(mp.ContainsKey(ar1[i]))
            {
                mp[ar1[i]] = mp[ar1[i]] + 1;
            }
            else
            {
                mp.Add(ar1[i], 1);
            }
        }

        // Traverse second array and reduce frequencies
        // of common elements.
        for (int i = 0; i < n; i++)
            if (mp.ContainsKey(ar2[i]))
                mp[ar2[i]] = mp[ar2[i]] - 1;

        // Now traverse first array again and print
        // all those elements whose frequencies are
        // more than 0\. To avoid repeated printing,
        // we set frequency as 0 after printing.
        for (int i = 0; i < m; i++)
        {
            if (mp[ar1[i]] > 0)
            {
                Console.Write(ar1[i] + " ");
                mp[ar1[i]] = 0;
            }
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []ar1 = { 1, 2, 2, 2, 3, 3, 4, 5 };
        int []ar2 = { 2, 2, 3, 3, 3, 4 };
        int m = ar1.Length;
        int n = ar2.Length;
        moreFreq(ar1, ar2, m, n);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to print all those elements of
// first array that have more frequencies than
// second array.

// Compares two intervals according to starting times.
function moreFreq(ar1, ar2, m, n)
{
    // Traverse first array and store frequencies
    // of all elements
    var mp = new Map();
    for (var i = 0; i < m; i++)
    {
        if(mp.has(ar1[i]))
            mp.set(ar1[i], mp.get(ar1[i])+1)
        else 
            mp.set(ar1[i], 1)
    }

    // Traverse second array and reduce frequencies
    // of common elements.
    for (var i = 0; i < n; i++)
        if (mp.has(ar2[i]))
        {
            mp.set(ar2[i], mp.get(ar2[i])-1)
        }

    // Now traverse first array again and print
    // all those elements whose frequencies are
    // more than 0\. To avoid repeated printing,
    // we set frequency as 0 after printing.
    for (var i = 0; i < m; i++) {
        if (mp.get(ar1[i]) > 0) {
            document.write( ar1[i] + " ");
            mp.set(ar1[i], 0);
        }
    }
}

// Driver code
var ar1 = [1, 2, 2, 2, 3, 3, 4, 5];
var ar2 = [2, 2, 3, 3, 3, 4];
var m = ar1.length;
var n = ar2.length;
moreFreq(ar1, ar2, m, n);

</script>
```

**Output:** 

```
1 2 5
```

**时间复杂度:**在无序 _map find()和 insert()在 O(1)时间内工作的假设下，O(m + n)。