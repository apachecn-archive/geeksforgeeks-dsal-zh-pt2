# 最大化可以从数组

中选择的 K 个唯一元素的数量

> 原文:[https://www . geeksforgeeks . org/从数组中选择 k 个唯一元素的最大计数/](https://www.geeksforgeeks.org/maximize-count-of-k-unique-elements-that-can-be-chosen-from-array/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/arrays-in-c-cpp/) **arr[]** 和大小为 **M、**的查询数组 **Q[]** ，其中 **Q[i]** 定义必须从数组 **arr[]中选择的唯一元素的计数。**查找**每个查询可以选择的最大**元素数量的任务。

**示例:**

> **输入:** arr[ ] = {30，31，32，33，32，32，31，30，32}，Q[ ] = {1，3}
> **输出:** 4 9
> **解释:**
> 32 的频率为 4，30 为 3，31 为 2，33 为 1。
> 对于 **Q[0](=1)，**选择全部 32。因此计数= 4。
> 对于 **Q[1](=3)，**选择所有 32、30 和 31。因此计数= 4 + 3 + 2 = 9。
> 
> **输入:** arr[ ] = {22，35，22，22，35}，Q[ ] = {4，5，1}
> **输出:** 5 5 3

**方法:**这个问题可以通过在地图中存储每个元素的[频率来解决。按照以下步骤解决此问题:](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)数据结构比如说，**映射**和[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)**arr[]，**然后将数组中每个元素的**频率**存储在**映射中 **arr[]** 。**
*   将**映射**的所有值存储在一个数组中，比如说， **Cum_freq[]，**，然后[按降序排列数组 **Cum_freq[]** 。](https://www.geeksforgeeks.org/python-list-sort/)
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，Cum_freq[]的大小】**，并更新 **Cum_freq[i]中**Cum _ freq[I]+Cum _ freq[I-1]**的值。**
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，查询大小】**中迭代
    *   如果**查询【I】>= Cum _ freq[]的大小，**则打印 **N.**
    *   否则，打印**Cum _ freq[查询[I]–1]。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number
// of elements can pick for each query
void findMaxEleCanPick(int arr[], int queries[], int n, int m)
{
    map<int,int>mp;
    for(int i = 0; i < n; i++)
    {
         if(mp.find(arr[i]) != mp.end())
         {
             mp[arr[i]] += 1;
         }
         else
         mp[arr[i]] = 1;
    }
    vector<int>Cum_freq;

    // taking out frequencies from map
    for(auto i:mp)
    Cum_freq.push_back(i.second);

    // Sorting in decreasing order
    sort(Cum_freq.begin(),Cum_freq.end(),greater<int>());

    // Taking cumulative sum
    for(int i = 1; i < Cum_freq.size(); i++)
    Cum_freq[i] += Cum_freq[i - 1];

    // Performing each query
    for(int k = 0; k < m; k++)
    {
         if(queries[k] >= m)
         cout << n << " ";
         else
         cout<<Cum_freq[queries[k] - 1];
    }

}

// Driver Code
int main()
{
    // Given Input
    int arr[5] = {22, 35, 22, 22, 35};
    int queries[3] = { 4, 5, 1 };

    // Function Call
    findMaxEleCanPick(arr,queries,5,3);
    return 0;
}

// This code is contributed by dwivediyash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

//Function to find the maximum number
//of elements can pick for each query
import java.io.*;
import java.util.*;
import java.util.HashMap;
class GFG {
static void findMaxEleCanPick(Integer arr[],Integer queries[],Integer n,Integer m)
{
HashMap<Integer, Integer> mp = new HashMap<>();
    for(int i=0;i<n;i++)
    {
         if(mp.containsKey(arr[i]))
         {
            mp.put(arr[i],mp.get(arr[i]+1));
         }
         else
         mp.put(arr[i],1);
    }
     int Cum_freq[] = new int[n];
    //taking out frequencies from map
    int x=0;
    for(Map.Entry<Integer, Integer> i : mp.entrySet())
    Cum_freq[x++]=i.getValue();
    //Sorting in decreasing order
    Arrays.sort(arr, Collections.reverseOrder());
    //Taking cumulative sum
    for(Integer i=1;i<n;i++)
    Cum_freq[i]+=Cum_freq[i-1];
    //Performing each query
    for(Integer k=0;k<m;k++)
    {
         if(queries[k]>=m)
         System.out.println(n+" ");
         else
         System.out.println(queries[k]-1);
    }

}

// Driver Code

     public static void main(String[] args)
    {
        //Given Input
        Integer arr[]={22, 35, 22, 22, 35};
        Integer queries[]={ 4, 5, 1 };
        // Function Call
        findMaxEleCanPick(arr,queries,5,3);

    }
}
// java code added by dwivediyash
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find the maximum number
# of elements can pick for each query
def findMaxEleCanPick(arr, queries):

    # Total elements
    N = len(arr)

    # Using dictionary
    Map = dict()

    # Traversing the arr
    for ele in arr:

        # Updating the dictionary
        Map[ele] = 1 + Map.get(ele, 0)

    # Taking out frequencies from dictionary
    Cum_freq = list(Map.values())

    # Sorting in decreasing order
    Cum_freq.sort(reverse = True)

    # Taking cumulative sum
    for i in range(1, len(Cum_freq)):
        Cum_freq[i] += Cum_freq[i-1]

    # Performing each query
    for K in queries:
        if K >= len(Cum_freq):
            print(N, end = " ")
        else:
            print(Cum_freq[K-1], end = " ")

# Driver Code
if __name__ == '__main__':

    # Given Input
    arr = [ 22, 35, 22, 22, 35 ]
    queries = [ 4, 5, 1 ]

    # Function Call
    findMaxEleCanPick(arr, queries)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum number
// of elements can pick for each query
static void findMaxEleCanPick(int []arr, int []queries, int n, int m)
{
    Dictionary<int,int> mp = new Dictionary<int,int>();
    for(int i = 0; i < n; i++)
    {
         if(mp.ContainsKey(arr[i]))
         {
             mp[arr[i]] += 1;
         }
         else
         mp.Add(arr[i],1);
    }
    List<int> Cum_freq = new List<int>();

    // taking out frequencies from map
    foreach(KeyValuePair<int,int> entry in mp)
    Cum_freq.Add(entry.Value);

    // Sorting in decreasing order
    Cum_freq.Sort();
    Cum_freq.Reverse();

    // Taking cumulative sum
    for(int i = 1; i < Cum_freq.Count; i++)
    Cum_freq[i] += Cum_freq[i - 1];

    // Performing each query
    for(int k = 0; k < m; k++)
    {
         if(queries[k] >= m)
         Console.Write(n + " ");
         else
         Console.Write(Cum_freq[queries[k] - 1]);
    }

}

// Driver Code
public static void Main()
{

    // Given Input
    int []arr = {22, 35, 22, 22, 35};
    int []queries = { 4, 5, 1 };

    // Function Call
    findMaxEleCanPick(arr,queries,5,3);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the maximum number
// of elements can pick for each query
function findMaxEleCanPick(arr, queries)
{

    // Total elements
    let N = arr.length;

    // Using dictionary
    let map = new Map();

    // Traversing the arr
    for(let ele of arr)
    {

        // Updating the dictionary
        if (map.has(ele))
            map.set(ele, map.get(ele) + 1);
        else
            map.set(ele, 1)
    }

    // Taking out frequencies from dictionary
    let Cum_freq = [...map.values()];

    // Sorting in decreasing order
    Cum_freq.sort((a, b) => b - a);

    // Taking cumulative sum
    for(let i = 1; i < Cum_freq.length; i++)
    {
        Cum_freq[i] += Cum_freq[i - 1];
    }

    // Performing each query
    for(let K of queries)
    {
        if (K >= Cum_freq.length)
        {
            document.write(N + " ");
        }
        else
        {
            document.write(Cum_freq[K - 1]);
        }
    }
}

// Driver Code

// Given Input
arr = [ 22, 35, 22, 22, 35 ];
queries = [ 4, 5, 1 ];

// Function Call
findMaxEleCanPick(arr, queries);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output**

```
5 5 3 
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)