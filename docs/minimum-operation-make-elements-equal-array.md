# 使数组中所有元素相等的最小运算

> 原文:[https://www . geesforgeks . org/minimum-operation-make-elements-equal-array/](https://www.geeksforgeeks.org/minimum-operation-make-elements-equal-array/)

给定一个有 n 个正整数的数组。我们需要找到使所有元素相等的最小运算次数。我们可以对数组元素上的任何元素执行加法、乘法、减法或除法。
**例:**

```
Input : arr[] = {1, 2, 3, 4}
Output : 3
Since all elements are different, 
we need to perform at least three
operations to make them same. For
example, we can make them all 1
by doing three subtractions. Or make
them all 3 by doing three additions.

Input : arr[] = {1, 1, 1, 1}
Output : 0
```

要使所有元素相等，可以选择一个目标值，然后使所有元素相等。现在，要将单个元素转换为目标值，只能执行一次操作。通过这种方式，您可以在最多 n 次操作中完成您的任务，但是您必须最大限度地减少操作数量，因此您对目标的选择非常重要，因为如果您选择的目标在数组中的频率是 x，那么您只需执行 n-x 次以上的操作，因为您已经有 x 个元素等于您的目标值。所以最后，我们的任务是找到频率最高的元素。这可以通过不同的方法来实现，例如 O(n^2 的迭代方法)、O(nlogn)中的排序和 O(n)时间复杂度中的散列。

## C++

```
// CPP program to find the minimum number of
// operations required to make all elements
// of array equal
#include <bits/stdc++.h>
using namespace std;

// function for min operation
int minOperation (int arr[], int n)
{
    // Insert all elements in hash.
    unordered_map<int, int> hash;
    for (int i=0; i<n; i++)
        hash[arr[i]]++;

    // find the max frequency
    int max_count = 0;
    for (auto i : hash)
        if (max_count < i.second)
            max_count = i.second;

    // return result
    return (n - max_count);
}

// driver program
int main()
{
    int arr[] = {1, 5, 2, 1, 3, 2, 1};
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << minOperation(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code For Minimum operation to make
// all elements equal in array
import java.util.*;

class GFG {

    // function for min operation
    public static int minOperation (int arr[], int n)
    {
        // Insert all elements in hash.
       HashMap<Integer, Integer> hash = new HashMap<Integer,
                                           Integer>();

        for (int i=0; i<n; i++)
            if(hash.containsKey(arr[i]))
                hash.put(arr[i], hash.get(arr[i])+1);
            else hash.put(arr[i], 1);

        // find the max frequency
        int max_count = 0;
        Set<Integer> s = hash.keySet();

        for (int i : s)
            if (max_count < hash.get(i))
                max_count = hash.get(i);

        // return result
        return (n - max_count);
    }

    /* Driver program to test above function */
    public static void main(String[] args)
    {
        int arr[] = {1, 5, 2, 1, 3, 2, 1};
        int n = arr.length;
        System.out.print(minOperation(arr, n));

    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 program to find the minimum
# number of operations required to
# make all elements of array equal
from collections import defaultdict

# Function for min operation
def minOperation(arr, n):

    # Insert all elements in hash.
    Hash = defaultdict(lambda:0)
    for i in range(0, n):
        Hash[arr[i]] += 1

    # find the max frequency
    max_count = 0
    for i in Hash:
        if max_count < Hash[i]:
            max_count = Hash[i]

    # return result
    return n - max_count

# Driver Code
if __name__ == "__main__":

    arr = [1, 5, 2, 1, 3, 2, 1]
    n = len(arr)
    print(minOperation(arr, n))

# This code is contributed
# by Rituraj Jain
```

## C#

```
// C# Code For Minimum operation to make
// all elements equal in array
using System;
using System.Collections.Generic;

class GFG
{

    // function for min operation
    public static int minOperation (int []arr, int n)
    {
        // Insert all elements in hash.
        Dictionary<int,int> m = new Dictionary<int,int>();
        for (int i = 0 ; i < n; i++)
        {
            if(m.ContainsKey(arr[i]))
            {
                var val = m[arr[i]];
                m.Remove(arr[i]);
                m.Add(arr[i], val + 1);
            }
            else
            {
                m.Add(arr[i], 1);
            }
        }

        // find the max frequency
        int max_count = 0;
        HashSet<int> s = new HashSet<int>(m.Keys);

        foreach (int i in s)
            if (max_count < m[i])
                max_count = m[i];

        // return result
        return (n - max_count);
    }

    /* Driver code */
    public static void Main(String[] args)
    {
        int []arr = {1, 5, 2, 1, 3, 2, 1};
        int n = arr.Length;
        Console.Write(minOperation(arr, n));

    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript Code For Minimum operation to make
// all elements equal in array

// function for min operation
function minOperation(arr, n) {
    // Insert all elements in hash.
    let hash = new Map();

    for (let i = 0; i < n; i++)
        if (hash.has(arr[i]))
            hash.set(arr[i], hash.get(arr[i]) + 1);
        else hash.set(arr[i], 1);

    // find the max frequency
    let max_count = 0;
    let s = hash.keys();

    for (let i of s)
        if (max_count < hash.get(i))
            max_count = hash.get(i);

    // return result
    return (n - max_count);
}

/* Driver program to test above function */

let arr = [1, 5, 2, 1, 3, 2, 1];
let n = arr.length;
document.write(minOperation(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**输出:**

```
4
```

本文由[**Shivam Pradhan(anuj _ charm)**](http://www.facebook.com/ma5ter6it)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。