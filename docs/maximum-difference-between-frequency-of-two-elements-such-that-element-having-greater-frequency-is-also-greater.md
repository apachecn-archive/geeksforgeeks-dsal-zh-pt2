# 两个元件频率之间的最大差值，使得具有更大频率的元件也更大

> 原文:[https://www . geeksforgeeks . org/两个元素的频率之间的最大差异-这样具有更高频率的元素也更大/](https://www.geeksforgeeks.org/maximum-difference-between-frequency-of-two-elements-such-that-element-having-greater-frequency-is-also-greater/)

给定一个包含多个重复元素的正整数数组。任务是找到任何两个不同元素的频率之间的最大差异，这样频率较大的元素的值也大于第二个整数。

**示例:**

```
Input :  arr[] = { 3, 1, 3, 2, 3, 2 }.
Output : 2
Frequency of 3 = 3.
Frequency of 2 = 2.
Frequency of 1 = 1.
Here difference of frequency of element 3 and 1 is = 3 - 1 = 2.
Also 3 > 1.
```

**方法 1(使用哈希):**
最简单的方法可以是，找到每个元素的频率，并为每个元素找到具有比当前元素更小的值和频率的元素。

下面是该方法的实现:

## C++

```
// C++ program to find maximum difference
// between frequency of any two element
// such that element with greater frequency
// is also greater in value.
#include<bits/stdc++.h>
using namespace std;

// Return the maximum difference between
// frequencies of any two elements such that
// element with greater frequency is also
// greater in value.
int maxdiff(int arr[], int n)
{
    unordered_map<int, int> freq;

    // Finding the frequency of each element.
    for (int i = 0; i < n; i++)
        freq[arr[i]]++;

    int ans = 0;
    for (int i=0; i<n; i++)
    {
        for (int j=0; j<n; j++)
        {
            // finding difference such that element
            // having greater frequency is also
            // greater in value.
            if (freq[arr[i]] > freq[arr[j]] &&
                arr[i] > arr[j] )
                ans = max(ans, freq[arr[i]]-freq[arr[j]]);
            else if (freq[arr[i]] < freq[arr[j]] &&
                      arr[i] < arr[j] )
                ans = max(ans, freq[arr[j]]-freq[arr[i]]);
        }
    }

    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 3, 1, 3, 2, 3, 2 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << maxdiff(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum difference
// between frequency of any two element
// such that element with greater frequency
// is also greater in value.
import java.util.*;
class GFG
{

// Return the maximum difference between
// frequencies of any two elements such that
// element with greater frequency is also
// greater in value.
static int maxdiff(int arr[], int n)
{
    Map<Integer, Integer> freq = new HashMap<>();

    // Finding the frequency of each element.
    for (int i = 0; i < n; i++)
        freq.put(arr[i],
        freq.get(arr[i]) == null ? 1 :
        freq.get(arr[i]) + 1);

    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < n; j++)
        {
            // finding difference such that element
            // having greater frequency is also
            // greater in value.
            if (freq.get(arr[i]) > freq.get(arr[j]) &&
                arr[i] > arr[j])
                ans = Math.max(ans, freq.get(arr[i]) -
                                    freq.get(arr[j]));
            else if (freq.get(arr[i]) < freq.get(arr[j]) &&
                    arr[i] < arr[j] )
                ans = Math.max(ans, freq.get(arr[j]) -
                                    freq.get(arr[i]));
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 3, 1, 3, 2, 3, 2 };
    int n = arr.length;

    System.out.println(maxdiff(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python program to find maximum difference
# between frequency of any two element
# such that element with greater frequency
# is also greater in value.

from collections import defaultdict

# Return the maximum difference between
# frequencies of any two elements such that
# element with greater frequency is also
# greater in value.
def maxdiff(arr, n):
    freq = defaultdict(lambda: 0)

    # Finding the frequency of each element.
    for i in range(n):
        freq[arr[i]] += 1
    ans = 0
    for i in range(n):
        for j in range(n):

            # finding difference such that element
            # having greater frequency is also
            # greater in value.
            if freq[arr[i]] > freq[arr[j]] and arr[i] > arr[j]:
                ans = max(ans, freq[arr[i]] - freq[arr[j]])
            elif freq[arr[i]] < freq[arr[j]] and arr[i] < arr[j]:
                ans = max(ans, freq[arr[j]] - freq[arr[i]])
    return ans

arr = [3,1,3,2,3,2]
n = len(arr)
print(maxdiff(arr,n))

# This code is contributed by Shrikant13
```

## C#

```
// C# program to find maximum difference
// between frequency of any two element
// such that element with greater frequency
// is also greater in value.
using System;
using System.Collections.Generic;

class GFG
{
    // Return the maximum difference between
    // frequencies of any two elements such that
    // element with greater frequency is also
    // greater in value.
    static int maxdiff(int[] arr, int n)
    {
        Dictionary<int,
                   int> freq = new Dictionary<int,
                                              int>();

        // Finding the frequency of each element.
        for (int i = 0; i < n; i++)
        {
            if (freq.ContainsKey(arr[i]))
                freq[arr[i]]++;
            else
                freq.Add(arr[i], 1);
        }
        int ans = 0;
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < n; j++)
            {
                // finding difference such that element
                // having greater frequency is also
                // greater in value.
                if (freq[arr[i]] > freq[arr[j]] && arr[i] > arr[j])
                    ans = Math.Max(ans, freq[arr[i]] - freq[arr[i]]);
                else if (freq[arr[i]] < freq[arr[j]] && arr[i] < arr[j])
                    ans = Math.Max(ans, freq[arr[j]] - freq[arr[i]]);
            }
        }
        return ans;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int[] arr = { 3, 1, 3, 2, 3, 2 };
        int n = arr.Length;
        Console.WriteLine(maxdiff(arr, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>

//  JavaScript program to find maximum difference
// between frequency of any two element
// such that element with greater frequency
// is also greater in value.

// Return the maximum difference between
// frequencies of any two elements such that
// element with greater frequency is also
// greater in value.
function maxdiff(arr, n)
{
    let freq = new Map();

    // Finding the frequency of each element.
    for (let i = 0; i < n; i++)
        freq.set(arr[i],
        freq.get(arr[i]) == null ? 1 :
        freq.get(arr[i]) + 1);

    let ans = 0;
    for (let i = 0; i < n; i++)
    {
        for (let j = 0; j < n; j++)
        {
            // finding difference such that element
            // having greater frequency is also
            // greater in value.
            if (freq.get(arr[i]) > freq.get(arr[j]) &&
                arr[i] > arr[j])
                ans = Math.max(ans, freq.get(arr[i]) -
                                    freq.get(arr[j]));
            else if (freq.get(arr[i]) < freq.get(arr[j]) &&
                    arr[i] < arr[j] )
                ans = Math.max(ans, freq.get(arr[j]) -
                                    freq.get(arr[i]));
        }
    }
    return ans;
}

    // Driver code

    let arr = [ 3, 1, 3, 2, 3, 2 ];
    let n = arr.length;

   document.write(maxdiff(arr, n));

</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n <sup>2</sup> )。

**辅助空间:** O(n)

**方法 2(使用哈希和排序):**
想法是找到所有不同的元素并将其存储在一个数组中，比如 dist[ ]。按递增顺序对不同元素数组 dist[]进行排序。现在对于索引 I 处的任何不同元素，对于所有索引 j，使得 i > j > 0，找到索引 0 到 i-1 之间具有最小频率的元素。我们可以用与方法 1 相同的方法找到一个元素的频率，即在哈希表中存储频率。
所以对所有的 I 都这样做，找到最大的差异。为了找到所有的最小频率，我保持前缀最小值。

下面是这种方法的表示:

## C++

```
// Efficient C++ program to find maximum
// difference between frequency of any two
// elements such that element with greater
// frequency is also greater in value.
#include<bits/stdc++.h>
using namespace std;

// Return the maximum difference between
// frequencies of any two elements such that
// element with greater frequency is also
// greater in value.
int maxdiff(int arr[], int n)
{
    unordered_map<int, int> freq;

    int dist[n];

    // Finding the frequency of each element.
    int j = 0;
    for (int i = 0; i < n; i++)
    {
        if (freq.find(arr[i]) == freq.end())
            dist[j++] = arr[i];

        freq[arr[i]]++;
    }

    // Sorting the distinct element
    sort(dist, dist + j);

    int min_freq = n+1;

    // Iterate through all sorted distinct elements.
    // For each distinct element, maintaining the
    // element with minimum frequency than that
    // element and also finding the maximum
    // frequency difference
    int ans = 0;
    for (int i=0; i<j; i++)
    {
        int cur_freq = freq[dist[i]];
        ans = max(ans, cur_freq - min_freq);
        min_freq = min(min_freq, cur_freq);
    }

    return ans;
}

// Driven Program
int main()
{
    int arr[] = { 3, 1, 3, 2, 3, 2 };
    int n = sizeof(arr)/sizeof(arr[0]);

    cout << maxdiff(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Efficient Java program to find maximum
// difference between frequency of any two
// elements such that element with greater
// frequency is also greater in value.
import java.util.*;
class GFG
{

  // Return the maximum difference between
  // frequencies of any two elements such that
  // element with greater frequency is also
  // greater in value.
  static int maxdiff(int arr[], int n)
  {
    HashMap<Integer,Integer> freq= new HashMap<>();

    int []dist = new int[n];

    // Finding the frequency of each element.
    int j = 0;
    for (int i = 0; i < n; i++)
    {
      dist[j++] = arr[i];
      if (!freq.containsKey(arr[i]))
        freq.put(arr[i], 1);
      else
        freq.put(arr[i], freq.get(arr[i]) + 1);

    }

    // Sorting the distinct element
    Arrays.sort(dist);

    int min_freq = n + 1;

    // Iterate through all sorted distinct elements.
    // For each distinct element, maintaining the
    // element with minimum frequency than that
    // element and also finding the maximum
    // frequency difference
    int ans = 0;
    for (int i = 0; i < j; i++)
    {
      int cur_freq = freq.get(dist[i]);
      ans = Math.max(ans, cur_freq - min_freq);
      min_freq = Math.min(min_freq, cur_freq);
    }

    return ans;
  }

  // Driven Program
  public static void main(String[] args)
  {
    int arr[] = { 3, 1, 3, 2, 3, 2 };
    int n = arr.length;

    System.out.print(maxdiff(arr, n) +"\n");
  }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Efficient Python3 program to find maximum
# difference between frequency of any two
# elements such that element with greater
# frequency is also greater in value.

# Return the maximum difference between
# frequencies of any two elements such that
# element with greater frequency is also
# greater in value.
def maxdiff(arr, n):
    freq = {}
    dist = [0] * n

    # Finding the frequency of each element.
    j = 0
    for i in range(n):
        if (arr[i] not in freq):
            dist[j] = arr[i]
            j += 1
            freq[arr[i]] = 0
        if (arr[i] in freq):
            freq[arr[i]] += 1
    dist = dist[:j]

    # Sorting the distinct element
    dist.sort()
    min_freq = n + 1

    # Iterate through all sorted distinct elements.
    # For each distinct element, maintaining the
    # element with minimum frequency than that
    # element and also finding the maximum
    # frequency difference
    ans = 0
    for i in range(j):
        cur_freq = freq[dist[i]]
        ans = max(ans, cur_freq - min_freq)
        min_freq = min(min_freq, cur_freq)

    return ans

# Driven Program
arr = [3, 1, 3, 2, 3, 2]
n = len(arr)

print(maxdiff(arr, n))

# This code is contributed by SHUBHAMSINGH10
```

## C#

```
// Efficient C# program to find maximum
// difference between frequency of any two
// elements such that element with greater
// frequency is also greater in value.
using System.Collections.Generic;
using System;

class GFG{

// Return the maximum difference between
// frequencies of any two elements such
// that element with greater frequency
// is also greater in value.
static int maxdiff(int []arr, int n)
{
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();
    List<int> dist = new List<int>();

    // Finding the frequency of each element.
    int j = 0;
    for(int i = 0; i < n; i++)
    {
        if (freq.ContainsKey(arr[i]) == false)
        {
            dist.Add(arr[i]);
            j++;
        }

        if (freq.ContainsKey(arr[i]))
            freq[arr[i]]++;
        else
            freq[arr[i]]=1;
    }

    // Sorting the distinct element
    dist.Sort();
    int min_freq = n + 1;

    // Iterate through all sorted distinct elements.
    // For each distinct element, maintaining the
    // element with minimum frequency than that
    // element and also finding the maximum
    // frequency difference
    int ans = 0;
    for(int i = 0; i < j; i++)
    {
        int cur_freq = freq[dist[i]];
        ans = Math.Max(ans, cur_freq - min_freq);
        min_freq = Math.Min(min_freq, cur_freq);
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 3, 1, 3, 2, 3, 2 };
    int n = arr.Length;

    Console.WriteLine(maxdiff(arr, n));
}
}

// This code is contributed by Stream_Cipher
```

## java 描述语言

```
<script>

// Efficient Javascript program to find maximum
// difference between frequency of any two
// elements such that element with greater
// frequency is also greater in value.

// Return the maximum difference between
// frequencies of any two elements such that
// element with greater frequency is also
// greater in value.
function maxdiff(arr, n)
{
    var freq = new Map(); 

    var dist = Array(n);

    // Finding the frequency of each element.
    var j = 0;
    for (var i = 0; i < n; i++)
    {
        if (!freq.has(arr[i]))
            dist[j++] = arr[i];

        if(freq.has(arr[i]))
            freq.set(arr[i], freq.get(arr[i])+1)
        else
            freq.set(arr[i], 1)
    }

    // Sorting the distinct element
    dist.sort();

    var min_freq = n+1;

    // Iterate through all sorted distinct elements.
    // For each distinct element, maintaining the
    // element with minimum frequency than that
    // element and also finding the maximum
    // frequency difference
    var ans = 0;
    for (var i=0; i<j; i++)
    {
        var cur_freq = freq.get(dist[i]);
        ans = Math.max(ans, cur_freq - min_freq);
        min_freq = Math.min(min_freq, cur_freq);
    }

    return ans;
}

// Driven Program
var arr = [3, 1, 3, 2, 3, 2 ];
var n = arr.length;
document.write( maxdiff(arr, n))

// This code is contributed by famously.
</script>
```

**输出:**

```
2
```

**时间复杂度:** O(n log n)。

**辅助空间:** O(n)

本文由[**Anuj Chauhan(Anuj 0503)**](https://web.facebook.com/anuj0503)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。