# 当允许混洗时，Q 查询的给定数组范围内的最大值和

> 原文:[https://www . geeksforgeeks . org/给定 q 查询数组范围内的最大值总和/允许洗牌的时间/](https://www.geeksforgeeks.org/maximum-sum-of-values-in-a-given-range-of-an-array-for-q-queries-when-shuffling-is-allowed/)

给定一个数组 **arr[]** 和 **K** 子数组的形式(L <sub>i</sub> ，R <sub>i</sub> ，任务是找到最大可能值

![\sum_{i = 1}^{K} arr[L_i:R_i]             ](img/387574918bc2caf556420b03a03dccd0.png "Rendered by QuickLaTeX.com")

。在计算该值以获得最大值之前，允许对数组进行洗牌。

**示例:**

> **输入:** arr[] = {1，1，2，2，4}，查询= {{1，2}，{2，4}，{1，3}，{5，5}，{3，5}}
> **输出:** 26
> **解释:**
> 混洗数组获取最大和–{ 2，4，2，1，1}
> 斯巴瑞 Sum = arr[1:2]+arr[2:4]+arr[1:1]
> 
> **输入:** arr[] = {4，1，2，1，9，2}，查询= {{1，2}，{1，3}，{1，4}，{3，4}}
> **输出:** 49
> **解释:**
> 混洗数组获取最大和–{ 2，4，9，2，1，1 }
> subarr Sum = arr[1:2]+arr[1:3]+arr[1:4]

**天真方法:**一个简单的解决方法是计算给定数组所有可能排列的最大和，并检查哪个序列给了我们最大和。

**有效方法:**想法是使用[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)找出所有子阵列上的索引频率。我们可以这样做:

```
//Initialize an array 
prefSum[n] = {0, 0, ...0}
for each Li, Ri:
    prefSum[Li]++
    prefSum[Ri+1]--

// Find Prefix sum
for i=1 to N:
    prefSum[i] += prefSum[i-1]

// prefSum contains frequency of 
// each index over all subarrays
```

最后，贪婪地选择频率最高的索引，将数组中最大的元素放在该索引处。这样我们将得到最大可能的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum sum of K subarrays
// when shuffling is allowed

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// maximum sum of all subarrays
int maximumSubarraySum(
    int a[], int n,
    vector<pair<int, int> >& subarrays)
{
    // Initialize maxsum
    // and prefixArray
    int i, maxsum = 0;
    int prefixArray[n] = { 0 };

    // Find the frequency
    // using prefix Array
    for (i = 0; i < subarrays.size(); ++i) {
        prefixArray[subarrays[i].first - 1]++;
        prefixArray[subarrays[i].second]--;
    }

    // Perform prefix sum
    for (i = 1; i < n; i++) {
        prefixArray[i] += prefixArray[i - 1];
    }

    // Sort both arrays to get a greedy result
    sort(prefixArray,
        prefixArray + n,
        greater<int>());
    sort(a, a + n, greater<int>());

    // Finally multiply largest frequency with
    // largest array element.
    for (i = 0; i < n; i++)
        maxsum += a[i] * prefixArray[i];

    // Return the answer
    return maxsum;
}

// Driver Code
int main()
{
    int n = 6;

    // Initial Array
    int a[] = { 4, 1, 2, 1, 9, 2 };

    // Subarrays
    vector<pair<int, int> > subarrays;
    subarrays.push_back({ 1, 2 });
    subarrays.push_back({ 1, 3 });
    subarrays.push_back({ 1, 4 });
    subarrays.push_back({ 3, 4 });

    // Function Call
    cout << maximumSubarraySum(a, n,
                            subarrays);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum sum of K subarrays
// when shuffling is allowed
import java.util.*;
import java.lang.*;

class GFG{

// Function to find the
// maximum sum of all subarrays
static int maximumSubarraySum(int a[], int n,
           ArrayList<List<Integer>> subarrays)
{

    // Initialize maxsum
    // and prefixArray
    int i, maxsum = 0;
    int[] prefixArray = new int[n];

    // Find the frequency
    // using prefix Array
    for(i = 0; i < subarrays.size(); ++i)
    {
        prefixArray[subarrays.get(i).get(0) - 1]++;
        prefixArray[subarrays.get(i).get(1)]--;
    }

    // Perform prefix sum
    for(i = 1; i < n; i++)
    {
        prefixArray[i] += prefixArray[i - 1];
    }

    // Sort both arrays to get a
    // greedy result
    Arrays.sort(prefixArray);
    Arrays.sort(a);

    // Finally multiply largest
    // frequency with largest
    // array element.
    for(i = 0; i < n; i++)
        maxsum += a[i] * prefixArray[i];

    // Return the answer
    return maxsum;
}

// Driver code
public static void main (String[] args)
{
    int n = 6;

    // Initial Array
    int a[] = { 4, 1, 2, 1, 9, 2 };

    // Subarrays
    ArrayList<List<Integer>> subarrays = new ArrayList<>();
    subarrays.add(Arrays.asList(1, 2));
    subarrays.add(Arrays.asList(1, 3));
    subarrays.add(Arrays.asList(1, 4));
    subarrays.add(Arrays.asList(3, 4));

    // Function call
    System.out.println(maximumSubarraySum(a, n,
                                          subarrays));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum sum of K subarrays
# when shuffling is allowed

# Function to find the
# maximum sum of all subarrays
def maximumSubarraySum(a, n, subarrays):

    # Initialize maxsum
    # and prefixArray
    maxsum = 0
    prefixArray = [0] * n

    # Find the frequency
    # using prefix Array
    for i in range(len(subarrays)):
        prefixArray[subarrays[i][0] - 1] += 1
        prefixArray[subarrays[i][1]] -= 1

    # Perform prefix sum
    for i in range(1, n):
        prefixArray[i] += prefixArray[i - 1]

    # Sort both arrays to get a greedy result
    prefixArray.sort()
    prefixArray.reverse()
    a.sort()
    a.reverse()

    # Finally multiply largest frequency with
    # largest array element.
    for i in range(n):
        maxsum += a[i] * prefixArray[i]

    # Return the answer
    return maxsum

# Driver Code
n = 6

# Initial Array
a = [ 4, 1, 2, 1, 9, 2 ]

# Subarrays
subarrays = [ [ 1, 2 ], [ 1, 3 ],
              [ 1, 4 ], [ 3, 4 ] ]

# Function Call
print(maximumSubarraySum(a, n, subarrays))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation to find the
// maximum sum of K subarrays
// when shuffling is allowed
using System;
using System.Collections.Generic;

class GFG{

// Function to find the
// maximum sum of all subarrays
static int maximumSubarraySum(int[] a, int n,
                    List<List<int>> subarrays)
{

    // Initialize maxsum
    // and prefixArray
    int i, maxsum = 0;
    int[] prefixArray = new int[n];

    // Find the frequency
    // using prefix Array
    for(i = 0; i < subarrays.Count; ++i)
    {
        prefixArray[subarrays[i][0] - 1]++;
        prefixArray[subarrays[i][1]]--;
    }

    // Perform prefix sum
    for(i = 1; i < n; i++)
    {
        prefixArray[i] += prefixArray[i - 1];
    }

    // Sort both arrays to get a
    // greedy result
    Array.Sort(prefixArray);
    Array.Sort(a);

    // Finally multiply largest
    // frequency with largest
    // array element.
    for(i = 0; i < n; i++)
        maxsum += a[i] * prefixArray[i];

    // Return the answer
    return maxsum;
}

// Driver Code
static void Main()
{
    int n = 6;

    // Initial Array
    int[] a = { 4, 1, 2, 1, 9, 2 };

    // Subarrays
    List<List<int>> subarrays = new List<List<int>>();
    subarrays.Add(new List<int>{ 1, 2 });
    subarrays.Add(new List<int>{ 1, 3 });
    subarrays.Add(new List<int>{ 1, 4 });
    subarrays.Add(new List<int>{ 3, 4 });

    // Function call
    Console.WriteLine(maximumSubarraySum(a, n,subarrays));
}
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

    // Javascript implementation to find the
    // maximum sum of K subarrays
    // when shuffling is allowed

    // Function to find the
    // maximum sum of all subarrays
    function maximumSubarraySum(a, n, subarrays)
    {

        // Initialize maxsum
        // and prefixArray
        let i, maxsum = 0;
        let prefixArray = new Array(n);
        prefixArray.fill(0);

        // Find the frequency
        // using prefix Array
        for(i = 0; i < subarrays.length; ++i)
        {
            prefixArray[subarrays[i][0] - 1]++;
            prefixArray[subarrays[i][1]]--;
        }

        // Perform prefix sum
        for(i = 1; i < n; i++)
        {
            prefixArray[i] += prefixArray[i - 1];
        }

        // Sort both arrays to get a
        // greedy result
        prefixArray.sort();
        a.sort();

        // Finally multiply largest
        // frequency with largest
        // array element.
        for(i = 0; i < n; i++)
            maxsum += a[i] * prefixArray[i];

        // Return the answer
        return maxsum;
    }

    let n = 6;

    // Initial Array
    let a = [ 4, 1, 2, 1, 9, 2 ];

    // Subarrays
    let subarrays = [];
    subarrays.push([ 1, 2 ]);
    subarrays.push([ 1, 3 ]);
    subarrays.push([ 1, 4 ]);
    subarrays.push([ 3, 4 ]);

    // Function call
    document.write(maximumSubarraySum(a, n,subarrays));

</script>
```

**Output:** 

```
49
```