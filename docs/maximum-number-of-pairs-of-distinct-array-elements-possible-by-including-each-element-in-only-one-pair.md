# 通过将每个元素仅包含在一对中，可能的不同阵列元素对的最大数量

> 原文:[https://www . geeksforgeeks . org/通过仅包含一对中的每个元素来尽可能增加不同数组元素的最大对数/](https://www.geeksforgeeks.org/maximum-number-of-pairs-of-distinct-array-elements-possible-by-including-each-element-in-only-one-pair/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找到数组元素对的最大数量，使得每对元素都有不同的元素，并且每个数组元素只能存在于一对中

**示例:**

> **输入:** arr[] = {4，5，4，5，4}
> **输出:** 2
> **解释:**
> 给定数组可以有 2 对形式，即{{4，5}，{4，5}}。因此，打印 2。
> 
> **输入:** arr[] = {2，3，2，1，3，1 }
> T3】输出: 3

**方法:**给定的问题可以通过[存储数组元素的频率](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)并使用两个最高频率数生成对来解决。这个想法可以使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)来实现。按照以下步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，比如说 **M** ，存储数组元素的频率。
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如说 **PQ** ，用于实现 [MaxHeap](https://www.geeksforgeeks.org/convert-min-heap-to-max-heap/) ，并将所有频率插入其中。
*   初始化一个变量，比如说**计数**为 **0** ，它存储结果对的最大计数。
*   遍历优先级队列 **PQ** 直到其大小大于 **1** ，并执行以下步骤:
    *   [从**PQ**T3 中弹出前两个元素。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
    *   将弹出元素的值减少 **1** ，并将两个元素再次插入 **PQ** 中。
    *   将**计数**的值增加 **1** 。
*   完成以上步骤后，打印数值**计数**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the maximum number
// of pairs having different element
// from the given array
int maximumPairs(int a[], int n)
{
    // Stores the frequency of
    // array element
    map<int, int> freq;

    // Stores maximum count of pairs
    int count = 0;

    // Increasing the frequency of
    // every element
    for (int i = 0; i < n; ++i)
        freq[a[i]]++;

    // Stores the frequencies of array
    // element from highest to lowest
    priority_queue<int> pq;

    for (auto itr = freq.begin();
         itr != freq.end();
         itr++) {

        // Pushing the frequencies to
        // the priority queue
        pq.push(itr->second);
    }

    // Iterate until size of PQ > 1
    while (pq.size() > 1) {

        // Stores the top two element
        int freq1 = pq.top();
        pq.pop();

        int freq2 = pq.top();
        pq.pop();

        // Form the pair between the
        // top two pairs
        count++;

        // Decrement the frequencies
        freq1--;
        freq2--;

        // Insert updated frequencies
        // if it is greater than 0
        if (freq1 > 0)
            pq.push(freq1);

        if (freq2 > 0)
            pq.push(freq2);
    }

    // Return the total count of
    // resultant pairs
    return count;
}

// Driver Code
int main()
{
    int arr[] = { 4, 2, 4, 1, 4, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << maximumPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.io.*;
import java.util.*;
class GFG {
    public static int maximumPairs(int[] a, int n)
    {

        // Stores the frequency of
        // array element
        HashMap<Integer, Integer> freq
            = new HashMap<Integer, Integer>();

        // Stores maximum count of pairs
        int count = 0;

        // Increasing the frequency of
        // every element
        for (int i = 0; i < n; i++) {
            int c = a[i];
            if (freq.containsKey(c)) {
                freq.put(c, freq.get(c) + 1);
            }
            else {

                freq.put(c, 1);
            }
        }

        // Stores the frequencies of array
        // element from highest to lowest
        PriorityQueue<Integer> pq
            = new PriorityQueue<Integer>();

        for (int i = 0;i<n;i++) {
            // Pushing the frequencies to
            // the priority queue
          if(freq.containsKey(a[i])){
            pq.add(freq.get(a[i]));
            freq.remove(a[i]);
          }
        }

        // Iterate until size of PQ > 1
        while (pq.size() > 1) {

            // Stores the top two element
            int freq1 = pq.poll();

            int freq2 = pq.poll();

            // Form the pair between the
            // top two pairs
            count++;

            // Decrement the frequencies
            freq1--;
            freq2--;

            // Insert updated frequencies
            // if it is greater than 0
            if (freq1 > 0)
                pq.add(freq1);

            if (freq2 > 0)
                pq.add(freq2);
        }

        // Return the total count of
        // resultant pairs
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int arr[] = { 4, 2, 4, 1, 4, 3 };
        int N = 6;
        System.out.println(maximumPairs(arr, N));
    }
}

// This code is contributed by maddler.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to count the maximum number
# of pairs having different element
# from the given array
def maximumPairs(a, n):

    # Stores the frequency of
    # array element
    freq = {}

    # Stores maximum count of pairs
    count = 0

    # Increasing the frequency of
    # every element
    for i in range(n):
        if a[i] in freq:
            freq[a[i]] += 1
        else:
            freq[a[i]] = 1

    # Stores the frequencies of array
    # element from highest to lowest
    pq = []

    for key,value in freq.items():
        # Pushing the frequencies to
        # the priority queue
        pq.append(value)

    pq.sort()

    # Iterate until size of PQ > 1
    while (len(pq) > 1):
        # Stores the top two element
        freq1 = pq[len(pq)-1]
        pq = pq[:-1]

        freq2 = pq[len(pq)-1]
        pq = pq[:-1]

        # Form the pair between the
        # top two pairs
        count += 1

        # Decrement the frequencies
        freq1 -= 1
        freq2 -= 1

        # Insert updated frequencies
        # if it is greater than 0
        if (freq1 > 0):
            pq.append(freq1)

        if (freq2 > 0):
            pq.append(freq2)

        pq.sort()

    # Return the total count of
    # resultant pairs
    return count

# Driver Code
if __name__ == '__main__':
    arr = [4, 2, 4, 1, 4, 3]
    N = len(arr)
    print(maximumPairs(arr, N))

    # This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the maximum number
// of pairs having different element
// from the given array
function maximumPairs(a, n)
{

    // Stores the frequency of
    // array element
    var freq = new Map();

    // Stores maximum count of pairs
    var count = 0;

    // Increasing the frequency of
    // every element
    for (var i = 0; i < n; ++i)
    {
        if(freq.has(a[i]))
            freq.set(a[i], freq.get(a[i])+1)
        else
            freq.set(a[i],1)
    }

    // Stores the frequencies of array
    // element from highest to lowest
    var pq = [...freq.values()];
    pq.sort((a,b)=>a-b);

    // Iterate until size of PQ > 1
    while (pq.length > 1) {

        // Stores the top two element
        var freq1 = pq[pq.length-1];
        pq.pop();

        var freq2 = pq[pq.length-1];
        pq.pop();

        // Form the pair between the
        // top two pairs
        count++;

        // Decrement the frequencies
        freq1--;
        freq2--;

        // Insert updated frequencies
        // if it is greater than 0
        if (freq1 > 0)
            pq.push(freq1);

        if (freq2 > 0)
            pq.push(freq2);

        pq.sort((a,b)=>a-b);
    }

    // Return the total count of
    // resultant pairs
    return count;
}

// Driver Code
var arr = [4, 2, 4, 1, 4, 3 ];
var N = arr.length;
document.write( maximumPairs(arr, N));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
3
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*

**另一种方法:**

这个问题也可以通过只存储数组中每个元素的频率来解决。之后，我们需要找到给定数组中某个元素的最大频率。确认一对不能有相同的值。假设我们有 arr[]={1，1，1，1，2}元素，那么将形成一对，因为数组中有两个不同的值。因此，如果剩下具有相同值的元素，就不能形成对。

下面是实现:

## C++

```
#include <bits/stdc++.h>
using namespace std;
int main()
{
    int arr[] = { 4, 2, 4, 1, 4, 3 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int maxi = 0, remain, ans;
    // stores the frequency array
    map<int, int> freq;
    for (int i = 0; i < n; i++) {
        freq[arr[i]]++;
    }
    for (auto it : freq) {
        // maxi stores the maximum
        // frequency of an element
        maxi = max(maxi, it.second);
    }
    // it stores the sum of all the frequency
    // other than the element which has maximum frequency
    remain = n - maxi;
    if (maxi >= remain) {
        // there will be always zero
        // or more element
        // which will not participate in making pairs
        ans = remain;
    }
    else {
        // if n is odd then except one element
        // we can always form pair for every element
        // if n is even then all the elements can form pair
        ans = n / 2;
    }
    cout << ans;
    freq.clear();
    return 0;
}
```

## C#

```
using System;
using System.Collections;
using System.Collections.Generic;

class GFG
{
public static void Main()
{
    int []arr = { 4, 2, 4, 1, 4, 3 };
    int n = arr.Length;
    int maxi = 0, remain, ans;

    // stores the frequency array
    Dictionary<int, int> freq =
          new Dictionary<int, int>();

    for (int i = 0; i < n; i++) {
        if (freq.ContainsKey(arr[i]))
        {
            freq[arr[i]] = freq[arr[i]] + 1;
        }
        else
        {
            freq.Add(arr[i], 1);
        }
    }

    foreach (KeyValuePair<int, int> it in freq)
    {

        // maxi stores the maximum
        // frequency of an element
        maxi = Math.Max(maxi, it.Value);
    }

    // it stores the sum of all the frequency
    // other than the element which has maximum frequency
    remain = n - maxi;
    if (maxi >= remain)
    {

        // there will be always zero
        // or more element
        // which will not participate in making pairs
        ans = remain;
    }
    else
    {

        // if n is odd then except one element
        // we can always form pair for every element
        // if n is even then all the elements can form pair
        ans = n / 2;
    }
    Console.Write(ans);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
let arr = [4, 2, 4, 1, 4, 3];
let n = arr.length;
let maxi = 0,
  remain,
  ans;

// stores the frequency array
let freq = new Map();
for (let i = 0; i < n; i++) {
  if (freq.has(arr[i])) {
    freq.set(arr[i], freq.get(arr[i]) + 1);
  } else {
    freq.set(arr[i], 1);
  }
}

for (let it of freq)
{

  // maxi stores the maximum
  // frequency of an element
  maxi = Math.max(maxi, it[1]);
}

// it stores the sum of all the frequency
// other than the element which has maximum frequency
remain = n - maxi;
if (maxi >= remain)
{

  // there will be always zero
  // or more element
  // which will not participate in making pairs
  ans = remain;
}
else
{

  // if n is odd then except one element
  // we can always form pair for every element
  // if n is even then all the elements can form pair
  ans = Math.floor(n / 2);
}
document.write(ans);
freq.clear();

// This code is contributed by gfgking.
</script>
```

**Output**

```
3
```

**这种方法的时间复杂度**是 O(N)，因为我们遍历所有元素来形成频率阵列。
T3【辅助空间】T4 是 O(N)。