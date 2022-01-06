# 一个区间可以相交的最大区间数

> 原文:[https://www . geeksforgeeks . org/一个区间可以相交的最大区间数/](https://www.geeksforgeeks.org/maximum-number-of-intervals-that-an-interval-can-intersect/)

给定一个由**【L，R】**形式的 **N** 区间组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **L，R** 表示区间的开始和结束位置，任务是计算一个区间可以彼此相交的最大区间数。

**示例:**

> **输入:** arr[] = {{1，2}，{3，4}，{2，5}}
> **输出:** 3
> **解释:**所需的一组间隔为{1，2}，{2，5}，{3，4}，因为{2，5}与所有其他间隔相交。
> 
> **输入:** arr[] = {{1，3}、{2，4}、{3，5}、{8，11}}
> **输出:** 3
> **解释:**所需的一组间隔为{1，3}、{2，4}、{3，5}，因为{2，4}与所有其他间隔相交。

**简单方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个区间，使用[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)计算其相交的区间数。检查每个间隔后，打印间隔可以相交的最大间隔数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of intervals that an interval
// can intersect
void findMaxIntervals(
    vector<pair<int, int> > v, int n)
{
    // Store the required answer
    int maxi = 0;

    // Traverse all the intervals
    for (int i = 0; i < n; i++) {

        // Store the number of
        // intersecting intervals
        int c = n;

        // Iterate in the range[0, n-1]
        for (int j = 0; j < n; j++) {

            // Check if jth interval lies
            // outside the ith interval
            if (v[i].second < v[j].first
                || v[i].first > v[j].second) {
                c--;
            }
        }

        // Update the overall maximum
        maxi = max(c, maxi);
    }

    // Print the answer
    cout << maxi;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr
        = { { 1, 2 },
            { 3, 4 },
            { 2, 5 } };
    int N = arr.size();

    // Function Call
    findMaxIntervals(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{

  static class Pair
  {
    int first, second;
    public Pair(int first, int second)
    {
      this.first = first;
      this.second = second;
    }
  }

  // Function to count the maximum number
  // of intervals that an interval
  // can intersect
  static void findMaxIntervals(ArrayList<Pair> v, int n)
  {

    // Store the required answer
    int maxi = 0;

    // Traverse all the intervals
    for (int i = 0; i < n; i++)
    {

      // Store the number of
      // intersecting intervals
      int c = n;

      // Iterate in the range[0, n-1]
      for (int j = 0; j < n; j++) {

        // Check if jth interval lies
        // outside the ith interval
        if (v.get(i).second < v.get(j).first
            || v.get(i).first > v.get(j).second) {
          c--;
        }
      }

      // Update the overall maximum
      maxi = Math.max(c, maxi);
    }

    // Print the answer
    System.out.print(maxi);
  }

  // Driver code
  public static void main(String[] args)
  {
    ArrayList<Pair> arr = new ArrayList<>();
    arr.add(new Pair(1,2));
    arr.add(new Pair(3,4));
    arr.add(new Pair(2,5));

    int N = arr.size();

    // Function Call
    findMaxIntervals(arr, N);
  }
}

// This code is contributed by susmitakundugoaldnga.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the maximum number
# of intervals that an interval
# can intersect
def findMaxIntervals(v, n) :

    # Store the required answer
    maxi = 0

    # Traverse all the intervals
    for i in range(n) :

        # Store the number of
        # intersecting intervals
        c = n

        # Iterate in the range[0, n-1]
        for j in range(n) :

            # Check if jth interval lies
            # outside the ith interval
            if (v[i][1] < v[j][0] or v[i][0] > v[j][1]) :

                c -= 1

        # Update the overall maximum
        maxi = max(c, maxi)

    # Print the answer
    print(maxi)

    # Driver code
arr = []
arr.append((1,2))
arr.append((3,4))
arr.append((2,5))
N = len(arr)

# Function Call
findMaxIntervals(arr, N)

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

    // Function to count the maximum number
    // of intervals that an interval
    // can intersect
    static void findMaxIntervals(List<Tuple<int, int> > v, int n)
    {

        // Store the required answer
        int maxi = 0;

        // Traverse all the intervals
        for (int i = 0; i < n; i++)
        {

            // Store the number of
            // intersecting intervals
            int c = n;

            // Iterate in the range[0, n-1]
            for (int j = 0; j < n; j++)
            {

                // Check if jth interval lies
                // outside the ith interval
                if (v[i].Item2 < v[j].Item1
                    || v[i].Item1 > v[j].Item2)
                {
                    c--;
                }
            }

            // Update the overall maximum
            maxi = Math.Max(c, maxi);
        }

        // Print the answer
        Console.Write(maxi);
    }

  // Driver code
  static void Main()
  {
    List<Tuple<int, int>> arr = new List<Tuple<int, int>>();
    arr.Add(new Tuple<int,int>(1,2));
    arr.Add(new Tuple<int,int>(3,4));
    arr.Add(new Tuple<int,int>(2,5));
    int N = arr.Count;

    // Function Call
    findMaxIntervals(arr, N);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the maximum number
// of intervals that an interval
// can intersect
function findMaxIntervals( v, n)
{
    // Store the required answer
    var maxi = 0;

    // Traverse all the intervals
    for (var i = 0; i < n; i++) {

        // Store the number of
        // intersecting intervals
        var c = n;

        // Iterate in the range[0, n-1]
        for (var j = 0; j < n; j++) {

            // Check if jth interval lies
            // outside the ith interval
            if (v[i][1] < v[j][0]
                || v[i][0] > v[j][1]) {
                c--;
            }
        }

        // Update the overall maximum
        maxi = Math.max(c, maxi);
    }

    // Print the answer
    document.write( maxi);
}

// Driver Code
var arr
    = [ [ 1, 2 ],
        [ 3, 4 ],
        [ 2, 5 ] ];
var N = arr.length;

// Function Call
findMaxIntervals(arr, N);

</script>
```

**Output:** 

```
3
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**高效方法:**上述方法可以通过计算不相交的区间数来优化，而不是计算相交的数量。不与特定区间相交的区间可以分为两个不相交的类别:完全向左或完全向右的区间。利用这个想法，按照以下步骤解决问题:

*   [创建一个 hashmap](https://www.geeksforgeeks.org/how-to-create-an-unordered_map-of-pairs-in-c/) ，比如 **M** ，来映射不与每个区间相交的区间数。
*   [根据间隔的起点对间隔](https://www.geeksforgeeks.org/sort-c-stl/)进行排序。
*   使用变量 **i** 遍历区间
    *   将 **ans** 初始化为 **-1** 以存储完全位于 **i <sup>th</sup>** 区间右侧的第一个区间的索引。
    *   将**低电平**和**高电平**初始化为 **(i + 1)** 和**(N–1)**，执行如下[二分搜索法](https://www.geeksforgeeks.org/binary-search/):
        *   求**中间**的值为**(低+高)/2** 。
        *   如果**区间【中间】**的起始位置大于**区间【I】**的结束位置，将当前索引**中间**存储在 **ans** 中，然后通过将**高**更新为**(中间–1)**来检查左半部分。
        *   否则，通过将**低电平**更新为**(中间+ 1)** 来检查右半部分。
    *   如果 **ans** 的值不是 **-1** ，则在 **M【区间[I]】**中加上**(N–ans)**。
*   现在，[根据间隔的结束点对间隔](https://www.geeksforgeeks.org/sort-c-stl/)进行排序。
*   再次，使用变量 **i** 遍历区间，并应用与上面类似的方法找到完全位于 **i <sup>第</sup>T5】区间左侧的区间。**
*   循环结束后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/) **M** ，将最小值存储在 **min** 中。
*   打印**(N–min)**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort in
// increasing order of second
// values in each pair
bool compare(pair<int, int> f,
             pair<int, int> s)
{
    return f.second < s.second;
}

// Function to hash a pair
struct hash_pair {
    template <class T1, class T2>
    size_t operator()(
        const pair<T1, T2>& p) const
    {
        auto hash1 = hash<T1>{}(p.first);
        auto hash2 = hash<T2>{}(p.second);
        return hash1 ^ hash2;
    }
};

// Function to count maximum number
// of intervals that an interval
// can intersect
void findMaxIntervals(
    vector<pair<int, int> > v, int n)
{

    // Create a hashmap
    unordered_map<pair<int, int>,
                  int,
                  hash_pair>
        um;

    // Sort by starting position
    sort(v.begin(), v.end());

    // Traverse all the intervals
    for (int i = 0; i < n; i++) {

        // Initialize um[v[i]] as 0
        um[v[i]] = 0;

        // Store the starting and
        // ending point of the
        // ith interval
        int start = v[i].first;
        int end = v[i].second;

        // Set low and high
        int low = i + 1;
        int high = n - 1;

        // Store the required number
        // of intervals
        int ans = -1;

        // Apply binary search to find
        // the number of intervals
        // completely lying to the
        // right of the ith interval
        while (low <= high) {

            // Find the mid
            int mid = low + (high - low) / 2;

            // Condition for searching
            // in the first half
            if (v[mid].first > end) {
                ans = mid;
                high = mid - 1;
            }

            // Otherwise search in the
            // second half
            else {
                low = mid + 1;
            }
        }

        // Increment um[v[i]] by n-ans
        // if ans!=-1
        if (ans != -1)
            um[v[i]] = n - ans;
    }

    // Sort by ending position
    sort(v.begin(), v.end(), compare);

    // Traverse all the intervals
    for (int i = 0; i < n; i++) {

        // Store the starting and
        // ending point of the
        // ith interval
        int start = v[i].first;
        int end = v[i].second;

        // Set low and high
        int low = 0;
        int high = i - 1;

        // Store the required number
        // of intervals
        int ans = -1;

        // Apply binary search to
        // find the number of intervals
        // completely lying to the
        // left of the ith interval
        while (low <= high) {
            int mid = low + (high - low) / 2;
            if (v[mid].second < start) {
                ans = mid;
                low = mid + 1;
            }
            else {
                high = mid - 1;
            }
        }

        // Increment um[v[i]] by ans+1
        // if ans!=-1
        if (ans != -1)
            um[v[i]] += (ans + 1);
    }

    // Store the answer
    int res = 0;

    // Traverse the map
    for (auto it = um.begin();
         it != um.end(); it++) {

        // Update the overall answer
        res = max(res, n - it->second);
    }

    // Print the answer
    cout << res;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr
        = { { 1, 2 },
            { 3, 4 },
            { 2, 5 } };

    int N = arr.size();

    // Function Call
    findMaxIntervals(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;
class GFG
{

  // Pair class to store in the um as a key
  // with hashcode and equals
  static class Pair
  {

    int first;
    int second;
    public Pair(int first, int second)
    {
      this.first = first;
      this.second = second;
    }

    @Override public int hashCode()
    {
      final int prime = 31;
      int result = 1;
      result = prime * result + first;
      result = prime * result + second;
      return result;
    }

    @Override public boolean equals(Object obj)
    {
      if (this == obj)
        return true;
      if (obj == null)
        return false;
      if (getClass() != obj.getClass())
        return false;
      Pair other = (Pair)obj;
      if (first != other.first)
        return false;
      if (second != other.second)
        return false;
      return true;
    }
  }

  // Function to count maximum number
  // of intervals that an interval
  // can intersect
  static void findMaxIntervals(ArrayList<Pair> v, int n)
  {

    // Create a hashmap
    HashMap<Pair, Integer> um = new HashMap<>();

    // Sort by starting position
    Collections.sort(v, (x, y) -> x.first - y.first);

    // Traverse all the intervals
    for (int i = 0; i < n; i++) {

      // Initialize um for v[i] as 0
      um.put(v.get(i), 0);

      // Store the starting and
      // ending point of the
      // ith interval
      int start = v.get(i).first;
      int end = v.get(i).second;

      // Set low and high
      int low = i + 1;
      int high = n - 1;

      // Store the required number
      // of intervals
      int ans = -1;

      // Apply binary search to find
      // the number of intervals
      // completely lying to the
      // right of the ith interval
      while (low <= high) {

        // Find the mid
        int mid = low + (high - low) / 2;

        // Condition for searching
        // in the first half
        if (v.get(mid).first > end) {
          ans = mid;
          high = mid - 1;
        }

        // Otherwise search in the
        // second half
        else {
          low = mid + 1;
        }
      }

      // Increment um for v[i] by n-ans
      // if ans!=-1
      if (ans != -1)
        um.put(v.get(i), n - ans);
    }

    // Sort by ending position
    Collections.sort(v, (x, y) -> x.second - y.second);

    // Traverse all the intervals
    for (int i = 0; i < n; i++) {

      // Store the starting and
      // ending point of the
      // ith interval
      int start = v.get(i).first;
      int end = v.get(i).second;

      // Set low and high
      int low = 0;
      int high = i - 1;

      // Store the required number
      // of intervals
      int ans = -1;

      // Apply binary search to
      // find the number of intervals
      // completely lying to the
      // left of the ith interval
      while (low <= high) {
        int mid = low + (high - low) / 2;
        if (v.get(mid).second < start) {
          ans = mid;
          low = mid + 1;
        }
        else {
          high = mid - 1;
        }
      }

      // Increment um for v[i] by ans+1
      // if ans!=-1
      if (ans != -1)
        um.put(v.get(i),
               um.get(v.get(i)) + (ans + 1));
    }

    // Store the answer
    int res = 0;

    // Traverse the map
    for (int second : um.values()) {

      // Update the overall answer
      res = Math.max(res, n - second);
    }

    // Print the answer
    System.out.println(res);
  }

  // Driver Code
  public static void main(String[] args)
  {

    ArrayList<Pair> arr = new ArrayList<>();
    arr.add(new Pair(1, 2));
    arr.add(new Pair(3, 4));
    arr.add(new Pair(2, 5));

    int N = arr.size();

    // Function Call
    findMaxIntervals(arr, N);
  }
}

// This code is contributed by Kingash.
```

**Output:** 

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*