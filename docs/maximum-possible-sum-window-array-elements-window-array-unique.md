# 一个数组中一个窗口的最大可能和，使得其他数组中相同窗口的元素是唯一的

> 原文:[https://www . geesforgeks . org/最大可能和-窗口-数组-元素-窗口-数组-唯一/](https://www.geeksforgeeks.org/maximum-possible-sum-window-array-elements-window-array-unique/)

给定两个元素数量相等的数组 A 和 B。任务是找到数组 B 中一个窗口的最大可能和，使得 A[]中同一窗口的元素是唯一的。
示例:

```
Input : A = [0, 1, 2, 3, 0, 1, 4] 
        B = [9, 8, 1, 2, 3, 4, 5]
Output : sum = 20
The maximum sum possible in B[] such that 
all corresponding elements in A[] are unique 
is (9+8+1+2) = 20.

Input : A = [0, 1, 2, 0, 2]
        B = [5, 6, 7, 8, 2]
Output :sum = 21
```

一个**简单的解决方案**就是考虑 B[]的所有子阵。对于每个子阵列，检查 A[]中相同子阵列元素是否不同。如果不同，则将总和与结果进行比较并更新结果。
这个解决方案的时间复杂度是 O(n <sup>2</sup> )
一个**高效的解决方案**就是使用哈希。

1.  创建一个空哈希表。
2.  遍历数组元素。对每个元素 A[i]执行以下操作。
    *   当散列表中存在 A[i]时，继续从当前窗口的开始移除元素，并继续从当前总和中减去 B[]的窗口开始元素。
3.  将 B[i]添加到当前总和，如果当前总和变得更多，则更新结果。
4.  返回结果。

下面是以上步骤的实现。

## C++

```
// C++ program to find the maximum
// possible sum of a window in one
// array such that elements in same
// window of other array are unique.
#include <bits/stdc++.h>
using namespace std;

// Function to return maximum sum of window
// in B[] according to given constraints.
int returnMaxSum(int A[], int B[], int n)
{
    // Map is used to store elements
    // and their counts.
    unordered_set<int> mp;

    int result = 0; // Initialize result

    // calculating the maximum possible
    // sum for each subarray containing
    // unique elements.
    int curr_sum = 0, curr_begin = 0;
    for (int i = 0; i < n; ++i) {

        // Remove all duplicate
        // instances of A[i] in
        // current window.
        while (mp.find(A[i]) != mp.end()) {
            mp.erase(A[curr_begin]);
            curr_sum -= B[curr_begin];
            curr_begin++;
        }

        // Add current instance of A[i]
        // to map and to current sum.
        mp.insert(A[i]);
        curr_sum += B[i];

        // Update result if current
        // sum is more.
        result = max(result, curr_sum);
    }

    return result;
}

// Driver code
int main()
{
    int A[] = { 0, 1, 2, 3, 0, 1, 4 };
    int B[] = { 9, 8, 1, 2, 3, 4, 5 };
    int n = sizeof(A)/sizeof(A[0]);
    cout << returnMaxSum(A, B, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// possible sum of a window in one
// array such that elements in same
// window of other array are unique.
import java.util.HashSet;
import java.util.Set;

public class MaxPossibleSuminWindow
{
    // Function to return maximum sum of window
    // in A[] according to given constraints.
    static int returnMaxSum(int A[], int B[], int n)
    {

        // Map is used to store elements
        // and their counts.
        Set<Integer> mp = new HashSet<Integer>();

        int result = 0; // Initialize result

        // calculating the maximum possible
        // sum for each subarray containing
        // unique elements.
        int curr_sum = 0, curr_begin = 0;
        for (int i = 0; i < n; ++i)
        {
            // Remove all duplicate
            // instances of A[i] in
            // current window.
            while (mp.contains(A[i]))
            {
                mp.remove(A[curr_begin]);
                curr_sum -= B[curr_begin];
                curr_begin++;
            }

            // Add current instance of A[i]
            // to map and to current sum.
            mp.add(A[i]);
            curr_sum += B[i];

            // Update result if current
            // sum is more.
            result = Integer.max(result, curr_sum);

        }
        return result;
    }

    //Driver Code to test above method
    public static void main(String[] args)
    {
        int A[] = { 0, 1, 2, 3, 0, 1, 4 };
        int B[] = { 9, 8, 1, 2, 3, 4, 5 };
        int n = A.length;
        System.out.println(returnMaxSum(A, B, n));
    }
}
// This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find the maximum
# possible sum of a window in one
# array such that elements in same
# window of other array are unique.

# Function to return maximum sum of window
# in B[] according to given constraints.
def returnMaxSum(A, B, n):

    # Map is used to store elements
    # and their counts.
    mp = set()
    result = 0 # Initialize result

    # calculating the maximum possible
    # sum for each subarray containing
    # unique elements.
    curr_sum = curr_begin = 0
    for i in range(0, n): 

        # Remove all duplicate instances
        # of A[i] in current window.
        while A[i] in mp: 
            mp.remove(A[curr_begin])
            curr_sum -= B[curr_begin]
            curr_begin += 1

        # Add current instance of A[i]
        # to map and to current sum.
        mp.add(A[i])
        curr_sum += B[i]

        # Update result if current
        # sum is more.
        result = max(result, curr_sum)

    return result

# Driver code
if __name__ == "__main__":

    A = [0, 1, 2, 3, 0, 1, 4] 
    B = [9, 8, 1, 2, 3, 4, 5]
    n = len(A)
    print(returnMaxSum(A, B, n))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to find the maximum
// possible sum of a window in one
// array such that elements in same
// window of other array are unique.
using System;
using System.Collections.Generic;

public class MaxPossibleSuminWindow
{

    // Function to return maximum sum of window
    // in A[] according to given constraints.
    static int returnMaxSum(int []A, int []B, int n)
    {

        // Map is used to store elements
        // and their counts.
        HashSet<int> mp = new HashSet<int>();

        int result = 0; // Initialize result

        // calculating the maximum possible
        // sum for each subarray containing
        // unique elements.
        int curr_sum = 0, curr_begin = 0;
        for (int i = 0; i < n; ++i)
        {
            // Remove all duplicate
            // instances of A[i] in
            // current window.
            while (mp.Contains(A[i]))
            {
                mp.Remove(A[curr_begin]);
                curr_sum -= B[curr_begin];
                curr_begin++;
            }

            // Add current instance of A[i]
            // to map and to current sum.
            mp.Add(A[i]);
            curr_sum += B[i];

            // Update result if current
            // sum is more.
            result = Math.Max(result, curr_sum);

        }
        return result;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int []A = { 0, 1, 2, 3, 0, 1, 4 };
        int []B = { 9, 8, 1, 2, 3, 4, 5 };
        int n = A.Length;
        Console.WriteLine(returnMaxSum(A, B, n));
    }
}

/* This code has been contributed
by PrinciRaj1992*/
```

## java 描述语言

```
<script>

// Javascript program to find the maximum
// possible sum of a window in one
// array such that elements in same
// window of other array are unique.

// Function to return maximum sum of window
// in B[] according to given constraints.
function returnMaxSum(A, B, n)
{
    // Map is used to store elements
    // and their counts.
    var mp = new Set();

    var result = 0; // Initialize result

    // calculating the maximum possible
    // sum for each subarray containing
    // unique elements.
    var curr_sum = 0, curr_begin = 0;
    for (var i = 0; i < n; ++i) {

        // Remove all duplicate
        // instances of A[i] in
        // current window.
        while (mp.has(A[i])) {
            mp.delete(A[curr_begin]);
            curr_sum -= B[curr_begin];
            curr_begin++;
        }

        // Add current instance of A[i]
        // to map and to current sum.
        mp.add(A[i]);
        curr_sum += B[i];

        // Update result if current
        // sum is more.
        result = Math.max(result, curr_sum);
    }

    return result;
}

// Driver code
var A = [0, 1, 2, 3, 0, 1, 4];
var B = [9, 8, 1, 2, 3, 4, 5];
var n = A.length;
document.write( returnMaxSum(A, B, n));

// This code is contributed by importantly.
</script>
```

**输出:**

```
 20
```

这个解的时间复杂度是 O(n)。请注意，数组的每个元素最多只能从数组中插入和移除一次。
本文由 **Parth Trehan** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。