# 最大化由给定类型和百搭牌组成的牌组数量

> 原文:[https://www . geeksforgeeks . org/最大化给定类型和百搭牌可以形成的牌组数/](https://www.geeksforgeeks.org/maximize-card-deck-count-that-can-be-formed-from-cards-of-given-type-and-joker/)

给定一个整数 **N** 表示特定副牌中的牌数，以及一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，其中 **i** 第一个元素表示第 **i** 种牌的频率。也给 **K** 开玩笑。任务是用给定的数据找到最大可能的有效套牌。

有效的套牌应符合上述两个条件之一:
**1。**一副牌，每种类型正好包含**一张牌，不开玩笑。**
**2。**一副牌，除了一张之外，每种类型正好包含**一张牌，正好包含一张百搭牌。**

**示例**:

> **输入** : N = 2，arr[] = {10，15}，K = 3
> **输出** : 13
> **说明**:以下是 13 副牌的制作方式:
> 10 副{1，2}
> 3 副{J，2}
> 因此最大可能副牌数为 10 + 3 = 13 副。
> 
> **输入** : N = 3，arr[] = {1，2，3}，K = 4
> **输出** : 3
> **说明**:以下是 13 副牌的制作方式:
> 1 副{1，2，3}
> 1 副{J，2，3}
> 1 副{J，2，3 }
> 1 副因此最大可能副牌数为 1+1+1 = 3 副。

**逼近**:给定问题可以使用[贪婪逼近](https://www.geeksforgeeks.org/greedy-algorithms/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)算法求解。按照以下步骤解决给定的问题。

*   [按非递减顺序对给定数组](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/) **arr[]** 进行排序。
*   [二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以应用在答案上得到最大值。
*   初始化两个变量，比如说 **L** = **0** 和**R**=**max _ element(arr)+K+1**，这将定义要找出的答案的初始范围。
*   一边迭代一边 **L +1 < R**
    *   初始化一个变量，比如 **mid = (L + R)/2** 来跟踪每次迭代中范围内的中间元素。
    *   使用变量表示，**需要= 0** 来计算当前中间**T5】元素所需的额外卡片。**
    *   [用变量 **i** 迭代整个数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **arr[]** :
        *   如果 **arr[i] < mid** 设置**need = need+arr[I]–mid。**
        *   如果**需要< =中****需要< = k** ，则设置 **L =中**。
        *   否则设置 **R =中间**。
*   最后最终答案将存储在 **L** 中，因此返回 **L** 作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum possible decks
// with given frequency of cards and
// number of jokers
int maximumCardDecks(int arr[], int n, int k)
{
    // Sort the whole array
    sort(arr, arr + n);
    // Store the binary search range

    int L = 0;
    int R = arr[n - 1] + k + 1;

    // Do a binary search on range
    while (L + 1 < R) {
        // Compute the mid value of the current
        // binary search range
        int mid = (L + R) / 2;

        // Store extra needed
        int need = 0;

        // Iterate over the total cards and
        // compute variable need.
        for (int i = 0; i < n; i++) {
            if (arr[i] < mid) {
                need += mid - arr[i];
            }
        }
        if (need <= mid && need <= k) {
            L = mid;
        }
        else {
            R = mid;
        }
    }
    return L;
}

// Driver Code
int main()
{
    int N = 3, K = 4;
    int arr[] = { 1, 2, 3 };
    cout << maximumCardDecks(arr, N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.Arrays;
class GFG
{

// Function to find maximum possible decks
// with given frequency of cards and
// number of jokers
static int maximumCardDecks(int arr[], int n, int k)
{

    // Sort the whole array
    Arrays.sort(arr);

    // Store the binary search range
    int L = 0;
    int R = arr[n - 1] + k + 1;

    // Do a binary search on range
    while (L + 1 < R)
    {

        // Compute the mid value of the current
        // binary search range
        int mid = (L + R) / 2;

        // Store extra needed
        int need = 0;

        // Iterate over the total cards and
        // compute variable need.
        for (int i = 0; i < n; i++) {
            if (arr[i] < mid) {
                need += mid - arr[i];
            }
        }
        if (need <= mid && need <= k) {
            L = mid;
        }
        else {
            R = mid;
        }
    }
    return L;
}

// Driver Code
public static void main (String[] args)
{
    int N = 3, K = 4;
    int arr[] = { 1, 2, 3 };
    System.out.print(maximumCardDecks(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to find maximum possible decks
# with given frequency of cards and
# number of jokers
def maximumCardDecks(arr, n, k):

    # Sort the whole array
    arr.sort()

    # Store the binary search range
    L = 0
    R = arr[n - 1] + k + 1

    # Do a binary search on range
    while (L + 1 < R) :

        # Compute the mid value of the current
        # binary search range
        mid = (L + R) // 2

        # Store extra needed
        need = 0

        # Iterate over the total cards and
        # compute variable need.
        for i in range(n):
            if (arr[i] < mid):
                need += mid - arr[i]

        if (need <= mid and need <= k):
            L = mid
        else:
            R = mid

    return L

# Driver Code
N = 3
K = 4
arr = [1, 2, 3]
print(maximumCardDecks(arr, N, K))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
class GFG
{

// Function to find maximum possible decks
// with given frequency of cards and
// number of jokers
static int maximumCardDecks(int []arr, int n, int k)
{

    // Sort the whole array
    Array.Sort(arr);

    // Store the binary search range
    int L = 0;
    int R = arr[n - 1] + k + 1;

    // Do a binary search on range
    while (L + 1 < R)
    {

        // Compute the mid value of the current
        // binary search range
        int mid = (L + R) / 2;

        // Store extra needed
        int need = 0;

        // Iterate over the total cards and
        // compute variable need.
        for (int i = 0; i < n; i++) {
            if (arr[i] < mid) {
                need += mid - arr[i];
            }
        }
        if (need <= mid && need <= k) {
            L = mid;
        }
        else {
            R = mid;
        }
    }
    return L;
}

// Driver Code
public static void Main (String[] args)
{
    int N = 3, K = 4;
    int []arr = { 1, 2, 3 };
    Console.Write(maximumCardDecks(arr, N, K));
}
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find maximum possible decks
        // with given frequency of cards and
        // number of jokers
        function maximumCardDecks(arr, n, k)
        {

            // Sort the whole array
            arr.sort(function (a, b) { return a - b })

            // Store the binary search range

            let L = 0;
            let R = arr[n - 1] + k + 1;

            // Do a binary search on range
            while (L + 1 < R) {
                // Compute the mid value of the current
                // binary search range
                let mid = (L + R) / 2;

                // Store extra needed
                let need = 0;

                // Iterate over the total cards and
                // compute variable need.
                for (let i = 0; i < n; i++) {
                    if (arr[i] < mid) {
                        need += mid - arr[i];
                    }
                }
                if (need <= mid && need <= k) {
                    L = mid;
                }
                else {
                    R = mid;
                }
            }
            return L;
        }

        // Driver Code

        let N = 3, K = 4;
        let arr = [1, 2, 3];
        document.write(maximumCardDecks(arr, N, K));

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

**时间复杂度** : O(N(log(N) + log(M + K))，其中 M 是数组的最大元素。
**辅助空间:** O(1)