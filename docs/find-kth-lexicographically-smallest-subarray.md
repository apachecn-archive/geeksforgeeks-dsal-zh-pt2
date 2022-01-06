# 查找第 k 个字典最小子阵列

> 原文:[https://www . geeksforgeeks . org/find-kth-按字典顺序排列-最小-subarray/](https://www.geeksforgeeks.org/find-kth-lexicographically-smallest-subarray/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是从字典顺序上找到给定数组的第 K 个<sup>个最小子集。</sup>

**示例:**

> **输入:** arr[] = {5，15}，K = 2
> **输出:** 5 15
> **解释:**给定集合的子集按字典顺序为{5}、{5，15}和{15}。因此，第二个最小子集是{5，15}。
> 
> **输入:** arr[] = {1，2，3，4}，K = 5
> T3】输出: 1 2 4

**方法:**给定的问题可以通过生成给定数组的所有[幂集](https://www.geeksforgeeks.org/power-set/)并随后在字典顺序 r 中排序[幂集的子集来解决。因此，排序的幂集的 **K <sup>第</sup>** 索引处的子集是所需的答案。](https://www.geeksforgeeks.org/powet-set-lexicographic-order/)

下面是上述方法的实现:

## C++

```
// C++ Program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the power set of the
// given array
vector<vector<int> > powerSet(int* arr, int N)
{
    int pow1 = pow(2, N);

    // Stores the power set
    vector<vector<int> > v;

    // Loop to iterate over all elements of
    // the power set
    for (int count = 0; count < pow1; count++) {

        // Stores the current subset
        vector<int> temp;
        for (int j = 0; j < N; j++) {
            if (count & (1 << j)) {
                temp.push_back(arr[j]);
            }
        }

        // Sorting the current subset
        sort(temp.begin(), temp.end());
        if (count != 0) {
            v.push_back(temp);
        }
    }

    // Return Power Ser
    return v;
}

// Function to find the
// Kth lexicographic smallest
// subset of the given array
vector<int> kthSmallestSubset(
    int* arr, int N, int K)
{
    // Stores the power set
    vector<vector<int> > powSet
        = powerSet(arr, N);

    // Sort the power set
    // in lexicographic order
    sort(powSet.begin(), powSet.end());

    // Return Answer
    return powSet[K - 1];
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);
    int K = 5;

    vector<int> ans
        = kthSmallestSubset(arr, N, K);
    for (auto x : ans) {
        cout << x << " ";
    }
}
```

## 蟒蛇 3

```
# Python Program of the above approach

# Function to find the power set of the
# given array
def powerSet(arr, N):
  pow1 = 2 ** N

  # Stores the power set
  v = [];

  # Loop to iterate over all elements of
  # the power set
  for count in range(pow1):

    # Stores the current subset
    temp = []
    for j in range(N):
      if (count & (1 << j)):
        temp.append(arr[j]);

    # Sorting the current subset
    temp.sort();
    if (count != 0):
      v.append(temp);

  # Return Power Ser
  return v;

# Function to find the
# Kth lexicographic smallest
# subset of the given array
def kthSmallestSubset(arr, N, K):

  # Stores the power set
  powSet = powerSet(arr, N);

  # Sort the power set
  # in lexicographic order
  powSet.sort();

  # Return Answer
  return powSet[K - 1];

# Driver Code
arr = [1, 2, 3, 4];
N = len(arr)
K = 5;

ans = kthSmallestSubset(arr, N, K);
for x in ans:
  print(x, end=" ");

  # This code is contributed by gfgking.
```

## java 描述语言

```
<script>
// Javascript Program of the above approach

// Function to find the power set of the
// given array
function powerSet(arr, N) {
  let pow1 = Math.pow(2, N);

  // Stores the power set
  let v = [];

  // Loop to iterate over all elements of
  // the power set
  for (let count = 0; count < pow1; count++) {

    // Stores the current subset
    let temp = [];
    for (let j = 0; j < N; j++) {
      if (count & (1 << j)) {
        temp.push(arr[j]);
      }
    }

    // Sorting the current subset
    temp.sort();
    if (count != 0) {
      v.push(temp);
    }
  }

  // Return Power Ser
  return v;
}

// Function to find the
// Kth lexicographic smallest
// subset of the given array
function kthSmallestSubset(arr, N, K) {
  // Stores the power set
  let powSet = powerSet(arr, N);

  // Sort the power set
  // in lexicographic order
  powSet.sort();

  // Return Answer
  return powSet[K - 1];
}

// Driver Code

let arr = [1, 2, 3, 4];
let N = arr.length;
let K = 5;

let ans = kthSmallestSubset(arr, N, K);
for (x of ans) {
  document.write(x + " ");
}

// This code is contributed by gfgking.
</script>
```

**Output**

```
1 2 4 
```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:** O(2 <sup>N</sup> )*