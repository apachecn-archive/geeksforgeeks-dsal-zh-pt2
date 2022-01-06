# 以最小绝对差的排序顺序查找数组中的所有对

> 原文:[https://www . geeksforgeeks . org/find-数组中所有对的排序顺序具有最小绝对差异/](https://www.geeksforgeeks.org/find-all-pairs-in-an-array-in-sorted-order-with-minimum-absolute-difference/)

给定一个整数[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**大小为 **N** ，任务是找到所有具有**最小绝对差**的**不同**对，并按**升序**顺序打印它们。

**示例**:

> **输入** : arr[] = {4，2，1，3}
> **输出** : {1，2}、{2，3}、{3，4}
> **解释**:两对之间的最小绝对差为 1。
> 
> **输入** : arr[] = {1，3，8，10，15}
> **输出** : {1，3}、{8，10}
> **解释**:两对{1，3}、{8，10}之间的最小绝对差为 2。

**逼近**:思路是考虑**排序**数组的**相邻**元素的**绝对差**。按照以下步骤解决问题:

*   [给定数组 arr[]排序](https://www.geeksforgeeks.org/merge-sort/)。
*   比较**排序的**数组中所有**相邻**对，找出所有相邻对之间的**最小绝对差**。
*   最后，打印所有差异等于最小绝对差异的相邻对。

下面是上述代码的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return all
// pairs having minimal absolute difference
vector<vector<int> > minAbsDiffPairs(vector<int>& arr)
{

    vector<vector<int> > ans;
    int n = arr.size();

    // Sort the array
    sort(arr.begin(), arr.end());

    // Stores the minimal absolute difference
    int minDiff = INT_MAX;

    for (int i = 0; i < n - 1; i++)
        minDiff = min(minDiff, abs(arr[i] - arr[i + 1]));

    for (int i = 0; i < n - 1; i++) {
        vector<int> pair;
        if (abs(arr[i] - arr[i + 1]) == minDiff) {
            pair.push_back(min(arr[i], arr[i + 1]));
            pair.push_back(max(arr[i], arr[i + 1]));
            ans.push_back(pair);
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<int> arr = { 4, 2, 1, 3 };
    int N = (sizeof arr) / (sizeof arr[0]);

    vector<vector<int> > pairs = minAbsDiffPairs(arr);

    // Print all pairs
    for (auto v : pairs)
        cout << v[0] << " " << v[1] << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;

class GFG
{

    // Function to return all
    // pairs having minimal absolute difference
    static ArrayList<ArrayList<Integer>> minAbsDiffPairs(ArrayList<Integer> arr) {

        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        int n = arr.size();

        // Sort the array
        Collections.sort(arr);

        // Stores the minimal absolute difference
        int minDiff = Integer.MAX_VALUE;

        for (int i = 0; i < n - 1; i++)
            minDiff = Math.min(minDiff, Math.abs(arr.get(i) - arr.get(i + 1)));

        for (int i = 0; i < n - 1; i++) {
            ArrayList<Integer> pair = new ArrayList<Integer>();
            if (Math.abs(arr.get(i) - arr.get(i + 1)) == minDiff) {
                pair.add(Math.min(arr.get(i), arr.get(i + 1)));
                pair.add(Math.max(arr.get(i), arr.get(i + 1)));
                ans.add(pair);
            }
        }

        return ans;
    }

    // Driver Code
    public static void main(String args[]) {
        ArrayList<Integer> arr = new ArrayList<Integer>();
        arr.add(4);
        arr.add(2);
        arr.add(1);
        arr.add(3);

        ArrayList<ArrayList<Integer>> pairs = minAbsDiffPairs(arr);

        // Print all pairs
        // System.out.println(pairs);
        for (ArrayList<Integer> v : pairs) {
            for (int w : v)
                System.out.print(w + " ");
            System.out.println("");
        }
    }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math as Math

# Function to return all pairs having
# minimal absolute difference
def minAbsDiffPairs(arr):

    ans = []
    n = len(arr)

    # Sort the array
    arr.sort()

    # Stores the minimal absolute difference
    minDiff = 10 ** 9

    for i in range(n - 1):
        minDiff = min(minDiff, Math.fabs(arr[i] -
                                         arr[i + 1]))

    for i in range(n - 1):
        pair = []
        if (Math.fabs(arr[i] - arr[i + 1]) == minDiff):
            pair.append(min(arr[i], arr[i + 1]))
            pair.append(max(arr[i], arr[i + 1]))
            ans.append(pair)

    return ans

# Driver Code
arr = [ 4, 2, 1, 3 ]
N = len(arr)

pairs = minAbsDiffPairs(arr)

# Print all pairs
for v in pairs:
    print(f"{v[0]} {v[1]}")

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
    // JavaScript code for the above approach

    // Function to return all
    // pairs having minimal absolute difference
    function minAbsDiffPairs(arr)
    {

      let ans = [];
      let n = arr.length;

      // Sort the array
      arr.sort(function (a, b) { return a - b })

      // Stores the minimal absolute difference
      let minDiff = Number.MAX_VALUE;

      for (let i = 0; i < n - 1; i++)
        minDiff = Math.min(minDiff, Math.abs(arr[i] - arr[i + 1]));

      for (let i = 0; i < n - 1; i++) {
        let pair = [];
        if (Math.abs(arr[i] - arr[i + 1]) == minDiff) {
          pair.push(Math.min(arr[i], arr[i + 1]));
          pair.push(Math.max(arr[i], arr[i + 1]));
          ans.push(pair);
        }
      }
      return ans;
    }

    // Driver Code
    let arr = [4, 2, 1, 3];
    let N = arr.length;

    let pairs = minAbsDiffPairs(arr);

    // Print all pairs
    for (let v of pairs)
      document.write(v[0] + " " + v[1] + '<br>')

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
1 2
2 3
3 4
```

***时间复杂度*** : O(NlogN)
***辅助空间*** : O(N)