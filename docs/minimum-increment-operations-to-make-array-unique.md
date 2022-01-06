# 使数组唯一的最小增量操作

> 原文:[https://www . geeksforgeeks . org/最小增量操作使数组唯一/](https://www.geeksforgeeks.org/minimum-increment-operations-to-make-array-unique/)

给定整数数组 A[]。在一次移动中，你可以选择任何元素 A[i]，并将其增加 1。任务是返回使数组 A[]中的每个值唯一所需的最小移动次数。
**例** :

```
Input: A[] = [3, 2, 1, 2, 1, 7]
Output: 6
Explanation:  After 6 moves, the array could be 
[3, 4, 1, 2, 5, 7].
It can be shown that it is impossible for the array 
to have all unique values with 5 or less moves.

Input: A[] = [1, 2, 2]
Output: 1
Explanation: After 1 move [2 -> 3], the array could be [1, 2, 3].
```

使每个重复值唯一的一个简单解决方案是不断重复递增它，直到它不唯一。然而，如果我们有一个全 1 的数组，我们可能会做很多额外的工作。
所以，我们可以做的是评估我们的增量应该是多少。例如，如果我们有[1，1，1，3，5]，我们不需要处理重复的 1 的所有增量。我们可以取两个 1(取= [1，1])并继续处理。每当我们发现一个空的(未使用的值)位置，比如 2 或 4，我们就可以恢复，我们的增量将分别是 2-1，4-1。
因此，我们首先计算数组中每个可能值的值:

*   如果 A 中有 2 个或更多的 X 值，请保存多余的重复值，以便以后递增。
*   如果 A 中有 0 个值 X，则保存的值将增加到 X

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ Implementation of above approach
#include <bits/stdc++.h>

using namespace std;

// function to find minimum increment required
int minIncrementForUnique(vector<int> A)
{

    // collect frequency of each element
    unordered_map<int, int> mpp;

    for(int i:A) mpp[i]++;

    // taken is to keep count
    // of duplicate items
    int taken=0, ans=0;

    for (int x = 0; x < 100000; x++)
    {

        // If number is present
          // multiple times
          if (mpp[x] >= 2){
          taken += mpp[x]-1;
          ans -= x*(mpp[x]-1);
        }

          // If there is no x in the array
        else if(taken > 0 and mpp[x] == 0)
        {
            ans += x;
            taken--;
        }
    }

    // return answer
    return ans;
}

// Driver code
int main()
{
    vector<int> A = {3, 2, 1, 2, 1, 7};

    // Function Call
    cout << minIncrementForUnique(A);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Implementation of above approach
import java.util.*;

class GFG {

    // function to find minimum increment required
    static int minIncrementForUnique(int[] A)
    {
        // collect frequency of each element
        TreeMap<Integer, Integer> dict
            = new TreeMap<Integer, Integer>();
        HashSet<Integer> used = new HashSet<Integer>();

      // Load Frequency Map (Element -> Count) and Used Set
        for (int i : A) {
            if (dict.containsKey(i))
                dict.put(i, dict.get(i) + 1);
            else {
                dict.put(i, 1);
                used.add(i);
            }
        }

        int maxUsed = 0; // Works for +ve numbers
        int ans = 0;

        for (Map.Entry<Integer, Integer> entry :
             dict.entrySet()) {

            int value = entry.getKey();
            int freq = entry.getValue();

            if (freq <= 1) //If not a duplicate, skip
                continue;

            int duplicates = freq - 1; // Number of duplicates 1 less than count

          // Start with next best option for this duplicate:
          // CurNum + 1 or an earlier maximum number that has been used
            int cur = Math.max(value + 1, maxUsed);
            while (duplicates > 0) {
                if (!used.contains(cur)) {
                    ans += cur - value; // Number of increments = Available Spot - Duplicate Value
                    used.add(cur);
                    duplicates--;
                    maxUsed = cur;
                }
                cur++;
            }
        }

        // return answer
        return ans;
    }

    // Driver code

    public static void main(String[] args)
    {
        int[] A = { 3, 2, 1, 2, 1, 2, 6, 7 };
        System.out.print(minIncrementForUnique(A));
    }
}

// This code is contributed by Aditya
```

## 蟒蛇 3

```
# Python3 Implementation of above approach
import collections

# function to find minimum increment required
def minIncrementForUnique(A):

    # collect frequency of each element
    count = collections.Counter(A)

    # array of unique values taken
    taken = []

    ans = 0

    for x in range(100000):
        if count[x] >= 2:
            taken.extend([x] * (count[x] - 1))
        elif taken and count[x] == 0:
            ans += x - taken.pop()

    # return answer
    return ans

# Driver code
A = [3, 2, 1, 2, 1, 7]
print(minIncrementForUnique(A))
```

## C#

```
// C# Implementation of above approach
using System;
using System.Collections.Generic;

class GFG
{

// function to find minimum increment required
static int minIncrementForUnique(int []A)
{

    // collect frequency of each element
    Dictionary<int,int> mpp = new Dictionary<int,int>();

    foreach(int i in A)
    {
        if(mpp.ContainsKey(i))
            mpp[i] = mpp[i] + 1;
        else
            mpp.Add(i, 1);
    }

    // array of unique values taken
    List<int> taken = new List<int>();

    int ans = 0;

    for (int x = 0; x < 100000; x++)
    {
        if (mpp.ContainsKey(x) && mpp[x] >= 2)
            taken.Add(x * (mpp[x] - 1));
        else if(taken.Count > 0 &&
                ((mpp.ContainsKey(x) &&
                mpp[x] == 0)||!mpp.ContainsKey(x)))
        {
            ans += x - taken[taken.Count - 1];
            taken.RemoveAt(taken.Count - 1);
        }
    }

    // return answer
    return ans;
}

// Driver code
public static void Main(String[] args)
{

    int []A = {3, 2, 1, 2, 1, 7};

    Console.Write(minIncrementForUnique(A));
}
}

// This code contributed by PrinciRaj1992
```

**Output:** 

```
6
```

**时间复杂度:** O(N)