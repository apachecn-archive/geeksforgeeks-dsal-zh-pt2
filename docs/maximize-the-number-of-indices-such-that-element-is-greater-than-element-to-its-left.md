# 最大化索引的数量，使得元素大于其左边的元素

> 原文:[https://www . geeksforgeeks . org/最大化索引数-元素大于其左边的元素/](https://www.geeksforgeeks.org/maximize-the-number-of-indices-such-that-element-is-greater-than-element-to-its-left/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是最大化索引的数量，使得一个元素大于其左边的元素，即在重新排列数组后 **arr[i+1] > arr[i]** 。
**举例:**

> **输入:** arr[] = {200，100，100，200}
> **输出:** 2
> **解释:**
> 通过按以下方式排列数组，我们有:arr[] = {100，200，100，200}
> 可能的索引是 0 和 2，这样:
> arr[1]>arr[0](200>100)
> 7}
> **输出:** 7
> **解释:**
> 通过按以下方式排列数组，我们有:arr[] = {1，5，7，8，9，5，7，8，8，4}
> 可能的索引是 0，1，2，3，5，6 和 7，这样:
> arr[1]>arr[0](5>1)
> arr[2]>

**进场:**这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  为了获得最大数量的索引(比如说 **i** ),使得 **arr[i+1] > arr[i]** ，排列 **arr[]** 的元素，使得所有唯一元素的集合首先出现，然后在第一个集合之后出现下一个唯一元素的集合，直到所有元素都被排列。
    **例如:**

> 让 arr[] = {1，8，5，9，8，8，7，7，5，7，7}
> 第一组= {1，5，7，8，9}
> 第二组= {5，7，8}
> 第三组= {7，8}
> 第四组= {4}
> 现在新数组将是:
> arr[] = {1，5，7，8， **9** ，5，7， **8** ，7，，

2.  在上述安排之后，具有较高值的元素将不是给定条件的一部分，因为它后面跟有一个比它本身小的数字。
3.  因此，满足给定条件的对的总数可以由下式给出:

> **total_pairs =(元素数量–a _ number 的最高频率)**

以下是上述方法的实现:

## C++

```
// C++ program of the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum pairs
// such that arr[i+1] > arr[i]
void countPairs(int arr[], int N)
{

    // To store the frequency of the
    // element in arr[]
    unordered_map<int, int> M;

    // Store the frequency in map M
    for (int i = 0; i < N; i++) {
        M[arr[i]]++;
    }

    int maxFreq = 0;

    // To find the maximum frequency
    // store in map M
    for (auto& it : M) {
        maxFreq = max(maxFreq,
                      it.second);
    }

    // Print the maximum number of
    // possible pairs
    cout << N - maxFreq << endl;
}

// Driver Code
int main()
{

    int arr[] = { 1, 8, 5, 9, 8, 8, 7,
                  7, 5, 7, 7 };
    int N = sizeof(arr) / sizeof(arr[0]);

    countPairs(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to find the maximum pairs
// such that arr[i+1] > arr[i]
static void countPairs(int arr[], int N)
{

    // To store the frequency of the
    // element in arr[]
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();

    // Store the frequency in map M
    for (int i = 0; i < N; i++) {
        if(mp.containsKey(arr[i])){
            mp.put(arr[i], mp.get(arr[i])+1);
        }else{
            mp.put(arr[i], 1);
    }
    }

    int maxFreq = 0;

    // To find the maximum frequency
    // store in map M
    for (Map.Entry<Integer,Integer> it : mp.entrySet()) {
        maxFreq = Math.max(maxFreq,
                      it.getValue());
    }

    // Print the maximum number of
    // possible pairs
    System.out.print(N - maxFreq +"\n");
}

// Driver Code
public static void main(String[] args)
{

    int arr[] = { 1, 8, 5, 9, 8, 8, 7,
                  7, 5, 7, 7 };
    int N = arr.length;

    countPairs(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to find the maximum pairs
# such that arr[i + 1] > arr[i]
def countPairs(arr, N) :

    # To store the frequency of the
    # element in arr[]
    M = dict.fromkeys(arr, 0);

    # Store the frequency in map M
    for i in range(N) :
        M[arr[i]] += 1;

    maxFreq = 0;

    # To find the maximum frequency
    # store in map M
    for it in M.values() :
        maxFreq = max(maxFreq,it);

    # Print the maximum number of
    # possible pairs
    print(N - maxFreq);

# Driver Code
if __name__ == "__main__" :

    arr = [ 1, 8, 5, 9, 8, 8, 7, 7, 5, 7, 7 ];
    N = len(arr);

    countPairs(arr, N);

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the maximum pairs
// such that arr[i+1] > arr[i]
static void countPairs(int []arr, int N)
{

    // To store the frequency of the
    // element in []arr
    Dictionary<int,int> mp = new Dictionary<int,int>();

    // Store the frequency in map M
    for (int i = 0; i < N; i++) {
        if(mp.ContainsKey(arr[i])){
            mp[arr[i]] = mp[arr[i]]+1;
        }else{
            mp.Add(arr[i], 1);
    }
    }

    int maxFreq = 0;

    // To find the maximum frequency
    // store in map M
    foreach (KeyValuePair<int,int> it in mp) {
        maxFreq = Math.Max(maxFreq,
                      it.Value);
    }

    // Print the maximum number of
    // possible pairs
    Console.Write(N - maxFreq +"\n");
}

// Driver Code
public static void Main(String[] args)
{

    int []arr = { 1, 8, 5, 9, 8, 8, 7,
                  7, 5, 7, 7 };
    int N = arr.Length;

    countPairs(arr, N);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Js program of the above approach

// Function to find the maximum pairs
// such that arr[i+1] > arr[i]
function countPairs( arr,  N){
    // To store the frequency of the
    // element in arr[]
    let M = new Map();

    // Store the frequency in map M
    for (let i = 0; i < N; i++) {
        if(M[arr[i]])
        M[arr[i]]++;
        else
        M[arr[i]] = 1
    }

    let maxFreq = 0;

    // To find the maximum frequency
    // store in map M
    for (let it in M) {
        maxFreq = Math.max(maxFreq,
                      M[it]);
    }

    // Print the maximum number of
    // possible pairs
    document.write(N - maxFreq,'<br>');
}

// Driver Code
let a = [ 1, 8, 5, 9, 8, 8, 7,
                  7, 5, 7, 7 ];
let N = a.length;

    countPairs(a, N);

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N)，其中 N 是数组中元素的个数。*
***辅助空间:** O(N)，其中 N 为阵中元素个数。*