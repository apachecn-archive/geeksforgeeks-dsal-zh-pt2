# 使用最大元素到达所有阵列元素所需的最小跳跃

> 原文:[https://www . geeksforgeeks . org/最小跳转-需要到达所有数组元素-使用最大元素/](https://www.geeksforgeeks.org/minimum-jumps-required-to-reach-all-array-elements-using-largest-element/)

给定一个由 **N** 个不同整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ， 任务是找到从[最大元素](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)到达所有数组元素所需的最小跳转次数，以便如果**arr【I】**的值大于**arr【j】**并且**arr【j】**的值大于**arr【I】**之间的所有其他元素，则可以从 **i <sup>第</sup>元素跳转到**元素

**示例:**

> **输入:** arr[] = {1，3，6，5}
> **输出:**【2，1，0，1】
> **说明:**
> 以下是到达各平台所需的跳跃:
> 
> *   对于第一个平台，需要从第三个平台跳到第二个平台，然后跳到第一个平台。因此，总共需要 2 次跳跃。
> *   对于第二平台，需要从第三平台直接跳到第二平台。因此，总共需要 1 次跳跃。
> *   对于第三平台，我们已经在第三平台上了。因此，总共需要 0 次跳跃。
> *   对于第四平台，需要从第三平台直接跳到第四平台。因此，总共需要 1 次跳跃。
> 
> **输入:** arr[] = {3，5}
> **输出:**【1，0】

**方法:**给定的问题可以使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)来解决，该动态规划基于从最大元素到第 **i <sup>第</sup>T7】元素的最小跳跃可能比左边或右边的下一个较大元素所需的最小跳跃大一个。因此，这个想法是预先计算较大元素的结果，并使用它们来寻找较小元素的答案。按照以下步骤解决给定的问题:**

