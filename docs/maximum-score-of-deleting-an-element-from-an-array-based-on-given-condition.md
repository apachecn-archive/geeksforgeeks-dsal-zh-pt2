# 根据给定条件从数组中删除元素的最大得分

> 原文:[https://www . geesforgeks . org/基于给定条件从数组中删除元素的最大分数/](https://www.geeksforgeeks.org/maximum-score-of-deleting-an-element-from-an-array-based-on-given-condition/)

给定一个数组 **arr[]** ，任务是找到删除一个元素的最大得分，其中数组的每个元素都可以用该元素的得分来删除，但约束是如果我们删除 **arr[i]** ，那么 **arr[i] + 1** 和**arr[I]–1**就会被自动删除，得分为 0。
**示例:**

> **输入:**arr[]=【7，2，1，8，3，3，6，6】
> **输出:** 27
> **解释:****step 0:**【arr[]】 **分数:** 6
> **步骤 3:**【arr[]7 = 8**6**6，**分数:** 7
> **步骤 4:**arr[]8

**方法:**思路是用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决这个问题。对这个问题的关键观察是，对于从数组中移除任何元素，元素和值本身的出现是重要的因素。
我们举个例子来理解一下，如果顺序是 4 4 5。然后，我们有两个选择，从 4 到 5。现在，选择 4，他的分数将是 4*2 = 8。另一方面，如果我们选择 5，他的分数将是 5*1 = 5。显然，最高分是 8 分。
因此，对于上述序列 4 4 5，freq[4] = 2，freq[5] = 1。
最后，要找到最优分数，首先很容易把问题分解成更小的问题。在这种情况下，我们将序列分成更小的序列，并为其找到最优解。对于只包含 0 的数字序列，答案是 0。类似地，如果一个序列只包含数字 0 和 1，那么解将是 count[1]*1。
**重复关系:**

> dp[i] = max（dp[i – 1]， dp[i – 2] + i*freq[i]）

基本上，我们有两种情况，一种是选择一个**I<sup>th</sup>T3】元素，另一种是不选择一个**I<sup>th</sup>T7】元素。****

**情况 1:** 如果我们选择第 ith 个元素，直到第 ith 个元素的最大得分将是 dp[i-2] + i*freq[i](选择第 ith 个元素意味着删除第(i-1)个元素)
情况 2: 如果我们不选择第 ith 个元素，直到第 ith 个元素的最大得分将是 dp[i-1]
现在，由于我们必须最大化得分，我们将取两者的最大值。
以下是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum score of the deleting a
// element from an array

#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum
// score of the deleting an element
// from an array
int findMaximumScore(vector<int> a, int n)
{

    // Creating a map to keep
    // the frequency of numbers
    unordered_map<int, int> freq;

    // Loop to iterate over the
    // elements of the array
    for (int i = 0; i < n; i++) {
        freq[a[i]]++;
    }

    // Creating a DP array to keep
    // count of max score at ith element
    // and it will be filled
    // in the bottom Up manner
    vector<int> dp(*max_element(a.begin(),
                                a.end())
                       + 1,
                   0);
    dp[0] = 0;
    dp[1] = freq[1];

    // Loop to choose the elements of the
    // array to delete from the array
    for (int i = 2; i < dp.size(); i++)
        dp[i] = max(
            dp[i - 1],
            dp[i - 2] + freq[i] * i);

    return dp[dp.size() - 1];
}

// Driver Code
int main()
{
    int n;
    n = 3;
    vector<int> a{ 1, 2, 3 };

    // Function Call
    cout << findMaximumScore(a, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// maximum score of the deleting a
// element from an array
import java.util.*;

class GFG{

// Function to find the maximum
// score of the deleting an element
// from an array
static int findMaximumScore(int []a, int n)
{

    // Creating a map to keep
    // the frequency of numbers
    @SuppressWarnings("unchecked")
    HashMap<Integer,
            Integer> freq = new HashMap();

    // Loop to iterate over the
    // elements of the array
    for(int i = 0; i < n; i++)
    {
        if(freq.containsKey(a[i]))
        {
            freq.put(a[i],
                     freq.get(a[i]) + 1);
        }
        else
        {
            freq.put(a[i], 1);
        }
    }

    // Creating a DP array to keep
    // count of max score at ith element
    // and it will be filled
    // in the bottom Up manner
    int []dp = new int[Arrays.stream(a).max().getAsInt() + 1];
    dp[0] = 0;
    dp[1] = freq.get(1);

    // Loop to choose the elements of the
    // array to delete from the array
    for(int i = 2; i < dp.length; i++)
        dp[i] = Math.max(dp[i - 1],
                         dp[i - 2] +
                       freq.get(i) * i);

    return dp[dp.length - 1];
}

// Driver Code
public static void main(String[] args)
{
    int n;
    n = 3;
    int []a = { 1, 2, 3 };

    // Function call
    System.out.print(findMaximumScore(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to find the
# maximum score of the deleting a
# element from an array
from collections import defaultdict

# Function to find the maximum
# score of the deleting an element
# from an array
def findMaximumScore(a, n):

    # Creating a map to keep
    # the frequency of numbers
    freq = defaultdict (int)

    # Loop to iterate over the
    # elements of the array
    for i in range (n):
        freq[a[i]] += 1

    # Creating a DP array to keep
    # count of max score at ith element
    # and it will be filled
    # in the bottom Up manner
    dp = [0] * (max(a) + 1)
    dp[0] = 0
    dp[1] = freq[1]

    # Loop to choose the elements of the
    # array to delete from the array
    for i in range (2, len(dp)):
        dp[i] = max(dp[i - 1],
                    dp[i - 2] +
                    freq[i] * i)

    return dp[- 1]

# Driver Code
if __name__ == "__main__":

    n = 3
    a = [1, 2, 3]

    # Function Call
    print(findMaximumScore(a, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to find the
// maximum score of the deleting a
// element from an array
using System;
using System.Linq;
using System.Collections.Generic;

class GFG{

// Function to find the maximum
// score of the deleting an element
// from an array
static int findMaximumScore(int []a, int n)
{

    // Creating a map to keep
    // the frequency of numbers
    Dictionary<int,
               int> freq = new Dictionary<int,
                                          int>();

    // Loop to iterate over the
    // elements of the array
    for(int i = 0; i < n; i++)
    {
        if(freq.ContainsKey(a[i]))
        {
            freq[a[i]] = freq[a[i]] + 1;
        }
        else
        {
            freq.Add(a[i], 1);
        }
    }

    // Creating a DP array to keep
    // count of max score at ith element
    // and it will be filled
    // in the bottom Up manner
    int []dp = new int[a.Max() + 1];
    dp[0] = 0;
    dp[1] = freq[1];

    // Loop to choose the elements of the
    // array to delete from the array
    for(int i = 2; i < dp.Length; i++)
        dp[i] = Math.Max(dp[i - 1],
                         dp[i - 2] +
                       freq[i] * i);

    return dp[dp.Length - 1];
}

// Driver Code
public static void Main(String[] args)
{
    int n;
    n = 3;
    int []a = { 1, 2, 3 };

    // Function call
    Console.Write(findMaximumScore(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to find the
// maximum score of the deleting a
// element from an array

// Function to find the maximum
// score of the deleting an element
// from an array
function findMaximumScore(a,n)
{
    // Creating a map to keep
    // the frequency of numbers
    let freq = new Map();

    // Loop to iterate over the
    // elements of the array
    for(let i = 0; i < n; i++)
    {
        if(freq.has(a[i]))
        {
            freq.set(a[i],
                     freq.get(a[i]) + 1);
        }
        else
        {
            freq.set(a[i], 1);
        }
    }

    // Creating a DP array to keep
    // count of max score at ith element
    // and it will be filled
    // in the bottom Up manner
    let dp = new Array(Math.max(...a)+1);
    dp[0] = 0;
    dp[1] = freq.get(1);

    // Loop to choose the elements of the
    // array to delete from the array
    for(let i = 2; i < dp.length; i++)
        dp[i] = Math.max(dp[i - 1],
                         dp[i - 2] +
                       freq.get(i) * i);

    return dp[dp.length - 1];
}

// Driver Code
let n = 3;
let a=[1, 2, 3];

// Function call
document.write(findMaximumScore(a, n));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)

**辅助空间:** O(N)