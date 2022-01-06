# 尺寸范围【L，R】

的最大和子阵

> 原文:[https://www . geeksforgeeks . org/maximum-sum-subarray-of-size-l-r/](https://www.geeksforgeeks.org/maximum-sum-subarray-of-size-range-l-r/)

给定一个大小为 **N** 的整数数组 **arr[]** ，以及两个整数 **L** 和 **R** 。任务是找出 **L** 和 **R** 之间(包括两者)尺寸的最大和子阵。
**例:**

> **输入:** arr[] = {1，2，2，1}，L = 1，R = 3
> **输出:** 5
> **解释:**
> 大小为 1 的子阵列为{1}、{2}、{2}、{1}，子阵列{2}的最大和子阵列= 2。
> 尺寸为 2 的子阵列为{1，2}、{2，2}、{2，1}，子阵列{2，2}的最大和子阵列= 4。
> 大小为 3 的子阵列为{1，2，2}、{2，2，1}，子阵列{2，2，1}的最大和子阵列= 5。
> 因此子阵列的最大可能和为 5。
> **输入:** arr[] = {-1，-3，-7，-11}，L = 1，R = 4
> **输出:** -1

**进场:**

1.  这里我们将使用[这篇](https://www.geeksforgeeks.org/maximum-subarray-sum-using-prefix-sum/)文章中讨论的[滑动窗口](https://www.geeksforgeeks.org/window-sliding-technique/)的概念。
2.  首先计算数组 **pre[]** 中数组的[前缀和。](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)
3.  接下来迭代范围 **L** 到 **N -1** ，并考虑所有尺寸 **L** 到 **R** 的子阵列。
4.  创建一个多集来存储子阵列长度 **L** 到 **R** 的前缀和。
5.  现在要找到以索引 **i** 结束的子阵列的最大和，只需减去**pre【I】**和从**pre【I–L】**到**pre【I–R】**的所有值的最小值。
6.  最后返回所有和的最大值。

下面是上述方法的实现:

## C++

```
// C++ program to find Maximum sum
// subarray of size between L and R.

#include <bits/stdc++.h>
using namespace std;

// function to find Maximum sum subarray
// of size between L and R
void max_sum_subarray(vector<int> arr,
                      int L, int R)
{
    int n = arr.size();
    int pre[n] = { 0 };

    // calculating prefix sum
    pre[0] = arr[0];
    for (int i = 1; i < n; i++) {
        pre[i] = pre[i - 1] + arr[i];
    }
    multiset<int> s1;

    // maintain 0 for initial
    // values of i upto R
    // Once i = R, then
    // we need to erase that 0 from
    // our multiset as our first
    // index of subarray
    // cannot be 0 anymore.
    s1.insert(0);
    int ans = INT_MIN;

    ans = max(ans, pre[L - 1]);

    // we maintain flag to
    // counter if that initial
    // 0 was erased from set or not.
    int flag = 0;

    for (int i = L; i < n; i++) {

        // erase 0 from multiset once i=b
        if (i - R >= 0) {
            if (flag == 0) {

                auto it = s1.find(0);
                s1.erase(it);
                flag = 1;
            }
        }
        // insert pre[i-L]
        if (i - L >= 0)
            s1.insert(pre[i - L]);

        // find minimum value in multiset.
        ans = max(ans,
                  pre[i] - *s1.begin());

        // erase pre[i-R]
        if (i - R >= 0) {
            auto it = s1.find(pre[i - R]);
            s1.erase(it);
        }
    }
    cout << ans << endl;
}

// Driver code
int main()
{
    int L, R;
    L = 1;
    R = 3;
    vector<int> arr = { 1, 2, 2, 1 };
    max_sum_subarray(arr, L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Maximum sum
// subarray of size between L and R.
import java.util.*;
class GFG
{
  // function to find Maximum sum subarray
  // of size between L and R
  static void max_sum_subarray(List<Integer> arr, int L, int R)
  {
    int n = arr.size();
    int[] pre = new int[n];

    // calculating prefix sum
    pre[0] = arr.get(0);
    for (int i = 1; i < n; i++)
    {
      pre[i] = pre[i - 1] + arr.get(i);
    }
    List<Integer> s1 = new ArrayList<>();

    // maintain 0 for initial
    // values of i upto R
    // Once i = R, then
    // we need to erase that 0 from
    // our multiset as our first
    // index of subarray
    // cannot be 0 anymore.
    s1.add(0);
    int ans = Integer.MIN_VALUE;

    ans = Math.max(ans, pre[L - 1]);

    // we maintain flag to
    // counter if that initial
    // 0 was erased from set or not.
    int flag = 0;

    for (int i = L; i < n; i++)
    {

      // erase 0 from multiset once i=b
      if (i - R >= 0)
      {
        if (flag == 0)
        {
          int it = s1.indexOf(0);
          s1.remove(it);
          flag = 1;
        }
      }

      // insert pre[i-L]
      if (i - L >= 0)
        s1.add(pre[i - L]);

      // find minimum value in multiset.
      ans = Math.max(ans, pre[i] - s1.get(0));

      // erase pre[i-R]
      if (i - R >= 0)
      {
        int it = s1.indexOf(pre[i - R]);
        s1.remove(it);
      }
    }
    System.out.println(ans);
  }

  // Driver code
  public static void main(String[] args)
  {
    int L, R;
    L = 1;
    R = 3;
    List<Integer> arr = Arrays.asList(1, 2, 2, 1);
    max_sum_subarray(arr, L, R); 
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find maximum sum
# subarray of size between L and R.
import sys

# Function to find maximum sum subarray
# of size between L and R
def max_sum_subarray(arr, L, R):

    n = len(arr)
    pre = n * [0]

    # Calculating prefix sum
    pre[0] = arr[0]
    for i in range(1, n):
        pre[i] = pre[i - 1] + arr[i]

    s1 = []

    # Maintain 0 for initial
    # values of i upto R
    # Once i = R, then
    # we need to erase that 0 from
    # our multiset as our first
    # index of subarray
    # cannot be 0 anymore.
    s1.append(0)
    ans = -sys.maxsize - 1

    ans = max(ans, pre[L - 1])

    # We maintain flag to
    # counter if that initial
    # 0 was erased from set or not.
    flag = 0

    for i in range(L, n):

        # Erase 0 from multiset once i=b
        if (i - R >= 0):
            if (flag == 0):
                s1.remove(0)
                flag = 1

        # Insert pre[i-L]
        if (i - L >= 0):
            s1.append(pre[i - L])

        # Find minimum value in multiset.
        ans = max(ans, pre[i] - s1[0])

        # Erase pre[i-R]
        if (i - R >= 0):
            s1.remove(pre[i - R])

    print(ans)

# Driver code
if __name__ == "__main__":

    L = 1
    R = 3
    arr = [ 1, 2, 2, 1 ]

    max_sum_subarray(arr, L, R)

# This code is contributed by chitranayal
```

## C#

```
// C# program to find Maximum sum
// subarray of size between L and R.
using System;
using System.Collections.Generic;
class GFG
{

    // function to find Maximum sum subarray
    // of size between L and R
    static void max_sum_subarray(List<int> arr, int L, int R)
    {
        int n = arr.Count;
        int[] pre = new int[n];

        // calculating prefix sum
        pre[0] = arr[0];
        for (int i = 1; i < n; i++)
        {
            pre[i] = pre[i - 1] + arr[i];
        }
        List<int> s1 = new List<int>();

        // maintain 0 for initial
        // values of i upto R
        // Once i = R, then
        // we need to erase that 0 from
        // our multiset as our first
        // index of subarray
        // cannot be 0 anymore.
        s1.Add(0);
        int ans = Int32.MinValue;

        ans = Math.Max(ans, pre[L - 1]);

        // we maintain flag to
        // counter if that initial
        // 0 was erased from set or not.
        int flag = 0;

        for (int i = L; i < n; i++)
        {

            // erase 0 from multiset once i=b
            if (i - R >= 0)
            {
                if (flag == 0)
                {

                    int it = s1.IndexOf(0);
                    s1.RemoveAt(it);
                    flag = 1;
                }
            }
            // insert pre[i-L]
            if (i - L >= 0)
                s1.Add(pre[i - L]);

            // find minimum value in multiset.
            ans = Math.Max(ans, pre[i] - s1[0]);

            // erase pre[i-R]
            if (i - R >= 0)
            {
                int it = s1.IndexOf(pre[i - R]);
                s1.RemoveAt(it);
            }
        }
        Console.WriteLine(ans);
    } 

  // Driver code
  static void Main()
  {
    int L, R;
    L = 1;
    R = 3;
    List<int> arr = new List<int>(){1, 2, 2, 1};
    max_sum_subarray(arr, L, R);
  }
}

// This code is contributed by divyesh072019
```

## java 描述语言

```
<script>

// Javascript program to find Maximum sum
// subarray of size between L and R.

// function to find Maximum sum subarray
  // of size between L and R
function max_sum_subarray(arr,L,R)
{
    let n = arr.length;
    let pre = new Array(n);

    // calculating prefix sum
    pre[0] = arr[0];
    for (let i = 1; i < n; i++)
    {
      pre[i] = pre[i - 1] + arr[i];
    }
    let s1 = []

    // maintain 0 for initial
    // values of i upto R
    // Once i = R, then
    // we need to erase that 0 from
    // our multiset as our first
    // index of subarray
    // cannot be 0 anymore.
    s1.push(0);
    let ans = Number.MIN_VALUE;

    ans = Math.max(ans, pre[L - 1]);

    // we maintain flag to
    // counter if that initial
    // 0 was erased from set or not.
    let flag = 0;

    for (let i = L; i < n; i++)
    {

      // erase 0 from multiset once i=b
      if (i - R >= 0)
      {
        if (flag == 0)
        {
          let it = s1.indexOf(0);
          s1.splice(it,1);
          flag = 1;
        }
      }

      // insert pre[i-L]
      if (i - L >= 0)
        s1.push(pre[i - L]);

      // find minimum value in multiset.
      ans = Math.max(ans, pre[i] - s1[0]);

      // erase pre[i-R]
      if (i - R >= 0)
      {
        let it = s1.indexOf(pre[i - R]);
        s1.splice(it,1);
      }
    }
    document.write(ans);
}

// Driver code
let L, R;
L = 1;
R = 3;
let arr = [1, 2, 2, 1];
max_sum_subarray(arr, L, R);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
5
```

***时间复杂度:** O (N * log N)*
***辅助空间:** O (N)*