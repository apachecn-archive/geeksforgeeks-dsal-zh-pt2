# 最长子阵列，其元素可以通过最大 K 增量相等

> 原文:[https://www . geeksforgeeks . org/最长子数组-其元素可以按最大 k 增量进行等比/](https://www.geeksforgeeks.org/longest-subarray-whose-elements-can-be-made-equal-by-maximum-k-increments/)

给定一个大小为 **N** 的正整数数组**arr【】**和一个正整数 **K** ，任务是找到一个子数组的最大可能长度，该长度可以通过给子数组的每个元素添加一些整数值而相等，使得添加的元素之和不超过 **K** 。

**示例:**

> **输入:** N = 5，arr[] = {1，4，9，3，6}，K = 9
> **输出:** 3
> **解释:**
> {1，4} : {1+3，4} = {4，4}
> {4，9} : {4+5，9} = {9，9}
> {3，6} : {3+3，6} = {6，6}
> {9，9}
> 
> **输入:** N = 6，arr[] = {2，4，7，3，8，5}，K = 10
> **输出:** 4

**方法:**这个问题可以用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)解决。

*   初始化:
    *   **dp[]** :存储添加到子阵列的元素之和。
    *   **de quee**:存储每个子阵列的最大元素的索引。
    *   **位置:**子阵列当前位置的索引。
    *   **ans:** 最大子阵的长度。
    *   **mx:** 子阵列的最大元素
    *   **pre:** 当前子阵列的前一个索引。
*   遍历数组并检查 deque 是否为空。如果是，则更新最大元素和最大元素的索引以及 **pre** 和 **pos** 的索引。
*   检查当前添加的元素是否大于 **K** 。如果是，则将其从 **dp[]** 数组中移除，并更新 **pos** 和 **pre** 的索引。
*   最后，更新有效子数组的最大长度。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maximum
// possible length of subarray
int validSubArrLength(int arr[],
                      int N, int K)
{
    // Stores the sum of elements
    // that needs to be added to
    // the sub array
    int dp[N + 1];

    // Stores the index of the
    // current position of subarray
    int pos = 0;

    // Stores the maximum
    // length of subarray.
    int ans = 0;

    // Maximum element from
    // each subarray length
    int mx = 0;

    // Previous index of the
    // current subarray of
    // maximum length
    int pre = 0;

    // Deque to store the indices
    // of maximum element of
    // each sub array
    deque<int> q;

    // For each array element,
    // find the maximum length of
    // required subarray
    for (int i = 0; i < N; i++) {
        // Traverse the deque and
        // update the index of
        // maximum element.
        while (!q.empty()
               && arr[q.back()] < arr[i])

            q.pop_back();

        q.push_back(i);

        // If it is first element
        // then update maximum
        // and dp[]
        if (i == 0) {
            mx = arr[i];
            dp[i] = arr[i];
        }

        // Else check if current
        // element exceeds max
        else if (mx <= arr[i]) {
            // Update max and dp[]
            dp[i] = dp[i - 1] + arr[i];
            mx = arr[i];
        }

        else {
            dp[i] = dp[i - 1] + arr[i];
        }

        // Update the index of the
        // current maximum length
        // subarray
        if (pre == 0)
            pos = 0;
        else
            pos = pre - 1;

        // While current element
        // being added to dp[] array
        // exceeds K
        while ((i - pre + 1) * mx
                       - (dp[i] - dp[pos])
                   > K
               && pre < i) {

            // Update index of
            // current position and
            // the previous position
            pos = pre;
            pre++;

            // Remove elements
            // from deque and
            // update the
            // maximum element
            while (!q.empty()
                   && q.front() < pre
                   && pre < i) {

                q.pop_front();
                mx = arr[q.front()];
            }
        }

        // Update the maximum length
        // of the required subarray.
        ans = max(ans, i - pre + 1);
    }
    return ans;
}

