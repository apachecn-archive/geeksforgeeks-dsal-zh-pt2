# 合并 k 个排序数组|集合 2(不同大小的数组)

> 原文:[https://www . geesforgeks . org/merge-k-sorted-arrays-set-2-不同大小的数组/](https://www.geeksforgeeks.org/merge-k-sorted-arrays-set-2-different-sized-arrays/)

给定 k 个可能大小不同的排序数组，合并它们并打印排序后的输出。
示例:

```
Input: k = 3 
      arr[][] = { {1, 3},
                  {2, 4, 6},
                  {0, 9, 10, 11}} ;
Output: 0 1 2 3 4 6 9 10 11 

Input: k = 2
      arr[][] = { {1, 3, 20},
                  {2, 4, 6}} ;
Output: 1 2 3 4 6 20 
```

我们已经讨论了一个解决方案，适用于[中所有大小相同的数组合并 k 个排序数组|集合 1](https://www.geeksforgeeks.org/merge-k-sorted-arrays/) 。
一个**简单的解决方案**是创建一个输出数组，并一个接一个地将所有数组复制到其中。最后，使用对输出数组进行排序。这种方法需要 O(N ^ Logn ^ N)个时间，其中 N 是所有元素的计数。
一个**高效的解决方案**就是使用堆数据结构。基于堆的解决方案的时间复杂度为 O(N Log k)。
1。创建输出数组。
2。创建一个 k 大小的最小堆，并将所有数组中的第一个元素插入到堆中
3。当优先级队列不为空时，重复以下步骤。
…..a)从堆中移除最小元素(最小值总是在根)，并将其存储在输出数组中。
…..b)从提取元素的数组中插入下一个元素。如果数组没有更多的元素，那么什么也不要做。

## C++

```
// C++ program to merge k sorted arrays
// of size n each.
#include <bits/stdc++.h>
using namespace std;

// A pair of pairs, first element is going to
// store value, second element index of array
// and third element index in the array.
typedef pair<int, pair<int, int> > ppi;

// This function takes an array of arrays as an
// argument and all arrays are assumed to be
// sorted. It merges them together and prints
// the final sorted output.
vector<int> mergeKArrays(vector<vector<int> > arr)
{
    vector<int> output;

    // Create a min heap with k heap nodes. Every
    // heap node has first element of an array
    priority_queue<ppi, vector<ppi>, greater<ppi> > pq;

    for (int i = 0; i < arr.size(); i++)
        pq.push({ arr[i][0], { i, 0 } });

    // Now one by one get the minimum element
    // from min heap and replace it with next
    // element of its array
    while (pq.empty() == false) {
        ppi curr = pq.top();
        pq.pop();

        // i ==> Array Number
        // j ==> Index in the array number
        int i = curr.second.first;
        int j = curr.second.second;

        output.push_back(curr.first);

        // The next element belongs to same array as
        // current.
        if (j + 1 < arr[i].size())
            pq.push({ arr[i][j + 1], { i, j + 1 } });
    }

    return output;
}

// Driver program to test above functions
int main()
{
    // Change n at the top to change number
    // of elements in an array
    vector<vector<int> > arr{ { 2, 6, 12 },
                              { 1, 9 },
                              { 23, 34, 90, 2000 } };

    vector<int> output = mergeKArrays(arr);

    cout << "Merged array is " << endl;
    for (auto x : output)
        cout << x << " ";

    return 0;
}
```

## 计算机编程语言

```
# merge function merge two arrays
# of different or same length
# if n = max(n1, n2)
# time complexity of merge is (o(n log(n)))

from heapq import merge

# function for meging k arrays
def mergeK(arr, k):

    l = arr[0]
    for i in range(k-1):

        # when k = 0 it merge arr[1]
        # with arr[0] here in l arr[0]
        # is stored
        l = list(merge(l, arr[i + 1]))
    return l

# for printing array
def printArray(arr):
    print(*arr)

# driver code
arr =[[2, 6, 12 ],
    [ 1, 9 ],
    [23, 34, 90, 2000 ]]
k = 3

l = mergeK(arr, k)

printArray(l)
```

## C#

```
// C# program to merge k sorted arrays
// of size n each. 
using System;
using System.Collections.Generic;
class GFG
{

    // This function takes an array of arrays as an
    // argument and all arrays are assumed to be
    // sorted. It merges them together and prints
    // the final sorted output.
    static List<int> mergeKArrays(List<List<int>> arr)
    {
        List<int> output = new List<int>();

        // Create a min heap with k heap nodes. Every
        // heap node has first element of an array
        List<Tuple<int,Tuple<int,int>>> pq =
          new List<Tuple<int,Tuple<int,int>>>();

        for (int i = 0; i < arr.Count; i++)
            pq.Add(new Tuple<int,
                   Tuple<int,int>>(arr[i][0],
                                   new Tuple<int,int>(i, 0)));

        pq.Sort();

        // Now one by one get the minimum element
        // from min heap and replace it with next
        // element of its array
        while (pq.Count > 0) {
            Tuple<int,Tuple<int,int>> curr = pq[0];
            pq.RemoveAt(0);

            // i ==> Array Number
            // j ==> Index in the array number
            int i = curr.Item2.Item1;
            int j = curr.Item2.Item2;

            output.Add(curr.Item1);

            // The next element belongs to same array as
            // current.
            if (j + 1 < arr[i].Count)
            {
                pq.Add(new Tuple<int,Tuple<int,int>>(arr[i][j + 1],
                                                     new Tuple<int,int>(i, j + 1)));
                pq.Sort();
            }
        }
        return output;
    }   

  // Driver code
  static void Main()
  {

    // Change n at the top to change number
    // of elements in an array
    List<List<int>> arr = new List<List<int>>();
    arr.Add(new List<int>(new int[]{2, 6, 12}));
    arr.Add(new List<int>(new int[]{1, 9}));
    arr.Add(new List<int>(new int[]{23, 34, 90, 2000}));

    List<int> output = mergeKArrays(arr);

    Console.WriteLine("Merged array is ");
    foreach(int x in output)
        Console.Write(x + " ");
  }
}

// This code is contributed by divyeshrabadiya07.
```

**Output:** 

```
Merged array is 
1 2 6 9 12 23 34 90 2000
```