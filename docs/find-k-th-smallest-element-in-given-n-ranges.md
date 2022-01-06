# 在给定的 n 个范围内找到第 k 个最小元素

> 原文:[https://www . geeksforgeeks . org/find-k-th-给定 n 范围内的最小元素/](https://www.geeksforgeeks.org/find-k-th-smallest-element-in-given-n-ranges/)

给定 n 和 q，即范围数和查询数，找到每个查询的第 k 个最小元素(假设 k>1)。如果存在，打印第 k 个最小元素的值，否则打印-1。

**示例:**

```
Input : arr[] = {{1, 4}, {6, 8}}
        queries[] = {2, 6, 10};
Output : 2
         7
        -1
After combining the given ranges, the numbers
become 1 2 3 4 6 7 8\. As here 2nd element is 2,
so we print 2\. As 6th element is 7, so we print
7 and as 10th element doesn't exist, so we
print -1.

Input : arr[] = {{2, 6}, {5, 7}}
        queries[] = {5, 8};
Output : 6
        -1
After combining the given ranges, the numbers 
become 2 3 4 5 6 7\. As here 5th element is 6, 
so we print 6 and as 8th element doesn't exist, 
so we print -1.
```

思路是先前提:[合并重叠区间](https://www.geeksforgeeks.org/merging-intervals/)保持所有区间按照开始时间升序排序。在一个合并了[]的数组中合并后，我们使用线性搜索来寻找第 k 个最小的元素。

下面是上述方法的实现:

## C++

```
// C++ implementation to solve k queries
// for given n ranges
#include <bits/stdc++.h>
using namespace std;

// Structure to store the
// start and end point
struct Interval
{
    int s;
    int e;
};

// Comparison function for sorting
bool comp(Interval a, Interval b)
{
    return a.s < b.s;
}

// Function to find Kth smallest number in a vector
// of merged intervals
int kthSmallestNum(vector<Interval> merged, int k)
{
    int n = merged.size();

    // Traverse merged[] to find
    // Kth smallest element using Linear search.
    for (int j = 0; j < n; j++)
    {
        if (k <= abs(merged[j].e -
                     merged[j].s + 1))
            return (merged[j].s + k - 1);

        k = k - abs(merged[j].e -
                     merged[j].s + 1);
    }

    if (k)
        return -1;
}

// To combined both type of ranges,
// overlapping as well as non-overlapping.
void mergeIntervals(vector<Interval> &merged,
                 Interval arr[], int n)
{
    // Sorting intervals according to start
    // time
    sort(arr, arr + n, comp);

    // Merging all intervals into merged
    merged.push_back(arr[0]);
    for (int i = 1; i < n; i++)
    {
        // To check if starting point of next
        // range is lying between the previous
        // range and ending point of next range
        // is greater than the Ending point
        // of previous range then update ending
        // point of previous range by ending
        // point of next range.
        Interval prev = merged.back();
        Interval curr = arr[i];
        if ((curr.s >= prev.s &&
             curr.s <= prev.e) &&
            (curr.e > prev.e))

            merged.back().e = curr.e;

        else
        {
            // If starting point of next range
            // is greater than the ending point
            // of previous range then store next range
            // in merged[].
            if (curr.s > prev.e)
                merged.push_back(curr);
        }
    }
}

// Driver\'s Function
int main()
{
    Interval arr[] = {{2, 6}, {4, 7}};
    int n = sizeof(arr)/sizeof(arr[0]);
    int query[] = {5, 8};
    int q = sizeof(query)/sizeof(query[0]);

    // Merge all intervals into merged[]
    vector<Interval>merged;
    mergeIntervals(merged, arr, n);

    // Processing all queries on merged
    // intervals
    for (int i = 0; i < q; i++)
        cout << kthSmallestNum(merged, query[i])
             << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to solve k queries
// for given n ranges
import java.util.*;

class GFG
{

// Structure to store the
// start and end point
static class Interval
{
    int s;
    int e;
    Interval(int a,int b)
    {
        s = a;
        e = b;
    }
};
static class Sortby implements Comparator<Interval>
{
    // Comparison function for sorting
    public int compare(Interval a, Interval b)
    {
        return a.s - b.s;
    }
}

// Function to find Kth smallest number in a Vector
// of merged intervals
static int kthSmallestNum(Vector<Interval> merged, int k)
{
    int n = merged.size();

    // Traverse merged.get( )o find
    // Kth smallest element using Linear search.
    for (int j = 0; j < n; j++)
    {
        if (k <= Math.abs(merged.get(j).e -
                    merged.get(j).s + 1))
            return (merged.get(j).s + k - 1);

        k = k - Math.abs(merged.get(j).e -
                    merged.get(j).s + 1);
    }

    if (k != 0)
        return -1;
    return 0;
}

// To combined both type of ranges,
// overlapping as well as non-overlapping.
static Vector<Interval> mergeIntervals(Vector<Interval> merged,
                Interval arr[], int n)
{
    // Sorting intervals according to start
    // time
    Arrays.sort(arr, new Sortby());

    // Merging all intervals into merged
    merged.add(arr[0]);
    for (int i = 1; i < n; i++)
    {
        // To check if starting point of next
        // range is lying between the previous
        // range and ending point of next range
        // is greater than the Ending point
        // of previous range then update ending
        // point of previous range by ending
        // point of next range.
        Interval prev = merged.get(merged.size() - 1);
        Interval curr = arr[i];
        if ((curr.s >= prev.s &&
            curr.s <= prev.e) &&
            (curr.e > prev.e))

            merged.get(merged.size()-1).e = curr.e;

        else
        {
            // If starting point of next range
            // is greater than the ending point
            // of previous range then store next range
            // in merged.get(.)         if (curr.s > prev.e)
                merged.add(curr);
        }
    }
    return merged;
}

// Driver code
public static void main(String args[])
{
    Interval arr[] = {new Interval(2, 6), new Interval(4, 7)};
    int n = arr.length;
    int query[] = {5, 8};
    int q = query.length;

    // Merge all intervals into merged.get())
    Vector<Interval> merged = new Vector<Interval>();
    merged=mergeIntervals(merged, arr, n);

    // Processing all queries on merged
    // intervals
    for (int i = 0; i < q; i++)
        System.out.println( kthSmallestNum(merged, query[i]));
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation to solve k queries
# for given n ranges

# Structure to store the
# start and end point
class Interval:
    def __init__(self, s, e):
        self.s = s
        self.e = e

# Function to find Kth smallest number in a vector
# of merged intervals
def kthSmallestNum(merged: list, k: int) -> int:
    n = len(merged)

    # Traverse merged[] to find
    # Kth smallest element using Linear search.
    for j in range(n):
        if k <= abs(merged[j].e - merged[j].s + 1):
            return merged[j].s + k - 1

        k = k - abs(merged[j].e - merged[j].s + 1)

    if k:
        return -1

# To combined both type of ranges,
# overlapping as well as non-overlapping.
def mergeIntervals(merged: list, arr: list, n: int):

    # Sorting intervals according to start
    # time
    arr.sort(key = lambda a: a.s)

    # Merging all intervals into merged
    merged.append(arr[0])
    for i in range(1, n):

        # To check if starting point of next
        # range is lying between the previous
        # range and ending point of next range
        # is greater than the Ending point
        # of previous range then update ending
        # point of previous range by ending
        # point of next range.
        prev = merged[-1]
        curr = arr[i]
        if curr.s >= prev.s and curr.s <= prev.e and\
          curr.e > prev.e:
            merged[-1].e = curr.e
        else:

            # If starting point of next range
            # is greater than the ending point
            # of previous range then store next range
            # in merged[].
            if curr.s > prev.e:
                merged.append(curr)

# Driver Code
if __name__ == "__main__":

    arr = [Interval(2, 6), Interval(4, 7)]
    n = len(arr)
    query = [5, 8]
    q = len(query)

    # Merge all intervals into merged[]
    merged = []
    mergeIntervals(merged, arr, n)

    # Processing all queries on merged
    # intervals
    for i in range(q):
        print(kthSmallestNum(merged, query[i]))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation to solve k queries
// for given n ranges
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

// Structure to store the
// start and end point
public class Interval
{
    public int s;
    public int e;

    public Interval(int a, int b)
    {
        s = a;
        e = b;
    }
};

class sortHelper : IComparer
{
    int IComparer.Compare(object a, object b)
    {
        Interval first = (Interval)a;
        Interval second = (Interval)b;
        return first.s - second.s;
    }
}

// Function to find Kth smallest number in
// a Vector of merged intervals
static int kthSmallestNum(ArrayList merged, int k)
{
    int n = merged.Count;

    // Traverse merged.get( )o find
    // Kth smallest element using Linear search.
    for(int j = 0; j < n; j++)
    {
        if (k <= Math.Abs(((Interval)merged[j]).e -
                          ((Interval)merged[j]).s + 1))
            return (((Interval)merged[j]).s + k - 1);

        k = k - Math.Abs(((Interval)merged[j]).e -
                         ((Interval)merged[j]).s + 1);
    }

    if (k != 0)
        return -1;

    return 0;
}

// To combined both type of ranges,
// overlapping as well as non-overlapping.
static ArrayList mergeIntervals(ArrayList merged,
                                Interval []arr, int n)
{

    // Sorting intervals according to start
    // time
    Array.Sort(arr, new sortHelper());

    // Merging all intervals into merged
    merged.Add((Interval)arr[0]);

    for(int i = 1; i < n; i++)
    {

        // To check if starting point of next
        // range is lying between the previous
        // range and ending point of next range
        // is greater than the Ending point
        // of previous range then update ending
        // point of previous range by ending
        // point of next range.
        Interval prev = (Interval)merged[merged.Count - 1];
        Interval curr = arr[i];

        if ((curr.s >= prev.s && curr.s <= prev.e) &&
            (curr.e > prev.e))
        {
            ((Interval)merged[merged.Count - 1]).e = ((Interval)curr).e;
        }
        else
        {

            // If starting point of next range
            // is greater than the ending point
            // of previous range then store next range
            // in merged.get(.) if (curr.s > prev.e)
            merged.Add(curr);
        }
    }
    return merged;
}

// Driver code
public static void Main(string []args)
{
    Interval []arr = { new Interval(2, 6),
                       new Interval(4, 7) };
    int n = arr.Length;
    int []query = { 5, 8 };
    int q = query.Length;

    // Merge all intervals into merged.get())
    ArrayList merged = new ArrayList();

    merged = mergeIntervals(merged, arr, n);

    // Processing all queries on merged
    // intervals
    for(int i = 0; i < q; i++)
        Console.WriteLine(kthSmallestNum(
            merged, query[i]));
}
}

// This code is contributed by pratham76
```

## java 描述语言

```
<script>

// JavaScript implementation to solve k queries
// for given n ranges

// Structure to store the
// start and end point
class Interval
{
    constructor(a,b)
    {
        this.s=a;
        this.e=b;
    }
}

// Function to find Kth smallest number in a Vector
// of merged intervals
function kthSmallestNum(merged,k)
{
    let n = merged.length;

    // Traverse merged.get( )o find
    // Kth smallest element using Linear search.
    for (let j = 0; j < n; j++)
    {
        if (k <= Math.abs(merged[j].e -
                    merged[j].s + 1))
            return (merged[j].s + k - 1);

        k = k - Math.abs(merged[j].e -
                    merged[j].s + 1);
    }

    if (k != 0)
        return -1;
    return 0;
}

// To combined both type of ranges,
// overlapping as well as non-overlapping.
function mergeIntervals(merged,arr,n)
{
    // Sorting intervals according to start
    // time
    arr.sort(function(a,b){return a.s-b.s;});

    // Merging all intervals into merged
    merged.push(arr[0]);
    for (let i = 1; i < n; i++)
    {
        // To check if starting point of next
        // range is lying between the previous
        // range and ending point of next range
        // is greater than the Ending point
        // of previous range then update ending
        // point of previous range by ending
        // point of next range.
        let prev = merged[merged.length - 1];
        let curr = arr[i];
        if ((curr.s >= prev.s &&
            curr.s <= prev.e) &&
            (curr.e > prev.e))

            merged[merged.length-1].e = curr.e;

        else
        {
            // If starting point of next range
            // is greater than the ending point
            // of previous range then store next range
            // in merged.get(.)         if (curr.s > prev.e)
                merged.push(curr);
        }
    }
    return merged;
}

// Driver code
let arr=[new Interval(2, 6), new Interval(4, 7)];
let n = arr.length;
let query = [5, 8];
let q = query.length;

// Merge all intervals into merged.get())
let merged = [];
merged=mergeIntervals(merged, arr, n);

// Processing all queries on merged
// intervals
for (let i = 0; i < q; i++)
    document.write( kthSmallestNum(merged, query[i])+"<br>");

// This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
 6
 -1
```

**时间复杂度:** O(nlog(n))
**辅助空间:** O(n)