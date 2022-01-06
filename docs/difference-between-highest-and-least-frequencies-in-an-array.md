# 阵列中最高和最低频率之间的差异

> 原文:[https://www . geesforgeks . org/阵列中最高频率和最低频率之差/](https://www.geeksforgeeks.org/difference-between-highest-and-least-frequencies-in-an-array/)

给定一个数组，找出数组中任意数字出现次数最多和最少的区别
示例:

```
Input  : arr[] = [7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5]
Output : 2
Lowest occurring element (5) occurs once.
Highest occurring element (1 or 7) occurs 3 times

Input  : arr[] = [1, 1, 1, 3, 3, 3]
Output : 0
```

一个**简单的解决方案**是用两个循环来统计每个元素的频率，并跟踪最大和最小频率。
A **更好的解决方案**是在 **O(n log n)** 中对数组进行排序，检查
连续元素的出现情况，并分别比较它们的个数。

## C++

```
// CPP code to find the difference between highest
// and least frequencies
#include <bits/stdc++.h>
using namespace std;

int findDiff(int arr[], int n)
{
    // sort the array
    sort(arr, arr + n);

    int count = 0, max_count = 0, min_count = n;
    for (int i = 0; i < (n - 1); i++) {

        // checking consecutive elements
        if (arr[i] == arr[i + 1]) {
            count += 1;
            continue;
        }
        else {
            max_count = max(max_count, count);
            min_count = min(min_count, count);
            count = 0;
        }
    }

    return (max_count - min_count);
}

// Driver code
int main()
{
    int arr[] = { 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findDiff(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA Code for Difference between
// highest and least frequencies
// in an array
import java.util.*;

class GFG {

    static int findDiff(int arr[], int n)
    {
        // sort the array
        Arrays.sort(arr);

        int count = 0, max_count = 0,
            min_count = n;

        for (int i = 0; i < (n - 1); i++) {

            // checking consecutive elements
            if (arr[i] == arr[i + 1]) {
                count += 1;
                continue;
            }
            else {
                max_count = Math.max(max_count,
                                     count);

                min_count = Math.min(min_count,
                                     count);
                count = 0;
            }
        }

        return (max_count - min_count);
    }

    // Driver program to test above function
    public static void main(String[] args)
    {

        int arr[] = { 7, 8, 4, 5, 4, 1,
                      1, 7, 7, 2, 5 };
        int n = arr.length;

        System.out.println(findDiff(arr, n));
    }
}

// This code is contributed by Arnav Kr. Mandal.
```

## 蟒蛇 3

```
# Python3 code to find the difference
# between highest nd least frequencies

def findDiff(arr, n):

    # sort the array
    arr.sort()

    count = 0; max_count = 0; min_count = n
    for i in range(0, (n-1)):

        # checking consecutive elements
        if arr[i] == arr[i + 1]:
            count += 1
            continue
        else:
            max_count = max(max_count, count)
            min_count = min(min_count, count)
            count = 0
    return max_count - min_count

# Driver Code
arr = [ 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 ]
n = len(arr)
print (findDiff(arr, n))

# This code is contributed by Shreyanshi Arun.
```

## C#

```
// C# Code for Difference between
// highest and least frequencies
// in an array
using System;

class GFG {

    static int findDiff(int[] arr, int n)
    {

        // sort the array
        Array.Sort(arr);

        int count = 0, max_count = 0,
            min_count = n;

        for (int i = 0; i < (n - 1); i++) {

            // checking consecutive elements
            if (arr[i] == arr[i + 1]) {
                count += 1;
                continue;
            }
            else {
                max_count = Math.Max(max_count,
                                    count);

                min_count = Math.Min(min_count,
                                    count);
                count = 0;
            }
        }

        return (max_count - min_count);
    }

    // Driver program to test above function
    public static void Main()
    {

        int[] arr = { 7, 8, 4, 5, 4, 1,
                       1, 7, 7, 2, 5 };
        int n = arr.Length;

        Console.WriteLine(findDiff(arr, n));
    }
}

// This code is contributed by vt_m.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the
// difference between highest
// and least frequencies

// function that
// returns difference
function findDiff($arr, $n)
{

    // sort the array
    sort($arr);

    $count = 0; $max_count = 0;
    $min_count = $n;
    for ($i = 0; $i < ($n - 1); $i++)
    {

        // checking consecutive elements
        if ($arr[$i] == $arr[$i + 1])
        {
            $count += 1;
            continue;
        }
        else
        {
            $max_count = max($max_count, $count);
            $min_count = min($min_count, $count);
            $count = 0;
        }
    }

    return ($max_count - $min_count);
}

// Driver Code
$arr = array(7, 8, 4, 5, 4, 1,
             1, 7, 7, 2, 5);
$n = sizeof($arr);

echo(findDiff($arr, $n) . "\n");

// This code is contributed by Ajit.
?>
```

## java 描述语言

```
<script>
    // Javascript Code for Difference between
    // highest and least frequencies
    // in an array

    function findDiff(arr, n)
    {

        // sort the array
        arr.sort(function(a, b){return a - b});

        let count = 0, max_count = 0, min_count = n;

        for (let i = 0; i < (n - 1); i++) {

            // checking consecutive elements
            if (arr[i] == arr[i + 1]) {
                count += 1;
                continue;
            }
            else {
                max_count = Math.max(max_count, count);

                min_count = Math.min(min_count, count);
                count = 0;
            }
        }

        return (max_count - min_count);
    }

    let arr = [ 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 ];
    let n = arr.length;

    document.write(findDiff(arr, n));

</script>
```

输出:

```
 2
```

一个有效的解决方案是使用散列法。我们计算所有元素的频率，最后遍历哈希表以找到最大值和最小值。
以下是执行情况。

## C++

```
// CPP code to find the difference between highest
// and least frequencies
#include <bits/stdc++.h>
using namespace std;

int findDiff(int arr[], int n)
{
    // Put all elements in a hash map
    unordered_map<int, int> hm;
    for (int i = 0; i < n; i++)
        hm[arr[i]]++;

    // Find counts of maximum and minimum
    // frequent elements
    int max_count = 0, min_count = n;
    for (auto x : hm) {
        max_count = max(max_count, x.second);
        min_count = min(min_count, x.second);
    }

    return (max_count - min_count);
}

// Driver
int main()
{
    int arr[] = { 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << findDiff(arr, n) << "\n";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the difference between highest
// and least frequencies
import java.util.*;

class GFG
{

static int findDiff(int arr[], int n)
{
    // Put all elements in a hash map
    Map<Integer,Integer> mp = new HashMap<>();
    for (int i = 0 ; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i])+1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // Find counts of maximum and minimum
    // frequent elements
    int max_count = 0, min_count = n;
    for (Map.Entry<Integer,Integer> x : mp.entrySet())
    {
        max_count = Math.max(max_count, x.getValue());
        min_count = Math.min(min_count, x.getValue());
    }

    return (max_count - min_count);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 };
    int n = arr.length;
    System.out.println(findDiff(arr, n));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python code to find the difference between highest
# and least frequencies

from collections import defaultdict
def findDiff(arr,n):

    # Put all elements in a hash map
    mp = defaultdict(lambda:0)
    for i in range(n):
        mp[arr[i]]+=1

    # Find counts of maximum and minimum
    # frequent elements
    max_count=0;min_count=n
    for key,values in mp.items():
        max_count= max(max_count,values)
        min_count = min(min_count,values)

    return max_count-min_count

# Driver code
arr = [ 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5]
n = len(arr)
print(findDiff(arr,n))

# This code is contributed by Shrikant13
```

## C#

```
// C# code to find the difference between highest
// and least frequencies
using System;
using System.Collections.Generic;

class GFG
{

static int findDiff(int []arr, int n)
{
    // Put all elements in a hash map
    Dictionary<int,int> mp = new Dictionary<int,int>();
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            var val = mp[arr[i]];
            mp.Remove(arr[i]);
            mp.Add(arr[i], val + 1);
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // Find counts of maximum and minimum
    // frequent elements
    int max_count = 0, min_count = n;
    foreach(KeyValuePair<int, int> entry in mp)
    {
        max_count = Math.Max(max_count, entry.Value);
        min_count = Math.Min(min_count, entry.Value);
    }

    return (max_count - min_count);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5 };
    int n = arr.Length;
    Console.WriteLine(findDiff(arr, n));
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
      // JavaScript code to find the difference between highest
      // and least frequencies
      function findDiff(arr, n)
      {

        // Put all elements in a hash map
        var mp = {};
        for (var i = 0; i < n; i++) {
          if (mp.hasOwnProperty(arr[i])) {
            var val = mp[arr[i]];
            delete mp[arr[i]];
            mp[arr[i]] = val + 1;
          } else {
            mp[arr[i]] = 1;
          }
        }

        // Find counts of maximum and minimum
        // frequent elements
        var max_count = 0,
          min_count = n;
        for (const [key, value] of Object.entries(mp)) {
          max_count = Math.max(max_count, value);
          min_count = Math.min(min_count, value);
        }

        return max_count - min_count;
      }

      // Driver code
      var arr = [7, 8, 4, 5, 4, 1, 1, 7, 7, 2, 5];
      var n = arr.length;
      document.write(findDiff(arr, n));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
 2
```

**时间复杂度:** O(n)
本文由**喜马拉雅冉冉**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。