*   对于每个数组元素**arr【I】**存储两个索引 **L** 和 **R** ，分别表示[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中左侧和右侧的下一个较大元素[的索引。](https://www.geeksforgeeks.org/next-greater-element/)
*   [按降序排列数组**arr[]**](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)。
*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**和**，它存储所有数组元素的最小跳跃。
*   [遍历数组**arr【】**T3】并执行以下步骤:](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)
    *   如果当前数组元素是最大的元素，那么当前元素需要 **0** 跳跃。
    *   [使用地图中存储的值，找到当前元素左侧](https://www.geeksforgeeks.org/distance-from-next-greater-element/)和右侧下一个较大元素的距离。将距离分别存储在变量 **L** 和 **R** 中。
    *   更新最小跳跃值，按照以下标准说 **M** :
        *   如果 L 至少为 0，R 小于 N，那么 M 的值为 min(ans[L]，ans[R]) + 1。
        *   如果 L 小于 0，R 小于 N，那么 M 的值就是 ans[R] + 1。
        *   如果 L 至少为 0，R 至少为 N，那么 M 的值就是 ans[L] + 1。
    *   将当前索引的最小跳跃值更新为 **M** 的值。
*   完成上述步骤后，打印数组**和**作为索引的跳转结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;
#define ar array

// Function to find next greater element
// to left and right of current element
ar<int, 2> expand(int idx, vector<int>& A)
{

    // Starting l and r from previous
    // and the next element of the
    // current element
    int l = idx - 1;
    int r = idx + 1;

    // FInd the next greater element
    // to the left
    while (l >= 0) {

        if ((int)(A[idx]) > A[l]) {
            --l;
        }
        else {
            break;
        }
    }

    if (l < 0 || l == idx) {
        l = -2;
    }

    // Find the next greater element
    // to the right
    while (r < (int)(A.size())) {
        if ((int)A[idx] > A[r]) {
            ++r;
        }
        else {
            break;
        }
    }

    if (r >= (int)(A.size()) || r == idx) {
        r = -2;
    }

    // Return l and r in the form of
    // array of size 2
    return { l, r };
}

// Function to find the minimum jumps
// required to reach to all elements from
// the largest element
vector<int> minJumps(int N, vector<int>& A)
{
    vector<int> ans(N, 0);

    // Stores the mapping from index
    // to the element in array A[]
    map<int, ar<int, 2> > mp;

    map<int, int> iToA;
    map<int, int> AToi;

    // Stores largest array element
    int big = A[0];

    // Find the two indices l, r such
    // that A[l] > A[i] < A[r] and
    // l<i<r using expand function
    for (int i = 0; i < N; ++i) {
        big = max({ big, A[i] });
        mp[i] = expand(i, A);

        iToA[i] = A[i];
        AToi[A[i]] = i;
    }

    // sorting A in descending order
    sort(A.begin(), A.end(), greater<int>());

    for (int i = 0; i < A.size(); ++i) {

        // Stores the resultant minimum
        // jumps required
        int m;

        // Check if the current element
        // is largest or not
        if (A[i] == big) {
            int cur = AToi[A[i]];
            ans[cur] = 0;
            continue;
        }

        // Find the answer to the
        // current element
        int cur = AToi[A[i]];
        int l = mp[cur][0];
        int r = mp[cur][1];

        if (l >= 0 && r < N) {
            m = min(ans[l], ans[r]) + 1;
        }
        else if (l < 0 && r < N) {
            m = ans[r] + 1;
        }
        else if (l >= 0 && r >= N) {
            m = ans[l] + 1;
        }

        // Update the resultant minimum
        // jumps for the current element
        ans[cur] = m;
    }

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 5, 1, 3, 4, 7 };
    int N = arr.size();

    vector<int> out = minJumps(N, arr);

    // Print the result
    for (auto& it : out)
        cout << it << ' ';

    return 0;
}
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to find next greater element
# to left and right of current element
def expand(idx, A):

    # Starting l and r from previous
    # and the next element of the
    # current element
    l = idx - 1
    r = idx + 1

    # FInd the next greater element
    # to the left
    while (l >= 0):
        if (A[idx] > A[l]):
          l -= 1
        else:
          break

    if (l < 0 or l == idx):
        l = -2

    # Find the next greater element
    # to the right
    while (r < len(A)):
        if (A[idx] > A[r]):
            r += 1
        else:
            break

    if (r >= len(A) or r == idx):
        r = -2

    # Return l and r in the form of
    # array of size 2
    return [l, r]

# Function to find the minimum jumps
# required to reach to all elements from
# the largest element
def minJumps(N, A):
    ans = [0 for i in range(N)]

    # Stores the mapping from index
    # to the element in array A[]
    mp = {}

    iToA = {}
    AToi = {}

    # Stores largest array element
    big = A[0]

    # Find the two indices l, r such
    # that A[l] > A[i] < A[r] and
    # l<i<r using expand function
    for i in range(N):
        big = max(big, A[i])
        mp[i] = expand(i, A)

        iToA[i] = A[i]
        AToi[A[i]] = i

    # sorting A in descending order
    A = sorted(A, reverse=True)

    for i in range(len(A)):
        # Stores the resultant minimum
        # jumps required
        m = None

        # Check if the current element
        # is largest or not
        if (A[i] == big):
            cur = AToi[A[i]]
            ans[cur] = 0
            continue

        # Find the answer to the
        # current element
        cur = AToi[A[i]]
        l = mp[cur][0]
        r = mp[cur][1]

        if (l >= 0 and r < N):
            m = min(ans[l], ans[r]) + 1
        elif (l < 0 and r < N):
            m = ans[r] + 1
        elif (l >= 0 and r >= N):
            m = ans[l] + 1

        # Update the resultant minimum
        # jumps for the current element
        ans[cur] = m

    # Return the result
    return ans

# Driver Code
arr = [5, 1, 3, 4, 7]
N = len(arr)

out = minJumps(N, arr)

# Prlet the result
for it in out:
    print(it, end=" ")

    # This code is contributed by saurabh_jaiswal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find next greater element
// to left and right of current element
function expand(idx, A)
{

  // Starting l and r from previous
  // and the next element of the
  // current element
  let l = idx - 1;
  let r = idx + 1;

  // FInd the next greater element
  // to the left
  while (l >= 0) {
    if (A[idx] > A[l]) {
      --l;
    } else {
      break;
    }
  }

  if (l < 0 || l == idx) {
    l = -2;
  }

  // Find the next greater element
  // to the right
  while (r < A.length) {
    if (A[idx] > A[r]) {
      ++r;
    } else {
      break;
    }
  }

  if (r >= A.length || r == idx) {
    r = -2;
  }

  // Return l and r in the form of
  // array of size 2
  return [l, r];
}

// Function to find the minimum jumps
// required to reach to all elements from
// the largest element
function minJumps(N, A) {
  let ans = new Array(N).fill(0);

  // Stores the mapping from index
  // to the element in array A[]
  let mp = new Map();

  let iToA = new Map();
  let AToi = new Map();

  // Stores largest array element
  let big = A[0];

  // Find the two indices l, r such
  // that A[l] > A[i] < A[r] and
  // l<i<r using expand function
  for (let i = 0; i < N; ++i) {
    big = Math.max(big, A[i]);
    mp.set(i, expand(i, A));

    iToA.set(i, A[i]);
    AToi.set(A[i], i);
  }

  // sorting A in descending order
  A.sort((a, b) => - a + b);

  for (let i = 0; i < A.length; ++i) {
    // Stores the resultant minimum
    // jumps required
    let m;

    // Check if the current element
    // is largest or not
    if (A[i] == big) {
      let cur = AToi.get(A[i]);
      ans[cur] = 0;
      continue;
    }

    // Find the answer to the
    // current element
    let cur = AToi.get(A[i]);
    let l = mp.get(cur)[0];
    let r = mp.get(cur)[1];

    if (l >= 0 && r < N) {
      m = Math.min(ans[l], ans[r]) + 1;
    } else if (l < 0 && r < N) {
      m = ans[r] + 1;
    } else if (l >= 0 && r >= N) {
      m = ans[l] + 1;
    }

    // Update the resultant minimum
    // jumps for the current element
    ans[cur] = m;
  }

  // Return the result
  return ans;
}

// Driver Code

let arr = [5, 1, 3, 4, 7];
let N = arr.length;

let out = minJumps(N, arr);

// Print the result
for (it of out) document.write(it + " ");

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
1 2 2 1 0
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*