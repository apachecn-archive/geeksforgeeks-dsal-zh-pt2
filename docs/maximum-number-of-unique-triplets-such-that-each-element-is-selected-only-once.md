# 唯一三元组的最大数量，使得每个元素仅被选择一次

> 原文:[https://www . geesforgeks . org/唯一三元组的最大数量-这样每个元素只被选择一次/](https://www.geeksforgeeks.org/maximum-number-of-unique-triplets-such-that-each-element-is-selected-only-once/)

给定一个[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】的大小， **N** 。找到使用数组元素可以生成的三元组的最大数量，这样每个三元组中的所有元素都是不同的。打印可能的三胞胎的最大数量以及三胞胎列表。
**注意:**数组的每个元素只能属于 1 个三元组。
**示例:**

> **输入:** arr[] = {2，2，3，3，4，4，4，5}
> **输出:**
> 最大可能三元组数:2
> 2 3 4
> 3 4 5
> **解释:**
> 我们最多可以使用给定的数组形成 2 个三元组，这样每个三元组包含不同的元素。
> **输入:** arr[] = {1，2，3，4，5，6，7 }
> **输出:**
> 最大可能三元组数:2
> 5 6 7
> 2 3 4
> **解释:**
> 我们使用给定的数组最多可以形成 2 个三元组，这样每个三元组包含不同的元素。

**天真方法:**想法是运行三个嵌套循环来生成所有三元组，对于每个三元组，检查它们是否成对不同，并且还检查数组的每个元素是否恰好属于一个三元组。
***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*
**高效进场:**问题可以解决[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)继续取频率最大的三胞胎。以下是步骤:

*   将所有数字的频率存储在[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   创建一个最大[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) *和*来存储对，其中对中的第一个元素是某个元素的**频率**，对中的第二个元素是**元素**本身。
*   现在，从优先级队列中重复提取前 3 个元素，使用这 3 个元素创建三元组，将它们的频率减少 1，并再次使用大于 0 的频率在优先级队列中插入元素。

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds maximum number
// of triplets with different elements
void findTriplets(int ar[], int n)
{

    // Map M will store the frequency
    // of each element in the array
    unordered_map<int, int> mp;

    for (int x = 0; x < n; x++)
        mp[ar[x]]++;

    // Priority queue of pairs
    // {frequency, value}
    priority_queue<pair<int, int> > pq;

    for (auto& pa : mp)
        pq.push({ pa.second, pa.first });

    // ans will store possible triplets
    vector<array<int, 3> > ans;

    while (pq.size() >= 3) {

        // Extract top 3 elements
        pair<int, int> ar[3];
        for (int x = 0; x < 3; x++) {
            ar[x] = pq.top();
            pq.pop();
        }

        // Make a triplet
        ans.push_back({ ar[0].second,
                        ar[1].second,
                        ar[2].second });

        // Decrease frequency and push
        // back into priority queue if
        // non-zero frequency
        for (int x = 0; x < 3; x++) {
            ar[x].first--;
            if (ar[x].first)
                pq.push(ar[x]);
        }
    }

    // Print the triplets
    cout << "Maximum number of "
         << "possible triples: ";
    cout << ans.size() << endl;

    for (auto& pa : ans) {

        // Print the triplets
        for (int v : pa)
            cout << v << " ";
        cout << endl;
    }
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 2, 2, 3, 3, 4, 4, 4, 4, 5 };

    int n = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    findTriplets(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
import java.lang.*;
class GFG{

static class pair
{
  int first, second;
  pair(int first, int second)
  {
    this.first = first;
    this.second = second;
  }
}

// Function that finds maximum
// number of triplets with
// different elements
static void findTriplets(int arr[],
                         int n)
{
  // Map M will store the frequency
  // of each element in the array
  Map<Integer,
      Integer> mp = new HashMap<>();

  for (int x = 0; x < n; x++)
    mp.put(arr[x],
    mp.getOrDefault(arr[x], 0) + 1);

  // Priority queue of pairs
  // {frequency, value}
  PriorityQueue<pair> pq =
          new PriorityQueue<>((a, b) ->
                               a.first -
                               b.first);

  for (Map.Entry<Integer,
                 Integer> k : mp.entrySet())
    pq.add(new pair(k.getValue(),
                    k.getKey()));

  // ans will store possible
  // triplets
  ArrayList<List<Integer> > ans =
                 new ArrayList<>();

  while (pq.size() >= 3)
  {
    // Extract top 3 elements
    pair[] ar = new pair[3];
    for (int x = 0; x < 3; x++)
    {
      ar[x] = pq.peek();
      pq.poll();
    }

    // Make a triplet
    ans.add(Arrays.asList(ar[0].second,
                          ar[1].second,
                          ar[2].second));

    // Decrease frequency and push
    // back into priority queue if
    // non-zero frequency
    for (int x = 0; x < 3; x++)
    {
      ar[x].first--;
      if (ar[x].first != 0)
        pq.add(ar[x]);
    }
  }

  // Print the triplets
  System.out.println("Maximum number of " +
                     "possible triples: " +
                      ans.size());

  for (List<Integer> pa : ans)
  {
    // Print the triplets
    for (Integer v : pa)
      System.out.print(v + " ");

    System.out.println();
  }
}

// Driver function
public static void main(String[] args)
{
  // Given array arr[]
  int arr[] = {2, 2, 3, 3, 4,
               4, 4, 4, 5};

  int n = arr.length;

  // Function Call
  findTriplets(arr, n);
}
}

// This code is contributed by offbeat
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

  // Function that finds maximum number
  // of triplets with different elements
  static void findTriplets(int[] arr, int n)
  {

    // Map M will store the frequency
    // of each element in the array
    Dictionary<int, int> mp = new Dictionary<int, int>();
    for (int x = 0; x < n; x++)
    {
      if(mp.ContainsKey(arr[x]))
      {
        mp[arr[x]]++;
      }
      else
      {
        mp[arr[x]] = 1;
      }
    }

    // Priority queue of pairs
    // {frequency, value}
    List<Tuple<int, int> > pq = new List<Tuple<int,int>>();
    int cnt = 0;
    foreach(KeyValuePair<int, int> pa in mp)
      pq.Add(new Tuple<int,int>(pa.Value, pa.Key));

    // ans will store possible triplets
    List<List<int>> ans = new List<List<int>>();
    pq.Sort();
    pq.Reverse();
    while (pq.Count >= 3)
    {

      // Extract top 3 elements
      Tuple<int, int>[] ar = new Tuple<int,int>[3];
      for (int x = 0; x < 3; x++)
      {
        ar[x] = pq[0];
        pq.RemoveAt(0);
      }
      ans.Add(new List<int>());
      ans[cnt].Add(ar[0].Item2);
      ans[cnt].Add(ar[1].Item2);
      ans[cnt].Add(ar[2].Item2);

      // Decrease frequency and push
      // back into priority queue if
      // non-zero frequency
      for (int x = 0; x < 3; x++)
      {
        ar[x] = new Tuple<int,int>(ar[x].Item1 - 1, ar[x].Item2);
        if (ar[x].Item1 != 0)
        {
          pq.Add(ar[x]);
          pq.Sort();
          pq.Reverse();
        }
      }
      cnt++;
    }

    // Print the triplets
    Console.Write("Maximum number of possible triples: ");
    Console.WriteLine(ans.Count);
    foreach(List<int> pa in ans)
    {

      // Print the triplets
      foreach(int v in pa)
        Console.Write(v + " ");
      Console.WriteLine();
    }
  }

  // Driver code
  static void Main()
  {

    // Given array arr[]
    int[] arr = { 2, 2, 3, 3, 4, 4, 4, 4, 5 };

    int n = arr.Length;

    // Function Call
    findTriplets(arr, n);
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds maximum number
// of triplets with different elements
function findTriplets(ar, n)
{

    // Map M will store the frequency
    // of each element in the array
    var mp = new Map();

    for (var x = 0; x < n; x++)
    {
        if(mp.has(ar[x]))
          mp.set(ar[x], mp.get(ar[x])+1)
        else
            mp.set(ar[x],1)
    }

    // Priority queue of pairs
    // {frequency, value}
    var pq = [];

    for(var pa of mp)
        pq.push([pa[1], pa[0]]);

    // ans will store possible triplets
    var ans = [];
    pq.sort((a,b)=>{
          if(a[0]==b[0])
            return a[1]-b[1];
         return a[0]-b[0];
      });

    while (pq.length >= 3) {

        // Extract top 3 elements
        var ar = Array.from(Array(3), ()=>Array(2).fill(0));
        for (var x = 0; x < 3; x++) {
            ar[x] = pq[pq.length-1];
            pq.pop();
        }

        // Make a triplet
        ans.push([ar[0][1],
                        ar[1][1],
                        ar[2][1] ]);

        // Decrease frequency and push
        // back into priority queue if
        // non-zero frequency
        for (var x = 0; x < 3; x++) {
            ar[x][0]--;
            if (ar[x][0])
                pq.push(ar[x]);
        }
      pq.sort((a,b)=>{
          if(a[0]==b[0])
            return a[1]-b[1];
         return a[0]-b[0];
      });
    }

    // Print the triplets
    document.write("Maximum number of "
          + "possible triples: ");
    document.write(ans.length + "<br>");

    for (var pa of ans) {

        // Print the triplets
        for (var v of pa)
            document.write( v + " ");
        document.write("<br>");
    }
}

// Driver Code
// Given array arr[]
var arr = [2, 2, 3, 3, 4, 4, 4, 4, 5];
var n = arr.length;

// Function Call
findTriplets(arr, n);

// This code is contributed by noob20000
</script>
```

**Output:** 

```
Maximum number of possible triples: 2
4 3 2 
4 5 3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*