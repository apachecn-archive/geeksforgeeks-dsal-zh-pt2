# 为使 0 和 1 的计数相等需要移除的最小元素

> 原文:[https://www . geeksforgeeks . org/要移除的最小元素-使 0 和 1 的计数相等/](https://www.geeksforgeeks.org/minimum-elements-to-be-removed-to-make-count-of-0s-and-1s-equal/)

给定两个长度相等的二进制数组 **A** 和 **B** ，任务是从前面找到要移除的元素的最小数量，以使给定的两个二进制数组中 0 和 1 的计数相等。

**示例:**

> **输入:** A = {0，1，0，1，1，0}，B = {1，0，0，1，1}
> **输出:** 6
> **解释:**
> - >从数组 A 中移除前 5 个元素
> - >从 B 中移除第一个元素
> - >因此至少需要移除 6 个元素，才能使 1 和 0 的总数相等
> 
> **输入:** a = {1，0}，b = {0，1}
> **输出:** 0
> **说明:**
> 1 和 0 的计数已经相等。因此，不需要移除任何元素。

**方法:**想法是分别找出 1 的总数和 0 的总数之间的差异，并将这种差异最小化。移除 1 会将差异减少 1，移除 0 会将差异增加 1。
因此，使差值等于 0 所需的步骤是:

*   计算 1 和 0 的总数的初始差值**。我们称之为*初始 _ 差异*。**
*   **从第一个数组中移除前 l 个元素**，并将差值存储在变量 *left_diff* 中。
*   **从第二个数组中移除前 r 个元素**，并将差值存储在变量 right_diff 中。
*   现在求出 l 和 r 的值，这样:

> *initial _ diff–left _ diff–right _ diff = 0。*

*   为了最佳地找到 l 和 r，对于 right_diff 的每个唯一值，保存最小的 r 以在[无序 _ 映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中达到该值。最后，迭代 l，找到最小答案。

下面是上述方法的实现

## C++

```
// C++ program to find minimum elements
// to be removed to make count
// of 0s and 1s equal

#include <bits/stdc++.h>
using namespace std;

// Function that returns minimum elements
// need to be removed
int MinRemovedElements(int a[], int b[],
                    int n)
{

    int no_of_ones = 0;
    int no_of_zeroes = 0;

    // Counting total number of
    // zeroes and ones
    for (int i = 0; i < n; i++) {
        if (a[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;

        if (b[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;
    }

    // Computing difference in ones and
    // zeroes
    int diff = no_of_ones - no_of_zeroes;

    unordered_map<int, int> mp;
    mp[0] = 0;
    int curr = 0;

    // Filling the difference of number
    // of 1's and 0's of 1st array in
    // unoredered_map
    for (int i = 0; i < n; i++) {
        if (a[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference
        // not found in map
        if (mp.find(curr) == mp.end())
            mp[curr] = i + 1;
    }

    curr = 0;
    int answer = 2 * n;

    for (int i = 0; i < n; i++) {
        if (b[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference is
        // present in map then compute the
        // minimum one
        if (mp.find(diff - curr) != mp.end())
            answer
                = min(answer,
                    i + 1 + mp);
    }

    // Condition if the total difference
    // is present in 1st array
    if (mp.find(diff) != mp.end())
        answer = min(answer, mp);

    return answer;
}

// Driver Code
int main()
{
    int a[] = { 0, 1, 0, 1, 1, 0 };
    int b[] = { 1, 0, 0, 1, 1, 1 };
    int size = sizeof(a) / sizeof(a[0]);

    cout << MinRemovedElements(a, b, size)
        << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum elements
// to be removed to make count
// of 0s and 1s equal
import java.util.*;

class GFG{

// Function that returns minimum elements
// need to be removed
static int MinRemovedElements(int a[], int b[],
                    int n)
{

    int no_of_ones = 0;
    int no_of_zeroes = 0;

    // Counting total number of
    // zeroes and ones
    for (int i = 0; i < n; i++) {
        if (a[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;

        if (b[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;
    }

    // Computing difference in ones and
    // zeroes
    int diff = no_of_ones - no_of_zeroes;

    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>();
    mp.put(0, 0);
    int curr = 0;

    // Filling the difference of number
    // of 1's and 0's of 1st array in
    // unoredered_map
    for (int i = 0; i < n; i++) {
        if (a[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference
        // not found in map
        if (!mp.containsKey(curr))
            mp.put(curr, i + 1);
    }

    curr = 0;
    int answer = 2 * n;

    for (int i = 0; i < n; i++) {
        if (b[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference is
        // present in map then compute the
        // minimum one
        if (mp.containsKey(diff - curr))
            answer
                = Math.min(answer,mp.get(diff - curr) + 1 + i);
    }

    // Condition if the total difference
    // is present in 1st array
    if (mp.containsKey(diff))
        answer = Math.min(answer, mp.get(diff));

    return answer;
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 0, 1, 0, 1, 1, 0 };
    int b[] = { 1, 0, 0, 1, 1, 1 };
    int size = a.length;

    System.out.print(MinRemovedElements(a, b, size)
        + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find minimum
# elements to be removed to make
# count of 0s and 1s equal

# Function that returns minimum
# elements need to be removed
def MinRemovedElements(a, b, n):

    no_of_ones = 0;
    no_of_zeroes = 0;

    # Counting total number of
    # zeroes and ones
    for i in range(n):
        if (a[i] == 1):
            no_of_ones += 1;
        else:
            no_of_zeroes += 1;

        if (b[i] == 1):
            no_of_ones += 1;
        else:
            no_of_zeroes += 1;

    # Computing difference in ones and
    # zeroes
    diff1 = no_of_ones - no_of_zeroes;

    mp = {};
    mp[0] = 0;
    curr = 0;

    # Filling the difference of number
    # of 1's and 0's of 1st array in
    # unoredered_map
    for i in range(n):
        if (a[i] == 1):
            curr += 1;
        else :
            curr -= 1;

        # Condition if current difference
        # not found in map
        if curr not in mp:
            mp[curr] = i + 1;

    curr = 0;
    answer = 2 * n;

    for i in range(n):
        if (b[i] == 1):
            curr += 1;
        else:
            curr -= 1;

        # Condition if current difference is
        # present in map then compute the
        # minimum one
        if (diff1 - curr) in mp :
            answer = min(answer, i + 1 + mp[diff1 -
                                            curr]);

    # Condition if the total difference
    # is present in 1st array
    if diff1 in mp:
        answer = min(answer, mp[diff1]);

    return answer;

# Driver Code
if __name__ == "__main__" :

    a = [ 0, 1, 0, 1, 1, 0 ];
    b = [ 1, 0, 0, 1, 1, 1 ];

    size = len(a);

    print(MinRemovedElements(a, b, size));

# This code is contributed by Yash_R
```

## C#

```
// C# program to find minimum elements
// to be removed to make count
// of 0s and 1s equal
using System;
using System.Collections.Generic;

class GFG{

// Function that returns minimum elements
// need to be removed
static int MinRemovedElements(int[] a, int[] b,
                              int n)
{
    int no_of_ones = 0;
    int no_of_zeroes = 0;

    // Counting total number of
    // zeroes and ones
    for(int i = 0; i < n; i++)
    {
        if (a[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;

        if (b[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;
    }

    // Computing difference in ones and
    // zeroes
    int diff = no_of_ones - no_of_zeroes;

    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    mp.Add(0, 0);
    int curr = 0;

    // Filling the difference of number
    // of 1's and 0's of 1st array in
    // unoredered_map
    for(int i = 0; i < n; i++)
    {
        if (a[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference
        // not found in map
        if (!mp.ContainsKey(curr))
            mp.Add(curr, i + 1);
    }

    curr = 0;
    int answer = 2 * n;

    for(int i = 0; i < n; i++)
    {
        if (b[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference is
        // present in map then compute the
        // minimum one
        if (mp.ContainsKey(diff - curr))
            answer = Math.Min(answer,
             i + 1 + mp);
    }

    // Condition if the total difference
    // is present in 1st array
    if (mp.ContainsKey(diff))
        answer = Math.Min(answer, mp);

    return answer;
}

// Driver code
static void Main()
{
    int[] a = { 0, 1, 0, 1, 1, 0 };
    int[] b = { 1, 0, 0, 1, 1, 1 };
    int size = a.Length;

    Console.WriteLine(MinRemovedElements(
        a, b, size));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program to find minimum elements
// to be removed to make count
// of 0s and 1s equal

// Function that returns minimum elements
// need to be removed
function MinRemovedElements(a, b, n)
{

    let no_of_ones = 0;
    let no_of_zeroes = 0;

    // Counting total number of
    // zeroes and ones
    for (let i = 0; i < n; i++) {
        if (a[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;

        if (b[i] == 1)
            no_of_ones++;
        else
            no_of_zeroes++;
    }

    // Computing difference in ones and
    // zeroes
    let diff = no_of_ones - no_of_zeroes;

    let mp = new Map();
    mp.set(0 , 0);
    let curr = 0;

    // Filling the difference of number
    // of 1's and 0's of 1st array in
    // unoredered_map
    for (let i = 0; i < n; i++) {
        if (a[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference
        // not found in map
        if (!mp.has(curr))
            mp.set(curr, i + 1);
    }

    curr = 0;
    let answer = 2 * n;

    for (let i = 0; i < n; i++) {
        if (b[i] == 1)
            curr++;
        else
            curr--;

        // Condition if current difference is
        // present in map then compute the
        // minimum one
        if (mp.has(diff - curr))
            answer = Math.min(answer, mp.get(diff - curr) + i + 1);
    }

    // Condition if the total difference
    // is present in 1st array
    if (mp.has(diff))
        answer = Math.min(answer, mp.get(diff));

    return answer;
}

// Driver Code

let a = [ 0, 1, 0, 1, 1, 0 ];
let b = [ 1, 0, 0, 1, 1, 1 ];
let size = a.length;

document.write(MinRemovedElements(a, b, size) + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**输出:**

```
6
```

***时间复杂度:** O(N)*