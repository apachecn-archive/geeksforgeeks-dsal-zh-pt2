# 子阵列范围内最大出现元素(模式查询)

> 原文:[https://www . geesforgeks . org/最大出现元素子数组范围模式查询/](https://www.geeksforgeeks.org/maximum-occurring-element-in-a-subarray-range-mode-queries/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，以及一个由 **M** 对组成的数组**Q【】**，其中一对代表形式为 **{L，R}，**的查询，任务是为每个查询找到范围**【L，R】**中最大出现的元素及其频率。如果有多个最大频率的元素，则打印其中的最大元素。

**示例:**

> **输入:** arr[] = {5，7，5，5，2，7，3，2，5，2}，Q[] = {{0，9}，{3，6}，{4，8}，{1，5 }
> 输出: 5 发生 4 次
> 3 发生 1 次
> 2 发生 2 次
> 7 发生 2 次
> **解释:**
> 查询执行如下:
> 
> 1.  查询(0，9):范围内的子阵列为{5，7，5，5，2，7，3，2，5，2}。元素 5、7、2 和 3 分别出现 4、2、3 和 1 次。因此，打印 5。
> 2.  查询(3，6):范围内的子阵列为{5，2，7，3}。每个元素都出现一次。所以打印元素 7。
> 3.  查询(4，8):范围内的子阵列为{2，7，3，2，5}。元素 2 出现两次，其余的都出现一次。因此，打印 2。
> 4.  查询(1，5):范围内的子阵列为{7，5，5，2，7，3}。元素 7 和 5 出现两次，其余元素出现一次。因此打印 7。

**朴素方法:**对于每个查询，迭代给定的范围[L，R]保持更新辅助数据结构中每个元素的频率(例如。[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/))。处理完当前查询的**整个范围**后，[遍历地图](https://www.geeksforgeeks.org/traversing-a-map-or-unordered_map-in-cpp-stl/)中的所有元素，找到**最大频率**的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the elements having
// maximum frequency for the query range
void getMaxOccuringElement(int arr[], int N, int M,
                           pair<int, int> Q[])
{
    // Iterate over all the queries
    for (int i = 0; i < M; ++i) {

        // Stores the frequency of each element
        // in the current query range [l, r]
        map<int, int> freq;

        int l = Q[i].first, r = Q[i].second;

        for (int j = l; j <= r; ++j)
            ++freq[arr[j]];

        int maxFreqElement = -1;
        int maxFreq = -1;

        // Iterate over the map and find the
        // element having maximum frequency
        for (auto it : freq) {
            if (it.second >= maxFreq) {
                maxFreqElement = it.first;
                maxFreq = it.second;
            }
        }

        // Print the answer for current query
        cout << maxFreqElement << " Occurs " << maxFreq
             << " times" << endl;
    }
}

// Driver Code
int main()
{

    int arr[] = { 5, 7, 5, 5, 2, 7, 3, 2, 5, 2 };
    pair<int, int> Q[]
        = { { 0, 9 }, { 3, 6 }, { 4, 8 }, { 1, 5 } };

    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(Q) / sizeof(Q[0]);

    getMaxOccuringElement(arr, N, M, Q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

class GFG{

    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Function to find the elements having
// maximum frequency for the query range
static void getMaxOccuringElement(int arr[], int N, int M,
                           pair Q[])
{
    // Iterate over all the queries
    for (int i = 0; i < M; ++i) {

        // Stores the frequency of each element
        // in the current query range [l, r]
        HashMap<Integer,Integer> freq = new HashMap<Integer,Integer>();

        int l = Q[i].first, r = Q[i].second;

        for (int j = l; j <= r; ++j) {
            if(freq.containsKey(arr[j]))
            freq.put(arr[j], freq.get(arr[j])+1);
            else
                freq.put(arr[j], 1);

        }

        int maxFreqElement = -1;
        int maxFreq = -1;

        // Iterate over the map and find the
        // element having maximum frequency
        for (Map.Entry<Integer,Integer> it : freq.entrySet()) {
            if (it.getValue() >= maxFreq) {
                maxFreqElement = it.getKey();
                maxFreq = it.getValue();
            }
        }

        // Print the answer for current query
        System.out.print(maxFreqElement+ " Occurs " +  maxFreq
            + " times" +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 5, 7, 5, 5, 2, 7, 3, 2, 5, 2 };
    pair Q[]
        = { new pair( 0, 9 ), new pair( 3, 6 ), new pair( 4, 8 ), new pair( 1, 5 ) };

    int N = arr.length;
    int M = Q.length;

    getMaxOccuringElement(arr, N, M, Q);

}
}

// This code contributed by Princi Singh
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

    class pair
    {
        public int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }

// Function to find the elements having
// maximum frequency for the query range
static void getMaxOccuringElement(int []arr, int N, int M,
                           pair []Q)
{

    // Iterate over all the queries
    for (int i = 0; i < M; ++i) {

        // Stores the frequency of each element
        // in the current query range [l, r]
        Dictionary<int,int> freq = new Dictionary<int,int>();

        int l = Q[i].first, r = Q[i].second;

        for (int j = l; j <= r; ++j) {
            if(freq.ContainsKey(arr[j]))
            freq[arr[j]] = freq[arr[j]]+1;
            else
                freq.Add(arr[j], 1);

        }

        int maxFreqElement = -1;
        int maxFreq = -1;

        // Iterate over the map and find the
        // element having maximum frequency
        foreach (KeyValuePair<int,int> it in freq) {
            if (it.Value >= maxFreq) {
                maxFreqElement = it.Key;
                maxFreq = it.Value;
            }
        }

        // Print the answer for current query
        Console.Write(maxFreqElement+ " Occurs " +  maxFreq
            + " times" +"\n");
    }
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 5, 7, 5, 5, 2, 7, 3, 2, 5, 2 };
    pair []Q
        = { new pair( 0, 9 ), new pair( 3, 6 ), new pair( 4, 8 ), new pair( 1, 5 ) };

    int N = arr.Length;
    int M = Q.Length;

    getMaxOccuringElement(arr, N, M, Q);

}
}

// This code is contributed by 29AjayKumar
```

**Output**

```
5 Occurs 4 times
7 Occurs 1 times
2 Occurs 2 times
7 Occurs 2 times
```

***时间复杂度:** O(M * N)*
***辅助空间:** O(N)*

**高效方法:**上述方法可以通过 [**莫氏算法**](https://www.geeksforgeeks.org/mos-algorithm-query-square-root-decomposition-set-1-introduction/) 基于 sqrt 分解的概念进行优化。按照以下步骤解决问题:

*   查询按照其左索引所在的块的非递减顺序排序。如果两个或多个查询的左索引在同一个块中，则根据它们的**右索引**对它们进行排序。
*   基本上，**计算所有查询的答案**，这些查询的**左索引**位于块 0，然后是块 1，依此类推，直到最后一个块。
*   维护一个[地图数据结构](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) ( **num_freq** )，存储当前查询范围内每个元素的**出现次数。**
*   另外，维护一个[集合数据结构](https://www.geeksforgeeks.org/set-in-cpp-stl/) ( **freq_num** )，其**每个元素是一对**(该对的第一个元素代表一个元素的出现计数，该对的第二个元素代表元素本身)。
*   [集合](https://www.geeksforgeeks.org/set-in-cpp-stl/) ( **freq_num** ) **以非递减顺序**存储元素。集合中元素的**排序基于配对的第一项**，代表**频率**。
*   因此，当**回答查询**(即具有最大频率的元素)时，可以在 **O(1)** 中完成。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int BLOCK_SIZE;

// Structure to represent a query range
// and its index
struct query {
    int l, r, idx;
};

// Custom comparator
bool comparator(query a, query b)
{
    if ((a.l / BLOCK_SIZE) != (b.l / BLOCK_SIZE))
        return (a.l / BLOCK_SIZE) < (b.l / BLOCK_SIZE);

    return ((a.l / BLOCK_SIZE) & 1) ? (a.r < b.r)
                                    : (a.r > b.r);
}

// Function to add elements to the current range
void expand(int idx, int* arr, map<int, int>& numFreq,
            set<pair<int, int> >& freqNum)
{
    // Remove current element from the set
    freqNum.erase({ numFreq[arr[idx]], arr[idx] });

    // Increment current element count in the
    // map
    ++numFreq[arr[idx]];

    // Insert current element into the set
    freqNum.insert({ numFreq[arr[idx]], arr[idx] });
}

// Function to remove elements from the current range
void shrink(int idx, int* arr, map<int, int>& numFreq,
            set<pair<int, int> >& freqNum)
{
    // Remove current element from the set
    freqNum.erase({ numFreq[arr[idx]], arr[idx] });

    // Decrement current element count in the
    // map
    --numFreq[arr[idx]];

    // Insert current element into the set
    freqNum.insert({ numFreq[arr[idx]], arr[idx] });
}

// Function for Mo's algorithm
pair<int, int>
sqrtDecomposition(int& L, int& R, int l, int r, int* arr,
                  set<pair<int, int> >& freqNum,
                  map<int, int>& numFreq)
{
    // Iterate until L is greater than l
    while (L > l) {
        --L;
        expand(L, arr, numFreq, freqNum);
    }

    // Iterate until R is less than r
    while (R < r) {
        ++R;
        expand(R, arr, numFreq, freqNum);
    }

    // Iterate until L is less than l
    while (L < l) {
        shrink(L, arr, numFreq, freqNum);
        ++L;
    }

    // Iterate until R is greater than r
    while (R > r) {
        shrink(R, arr, numFreq, freqNum);
        --R;
    }

    // Stores the answer for current query
    pair<int, int> last = *prev(freqNum.end());

    // Return the answer
    return last;
}

// Function to find the element having maximum
// frequency and its frequency for all the queries
void getMaxOccuringElement(int arr[], int N, int M,
                           pair<int, int> Q[])
{

    // Compute each block size
    BLOCK_SIZE = (int)sqrt(N + .0) + 1;

    // Stores the queries
    query queries[M];

    for (int i = 0; i < M; ++i) {
        queries[i].l = Q[i].first;
        queries[i].r = Q[i].second;
        queries[i].idx = i;
    }

    // Sort all the queries
    sort(queries, queries + M, comparator);

    // Initiali ranges of Mos
    int L = 0, R = -1;

    // Stores the answer
    pair<int, int> ans[M];

    set<pair<int, int> > freqNum;
    map<int, int> numFreq;

    // Traverse the query array
    for (int i = 0; i < M; ++i) {

        int l = queries[i].l;
        int r = queries[i].r;

        // Stores the answer for current
        // query
        ans[queries[i].idx] = sqrtDecomposition(
            L, R, l, r, arr, freqNum, numFreq);
    }

    // Print the answer
    for (int i = 0; i < M; ++i) {
        cout << ans[i].second << " Occurs " << ans[i].first
             << " times" << endl;
    }
}

// Driver Code
int main()
{
    int arr[] = { 5, 7, 5, 5, 2, 7, 3, 2, 5, 2 };
    pair<int, int> Q[]
        = { { 0, 9 }, { 3, 6 }, { 4, 8 }, { 1, 5 } };

    int N = sizeof(arr) / sizeof(arr[0]);
    int M = sizeof(Q) / sizeof(Q[0]);

    getMaxOccuringElement(arr, N, M, Q);

    return 0;
}
```

**Output**

```
5 Occurs 4 times
7 Occurs 1 times
2 Occurs 2 times
7 Occurs 2 times
```

***时间复杂度:**O((N+M)* log(N)* sqrt(N))*
***辅助空间:** O(N)*