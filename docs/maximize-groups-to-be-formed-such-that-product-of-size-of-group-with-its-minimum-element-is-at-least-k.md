# 最大化要形成的群，使得群的大小与其最小元素的乘积至少为 K

> 原文:[https://www . geeksforgeeks . org/最大化要形成的组，使得具有最小元素的组的大小乘积至少为-k/](https://www.geeksforgeeks.org/maximize-groups-to-be-formed-such-that-product-of-size-of-group-with-its-minimum-element-is-at-least-k/)

给定一个长度为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、 **arr[]** ，以及一个整数 **K** 。第**个**元素的值为**arr【I】**。任务是找到组的最大数量，使得对于每个组，该组中元素的数量与最小元素的乘积至少为 **K** 。

> **注意:**每个元素应该恰好属于一个组，有些元素可能不属于任何组。

**示例:**

> **输入:** N=5，arr[]={7，2，11，9，5}，K=10
> **输出:** 2
> **解释:**
> 
> *   做一个群[11，7](群大小=2)，其中群的大小和群的最小元素的乘积是大于 k 的 2*7=14
> *   做另一个群[9，5](群大小=2)，其中群的大小与群的最小元素之积为 2*5=10 等于 k。
> *   这样我们最多可以做 2 组
> 
> **输入:** N=4，arr[]={1，7，3，3}，K = 11
> T3】输出:0
> T6】解释:
> 
> *   如果我们做一个群[7，3，3]，那么群(3)的大小与群(3)的最小元素的乘积是 3*3=9，它小于 k。
> *   如果我们做一个群[7，3，3，1]，那么群(4)的大小与群(1)的最小元素的乘积是 1*4=4，小于 k。
> *   如果我们做一个群[7，3]，那么群(2)的大小与群(3)的最小元素的乘积是 2*3=6，小于 k。
> *   因此，我们不能用给定的数组组成任何群，使得群的大小与最小元素的乘积至少为 k。

**方法:**给定的问题可以通过[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。为了最大化组的数量，[对数组](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)进行排序，并通过首先获取更大的元素来开始创建组，因为这将帮助我们最大化每个组的最小元素。因此，每个组中所需的元素数量将减少，我们将最大化组的数量。按照以下步骤解决问题:

*   [给定数组按递增顺序排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。
*   初始化变量 **ans** 和**分别计数**到 **0** 和 **1** ， **ans** 将存储可创建的组总数，**计数**将存储当前组的大小。
*   [使用变量 **i** 从**【N-1 到 0】**遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，并执行以下步骤:
    *   如果**arr【I】**(当前组的最小元素)和计数(当前组的大小)的乘积大于或等于 **k** ，则将**计数**(组总数)增加 **1** ，并将**计数**初始化为 **1。**
    *   否则，将当前组中的元素数量增加 **1** 。
*   完成这些步骤后，打印**和**的值作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum number
// of groups that can be formed from given array
int maximumgroups(vector<int>& arr, int N, int k)
{

    // Sorting the given array in increasing order
    sort(arr.begin(), arr.end());

    int ans = 0, count = 1;

    // Start creating the groups by taking
    // the bigger elements first because this
    // will help us in maximizing our
    // minimum element of each group
    for (int i = N - 1; i >= 0; i--) {

        // If the product of minimum element of
        // current group and count is greater equal
        // to k then increase the ans by one and
        // initialize the count to 1
        if (arr[i] * count >= k) {
            ans++;
            count = 1;
        }
        // Otherwise increase the number of elements
        // in the current group by one
        else {
            count++;
        }
    }

    // Return the maximum number of groups possible
    return ans;
}

// Driver Code
int main()
{
    int N = 5;
    int k = 10;
    vector<int> arr = { 7, 11, 2, 9, 5 };
    int res = maximumgroups(arr, N, k);

    cout << res << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.Arrays;

class GFG {

  // Function to return the maximum number
  // of groups that can be formed from given array
  public static int maximumgroups(int[] arr, int N, int k) {

    // Sorting the given array in increasing order
    Arrays.sort(arr);

    int ans = 0, count = 1;

    // Start creating the groups by taking
    // the bigger elements first because this
    // will help us in maximizing our
    // minimum element of each group
    for (int i = N - 1; i >= 0; i--) {

      // If the product of minimum element of
      // current group and count is greater equal
      // to k then increase the ans by one and
      // initialize the count to 1
      if (arr[i] * count >= k) {
        ans++;
        count = 1;
      }
      // Otherwise increase the number of elements
      // in the current group by one
      else {
        count++;
      }
    }

    // Return the maximum number of groups possible
    return ans;
  }

  // Driver Code
  public static void main(String args[]) {
    int N = 5;
    int k = 10;
    int[] arr = { 7, 11, 2, 9, 5 };
    int res = maximumgroups(arr, N, k);

    System.out.println(res);
  }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to return the maximum number
# of groups that can be formed from given array
def maximumgroups(arr, N, k):

    # Sorting the given array in increasing order
    arr.sort();
    ans = 0
    count = 1;

    # Start creating the groups by taking
    # the bigger elements first because this
    # will help us in maximizing our
    # minimum element of each group
    for i in range(N - 1, -1, -1):

        # If the product of minimum element of
        # current group and count is greater equal
        # to k then increase the ans by one and
        # initialize the count to 1
        if (arr[i] * count >= k):
            ans += 1
            count = 1;

        # Otherwise increase the number of elements
        # in the current group by one
        else: 
            count += 1

    # Return the maximum number of groups possible
    return ans;

# Driver Code
if __name__ == "__main__":

    N = 5;
    k = 10;
    arr = [ 7, 11, 2, 9, 5 ];
    res = maximumgroups(arr, N, k);

    print(res );

    # This code is contributed by ukasp.
```

## java 描述语言

```
  <script>
      // JavaScript code for the above approach

      // Function to return the maximum number
      // of groups that can be formed from given array
      function maximumgroups(arr, N, k) {

          // Sorting the given array in increasing order
          arr.sort(function (a, b) { return a - b })

          let ans = 0, count = 1;

          // Start creating the groups by taking
          // the bigger elements first because this
          // will help us in maximizing our
          // minimum element of each group
          for (let i = N - 1; i >= 0; i--) {

              // If the product of minimum element of
              // current group and count is greater equal
              // to k then increase the ans by one and
              // initialize the count to 1
              if (arr[i] * count >= k) {
                  ans++;
                  count = 1;
              }
              // Otherwise increase the number of elements
              // in the current group by one
              else {
                  count++;
              }
          }

          // Return the maximum number of groups possible
          return ans;
      }

      // Driver Code

      let N = 5;
      let k = 10;
      let arr = [7, 11, 2, 9, 5];
      let res = maximumgroups(arr, N, k);

      document.write(res)

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度:**O(N *(log(N))*
***辅助空间:** O(1)*