# 具有最大不同元素的子序列计数

> 原文:[https://www . geesforgeks . org/count-subseries-max-distinct-elements/](https://www.geeksforgeeks.org/count-subsequences-maximum-distinct-elements/)

给定一个大小为 **n** 的 **arr** 。问题是计算所有具有最大数量不同元素的子序列。
**例:**

```
Input : arr[] = {4, 7, 6, 7}
Output : 2
The indexes for the subsequences are:
{0, 1, 2} - Subsequence is {4, 7, 6} and
{0, 2, 3} - Subsequence is {4, 6, 7}

Input : arr[] = {9, 6, 4, 4, 5, 9, 6, 1, 2}
Output : 8
```

**天真方法:**考虑所有具有不同元素的子序列，并计算具有最大不同元素的子序列。
**高效方法:**创建哈希表来存储数组中每个元素的频率。取所有频率的乘积。
解决方案基于这样一个事实，即当所有元素都不同时，总是有 1 个子序列是可能的。如果元素重复，重复元素的每一次出现都会产生一个不同元素的新子序列。

## C++

```
// C++ implementation to count subsequences having
// maximum distinct elements
#include <bits/stdc++.h>
using namespace std;

typedef unsigned long long int ull;

// function to count subsequences having
// maximum distinct elements
ull countSubseq(int arr[], int n)
{
    // unordered_map 'um' implemented as
    // hash table
    unordered_map<int, int> um;

    ull count = 1;

    // count frequency of each element
    for (int i = 0; i < n; i++)
        um[arr[i]]++;

    // traverse 'um'
    for (auto itr = um.begin(); itr != um.end(); itr++)

        // multiply frequency of each element
        // and accumulate it in 'count'
        count *= (itr->second);

    // required number of subsequences
    return count;
}

// Driver program to test above
int main()
{
    int arr[] = { 4, 7, 6, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Count = "
         << countSubseq(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count subsequences having
// maximum distinct elements
import java.util.HashMap;

class geeks
{

    // function to count subsequences having
    // maximum distinct elements
    public static long countSubseq(int[] arr, int n)
    {

        // unordered_map 'um' implemented as
        // hash table
        HashMap<Integer, Integer> um = new HashMap<>();

        long count = 1;

        // count frequency of each element
        for (int i = 0; i < n; i++)
        {
            if (um.get(arr[i]) != null)
            {
                int a = um.get(arr[i]);
                um.put(arr[i], ++a);
            }
            else
                um.put(arr[i], 1);
        }

        // traverse 'um'
        for (HashMap.Entry<Integer, Integer> entry : um.entrySet())
        {

            // multiply frequency of each element
            // and accumulate it in 'count'
            count *= entry.getValue();
        }

        // required number of subsequences
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[] arr = { 4, 7, 6, 7 };
        int n = arr.length;
        System.out.println("Count = " + countSubseq(arr, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python 3 implementation to count subsequences
# having maximum distinct elements

# function to count subsequences having
# maximum distinct elements
def countSubseq(arr, n):

    # unordered_map 'um' implemented
    # as hash table
    # take range equal to maximum
    # value of arr
    um = {i:0 for i in range(8)}

    count = 1

    # count frequency of each element
    for i in range(n):
        um[arr[i]] += 1

    # traverse 'um'
    for key, values in um.items():

        # multiply frequency of each element
        # and accumulate it in 'count'
        if(values > 0):
            count *= values

    # required number of subsequences
    return count

# Driver Code
if __name__ == '__main__':
    arr = [4, 7, 6, 7]
    n = len(arr)
    print("Count =", countSubseq(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation to count subsequences
// having maximum distinct elements
using System;
using System.Collections.Generic;

class GFG
{

    // function to count subsequences having
    // maximum distinct elements
    public static long countSubseq(int[] arr,
                                   int n)
    {

        // unordered_map 'um' implemented as
        // hash table
        Dictionary<int,
                   int> um = new Dictionary<int,
                                            int>();

        long count = 1;

        // count frequency of each element
        for (int i = 0; i < n; i++)
        {
            if (um.ContainsKey(arr[i]))
            {
                int a = um[arr[i]];
                um.Remove(arr[i]);
                um.Add(arr[i], ++a);
            }
            else
                um.Add(arr[i], 1);
        }

        // traverse 'um'
        foreach(KeyValuePair<int, int> entry in um)
        {

            // multiply frequency of each element
            // and accumulate it in 'count'
            count *= entry.Value;
        }

        // required number of subsequences
        return count;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 4, 7, 6, 7 };
        int n = arr.Length;
        Console.WriteLine("Count = " +
                           countSubseq(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation to count subsequences having
// maximum distinct elements

// function to count subsequences having
// maximum distinct elements
function countSubseq(arr, n)
{

    // unordered_map 'um' implemented as
    // hash table
    var um = new Map();

    var count = 1;

    // count frequency of each element
    for (var i = 0; i < n; i++)
    {
        if(um.has(arr[i]))
            um.set(arr[i], um.get(arr[i])+1)
        else
            um.set(arr[i], 1);
    }

    // traverse 'um'
    um.forEach((value, key) => {

        // multiply frequency of each element
        // and accumulate it in 'count'
        count *= value;
    });

    // required number of subsequences
    return count;
}

// Driver program to test above
var arr = [4, 7, 6, 7];
var n = arr.length;
document.write( "Count = "
      + countSubseq(arr, n));

// This code is contributed by noob2000.
</script>
```

**输出:**

```
Count = 2
```

**时间复杂度:** O(n)。
**辅助空间:** O(n)。