// Driver Program
int main()
{
    int N = 6;
    int K = 8;
    int arr[] = { 2, 7, 1, 3, 4, 5 };
    cout << validSubArrLength(arr, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find maximum
// possible length of subarray
static int validSubArrLength(int arr[],
                             int N, int K)
{
    // Stores the sum of elements
    // that needs to be added to
    // the sub array
    int []dp = new int[N + 1];

    // Stores the index of the
    // current position of subarray
    int pos = 0;

    // Stores the maximum
    // length of subarray.
    int ans = 0;

    // Maximum element from
    // each subarray length
    int mx = 0;

    // Previous index of the
    // current subarray of
    // maximum length
    int pre = 0;

    // Deque to store the indices
    // of maximum element of
    // each sub array
    Deque<Integer> q = new LinkedList<>();

    // For each array element,
    // find the maximum length of
    // required subarray
    for(int i = 0; i < N; i++)
    {

       // Traverse the deque and
       // update the index of
       // maximum element.
       while (!q.isEmpty() &&
               arr[q.getLast()] < arr[i])
           q.removeLast();
       q.add(i);

       // If it is first element
       // then update maximum
       // and dp[]
       if (i == 0)
       {
           mx = arr[i];
           dp[i] = arr[i];
       }

       // Else check if current
       // element exceeds max
       else if (mx <= arr[i])
       {

           // Update max and dp[]
           dp[i] = dp[i - 1] + arr[i];
           mx = arr[i];
       }
       else
       {
           dp[i] = dp[i - 1] + arr[i];
       }

       // Update the index of the
       // current maximum length
       // subarray
       if (pre == 0)
           pos = 0;
       else
           pos = pre - 1;

       // While current element
       // being added to dp[] array
       // exceeds K
       while ((i - pre + 1) * mx -
          (dp[i] - dp[pos]) > K && pre < i)
       {

           // Update index of
           // current position and
           // the previous position
           pos = pre;
           pre++;

           // Remove elements from
           // deque and update the
           // maximum element
           while (!q.isEmpty() &&
                   q.peek() < pre && pre < i)
           {
               q.removeFirst();
               mx = arr[q.peek()];
           }
       }

       // Update the maximum length
       // of the required subarray.
       ans = Math.max(ans, i - pre + 1);
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 6;
    int K = 8;
    int arr[] = { 2, 7, 1, 3, 4, 5 };

    System.out.print(validSubArrLength(arr, N, K));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to find maximum
# possible length of subarray
def validSubArrLength(arr, N, K):

    # Stores the sum of elements
    # that needs to be added to
    # the sub array
    dp = [0 for i in range(N + 1)]

    # Stores the index of the
    # current position of subarray
    pos = 0

    # Stores the maximum
    # length of subarray.
    ans = 0

    # Maximum element from
    # each subarray length
    mx = 0

    # Previous index of the
    # current subarray of
    # maximum length
    pre = 0

    # Deque to store the indices
    # of maximum element of
    # each sub array
    q = []

    # For each array element,
    # find the maximum length of
    # required subarray
    for i in range(N):

        # Traverse the deque and
        # update the index of
        # maximum element.
        while (len(q) and arr[len(q) - 1] < arr[i]):
            q.remove(q[len(q) - 1])

        q.append(i)

        # If it is first element
        # then update maximum
        # and dp[]
        if (i == 0):
            mx = arr[i]
            dp[i] = arr[i]

        # Else check if current
        # element exceeds max
        elif (mx <= arr[i]):

            # Update max and dp[]
            dp[i] = dp[i - 1] + arr[i]
            mx = arr[i]

        else:
            dp[i] = dp[i - 1] + arr[i]

        # Update the index of the
        # current maximum length
        # subarray
        if (pre == 0):
            pos = 0
        else:
            pos = pre - 1

        # While current element
        # being added to dp[] array
        # exceeds K
        while ((i - pre + 1) *
               mx - (dp[i] - dp[pos]) > K and
              pre < i):

            # Update index of
            # current position and
            # the previous position
            pos = pre
            pre += 1

            # Remove elements
            # from deque and
            # update the
            # maximum element
            while (len(q) and
                   q[0] < pre and
                   pre < i):
                q.remove(q[0])
                mx = arr[q[0]]

        # Update the maximum length
        # of the required subarray.
        ans = max(ans, i - pre + 1)

    return ans

# Driver code
if __name__ == '__main__':

    N = 6
    K = 8

    arr =  [ 2, 7, 1, 3, 4, 5 ]

    print(validSubArrLength(arr, N, K))

# This code is contributed by ipg2016107
```

## java 描述语言

```
<script>

// Javascript code for the above approach

// Function to find maximum
// possible length of subarray
function validSubArrLength(arr, N, K)
{
    // Stores the sum of elements
    // that needs to be added to
    // the sub array
    var dp = Array(N+1);

    // Stores the index of the
    // current position of subarray
    var pos = 0;

    // Stores the maximum
    // length of subarray.
    var ans = 0;

    // Maximum element from
    // each subarray length
    var mx = 0;

    // Previous index of the
    // current subarray of
    // maximum length
    var pre = 0;

    // Deque to store the indices
    // of maximum element of
    // each sub array
    var q = [];

    // For each array element,
    // find the maximum length of
    // required subarray
    for (var i = 0; i < N; i++) {
        // Traverse the deque and
        // update the index of
        // maximum element.
        while (q.length!=0
               && arr[q[q.length-1]] < arr[i])

            q.pop();

        q.push(i);

        // If it is first element
        // then update maximum
        // and dp[]
        if (i == 0) {
            mx = arr[i];
            dp[i] = arr[i];
        }

        // Else check if current
        // element exceeds max
        else if (mx <= arr[i]) {
            // Update max and dp[]
            dp[i] = dp[i - 1] + arr[i];
            mx = arr[i];
        }

        else {
            dp[i] = dp[i - 1] + arr[i];
        }

        // Update the index of the
        // current maximum length
        // subarray
        if (pre == 0)
            pos = 0;
        else
            pos = pre - 1;

        // While current element
        // being added to dp[] array
        // exceeds K
        while ((i - pre + 1) * mx
                       - (dp[i] - dp[pos])
                   > K
               && pre < i) {

            // Update index of
            // current position and
            // the previous position
            pos = pre;
            pre++;

            // Remove elements
            // from deque and
            // update the
            // maximum element
            while (q.length!=0
                   && q[0] < pre
                   && pre < i) {

                q.shift();
                mx = arr[q[0]];
            }
        }

        // Update the maximum length
        // of the required subarray.
        ans = Math.max(ans, i - pre + 1);
    }
    return ans;
}

// Driver Program
var N = 6;
var K = 8;
var arr = [2, 7, 1, 3, 4, 5];
document.write( validSubArrLength(arr, N, K));

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间复杂度:** O(N)*