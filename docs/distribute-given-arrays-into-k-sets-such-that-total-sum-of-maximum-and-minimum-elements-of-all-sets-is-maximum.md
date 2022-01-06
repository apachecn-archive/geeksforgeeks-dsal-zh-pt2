# 将给定的数组分配到 K 个集合中，使得所有集合的最大和最小元素的总和最大

> 原文:[https://www . geeksforgeeks . org/将给定数组分布到 k 个集合中，这样所有集合中最大和最小元素的总和就是最大值/](https://www.geeksforgeeks.org/distribute-given-arrays-into-k-sets-such-that-total-sum-of-maximum-and-minimum-elements-of-all-sets-is-maximum/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)，第一个 **arr[]** 大小为 **N** ，第二个 **brr[]** 大小为 **K** 。任务是将第一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 分成 **K** 个集合，使得第**I**个集合应该包含来自第二个[数组](https://www.geeksforgeeks.org/array-data-structure/) **brr[]** 的 **brr[i]** 个元素，所有集合的最大和最小元素之和最大。

**示例:**

> **输入:** n = 4，k = 2，arr[] = {10，10，11，11 }，brr[] = {2，2 }
> **输出:** 42
> **说明:**第一组= 10 ^ 11，最大值和最小值之和= 21，第二组= 10 ^ 11，最大值和最小值之和= 21。总和= 42(最大可能)
> 
> **输入:** n = 4，k = 4，arr[] = {10，10，10，10}，brr[] = {1，1，1，1 }
> T3】输出: 42

**方法:**给最大的元素设置大小=1。其余部分，[按照降序排列](https://www.geeksforgeeks.org/quick-sort/)[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，按照升序排列 **brr[]** 。现在，如果集合的大小不是 1，那么将最小元素添加到答案中。按照以下步骤解决问题:

*   [按降序排列](https://www.geeksforgeeks.org/quick-sort/)[阵列](https://www.geeksforgeeks.org/array-data-structure/)、**阵列[]** ，按升序排列 **brr[]** 。
*   初始化变量 say **ans** 为 **0** 存储答案的值， **cnt** 为 **0** 计数大小为 1 的集数。
*   [在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**内迭代，计算大小为 1 的集合数量，并将该值存储在变量 **cnt 中。**
*   [在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**范围内迭代，执行以下步骤。
    *   将 **arr[i]** 的值添加到变量**和**中，因为值 **arr[i]** 将是第**I-第**组的最大值。
    *   如果 **cnt** 的值大于 0，则再次将值**arr【I】**相加，因为它也是最小值，并将 **cnt** 的值减去 1。
*   将变量**从**初始化为 **K** 来维护计数器。
*   [在](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K】**范围内迭代，执行以下步骤。
    *   如果 **brr[i]** 的值为 **1、**，则[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
    *   将**arr[from+brr[I]–2]【T1]的值添加到答案中。**
    *   将**的值从**增加 **brr[i]-1。**
*   打印答案的最终值。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

typedef long long ll;

// Function to find K sets such that the
// sum of maximum and minimum of all sets
// is maximum
void findSets(int n, int k, vector<int>& arr,
              vector<int>& brr)
{
    ll ans = 0;

    // Sort both the arrays
    // arr[] in descending order.
    // brr[] in ascending order.
    sort(arr.begin(), arr.end());
    sort(brr.begin(), brr.end());
    reverse(arr.begin(), arr.end());

    int cnt = 0;

    // Count the number of sets with size 1
    for (int& v : brr) {
        if (v == 1)
            cnt++;
    }

    // Assign the first K maximum elements
    // to the sets and add them as minimum
    // also for sets with size 1.
    for (int i = 0; i < k; i++) {
        ans += arr[i];
        if (cnt > 0) {
            ans += arr[i];
            cnt--;
        }
    }

    int from = k;
    // Add the minimum element from the set.
    for (int i = 0; i < k; i++) {
        if (brr[i] == 1)
            continue;
        ans += arr[from + brr[i] - 2];
        from += brr[i] - 1;
    }

    cout << ans << '\n';
}

// Driver Code
int main()
{
    int n, k;

    n = 4;
    k = 2;

    vector<int> arr{ 10, 10, 11, 11 };
    vector<int> brr{ 2, 2 };

    findSets(n, k, arr, brr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.Arrays;
import java.util.Collections;

// C++ program for the above approach
class GFG {

    // Function to find K sets such that the
    // sum of maximum and minimum of all sets
    // is maximum
    public static void findSets(int n, int k, int[] arr, int[] brr) {
        int ans = 0;

        // Sort both the arrays
        // arr[] in descending order.
        // brr[] in ascending order.
        Arrays.sort(arr);
        Arrays.sort(brr);

        Collections.reverse(Arrays.asList(arr));

        int cnt = 0;

        // Count the number of sets with size 1
        for (int v : brr) {
            if (v == 1)
                cnt++;
        }

        // Assign the first K maximum elements
        // to the sets and add them as minimum
        // also for sets with size 1.
        for (int i = 0; i < k; i++) {
            ans += arr[i];
            if (cnt > 0) {
                ans += arr[i];
                cnt--;
            }
        }

        int from = k;
        // Add the minimum element from the set.
        for (int i = 0; i < k; i++) {
            if (brr[i] == 1)
                continue;
            ans += arr[from + brr[i] - 2];
            from += brr[i] - 1;
        }

        System.out.println(ans);
    }

    // Driver Code
    public static void main(String args[]) {
        int n, k;

        n = 4;
        k = 2;

        int[] arr = { 10, 10, 11, 11 };
        int[] brr = { 2, 2 };

        findSets(n, k, arr, brr);

    }

}

// This code is contributed by gfgking.
```

## 蟒蛇 3

```
# python 3 program for the above approach
# Function to find K sets such that the
# sum of maximum and minimum of all sets
# is maximum
def findSets(n, k, arr, brr):
    ans = 0

    # Sort both the arrays
    # arr[] in descending order.
    # brr[] in ascending order.
    arr.sort()
    brr.sort()
    arr = arr[:-1]

    cnt = 0

    # Count the number of sets with size 1
    for v in brr:
        if (v == 1):
            cnt += 1

    # Assign the first K maximum elements
    # to the sets and add them as minimum
    # also for sets with size 1.
    for i in range(k):
        ans += arr[i]
        if (cnt > 0):
            ans += arr[i]
            cnt -= 1

    from1 = k
    # Add the minimum element from the set.
    for i in range(k):
        if (brr[i] == 1):
            continue
        if from1 + brr[i] - 2>len(arr)-1:
            continue;
        ans += arr[from1 + brr[i] - 2]
        from1 += brr[i] - 1

    print(ans)

# Driver Code
if __name__ == '__main__':
    n = 4
    k = 2

    arr =  [10, 10, 11, 11]
    brr =  [2, 2]
    findSets(n, k, arr, brr)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find K sets such that the
// sum of maximum and minimum of all sets
// is maximum
static void findSets(int n, int k, List<int> arr,
              List<int> brr)
{
    int ans = 0;

    // Sort both the arrays
    // arr[] in descending order.
    // brr[] in ascending order.
    arr.Sort();
    brr.Sort();
    arr.Reverse();

    int cnt = 0;

    // Count the number of sets with size 1
    foreach (int v in brr) {
        if (v == 1)
            cnt++;
    }

    // Assign the first K maximum elements
    // to the sets and add them as minimum
    // also for sets with size 1.
    for (int i = 0; i < k; i++) {
        ans += arr[i];
        if (cnt > 0) {
            ans += arr[i];
            cnt--;
        }
    }

    int from = k;
    // Add the minimum element from the set.
    for (int i = 0; i < k; i++) {
        if (brr[i] == 1)
            continue;
        ans += arr[from + brr[i] - 2];
        from += brr[i] - 1;
    }

    Console.Write(ans);
}

// Driver Code
public static void Main()
{
    int n, k;

    n = 4;
    k = 2;

    List<int> arr = new List<int>(){ 10, 10, 11, 11 };
    List<int> brr = new List<int>(){ 2, 2 };

    findSets(n, k, arr, brr);
}
}

// This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find K sets such that the
        // sum of maximum and minimum of all sets
        // is maximum
        function findSets(n, k, arr, brr)
        {
            let ans = 0;

            // Sort both the arrays
            // arr[] in descending order.
            // brr[] in ascending order.
            arr.sort((a, b) => a - b);
            brr.sort((a, b) => a - b);

            arr.reverse();

            let cnt = 0;

            // Count the number of sets with size 1
            for (let v of brr) {
                if (v == 1)
                    cnt++;
            }

            // Assign the first K maximum elements
            // to the sets and add them as minimum
            // also for sets with size 1.
            for (let i = 0; i < k; i++) {
                ans += arr[i];
                if (cnt > 0) {
                    ans += arr[i];
                    cnt--;
                }
            }

            let from = k;
            // Add the minimum element from the set.
            for (let i = 0; i < k; i++) {
                if (brr[i] == 1)
                    continue;
                ans += arr[from + brr[i] - 2];
                from += brr[i] - 1;
            }

            document.write(ans);
        }

        // Driver Code
        let n, k;

        n = 4;
        k = 2;

        let arr = [10, 10, 11, 11];
        let brr = [2, 2];

        findSets(n, k, arr, brr);

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
42
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(1)*