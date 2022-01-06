# 大小为 K 的子阵列的计数，它是从 1 到 K 的数字排列

> 原文:[https://www . geeksforgeeks . org/大小为 k 的子阵列的计数，即从 1 到 k 的数字排列/](https://www.geeksforgeeks.org/count-of-subarrays-of-size-k-which-is-a-permutation-of-numbers-from-1-to-k/)

给定一个由不同整数组成的数组 **arr** ，任务是找到大小为 **i** 的子数组的计数，这些子数组具有从 **1 到 i** 的所有元素，换句话说，子数组是从 **1 到 i** 的元素的任意排列，其中 **1 < = i < = N** 。

**示例:**

> **输入:** arr[] = {2，3，1，5，4}
> **输出:** 3
> **解释:**
> 我们有{1}、{2，3，1}和{2，3，1，5，4}子阵列，分别为 i=1，i=3，i=5。
> 4 号和 2 号无法排列，因为 5 号和 3 号分别碍事。
> 
> **输入:** arr[] = {1，3，5，4，2}
> **输出:** 2
> **解释:**
> 对于 i=1 和 i=5，我们分别有{1}和{1，3，5，4，2}个子阵列。

一种**天真的方法**是从每个索引开始，试图找到每个大小(I)的子阵列，并检查从 1 到 I 的所有元素是否都存在。
T3】时间复杂度:O(N <sup>2</sup> )

通过检查是否有可能为从 **1 到 N** 的 I 的每个值创建一个大小为 **i** 的子阵列，可以给出一个**有效的方法**。
我们知道，每一个大小为 **K** 的子阵列都必须是从 **1 到 K** 的所有元素的排列，要知道我们可以按照顺序查看 **1 到 N** 的数字的索引，计算每一步的最小值和最大值的索引。

*   如果**最大 _ ind–最小 _ind + 1 = K** ，那么我们有一个大小为 K 的置换，否则没有。
*   在每一步更新最小值和最大值。

**时间复杂度:**O(n)
T3】图解:

> 给定 Arr = **{2，3，1，5，4}** ，让我们从 min_ind = INF 和 max_ind = -1 开始
> 
> 1.  索引 1 是 2，所以 min_ind = min(min_ind，2) = 2，max_ind = max(max_ind，2) = 2，
>     2-2+1 = 1，所以我们有一个大小为 1 的置换
> 2.  2 的索引是 0，所以 min_ind = min(min_ind，0) = 0，max_ind = max(max_ind，0) = 2，
>     2-0+1 = 3，所以我们没有大小为 2 的置换
> 3.  3 的索引是 1，所以 min_ind = min(min_ind，1) = 0，max_ind = max(max_ind，1) = 2，
>     2-0+1 = 3，所以我们有大小为 3 的置换
> 4.  4 的索引是 4，所以 min_ind = min(min_ind，4) = 0，max_ind = max(max_ind，4) = 4，
>     4-0+1 = 5，所以我们没有大小为 4 的置换
> 5.  5 的索引是 3，所以 min_ind = min(min_ind，3) = 0，max_ind = max(max_ind，4) = 4，
>     4-0+1 = 5，所以我们有一个大小为 5 的置换
> 
> 所以答案是 3

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <iostream>
#include <unordered_map>
#include <vector>
using namespace std;

int find_permutations(vector<int>& arr)
{
    int cnt = 0;
    int max_ind = -1, min_ind = 10000000;
    int n = arr.size();
    unordered_map<int, int> index_of;

    // Save index of numbers of the array
    for (int i = 0; i < n; i++) {
        index_of[arr[i]] = i + 1;
    }

    for (int i = 1; i <= n; i++) {

        // Update min and max index
        // with the current index
        // and check if it's a valid permutation
        max_ind = max(max_ind, index_of[i]);
        min_ind = min(min_ind, index_of[i]);
        if (max_ind - min_ind + 1 == i)
            cnt++;
    }

    return cnt;
}

// Driver code
int main()
{
    vector<int> nums;
    nums.push_back(2);
    nums.push_back(3);
    nums.push_back(1);
    nums.push_back(5);
    nums.push_back(4);

    cout << find_permutations(nums);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

public static int find_permutations(
    Vector<Integer> arr)
{
    int cnt = 0;
    int max_ind = -1, min_ind = 10000000;
    int n = arr.size();

    HashMap<Integer,
            Integer> index_of = new HashMap<>();

    // Save index of numbers of the array
    for(int i = 0; i < n; i++)
    {
        index_of.put(arr.get(i), i + 1);
    }

    for(int i = 1; i <= n; i++)
    {

        // Update min and max index with
        // the current index and check
        // if it's a valid permutation
        max_ind = Math.max(max_ind, index_of.get(i));
        min_ind = Math.min(min_ind, index_of.get(i));

        if (max_ind - min_ind + 1 == i)
            cnt++;
    }
    return cnt;
}

// Driver Code
public static void main(String[] args)
{
    Vector<Integer> nums = new Vector<Integer>();
    nums.add(2);
    nums.add(3);
    nums.add(1);
    nums.add(5);
    nums.add(4);

    System.out.print(find_permutations(nums));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
def find_permutations(arr):

    cnt = 0
    max_ind = -1
    min_ind = 10000000;

    n = len(arr)
    index_of = {}

    # Save index of numbers of the array
    for i in range(n):
        index_of[arr[i]] = i + 1

    for i in range(1, n + 1):

        # Update min and max index with the
        # current index and check if it's a
        # valid permutation
        max_ind = max(max_ind, index_of[i])
        min_ind = min(min_ind, index_of[i])

        if (max_ind - min_ind + 1 == i):
            cnt += 1

    return cnt

# Driver code
if __name__ == "__main__":

    nums = []
    nums.append(2)
    nums.append(3)
    nums.append(1)
    nums.append(5)
    nums.append(4)

    print(find_permutations(nums))

# This code is contributed by chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;

class GFG{

static int find_permutations(ArrayList arr)
{
    int cnt = 0;
    int max_ind = -1, min_ind = 10000000;
    int n = arr.Count;

    Dictionary<int,
               int> index_of = new Dictionary<int,
                                              int>();

    // Save index of numbers of the array
    for(int i = 0; i < n; i++)
    {
        index_of[(int)arr[i]] = i + 1;
    }

    for(int i = 1; i <= n; i++)
    {

        // Update min and max index with
        // the current index and check
        // if it's a valid permutation
        max_ind = Math.Max(max_ind, index_of[i]);
        min_ind = Math.Min(min_ind, index_of[i]);

        if (max_ind - min_ind + 1 == i)
            cnt++;
    }
    return cnt;
}

// Driver Code
public static void Main(string[] args)
{
    ArrayList nums = new ArrayList();

    nums.Add(2);
    nums.Add(3);
    nums.Add(1);
    nums.Add(5);
    nums.Add(4);

    Console.Write(find_permutations(nums));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>
// Javascript implementation
function find_permutations(arr)
{
    var cnt = 0;
    var max_ind = -1, min_ind = 10000000;
    var n = arr.length;
    var index_of = new Map();

    // Save index of numbers of the array
    for (var i = 0; i < n; i++) {
        index_of.set(arr[i], i + 1);
    }

    for (var i = 1; i <= n; i++) {

        // Update min and max index
        // with the current index
        // and check if it's a valid permutation
        max_ind = Math.max(max_ind, index_of.get(i));
        min_ind = Math.min(min_ind, index_of.get(i));
        if (max_ind - min_ind + 1 == i)
            cnt++;
    }

    return cnt;
}

var nums = [];
nums.push(2);
nums.push(3);
nums.push(1);
nums.push(5);
nums.push(4);

document.write(find_permutations(nums));
// This code contributed by shubhamsingh10
</script>
```

**Output:** 

```
3
```