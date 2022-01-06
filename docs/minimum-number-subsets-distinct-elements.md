# 具有不同元素的子集的最小数量

> 原文:[https://www . geeksforgeeks . org/最小数量-子集-不同-元素/](https://www.geeksforgeeks.org/minimum-number-subsets-distinct-elements/)

给你一个 n 元素数组。您必须从数组中创建子集，这样子集就不会包含重复的元素。找出可能的最小子集数。
**例:**

```
Input : arr[] = {1, 2, 3, 4}
Output :1
Explanation : A single subset can contains all 
values and all values are distinct

Input : arr[] = {1, 2, 3, 3}
Output : 2
Explanation : We need to create two subsets
{1, 2, 3} and {3} [or {1, 3} and {2, 3}] such
that both subsets have distinct elements.
```

我们基本上需要找到数组中最频繁的元素。结果等于最频繁元素的频率。
一个**简单的解决方案**是运行两个嵌套循环来统计每个元素的频率，并返回最频繁元素的频率。这个解的时间复杂度为 O(n <sup>2</sup> )。
更好的解决方案**是首先对数组进行排序，然后以迭代的方式开始计数元素的重复次数，因为任何数字的所有重复都位于数字本身的旁边。通过这种方法，您可以通过简单地遍历排序的数组来找到最大频率或重复。这种方法将花费 0(nlogn)的时间复杂度** 

## C++

```
// A sorting based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
#include <bits/stdc++.h>
using namespace std;

// Function to count subsets such that all
// subsets have distinct elements.
int subset(int ar[], int n)
{
    // Take input and initialize res = 0
    int res = 0;

    // Sort the array
    sort(ar, ar + n);

    // Traverse the input array and
    // find maximum frequency
    for (int i = 0; i < n; i++) {
        int count = 1;

        // For each number find its repetition / frequency
        for (; i < n - 1; i++) {
            if (ar[i] == ar[i + 1])
                count++;
            else
                break;
        }

        // Update res
        res = max(res, count);
    }

    return res;
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 9, 3, 4, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << subset(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A sorting based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
import java.util.*;
import java.lang.*;

public class GfG{

    // Function to count subsets such that all
    // subsets have distinct elements.
    public static int subset(int ar[], int n)
    {
        // Take input and initialize res = 0
        int res = 0;

        // Sort the array
        Arrays.sort(ar);

        // Traverse the input array and
        // find maximum frequency
        for (int i = 0; i < n; i++) {
            int count = 1;

            // For each number find its repetition / frequency
            for (; i < n - 1; i++) {
                if (ar[i] == ar[i + 1])
                    count++;
                else
                    break;
            }

            // Update res
            res = Math.max(res, count);
        }

        return res;
    }

    // Driver function
    public static void main(String argc[])
    {
        int arr[] = { 5, 6, 9, 3, 4, 3, 4 };
        int n = 7;
        System.out.println(subset(arr, n));
    }

}

/* This code is contributed by Sagar Shukla */
```

## 蟒蛇 3

```
# A sorting based solution to find the
# minimum number of subsets of a set
# such that every subset contains distinct
# elements.

# function to count subsets such that all
# subsets have distinct elements.
def subset(ar, n):

    # take input and initialize res = 0
    res = 0

    # sort the array
    ar.sort()

    # traverse the input array and
    # find maximum frequency
    for i in range(0, n) :
        count = 1

        # for each number find its repetition / frequency
        for i in range(n - 1):
            if ar[i] == ar[i + 1]:
                count+=1
            else:
                break

        # update res
        res = max(res, count)

    return res

# Driver code
ar = [ 5, 6, 9, 3, 4, 3, 4 ]
n = len(ar)
print(subset(ar, n))

# This code is contributed by
# Smitha Dinesh Semwal
```

## C#

```
// A sorting based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
using System;

public class GfG {

    // Function to count subsets such that all
    // subsets have distinct elements.
    public static int subset(int []ar, int n)
    {
        // Take input and initialize res = 0
        int res = 0;

        // Sort the array
        Array.Sort(ar);

        // Traverse the input array and
        // find maximum frequency
        for (int i = 0; i < n; i++) {
            int count = 1;

            // For each number find its
            // repetition / frequency
            for ( ; i < n - 1; i++) {
                if (ar[i] == ar[i + 1])
                    count++;
                else
                    break;
            }

            // Update res
            res = Math.Max(res, count);
        }

        return res;
    }

    // Driver function
    public static void Main()
    {
        int []arr = { 5, 6, 9, 3, 4, 3, 4 };
        int n = 7;

        Console.WriteLine(subset(arr, n));
    }

}

/* This code is contributed by Vt_m */
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// A sorting based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.

// Function to count subsets such that all
// subsets have distinct elements.
function subset($ar, $n)
{
    // Take input and initialize res = 0
    $res = 0;

    // Sort the array
    sort($ar);

    // Traverse the input array and
    // find maximum frequency
    for ($i = 0; $i < $n; $i++)
    {
        $count = 1;

        // For each number find its
        // repetition / frequency
        for (; $i < $n - 1; $i++)
        {
            if ($ar[$i] == $ar[$i + 1])
                $count++;
            else
                break;
        }

        // Update res
        $res = max($res, $count);
    }

    return $res;
}

// Driver code
$arr = array( 5, 6, 9, 3, 4, 3, 4 );
$n = sizeof($arr);
echo subset($arr, $n);

// This code is contributed
// by Sach_Code
?>
```

## java 描述语言

```
<script>

// JavaScript program sorting based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct

    // Function to count subsets such that all
    // subsets have distinct elements.
    function subset(ar, n)
    {

        // Take input and initialize res = 0
        let res = 0;

        // Sort the array
        ar.sort();

        // Traverse the input array and
        // find maximum frequency
        for (let i = 0; i < n; i++)
        {
            let count = 1;

            // For each number find its repetition / frequency
            for (; i < n - 1; i++)
            {
                if (ar[i] == ar[i + 1])
                    count++;
                else
                    break;
            }

            // Update res
            res = Math.max(res, count);
        }
        return res;
    }

// Driver Code
        let arr = [ 5, 6, 9, 3, 4, 3, 4 ];
        let n = 7;
        document.write(subset(arr, n));

// This code is contributed by chinmoy1997pal.
</script>
```

**输出:**

```
2
```

一个**有效的解决方案**是使用哈希。我们计算哈希表中所有元素的频率。最后我们返回哈希表中值最大的键。

## C++

```
// A hashing based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
#include <bits/stdc++.h>
using namespace std;

// Function to count subsets such that all
// subsets have distinct elements.
int subset(int arr[], int n)
{  
    // Traverse the input array and
    // store frequencies of elements
    unordered_map<int, int> mp;   
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // Find the maximum value in map.
    int res = 0;
    for (auto x : mp)
       res = max(res, x.second);

    return res;
}

// Driver code
int main()
{
    int arr[] = { 5, 6, 9, 3, 4, 3, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << subset(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.HashMap;
import java.util.Map;

// A hashing based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
class GFG
{

// Function to count subsets such that all
// subsets have distinct elements.
static int subset(int arr[], int n)
{
    // Traverse the input array and
    // store frequencies of elements
    HashMap<Integer, Integer> mp = new HashMap<>();
    for (int i = 0; i < n; i++)
        mp.put(arr[i],mp.get(arr[i]) == null?1:mp.get(arr[i])+1);

    // Find the maximum value in map.
    int res = 0;
    for (Map.Entry<Integer,Integer> entry : mp.entrySet())
    res = Math.max(res, entry.getValue());

    return res;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 5, 6, 9, 3, 4, 3, 4 };
    int n = arr.length;
    System.out.println( subset(arr, n));

}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# A hashing based solution to find the
# minimum number of subsets of a set such 
# that every subset contains distinct
# elements.

# Function to count subsets such that
# all subsets have distinct elements.
def subset(arr, n):

    # Traverse the input array and
    # store frequencies of elements
    mp = {i:0 for i in range(10)}
    for i in range(n):
        mp[arr[i]] += 1

    # Find the maximum value in map.
    res = 0
    for key, value in mp.items():
        res = max(res, value)

    return res

# Driver code
if __name__ == '__main__':
    arr = [5, 6, 9, 3, 4, 3, 4]
    n = len(arr)
    print(subset(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// A hashing based solution to find the
// minimum number of subsets of a set
// such that every subset contains distinct
// elements.
using System;
using System.Collections.Generic;

class GFG
{

// Function to count subsets such that all
// subsets have distinct elements.
static int subset(int []arr, int n)
{
    // Traverse the input array and
    // store frequencies of elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();
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

    // Find the maximum value in map.
    int res = 0;
    foreach(KeyValuePair<int, int> entry in mp)
        res = Math.Max(res, entry.Value);

    return res;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 5, 6, 9, 3, 4, 3, 4 };
    int n = arr.Length;
    Console.WriteLine(subset(arr, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
      // A hashing based solution to find the
      // minimum number of subsets of a set
      // such that every subset contains distinct
      // elements.
      // Function to count subsets such that all
      // subsets have distinct elements.
      function subset(arr, n) {
        // Traverse the input array and
        // store frequencies of elements
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

        // Find the maximum value in map.
        var res = 0;
        for (const [key, value] of Object.entries(mp)) {
          res = Math.max(res, value);
        }
        return res;
      }

      // Driver code
      var arr = [5, 6, 9, 3, 4, 3, 4];
      var n = arr.length;
      document.write(subset(arr, n));

      // This code is contributed by rdtank.
    </script>
```

**输出:**

```
2
```