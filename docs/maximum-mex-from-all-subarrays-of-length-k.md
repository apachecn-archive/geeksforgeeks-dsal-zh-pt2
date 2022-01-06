# 长度为 K 的所有子阵列的最大 MEX

> 原文:[https://www . geeksforgeeks . org/maximum-MEX-from-all-subarles-of-length-k/](https://www.geeksforgeeks.org/maximum-mex-from-all-subarrays-of-length-k/)

给定一个由 **N** 个不同整数和一个整数 **K** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从所有[子数组](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中找到最大 **MEX** 长度 **K** 。

> **MEX** 是数组中不存在的[最小正整数。](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array/)

**示例:**

> **输入:** arr[] = {3，2，1，4}，K = 2
> **输出:** 3
> **解释:**
> 所有长度为 2 的子阵都是{3，2}、{2，1}、{1，4}。
> 在子阵列{3，2}中，不存在的最小正整数为 1。
> 在子阵列{2，1}中，不存在的最小正整数为 3。
> 在子阵列{1，4}中，不存在的最小正整数为 2。
> 
> **输入:** arr[] = {6，1，3，2，4}，K = 3
> **输出:** 4
> **解释:**
> 所有长度为 3 的子阵都是{6，1，3}、{1，3，2}、{3，2，4}
> 在子阵{6，1，3}中，不存在的最小正整数是 2。
> 在子阵列{1，3，2}中，不存在的最小正整数为 4。
> 在子阵列{3，2，4}中，不存在的最小正整数为 1。

**天真方法:**最简单的方法是[生成所有长度的子阵**K**T5】并找到每个](https://www.geeksforgeeks.org/sliding-window-maximum-maximum-of-all-subarrays-of-size-k/)[子阵](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的 **MEX** 。找到所有**墨西哥**后，打印获得的最大值。

***时间复杂度:**O(K * N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效途径:**优化上述途径，思路是使用数据结构[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)和[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)。按照以下步骤解决问题:

*   初始化一组 **S** 来存储当前子阵列中不存在的值，并在其中初始插入 **1** 到 **N + 1** 号，因为最初窗口的大小是 **0** 。
*   遍历范围**【0，K–1】**并从集合中删除**arr【I】**，集合的第一个元素是从索引 **0** 和长度 **K** 开始的子阵列的 **MEX** ，初始化一个变量 **mex** 并将该值存储在 **mex** 中。
*   现在从 **K** 迭代到**N–1**并插入**arr【I】**以设置并清除**arr【I–K】**并更新 **mex = max(mex，集合的第一个元素)。**
*   完成上述步骤后，在长度为 **K** 的子阵列中，将 **mex** 打印为最大 **MEX** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return maximum MEX of
// all K length subarray
void maxMEX(int arr[], int N, int K)
{
    // Stores element from 1 to N + 1
    // is nor present in subarray
    set<int> s;

    // Store number 1 to N + 1 in set s
    for (int i = 1; i <= N + 1; i++)
        s.insert(i);

    // Find the MEX of K length subarray
    // starting from index 0
    for (int i = 0; i < K; i++)
        s.erase(arr[i]);

    int mex = *(s.begin());

    // Find the MEX of all subarray of
    // length K by erasing arr[i]
    // and inserting arr[i-K]
    for (int i = K; i < N; i++) {
        s.erase(arr[i]);

        s.insert(arr[i - K]);

        // Store first element of set
        int firstElem = *(s.begin());

        // Updating mex
        mex = max(mex, firstElem);
    }

    // Print maximum MEX of all K
    // length subarray
    cout << mex << ' ';
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 3, 2, 1, 4 };

    // Given length of subarray
    int K = 2;

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxMEX(arr, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the
// above approach
import java.util.*;
class GFG {

    // Function to return maximum
    // MEX of all K length subarray
    static void maxMEX(int arr[], int N, int k)
    {
        // Stores element from
        // 1 to N + 1 is nor
        // present in subarray

        // We need a Tree Set since
        // we want to store the
        // elements in ascending
        // order
        TreeSet<Integer> s = new TreeSet<>();

        // Store number 1 to
        // N + 1 in set s
          for(int l=1;l<=N+1;l++)   
          s.add(l);
          // i and j point to the start of the array
          // i.e index 0
          int i=0;
          int j=0;

          int mex = 0;
          // mex variable which stores the mex for
          // generated subArrays
          int maxMex = Integer.MIN_VALUE;
          //maxMex contains the maximum mex value for all subArrays

          while(j < N)
        {
          if(s.contains(arr[j]))
             s.remove(arr[j]);
          int windowSize = j-i+1;
          // window size at any instant is given by j-i+1;
          if(windowSize < k)
             j++;
             // here, windowSize < k , i.e we haven't reached the first
             // window of size k yet.. so we increment j;
          else if(windowSize == k)
          {
            //here , windowSize equals k, we are to get an answer everytime
            // we reached the windowSize of k , first element of the set has
            // mex for this subArray;
            mex = s.pollFirst();
            // set.pollFirst() function removes the firstElement in the treeset;
            maxMex = Math.max(maxMex,mex);

            // before sliding the window , we need to undo the calculations
            // done at the starting point , i.e i;
            s.add(arr[i]);
            i++;
            j++;
            // sliding the window by 1 each in i and j , so as to maintain
            // the windowSize k;
          }
        }
        System.out.println(maxMex);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given array
        int arr[] = { 6, 1, 3, 2, 4 };

        // Given length of subarray
        int K = 3;

        // Size of the array
        int N = arr.length;

        // Function Call
        maxMEX(arr, N, K);
    }
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to return maximum MEX of
# all K length subarray

def maxMEX(arr, N, K):

    # Stores element from 1 to N + 1
    # is nor present in subarray
    s = set()

    # Store number 1 to N + 1 in set s
    for i in range(1, N + 2):
        s.add(i)

    # Find the MEX of K length subarray
    # starting from index 0
    for i in range(K):
        s.remove(arr[i])

    mex = list(s)[0]

    # Find the MEX of all subarray of
    # length K by erasing arr[i]
    # and inserting arr[i-K]
    for i in range(K, N):
        s.remove(arr[i])

        s.add(arr[i - K])

        # Store first element of set
        firstElem = list(s)[0]

        # Updating mex
        mex = max(mex, firstElem)

    # Print maximum MEX of all K
    # length subarray
    print(mex)

# Driver code
if __name__ == '__main__':

    # Given array
    arr = [3, 2, 1, 4]

    # Size of the array
    N = len(arr)

    # Given length of subarray
    K = 2

    # Function Call
    maxMEX(arr, N, K)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to return maximum
    // MEX of all K length subarray
    static void maxMEX(int[] arr, int N, int K)
    {
        // Stores element from
        // 1 to N + 1 is nor
        // present in subarray
        HashSet<int> s = new HashSet<int>();

        // Store number 1 to
        // N + 1 in set s
        for (int i = 1; i <= N + 1; i++)
            s.Add(i);

        // Find the MEX of K length
        // subarray starting from index 0
        for (int i = 0; i < K; i++)
            s.Remove(arr[i]);

        List<int> v = new List<int>();
        foreach(int i in s) { v.Add(i); }
        int mex = v[0];

        // Find the MEX of all subarray of
        // length K by erasing arr[i]
        // and inserting arr[i-K]
        for (int i = K; i < N; i++)
        {
            v.Remove(arr[i]);
            v.Add(arr[i - K]);

            // Store first element
            // of set
            int firstElem = v[0];

            // Updating mex
            mex = Math.Max(mex, firstElem);
        }

        // Print maximum MEX of all K
        // length subarray
        Console.Write(mex - 2 + " ");
    }

    // Driver Code
    public static void Main(String[] args)
    {
        // Given array
        int[] arr = { 3, 2, 1, 4 };

        // Given length of subarray
        int K = 2;

        // Size of the array
        int N = arr.Length;

        // Function Call
        maxMEX(arr, N, K);
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to return maximum MEX of
// all K length subarray
function maxMEX( arr,  N, K)
{
    // Stores element from 1 to N + 1
    // is nor present in subarray
    let s = new Set();

    // Store number 1 to N + 1 in set s
    for (let i = 1; i <= N + 1; i++)
        s.add(i);

    // Find the MEX of K length subarray
    // starting from index 0
    for (let i = 0; i < K; i++)
        s.delete(arr[i]);

    let a = Array.from(s);
    var mex = a[0];

    // Find the MEX of all subarray of
    // length K by erasing arr[i]
    // and inserting arr[i-K]
    for (let i = K; i < N; i++) {
        s.delete(arr[i]);

        s.add(arr[i - K]);

        // Store first element of set
    let ss = Array.from(s);
    var firstElem = ss[ss.length-1];

        // Updating mex
        mex = Math.max(mex, firstElem);
    }

    // Print maximum MEX of all K
    // length subarray
    document.write( mex ,' ');
}

// Driver Code
    // Given array
    let arr = [ 3, 2, 1, 4 ];

    // Given length of subarray
    let K = 2;

    // Size of the array
    let N = arr.length;

    // Function Call
    maxMEX(arr, N, K);

</script>
```

**Output**

```
3 
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*