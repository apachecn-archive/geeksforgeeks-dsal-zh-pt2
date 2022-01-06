# 给定运算下数组最大值和最小值之间的最小差

> 原文:[https://www . geeksforgeeks . org/具有给定操作的数组的最大值和最小值之间的最小差值/](https://www.geeksforgeeks.org/minimum-difference-between-maximum-and-minimum-value-of-array-with-given-operations/)

给定一个数组 **arr[]** 和一个整数 **K** 。以下操作可以在任何数组元素上执行:

1.  将数组元素乘以 **K** 。
2.  如果元素可以被 **K** 整除，那么就用 **K** 整除。

以上两个操作可以应用任意次数，包括对任何数组元素应用零。任务是找到数组的最大值和最小值之间的最小可能差值。
**例:**

> **输入:** arr[] = {1，5000，9999}，K = 10000
> **输出:** 5000
> **说明:**
> 最大元素和最小元素之间的最小可能差是 5000。当元素 1 乘以 K 时，数组的最大元素变成 10000，最小元素变成 5000。而且，这是最不可能的值。
> **输入:** arr[] = {1，2，3，4，5，10，7}，K = 5
> **输出:** 5
> **说明:**
> 第一步，元素 5 和 10 可以用 5 除，分别是 1 和 2。
> 第二步，1 可以乘以 5。这使得 2 是数组中的最小元素，7 是数组中的最大元素。因此，差异为 5。

**方法:**想法是使用[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)作为[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)。可以按照以下步骤计算答案:

1.  最初，所有可能的值(即，当数组元素乘以 K，除以 K 时获得的值)与索引一起被插入多集。
2.  连续从多集弹出值。在每种情况下，带有索引 **i** 的弹出值 **X** 是最大值，如果所有索引都至少弹出了一个值，则除了 I 之外，所有索引的当前答案都是**X–min(一个索引先前弹出值的最大值)**
3.  如果当前差值小于到目前为止的计算值，请更新答案。
4.  这种情况一直持续到多集合中剩下元素。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate Minimum
// difference between maximum and
// minimum value of the array
int calculateMinDiff(int arr[], int k , int n)
{

    // Variable to store minimum difference
    int ans = INT_MAX;

    // PriorityQueue which is used as a multiset
    // to store all possible values
    priority_queue< pair<int,int> > pq;

    // Iterate through all the values and
    // add it to the priority queue
    for (int i = 0; i < n; i++)
    {

        // If the number is divisible by k
        // divide it by K and add to priority queue
        if (arr[i] % k == 0)
            pq.push(make_pair( arr[i] / k, i ));

        // Adding number as it is
        pq.push(make_pair( arr[i], i ));

        // Adding number after multiplying it by k
        pq.push(make_pair(arr[i] * k, i ));
    }

    // HashMap to keep track of current values

    map<int ,int>mp;

    while (!pq.empty())
    {
        pair<int,int>temp = pq.top();
        pq.pop();
        mp.insert(temp);

        // if for every index there is at-least
        // 1 value we calculate the answer
        if (mp.size() == n)
        {
            int min_value = INT_MAX;

            for(auto x:mp)
            min_value=min(min_value, x.second);

            ans = min(ans, temp.first - min_value);
        }
    }

    // Returning the calculated answer

    return ans;
}

// Driver code
int main()
{
    // Input Array
    int arr[7] = { 1, 2, 3, 4, 5, 10, 7 };
    int K = 5;

    // Size of the array
    int N = sizeof(arr)/sizeof(int);

    // Printing final output
    cout << (calculateMinDiff(arr, K, N));
}

// This code is contributed by ishayadav2918
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GfG {

    // Function to calculate Minimum
    // difference between maximum and
    // minimum value of the array
    private static int calculateMinDiff(int arr[], int k)
    {
        // Length of the array
        int n = arr.length;

        // Variable to store minimum difference
        int ans = Integer.MAX_VALUE;

        // PriorityQueue which is used as a multiset
        // to store all possible values
        PriorityQueue<int[]> pq
            = new PriorityQueue<>((int x[], int y[]) -> x[0] - y[0]);

        // Iterate through all the values and
        // add it to the priority queue
        for (int i = 0; i < n; i++) {

            // If the number is divisible by k
            // divide it by K and add to priority queue
            if (arr[i] % k == 0)
                pq.add(new int[] { arr[i] / k, i });

            // Adding number as it is
            pq.add(new int[] { arr[i], i });

            // Adding number after multiplying it by k
            pq.add(new int[] { arr[i] * k, i });
        }

        // HashMap to keep track of current values
        HashMap<Integer, Integer> map = new HashMap<>();

        while (!pq.isEmpty()) {
            int temp[] = pq.poll();
            map.put(temp[1], temp[0]);

            // if for every index there is at-least
            // 1 value we calculate the answer
            if (map.size() == n) {
                ans = Math.min(ans,
                               temp[0]
                                   - Collections.min(map.values()));
            }
        }

        // Returning the calculated answer
        return ans;
    }

    // Driver code
    public static void main(String args[])
    {
        // Input Array
        int arr[] = { 1, 2, 3, 4, 5, 10, 7 };
        int K = 5;

        // Printing final output
        System.out.println(calculateMinDiff(arr, K));
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the above approach 
import sys

# Function to calculate Minimum 
# difference between maximum and 
# minimum value of the array 
def calculateMinDiff(arr, k , n) : 

    # Variable to store minimum difference 
    ans = sys.maxsize

    # PriorityQueue which is used as a multiset 
    # to store all possible values 
    pq = []

    # Iterate through all the values and 
    # add it to the priority queue 
    for i in range(n) :

        # If the number is divisible by k 
        # divide it by K and add to priority queue 
        if (arr[i] % k == 0) :
            pq.append((arr[i] // k, i )) 

        # Adding number as it is 
        pq.append((arr[i], i)) 

        # Adding number after multiplying it by k 
        pq.append((arr[i] * k, i))

    pq.sort()
    pq.reverse()

    # HashMap to keep track of current values 

    mp = {} 

    while (len(pq) > 0) : 

        temp = pq[0] 
        pq.pop(0)
        mp[temp[0]] = temp[1] 

        # if for every index there is at-least 
        # 1 value we calculate the answer 
        if (len(mp) == n) :

            min_value = sys.maxsize

            for x in mp :
                min_value = min(min_value, mp[x])

            ans = min(ans, temp[0] - min_value - 1)

    # Returning the calculated answer 

    return ans

# Input Array 
arr = [ 1, 2, 3, 4, 5, 10, 7 ]
K = 5

# Size of the array 
N = len(arr)

# Printing final output 
print(calculateMinDiff(arr, K, N))

# This code is contributed by divyesh072019.
```

## C#

```
// C# implementation of the above approach 
using System;
using System.Collections.Generic;
class GFG
{

  // Function to calculate Minimum 
  // difference between maximum and 
  // minimum value of the array 
  static int calculateMinDiff(int[] arr, int k , int n) 
  { 

    // Variable to store minimum difference 
    int ans = Int32.MaxValue; 

    // PriorityQueue which is used as a multiset 
    // to store all possible values 
    List<Tuple<int,int>> pq = new List<Tuple<int,int>>();

    // Iterate through all the values and 
    // add it to the priority queue 
    for (int i = 0; i < n; i++) 
    { 

      // If the number is divisible by k 
      // divide it by K and add to priority queue 
      if (arr[i] % k == 0) 
        pq.Add(new Tuple<int,int>( arr[i] / k, i )); 

      // Adding number as it is 
      pq.Add(new Tuple<int,int>( arr[i], i )); 

      // Adding number after multiplying it by k 
      pq.Add(new Tuple<int,int>(arr[i] * k, i )); 
    }

    pq.Sort();
    pq.Reverse();

    // HashMap to keep track of current values 
    Dictionary<int, int> mp = new Dictionary<int, int>();

    while (pq.Count > 0) 
    { 
      Tuple<int,int> temp = pq[0]; 
      pq.RemoveAt(0);
      mp[temp.Item1] = temp.Item2; 

      // if for every index there is at-least 
      // 1 value we calculate the answer 
      if (mp.Count == n)
      { 
        int min_value = Int32.MaxValue;

        foreach(KeyValuePair<int, int> x in mp)
        {
          min_value=Math.Min(min_value, x.Value);
        }

        ans = Math.Min(ans, temp.Item1 - min_value - 1); 
      } 
    } 

    // Returning the calculated answer 

    return ans; 
  }

  // Driver code
  static void Main()
  {

    // Input Array 
    int[] arr = { 1, 2, 3, 4, 5, 10, 7 }; 
    int K = 5;

    // Size of the array 
    int N = arr.Length;

    // Printing final output
    Console.WriteLine(calculateMinDiff(arr, K, N));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

// Function to calculate Minimum
// difference between maximum and
// minimum value of the array
function calculateMinDiff(arr, k, n) {

    // Variable to store minimum difference
    let ans = Number.MAX_SAFE_INTEGER;

    // PriorityQueue which is used as a multiset
    // to store all possible values
    let pq = new Array();

    // Iterate through all the values and
    // push it to the priority queue
    for (let i = 0; i < n; i++) {

        // If the number is divisible by k
        // divide it by K and push to priority queue
        if (arr[i] % k == 0)
            pq.push(new Array(Math.floor(arr[i] / k), i));

        // pushing number as it is
        pq.push(new Array(arr[i], i));

        // pushing number after multiplying it by k
        pq.push(new Array(arr[i] * k, i));
    }

    pq.sort((a, b) => a[0] - b[0]);
    pq.reverse();

    // HashMap to keep track of current values
    let mp = new Map();

    while (pq.length > 0) {
        let temp = pq[0];
        pq.shift();
        mp.set(temp[0], temp[1]);

        // if for every index there is at-least
        // 1 value we calculate the answer
        if (mp.size == n) {
            let min_value = Number.MAX_SAFE_INTEGER;

            for (let x of mp) {
                min_value = Math.min(min_value, x[1]);
            }

            ans = Math.min(ans, temp[1] - min_value);
        }
    }

    // Returning the calculated answer

    return ans;
}

// Driver code

// Input Array
let arr = [1, 2, 3, 4, 5, 10, 7];
let K = 5;

// Size of the array
let N = arr.length;

// Printing final output
document.write(calculateMinDiff(arr, K, N));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
5
```

**时间复杂度:** O(NlogN)