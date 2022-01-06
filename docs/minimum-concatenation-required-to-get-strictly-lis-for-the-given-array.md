# 获得给定数组的严格 LIS 所需的最小连接

> 原文:[https://www . geeksforgeeks . org/最小串联-要求为给定数组获取严格列表/](https://www.geeksforgeeks.org/minimum-concatenation-required-to-get-strictly-lis-for-the-given-array/)

给定一个大小为 n 的**数组 A[]** ，其中数组中只有唯一的元素。我们必须找到序列 A 所需的最小连接，才能得到严格的最长递增子序列。对于数组 A[]，我们遵循基于 1 的索引。

**示例:**

> **输入:** A = {1，3，2}
> **输出:** 2
> **解释:**
> 我们可以将 A 连起来两次作为[1，3，2，1，3，2]，然后输出索引 1，3，5，它给出的子序列为 1- > 2- > 3。
> **输入:** A = {2，1，4，3，5}
> **输出:** 3
> **解释:**
> 给定的数组必须连接 3 次才能生成最长的递增子序列。

**方法:**
解决上述问题的第一个观察结果是，严格递增的子序列的长度总是等于序列 A[]中存在的唯一元素的数量。因此，我们必须找到一种方法来保持最大连续数字在一起的顺序。我们可以这样做:在选择串联之前，在一个序列中取尽可能多的严格连续的数字，并在下一个串联中处理其他数字。

*   形成元素对及其索引，并按照值的排序顺序存储它们。初始化一个变量来计算所需的串联操作。
*   运行从索引 2 到 n 的循环，如果对[i-1]>对[i]的索引，则将变量增加 1，该变量正在计算所需的串联操作，否则继续该过程。

下面是上述方法的实现:

## C++

```
// CPP implementation to Find the minimum
// concatenation required to get strictly
// Longest Increasing Subsequence for the
// given array
#include <bits/stdc++.h>
using namespace std;

int increasingSubseq(int a[], int n)
{
    // Ordered map containing pairs
    // of value and index.
    map<int, int> mp;

    for (int i = 0; i < n; i++) {
        // Form pairs of value at index i
        // and it's index that is i.
        mp.insert(make_pair(a[i], i));
    }

    // Variable to insert the minimum
    // concatenations that are needed
    int ans = 1;

    // Iterator pointing to the
    // second pair in the map
    auto itr = ++mp.begin();

    // Iterator pointing to the
    // first pair in the map
    for (auto it = mp.begin(); it != mp.end(); ++it) {

        // Check if itr tends to end of map
        if (itr != mp.end()) {

            // Check if index2 is not greater than index1
            // then we have to perform a concatenation.
            if (itr->second <= it->second)
                ans += 1;

            ++itr;
        }
    }

    // Return the final answer
    cout << ans << endl;
}

// Driver code
int main()
{
    int a[] = { 2, 1, 4, 3, 5 };

    int n = sizeof(a) / sizeof(a[0]);

    increasingSubseq(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
/*package whatever //do not write package name here */
import java.util.*;
import java.io.*;

class GFG {

    private static void increasingSubseq(int a[], int n)
    {

        // Ordered map containing pairs
        // of value and index.
        TreeMap<Integer, Integer> mp
            = new TreeMap<Integer, Integer>();

        for (int i = 0; i < n; i++) {
            // Form pairs of value at index i
            // and it's index that is i.
            mp.put(a[i], i);
        }

        // Variable to insert the minimum
        // concatenations that are needed
        int ans = 1;

        // Iterator pointing to the
        // first entry in the map
        Map.Entry<Integer, Integer> itr
            = mp.pollFirstEntry();

        for (Map.Entry<Integer, Integer> it :
             mp.entrySet())
        {

            // Check if index2 is not greater than index1
            // then we have to perform a concatenation.
            if (itr.getValue() >= it.getValue())
                ans++;

            itr = it;
        }

        System.out.println(ans);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = { 2, 1, 4, 3, 5 };

        int n = a.length;

        increasingSubseq(a, n);
    }
}
```

## 蟒蛇 3

```
# Python 3 implementation to
# Find the minimum concatenation
# required to get strictly Longest
# Increasing Subsequence for the
# given array
def increasingSubseq(a, n):

    # Ordered map containing pairs
    # of value and index.
    mp = {}

    for i in range(n):
        # Form pairs of value at
        # index i and it's index
        # that is i.
        mp[a[i]] = i

    # Variable to insert the
    # minimum concatenations
    # that are needed
    ans = 1

    # Iterator pointing to the
    # second pair in the map
    itr = 1
    li= list(mp.values())
    # Iterator pointing to the
    # first pair in the map
    for key, value in mp.items():

        # Check if itr tends to
        # end of map
        if (itr < len(mp)):

            # Check if index2 is not
            # greater than index1
            # then we have to perform
            # a concatenation.
            if (li[itr] <= key):
                ans += 1

            itr+=1

    # Return the final
    # answer

    print(ans)

# Driver code
if __name__ == '__main__':

    a = [2, 1, 4, 3, 5]
    n = len(a)
    increasingSubseq(a, n)

# This code is contributed by bgangwar59
```

**Output**

```
3

```

**时间复杂度:** O(N * log N)