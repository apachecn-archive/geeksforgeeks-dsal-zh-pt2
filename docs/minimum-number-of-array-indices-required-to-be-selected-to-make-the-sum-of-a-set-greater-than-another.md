# 使一个集合的和大于另一个集合所需选择的最小数组索引数

> 原文:[https://www . geeksforgeeks . org/最小数组索引数-需要选择才能使集合之和大于另一个/](https://www.geeksforgeeks.org/minimum-number-of-array-indices-required-to-be-selected-to-make-the-sum-of-a-set-greater-than-another/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** 和 **brr[]** 大小为 **N** 和一个整数 **K** 。考虑两套 **A** ，初始包含 **K** ，初始为空的 **B** 。在每个操作中，需要选择一个索引。对于每个选定的指标，说 **i** 、**arr【I】**和**brr【I】**被添加到 **B** 中。对于每一个未选择的指标， **arr[i]** 被添加到 **A.** 任务是找到使 **B** 之和大于 **A** 之和所需选择的最小指标数。如果不可能，则打印-1。

**示例:**

> **输入:** arr[] = {3，2，5，6}，brr[] = {4，4，2，3}，K = 12
> **输出:** 3
> 4 3 1
> **说明:**选择指数 2，3 和 0。B = arr[0]+brr[0]+arr[2]+brr[2]+arr[3]+brr[3]= 3+4+5+2+6+3 = 23 的和。A = K + arr[1] = 12 + 2 = 14 的和。
> 
> **输入:** arr[] = {3，2，5，6}，brr[] = {4，4，2，3}，K = 34
> **输出:** -1

**进场:**思路是用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)。按照以下步骤解决问题:

*   初始化一对 **B[]** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)来跟踪索引。
*   初始化一个变量， **A** 用 **K** 来存储设置 **A** 的值。
*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**，
    *   如果没有选择指数，将值**arr【I】**加到 **A** 上。
    *   在向量 **B** 中插入 **{brr[i] + 2 * arr[i]，i}** 作为[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)。
*   [排序向量**B**T3】按降序排列。](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)
*   初始化向量**和**来存储选择的索引。
*   一边循环一边运行[，并继续选择指数，直到 **A 的**值大于 **B 的**。](https://www.geeksforgeeks.org/c-c-while-loop-with-examples/)
*   如果选择了所有指标但 **B 的**值仍小于 **A** ，则打印**-1”**。
*   否则，将向量**和**的大小打印为最小移动次数。
*   [遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)、**和**，打印选择的索引。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum number
// of indices required to be selected
void numberOfIndexes(int arr[], int brr[],
                     int N, int K)
{
    // Declare vector to keep track of indexes
    vector<pair<int, int> > B;

    // Set A contains K
    int A = K;

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Adding value that set A can
        // get if no index was chosen
        A += arr[i];

        // Insert as B's value
        B.push_back({ brr[i] + 2 * arr[i], i });
    }

    // Sort the vector
    sort(B.begin(), B.end());

    // Reverse the vector
    reverse(B.begin(), B.end());

    int tot = 0, idx = 0;

    // Stores chosen indexes
    vector<int> ans;

    // Keep on choosing more indices until
    // B's value is bigger than A or stop
    // incase all the indexes is chosen
    while (A >= tot && idx < B.size()) {

        // Update tot
        tot += B[idx].first;

        // Update ans
        ans.push_back(B[idx].second);

        // Increment idx
        idx++;
    }

    // If all indices are selected and
    // sum of B is less than sum of A
    if (tot <= A) {
        cout << -1 << endl;
        return;
    }

    // Print the minimum number of indices
    cout << ans.size() << endl;

    // Print chosen indices
    for (auto c : ans)
        cout << c + 1 << " ";
}

// Driver Code
int main()
{
    // Given arrays
    int arr[] = { 3, 2, 5, 6 };
    int brr[] = { 4, 4, 2, 3 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Given value of K
    int K = 12;

    // Function Call
    numberOfIndexes(arr, brr, N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to print the minimum number
# of indices required to be selected
def numberOfIndexes(arr, brr, N, K):

    # Declare vector to keep track of indexes
    B = []

    # Set A contains K
    A = K

    # Traverse the array
    for i in range(N):

        # Adding value that set A can
        # get if no index was chosen
        A += arr[i]

        # Insert as B's value
        B.append([brr[i] + 2 * arr[i], i])

    # Sort the vector
    B.sort()

    # Reverse the vector
    B = B[::-1]
    tot = 0
    idx = 0

    # Stores chosen indexes
    ans = []

    # Keep on choosing more indices until
    # B's value is bigger than A or stop
    # incase all the indexes is chosen
    while (A >= tot and idx < len(B)):

        # Update tot
        tot += B[idx][0]

        # Update ans
        ans.append(B[idx][1])

        # Increment idx
        idx += 1

    # If all indices are selected and
    # sum of B is less than sum of A
    if (tot <= A):
        print(-1)
        return

    # Print the minimum number of indices
    print(len(ans))

    # Print chosen indices
    for c in ans:
        print(c + 1,end = " ")

# Driver Code
if __name__ == '__main__':

    # Given arrays
    arr = [3, 2, 5, 6]
    brr = [4, 4, 2, 3]

    # Size of the array
    N = len(arr)

    # Given value of K
    K = 12

    # Function Call
    numberOfIndexes(arr, brr, N, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to print the minimum number
// of indices required to be selected
function numberOfIndexes(arr, brr, N, K) {
  // Declare vector to keep track of indexes
  let B = [];

  // Set A contains K
  let A = K;

  // Traverse the array
  for (let i = 0; i < N; i++) {
    // Adding value that set A can
    // get if no index was chosen
    A += arr[i];

    // Insert as B's value
    B.push([brr[i] + 2 * arr[i], i]);
  }

  // Sort the vector

  // Reverse the vector
  B.sort((a, b) => a[0] - b[0]).reverse();

  let tot = 0,
    idx = 0;

  // Stores chosen indexes
  let ans = [];

  // Keep on choosing more indices until
  // B's value is bigger than A or stop
  // incase all the indexes is chosen
  while (A >= tot && idx < B.length) {
    // Update tot
    tot += B[idx][0];

    // Update ans
    ans.push(B[idx][1]);

    // Increment idx
    idx++;
  }

  // If all indices are selected and
  // sum of B is less than sum of A
  if (tot <= A) {
    document.write(-1 + "<br>");
    return;
  }

  // Print the minimum number of indices
  document.write(ans.length + "<br>");
  // Print chosen indices
  for (let c of ans) document.write(Number(c) + 1 + " ");
}

// Driver Code

// Given arrays
let arr = [3, 2, 5, 6];
let brr = [4, 4, 2, 3];

// Size of the array
let N = arr.length;

// Given value of K
let K = 12;

// Function Call
numberOfIndexes(arr, brr, N, K);

</script>
```

**Output:** 

```
3
4 3 1
```

***时间复杂度:** O(N*log(N))*
***辅助空间:** O(N)*