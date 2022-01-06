# 在对数组执行给定运算后，位于范围[L，R]内的模 M 的值的最大计数

> 原文:[https://www . geeksforgeeks . org/在阵列上执行给定操作后，s 模 m 范围内的最大计数值 l-r/](https://www.geeksforgeeks.org/maximum-count-values-of-s-modulo-m-lying-in-a-range-l-r-after-performing-given-operations-on-the-array/)

给定一个由 **N** 个整数和整数 **M、L、R** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。考虑一个变量 **S** (最初 **0** )。任务是对给定数组中的每个元素执行以下操作后，找到位于**【L，R】**范围内的 **S % M** 的最大值计数:

*   将 **arr[i]** 或**arr[I]–1**添加至 **S** 。
*   将 **S 改为 S % M** 。

**示例:**

> ***输入:** arr[] = {17，11，10，8，15}，M = 22，L = 14，R = 16*
> ***输出:** 3*
> ***解释:***
> *最初 S = 0、*
> *步骤 1:选择，arr[0]–1 = 16 并将其添加到 S = 16 和 S %中因此，计数= 1*
> *第二步:选择，arr[1] = 11，加到 S = 16 + 11 = 27，S%M = 5。因此，count = 1*
> *第三步:选择，arr[2] = 10，加到 S = 16 + 10 +11 = 37，S%M = 15。因此，count = 2*
> *第四步:选择，arr[3] = 8，加到 S = 16 + 10 + 11 + 8 = 45，S%M = 1。所以，count = 2*
> *第五步:选择，arr[4] = 15，加到 S = 16 + 10 + 11 + 8 + 15 = 60，S%M = 16。因此，计数= 3。*
> *因此最大计数为 3。*
> 
> ***输入:** arr[] = {23，1}，M = 24，L = 21，R = 23*
> ***输出:** 2*

**天真方法:**最简单的方法是[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将**arr【I】**或**arr【I–1】**添加到给定的 **S** 中，检查 **S%M** 是否在范围**【L，R】**内。因为有两种选择给定数字的可能性。因此，使用[递归](https://www.geeksforgeeks.org/recursion/)递归得到 **S%M** 值的最大计数位于**【L，R】**范围内。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N)*

**高效方法:**优化上述方法的思路是使用[动态规划](https://www.geeksforgeeks.org/dynamic-programming/)存储[重叠子问题](https://www.geeksforgeeks.org/overlapping-subproblems-property-in-dynamic-programming-dp-1/)，然后找到 S%M 的最大计数位于范围**【L，R】**内。按照以下步骤解决问题:

1.  初始化一个[无序映射](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) **dp** 来存储有重叠子问题的状态值。
2.  将总和初始化为 **0** ，然后将 **arr[i]或 arr[I]–1**值递归添加到总和 **S** 中。
3.  每走一步，检查 **S%M** 是否在**【L，R】**范围内。如果在该范围内，则计算该值，并将上图 **dp** 中的当前状态更新为 1。否则更新为 **0** 。
4.  找出所有可能的组合后，返回位于范围**【L，R】**内的 **S%M** 值的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Lookup table
map<pair<int, int>, int> dp;

// Function to count the value of S
// after adding arr[i] or arr[i - 1]
// to the sum S at each time
int countMagicNumbers(int idx, int sum,
                      int a[], int n,
                      int m, int l, int r)
{
    // Base Case
    if (idx == n) {

        // Store the mod value
        int temp = sum % m;

        // If the mod value lies in
        // the range then return 1
        if (temp == l || temp == r
            || (temp > l && temp < r))
            return dp[{ idx, sum }] = 1;

        // Else return 0
        else
            return dp[{ idx, sum }] = 0;
    }

    // Store the current state
    pair<int, int> curr
        = make_pair(idx, sum);

    // If already computed, return the
    // computed value
    if (dp.find(curr) != dp.end())
        return dp[curr];

    // Recursively adding the elements
    // to the sum adding ai value
    int ls = countMagicNumbers(idx + 1,
                               sum + a[idx],
                               a, n,
                               m, l, r);

    // Adding arr[i] - 1 value
    int rs = countMagicNumbers(idx + 1,
                               sum + (a[idx] - 1),
                               a, n, m, l, r);

    // Return the maximum count to
    // check for root value as well
    int temp1 = max(ls, rs);
    int temp = sum % m;

    // Avoid counting idx = 0 as possible
    // solution we are using idx != 0
    if ((temp == l || temp == r
         || (temp > l && temp < r))
        && idx != 0) {
        temp1 += 1;
    }

    // Return the value of current state
    return dp[{ idx, sum }] = temp1;
}

// Driver Code
int main()
{
    int N = 5, M = 22, L = 14, R = 16;
    int arr[] = { 17, 11, 10, 8, 15 };

    cout << countMagicNumbers(0, 0, arr,
                              N, M, L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.awt.Point;
public class Main
{
    // Lookup table
    static HashMap<Point, Integer> dp = new HashMap<Point, Integer>();

    // Function to count the value of S
    // after adding arr[i] or arr[i - 1]
    // to the sum S at each time
    static int countMagicNumbers(int idx, int sum, int[] a,
                                 int n, int m, int l, int r)
    {
        // Base Case
        if (idx == n) {

            // Store the mod value
            int Temp = sum % m;

            // If the mod value lies in
            // the range then return 1
            if (Temp == l || Temp == r || (Temp > l && Temp < r))
            {
                dp.put(new Point(idx, sum), 1);
                return dp.get(new Point(idx, sum));
            }

            // Else return 0
            else
            {
                dp.put(new Point(idx, sum), 0);
                return dp.get(new Point(idx, sum));
            }
        }

        // Store the current state
        Point curr = new Point(idx, sum);

        // If already computed, return the
        // computed value
        if (dp.containsKey(curr))
            return dp.get(curr);

        // Recursively adding the elements
        // to the sum adding ai value
        int ls = countMagicNumbers(idx + 1,
                                   sum + a[idx],
                                   a, n,
                                   m, l, r);

        // Adding arr[i] - 1 value
        int rs = countMagicNumbers(idx + 1,
                                   sum + (a[idx] - 1),
                                   a, n, m, l, r);

        // Return the maximum count to
        // check for root value as well
        int temp1 = Math.max(ls, rs);
        int temp = sum % m;

        // Avoid counting idx = 0 as possible
        // solution we are using idx != 0
        if ((temp == l || temp == r
             || (temp > l && temp < r))
            && idx != 0) {
            temp1 += 1;
        }

        // Return the value of current state
        dp.put(new Point(idx, sum), temp1);
        return dp.get(new Point(idx, sum));
    }

    public static void main(String[] args) {
        int N = 5, M = 22, L = 14, R = 16;
        int[] arr = { 17, 11, 10, 8, 15 };

        System.out.print(countMagicNumbers(0, 0, arr, N, M, L, R));
    }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Lookup table
dp = {}

# Function to count the value of S
# after adding arr[i] or arr[i - 1]
# to the sum S at each time
def countMagicNumbers(idx, sum, a, n, m, l, r):

    # Base Case
    if (idx == n):

        # Store the mod value
        temp = sum % m

        # If the mod value lies in
        # the range then return 1
        if (temp == l or temp == r or
           (temp > l and temp < r)):
            dp[(idx, sum)] = 1
            return dp[(idx, sum)]

        # Else return 0
        else:
            dp[(idx, sum)] = 0
            return dp[(idx, sum)]

    # Store the current state
    curr = (idx, sum)

    # If already computed, return the
    # computed value
    if (curr in dp):
        return dp[curr]

    # Recursively adding the elements
    # to the sum adding ai value
    ls = countMagicNumbers(idx + 1,
                           sum + a[idx],
                           a, n, m, l, r)

    # Adding arr[i] - 1 value
    rs = countMagicNumbers(idx + 1,
                           sum + (a[idx] - 1),
                           a, n, m, l, r)

    # Return the maximum count to
    # check for root value as well
    temp1 = max(ls, rs)
    temp = sum % m

    # Avoid counting idx = 0 as possible
    # solution we are using idx != 0
    if ((temp == l or temp == r or
        (temp > l and temp < r)) and
         idx != 0):
        temp1 += 1

    # Return the value of current state
    dp[(idx, sum)] = temp1
    return dp[(idx, sum)]

# Driver Code
if __name__ == '__main__':

    N = 5
    M = 22
    L = 14
    R = 16

    arr = [ 17, 11, 10, 8, 15 ]

    print(countMagicNumbers(0, 0, arr, N, M, L, R))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Lookup table
    static Dictionary<Tuple<int, int>, int> dp = new Dictionary<Tuple<int, int>, int>();

    // Function to count the value of S
    // after adding arr[i] or arr[i - 1]
    // to the sum S at each time
    static int countMagicNumbers(int idx, int sum, int[] a, int n, int m, int l, int r)
    {
        // Base Case
        if (idx == n) {

            // Store the mod value
            int Temp = sum % m;

            // If the mod value lies in
            // the range then return 1
            if (Temp == l || Temp == r
                || (Temp > l && Temp < r))
                return dp[new Tuple<int,int>(idx, sum)] = 1;

            // Else return 0
            else
                return dp[new Tuple<int,int>(idx, sum)] = 0;
        }

        // Store the current state
        Tuple<int,int> curr
            = new Tuple<int,int>(idx, sum);

        // If already computed, return the
        // computed value
        if (dp.ContainsKey(curr))
            return dp[curr];

        // Recursively adding the elements
        // to the sum adding ai value
        int ls = countMagicNumbers(idx + 1,
                                   sum + a[idx],
                                   a, n,
                                   m, l, r);

        // Adding arr[i] - 1 value
        int rs = countMagicNumbers(idx + 1,
                                   sum + (a[idx] - 1),
                                   a, n, m, l, r);

        // Return the maximum count to
        // check for root value as well
        int temp1 = Math.Max(ls, rs);
        int temp = sum % m;

        // Avoid counting idx = 0 as possible
        // solution we are using idx != 0
        if ((temp == l || temp == r
             || (temp > l && temp < r))
            && idx != 0) {
            temp1 += 1;
        }

        // Return the value of current state
        return dp[new Tuple<int,int>(idx, sum)] = temp1;
    }

  static void Main() {
    int N = 5, M = 22, L = 14, R = 16;
    int[] arr = { 17, 11, 10, 8, 15 };

    Console.Write(countMagicNumbers(0, 0, arr, N, M, L, R));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Lookup table
    let dp = new Map();

    // Function to count the value of S
    // after adding arr[i] or arr[i - 1]
    // to the sum S at each time
    function countMagicNumbers(idx, sum, a, n, m, l, r)
    {
        // Base Case
        if (idx == n) {

            // Store the mod value
            let temp = sum % m;

            // If the mod value lies in
            // the range then return 1
            if (temp == l || temp == r
                || (temp > l && temp < r))
                return dp[[ idx, sum ]] = 1;

            // Else return 0
            else
                return dp[[ idx, sum ]] = 0;
        }

        // Store the current state
        let curr = [idx, sum];

        // If already computed, return the
        // computed value
        if (dp.has(curr))
            return dp[curr];

        // Recursively adding the elements
        // to the sum adding ai value
        let ls = countMagicNumbers(idx + 1,
                                   sum + a[idx],
                                   a, n,
                                   m, l, r);

        // Adding arr[i] - 1 value
        let rs = countMagicNumbers(idx + 1,
                                   sum + (a[idx] - 1),
                                   a, n, m, l, r);

        // Return the maximum count to
        // check for root value as well
        let temp1 = Math.max(ls, rs);
        let temp = sum % m;

        // Avoid counting idx = 0 as possible
        // solution we are using idx != 0
        if ((temp == l || temp == r
             || (temp > l && temp < r))
            && idx != 0) {
            temp1 += 1;
        }

        // Return the value of current state
        dp[[ idx, sum ]] = temp1;
        return dp[[ idx, sum ]];
    }

    let N = 5, M = 22, L = 14, R = 16;
    let arr = [ 17, 11, 10, 8, 15 ];

    document.write(countMagicNumbers(0, 0, arr, N, M, L, R));

  // This code is contributed by mukesh07.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(S*N)，其中 N 是给定数组*、*的大小，S 是所有数组元素的和。*
***空间复杂度:** O(S*N)*