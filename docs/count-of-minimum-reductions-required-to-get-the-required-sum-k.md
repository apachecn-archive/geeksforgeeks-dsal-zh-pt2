# 获得所需总和 K 所需的最小减少量的计数

> 原文:[https://www . geesforgeks . org/count-of-minimum-reducts-required-to-get-required-sum-k/](https://www.geeksforgeeks.org/count-of-minimum-reductions-required-to-get-the-required-sum-k/)

给定 **N** 对整数和一个整数 **K** ，任务是找到所需的最小约简数，使得每对的第一个元素之和为 **≤ K** 。每次约简都包括将一对中的第一个值约简为其第二个值。如果无法求和≤ **K** ，打印-1。

> **例:**
> **输入:** N = 5，K = 32
> 10 6
> 6 4
> 8 5
> 9 8
> 5 2
> **输出:** 2
> **解释:**
> 总和= 10 + 6 + 8 + 9 + 5 = 38 > K
> 减 10–>6 和 8–>5 减
> 
> **输入:** N = 4，K = 25
> 10 5
> 20 9
> 12 10
> 4 2
> T7】输出: -1

**方法:**
按照以下步骤解决问题:

1.  计算每对的第一个元素的和。如果总和已经≤ K，打印 0。
2.  根据给定配对的差异对其进行排序。
3.  以非递增的顺序计算需要相加的对的差数，得到的和小于 **K** 。
4.  如果遍历所有对后总和超过 K，打印-1。否则，打印计数。

下面是上述方法的实现:

## C++

```
// C++ Program to find the count of
// minimum reductions required to
// get the required sum K
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of minimum reductions
int countReductions(
    vector<pair<int, int> >& v,
    int K)
{

    int sum = 0;
    for (auto i : v) {
        sum += i.first;
    }

    // If the sum is already
    // less than K
    if (sum <= K) {
        return 0;
    }

    // Sort in non-increasing
    // order of difference
    sort(v.begin(), v.end(),
         [&](
             pair<int, int> a,
             pair<int, int> b) {
             return (a.first - a.second)
                    > (b.first - b.second);
         });

    int i = 0;
    while (sum > K && i < v.size()) {
        sum -= (v[i].first
                - v[i].second);
        i++;
    }

    if (sum <= K)
        return i;

    return -1;
}

// Driver Code
int main()
{
    int N = 4, K = 25;

    vector<pair<int, int> > v(N);
    v[0] = { 10, 5 };
    v[1] = { 20, 9 };
    v[2] = { 12, 10 };
    v[3] = { 4, 2 };

    // Function Call
    cout << countReductions(v, K)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count of
// minimum reductions required to
// get the required sum K
import java.util.*;

class GFG{

// Function to return the count
// of minimum reductions
static int countReductions(ArrayList<int[]> v,
                           int K)
{
    int sum = 0;
    for(int[] i : v)
    {
        sum += i[0];
    }

    // If the sum is already
    // less than K
    if (sum <= K)
    {
        return 0;
    }

    // Sort in non-increasing
    // order of difference
    Collections.sort(v, (a, b) -> Math.abs(b[0] - b[1]) -
                                  Math.abs(a[0] - a[1]));

    int i = 0;
    while (sum > K && i < v.size())
    {
        sum -= (v.get(i)[0] - v.get(i)[1]);
        i++;
    }

    if (sum <= K)
        return i;

    return -1;
}

// Driver code
public static void main(String[] args)
{
    int N = 4, K = 25;

    ArrayList<int[]> v = new ArrayList<>();

    v.add(new int[] { 10, 5 });
    v.add(new int[] { 20, 9 });
    v.add(new int[] { 12, 10 });
    v.add(new int[] { 4, 2 });

    // Function Call
    System.out.println(countReductions(v, K));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the count of
# minimum reductions required to
# get the required sum K
from typing import Any, List

# Function to return the count
# of minimum reductions
def countReductions(v: List[Any], K: int) -> int:

    sum = 0

    for i in v:
        sum += i[0]

    # If the sum is already
    # less than K
    if (sum <= K):
        return 0

    # Sort in non-increasing
    # order of difference
    v.sort(key = lambda a : a[0] - a[1])

    i = 0

    while (sum > K and i < len(v)):
        sum -= (v[i][0] - v[i][1])
        i += 1

    if (sum <= K):
        return i

    return -1

# Driver Code
if __name__ == "__main__":

    N = 4
    K = 25

    v = [[0, 0] for _ in range(N)]
    v[0] = [10, 5]
    v[1] = [20, 9]
    v[2] = [12, 10]
    v[3] = [4, 2]

    # Function Call
    print(countReductions(v, K))

# This code is contributed by sanjeev2552
```

**Output:** 

```
-1
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(1)*