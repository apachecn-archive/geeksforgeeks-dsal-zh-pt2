# 通过转换 0 可以从数组形成的最长连续序列的长度

> 原文:[https://www . geeksforgeeks . org/最长连续序列长度可通过转换 0 从数组形成/](https://www.geeksforgeeks.org/length-of-longest-consecutive-sequence-that-can-be-formed-from-array-by-converting-0s/)

给定一个由 **N** 个整数组成的数组 **arr** ，任务是计算从该数组中可以形成的连续整数的最长序列的长度。还假设数组中的 0 可以转换为任何值。

**示例:**

> **输入:** N = 7，A = {0，6，5，10，3，0，11}
> **输出:** 5
> **说明:**形成的最大连续序列可以是{3，4，5，6，7}。由于数组中没有 4、7，我们可以将 2 个零改为 4 和 7。
> 
> **输入:** N = 6，A = {0，0，1，2，6，0}
> **输出:** 6
> **说明:**形成的最大连续序列可以是{1，2，3，4，5，6}

**方法:**给定问题可以借助[二分搜索法](https://www.geeksforgeeks.org/binary-search/)和[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)解决:

*   计算数组中的零总数，并将它们存储在变量 **count** 中，该变量指示可以进行的所有可能的更改
*   给定数组中的重复值和零值将被删除，以便数组只包含唯一的非零值
*   创建一个辅助数组，并将这些索引值初始化为 1，其值出现在给定数组中
*   辅助数组变成前缀和数组
*   迭代前缀数组，并在每次迭代时执行二分搜索法运算，下限作为当前索引，上限作为数组的最后一个索引
*   让当前指数为 **l** ，最右边的可能指数为 **r** 。对于每个 **mid = (l + r) / 2** ，检查该范围[ **l** ， **mid** ]是否可通过总允许变化实现
*   更新 **l = mid +1** 如果上述说法为真，否则**r = mid–1**
*   计算所有起始值的最大长度

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to calculate maximum
// possible consecutive numbers
// with changes allowed
int maximumConsecutiveNumbers(int arr[], int N)
{
    // Store all non-zero elements
    // in a new vector and
    // calculate total zero elements
    vector<int> v;

    // Variable to store the
    // count of zero elements
    int count = 0;

    for (int i = 0; i < N; i++) {
        if (arr[i] == 0) {
            count++;
        }
        else {
            v.push_back(arr[i]);
        }
    }

    // Sort the array
    sort(v.begin(), v.end());

    // Remove all the duplicates
    // from the array
    (v).erase(unique(v.begin(),
                     v.end()),
              (v).end());

    // Variable to store the maximum
    // value of the sequence
    int MAXN = 1100000;

    // Make the prefix array
    vector<int> pref(MAXN + 1, 0);

    for (int i = 0; i < v.size(); i++) {
        pref[v[i]]++;
    }

    for (int i = 1; i <= MAXN; i++) {
        pref[i] += pref[i - 1];
    }

    int mx = 0;

    // Iterate for each element and
    // use binary search
    for (int i = 1; i <= MAXN; i++) {

        int l = i, r = MAXN;
        int local_max = 0;
        while (l <= r) {
            int mid = (l + r) / 2;

            // Conversions equal to number
            // of zeros, can be made upto mid
            if (pref[mid] - pref[i - 1]
                    + count
                >= (mid - i + 1)) {

                l = mid + 1;
                local_max = max(local_max,
                                mid - i + 1);
            }

            else {
                r = mid - 1;
            }
        }
        mx = max(mx, local_max);
    }
    return mx;
}

// Driver Code
int main()
{
    int N = 7;
    int arr[] = { 0, 6, 5, 10, 3, 0, 11 };
    cout << maximumConsecutiveNumbers(arr, N);
}
```

## 蟒蛇 3

```
# Python 3 implementation for the above approach

# Function to calculate maximum
# possible consecutive numbers
# with changes allowed
def maximumConsecutiveNumbers(arr, N):

    # Store all non-zero elements
    # in a new vector and
    # calculate total zero elements
    v = []

    # Variable to store the
    # count of zero elements
    count = 0

    for i in range(N):
        if(arr[i] == 0):
            count += 1
        else:
            v.append(arr[i])

    # Sort the array
    v.sort()

    # Remove all the duplicates
    # from the array
    v = set(v)
    v = list(v)
    # Variable to store the maximum
    # value of the sequence
    MAXN = 110000

    # Make the prefix array
    pref = [0 for i in range(MAXN+1)]

    for i in range(len(v)):
        pref[v[i]] += 1

    for i in range(1,MAXN+1,1):
        pref[i] += pref[i - 1]

    mx = 0

    # Iterate for each element and
    # use binary search
    for i in range(1,MAXN+1,1):
        l = i
        r = MAXN
        local_max = 0
        while (l <= r):
            mid = (l + r) // 2

            # Conversions equal to number
            # of zeros, can be made upto mid
            if (pref[mid] - pref[i - 1] + count >= (mid - i + 1)):
                l = mid + 1
                local_max = max(local_max,mid - i + 1)

            else:
                r = mid - 1
        mx = max(mx, local_max)
    return mx

# Driver Code
if __name__ == '__main__':
    N = 7
    arr = [0, 6, 5, 10, 3, 0, 11]
    print(maximumConsecutiveNumbers(arr, N))

    # This code is contributed by ipg2016107.
```

## C#

```
// C# implementation for the above approach
using System;
using System.Collections.Generic;
using System.Linq;

class GFG
{

    // Function to calculate maximum
    // possible consecutive numbers
    // with changes allowed
    static int maximumConsecutiveNumbers(int[] arr, int N)
    {
        // Store all non-zero elements
        // in a new vector and
        // calculate total zero elements
        List<int> v = new List<int>();

        // Variable to store the
        // count of zero elements
        int count = 0;

        for (int i = 0; i < N; i++) {
            if (arr[i] == 0) {
                count++;
            }
            else {
                v.Add(arr[i]);
            }
        }

        // Sort the array
        v.Sort();

        // Remove all the duplicates
        // from the array
        List<int> distinct = v.Distinct().ToList();

        // Variable to store the maximum
        // value of the sequence
        int MAXN = 1100000;

        // Make the prefix array
        List<int> pref = new List<int>(new int[MAXN + 1]);

        for (int i = 0; i < distinct.Count; i++) {
            pref[distinct[i]]++;
        }

        for (int i = 1; i <= MAXN; i++) {
            pref[i] += pref[i - 1];
        }

        int mx = 0;

        // Iterate for each element and
        // use binary search
        for (int i = 1; i <= MAXN; i++) {

            int l = i, r = MAXN;
            int local_max = 0;
            while (l <= r) {
                int mid = (l + r) / 2;

                // Conversions equal to number
                // of zeros, can be made upto mid
                if (pref[mid] - pref[i - 1] + count
                    >= (mid - i + 1)) {

                    l = mid + 1;
                    local_max
                        = Math.Max(local_max, mid - i + 1);
                }

                else {
                    r = mid - 1;
                }
            }
            mx = Math.Max(mx, local_max);
        }
        return mx;
    }

    // Driver Code
    public static void Main()
    {
        int N = 7;
        int[] arr = { 0, 6, 5, 10, 3, 0, 11 };
        Console.Write(maximumConsecutiveNumbers(arr, N));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
    // Javascript implementation for the above approach

    // Function to calculate maximum
    // possible consecutive numbers
    // with changes allowed
    const maximumConsecutiveNumbers = (arr, N) => {

       // Store all non-zero elements
        // in a new vector and
        // calculate total zero elements
        let v = [];

        // Variable to store the
        // count of zero elements
        let count = 0;

        for (let i = 0; i < N; i++) {
            if (arr[i] == 0) {
                count++;
            }
            else {
                v.push(arr[i]);
            }
        }

        // Sort the array

        // Remove all the duplicates
        // from the array

        v = [...new Set(v)];

        // Variable to store the maximum
        // value of the sequence
        let MAXN = 1100000;

        // Make the prefix array
        let pref = new Array(MAXN + 1).fill(0);

        for (let i = 0; i < v.length; i++) {
            pref[v[i]]++;
        }

        for (let i = 1; i <= MAXN; i++) {
            pref[i] += pref[i - 1];
        }

        let mx = 0;

        // Iterate for each element and
        // use binary search
        for (let i = 1; i <= MAXN; i++) {

            let l = i, r = MAXN;
            let local_max = 0;
            while (l <= r) {
                let mid = parseInt((l + r) / 2);

                // Conversions equal to number
                // of zeros, can be made upto mid
                if (pref[mid] - pref[i - 1]
                    + count
                    >= (mid - i + 1)) {

                    l = mid + 1;
                    local_max = Math.max(local_max,
                        mid - i + 1);
                }

                else {
                    r = mid - 1;
                }
            }
            mx = Math.max(mx, local_max);
        }
        return mx;
    }

    // Driver Code
    let N = 7;
    let arr = [0, 6, 5, 10, 3, 0, 11];

    document.write(maximumConsecutiveNumbers(arr, N))

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
5
```

**时间复杂度:** O(N*log(K))，其中 K 为数组中最大值
T3】辅助空间: O(N)