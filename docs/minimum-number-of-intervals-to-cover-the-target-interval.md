# 覆盖目标区间的最小区间数

> 原文:[https://www . geesforgeks . org/最小间隔数-覆盖目标间隔/](https://www.geeksforgeeks.org/minimum-number-of-intervals-to-cover-the-target-interval/)

给定一个由 **N** 间隔和一个目标间隔 **X** 组成的[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**，任务是从给定的阵列**A【】**中找到最小数量的间隔，使得它们完全覆盖目标间隔。如果不存在这样的间隔，则打印**-1”**。

**示例:**

> **输入:** A[] = {{1，3}、{2，4}、{2，10}、{2，3}、{1，1}}，X = {1，10}
> **输出:** 2
> **解释:**
> 从给定的 5 个区间中，可以选择{1，3}和{3，10}。因此，范围[1，3]中的点被区间{1，3}覆盖，范围[4，10]中的点被区间{2，10}覆盖。
> 
> **输入:** A[] = {{2，6}，{7，9}，{3，5}，{6，10}}，X = {1，4}
> **输出:** -1
> **说明:**给定数组 A 中不存在覆盖整个目标区间的区间集。

**方法:**给定的问题可以通过使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。可以观察到，从目标范围内的点 **p** 开始的区间的最佳选择是区间 **(u，v)** ，使得 **u < = p** 和 **v** 是最大可能。根据这一观察，按照以下步骤解决给定的问题:

*   [按照区间起点的递增顺序对给定数组](https://www.geeksforgeeks.org/sorting-algorithms/) **A[]** 进行排序。
*   创建一个变量 **start** 并用目标区间 **X** 的起点初始化。它存储当前选定时间间隔的起点。同样，变量 **end** 存储当前变量的结束点。用**start–1**初始化。
*   创建一个变量 **cnt** ，它存储所选间隔的计数。
*   使用变量 **i** 遍历给定的数组 **A[]** 。
*   如果第 i <sup>个</sup>间隔<的起始点=开始，用最大值更新结束值(第 i <sup>个</sup>间隔的结束点，结束点)，否则设置**开始=结束**并将 **cnt** 的值增加 **1** 。
*   如果第 i <sup>个</sup>区间>结束的起点或**结束**的值已经大于目标区间的终点，则中断循环。
*   返回 **-1** 如果目标区间的<终点的值结束，否则返回 **cnt** 的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of intervals in the array A[] to
// cover the entire target interval
int minimizeSegment(vector<pair<int, int> > A,
                    pair<int, int> X)
{
    // Sort the array A[] in increasing
    // order of starting point
    sort(A.begin(), A.end());

    // Insert a pair of INT_MAX to
    // prevent going out of bounds
    A.push_back({ INT_MAX, INT_MAX });

    // Stores start of current interval
    int start = X.first;

    // Stores end of current interval
    int end = X.first - 1;

    // Stores the count of intervals
    int cnt = 0;

    // Iterate over all the intervals
    for (int i = 0; i < A.size();) {

        // If starting point of current
        // index <= start
        if (A[i].first <= start) {
            end = max(A[i++].second, end);
        }
        else {

            // Update the value of start
            start = end;

            // Increment the value
            // of count
            ++cnt;

            // If the target interval is
            // already covered or it is
            // not possible to move
            // then break the loop
            if (A[i].first > end
                || end >= X.second) {
                break;
            }
        }
    }

    // If the entire target interval
    // is not covered
    if (end < X.second) {
        return -1;
    }

    // Return Answer
    return cnt;
}

// Driver Code
int main()
{
    vector<pair<int, int> > A = {
        { 1, 3 }, { 2, 4 }, { 2, 10 }, { 2, 3 }, { 1, 1 }
    };
    pair<int, int> X = { 1, 10 };
    cout << minimizeSegment(A, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Comparator;

class GFG
{

  static class Pair
  {
    int first;
    int second;

    public Pair(int f, int s)
    {
      this.first = f;
      this.second = s;
    }
  }

  // Function to find the minimum number
  // of intervals in the array A[] to
  // cover the entire target interval
  public static int minimizeSegment(ArrayList<Pair> A, Pair X)
  {

    // Sort the array A[] in increasing
    // order of starting point
    final Comparator<Pair> arrayComparator = new Comparator<GFG.Pair>() {
      @Override
      public int compare(Pair o1, Pair o2) {
        return Integer.compare(o1.first, o2.first);
      }
    };

    A.sort(arrayComparator);

    // Insert a pair of INT_MAX to
    // prevent going out of bounds
    A.add(new Pair(Integer.MAX_VALUE, Integer.MIN_VALUE));

    // Stores start of current interval
    int start = X.first;

    // Stores end of current interval
    int end = X.first - 1;

    // Stores the count of intervals
    int cnt = 0;

    // Iterate over all the intervals
    for (int i = 0; i < A.size();) {

      // If starting point of current
      // index <= start
      if (A.get(i).first <= start) {
        end = Math.max(A.get(i++).second, end);
      } else {

        // Update the value of start
        start = end;

        // Increment the value
        // of count
        ++cnt;

        // If the target interval is
        // already covered or it is
        // not possible to move
        // then break the loop
        if (A.get(i).first > end
            || end >= X.second) {
          break;
        }
      }
    }

    // If the entire target interval
    // is not covered
    if (end < X.second) {
      return -1;
    }

    // Return Answer
    return cnt;
  }

  // Driver Code
  public static void main(String args[]) {
    ArrayList<Pair> A = new ArrayList<Pair>();
    A.add(new Pair(1, 3));
    A.add(new Pair(2, 4));
    A.add(new Pair(2, 10));
    A.add(new Pair(2, 3));
    A.add(new Pair(1, 1));
    Pair X = new Pair(1, 10);
    System.out.println(minimizeSegment(A, X));
  }
}

// This code is contributed by saurabh_jaiswal.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the minimum number
# of intervals in the array A[] to
# cover the entire target interval
def minimizeSegment(A, X):

    # Sort the array A[] in increasing
    # order of starting point

    A.sort()

    # Insert a pair of INT_MAX to
    # prevent going out of bounds

    INT_MAX = 2147483647
    A.append([INT_MAX, INT_MAX])

    # Stores start of current interval
    start = X[0]

    # Stores end of current interval
    end = X[0] - 1

    # Stores the count of intervals
    cnt = 0

    # Iterate over all the intervals
    for i in range(0, len(A)):
        # If starting point of current
        # index <= start

        if (A[i][0] <= start):
            end = max(A[i][1], end)
            i = i + 1
        else:

                        # Update the value of start
            start = end

            # Increment the value
            # of count
            cnt = cnt + 1

            # If the target interval is
            # already covered or it is
            # not possible to move
            # then break the loop
            if (A[i][0] > end or end >= X[1]):
                break

        # If the entire target interval
        # is not covered
    if (end < X[1]):
        return -1

        # Return Answer
    return cnt

# Driver Code
if __name__ == "__main__":
    A = [[1, 3], [2, 4], [2, 10], [2, 3], [1, 1]]

    X = [1, 10]

    print(minimizeSegment(A, X))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to find the minimum number
        // of intervals in the array A[] to
        // cover the entire target interval
        function minimizeSegment(A,
            X)
           {

            // Sort the array A[] in increasing
            // order of starting point
            A.sort(function (a, b) { return a.first - b.first; })

            // Insert a pair of INT_MAX to
            // prevent going out of bounds
            A.push({ first: Number.MAX_VALUE, second: Number.MAX_VALUE });

            // Stores start of current interval
            let start = X.first;

            // Stores end of current interval
            let end = X.first - 1;

            // Stores the count of intervals
            let cnt = 0;

            // Iterate over all the intervals
            for (let i = 0; i < A.length;) {

                // If starting point of current
                // index <= start
                if (A[i].first <= start) {
                    end = Math.max(A[i++].second, end);
                }
                else {

                    // Update the value of start
                    start = end;

                    // Increment the value
                    // of count
                    ++cnt;

                    // If the target interval is
                    // already covered or it is
                    // not possible to move
                    // then break the loop
                    if (A[i].first > end
                        || end >= X.second) {
                        break;
                    }
                }
            }

            // If the entire target interval
            // is not covered
            if (end < X.second) {
                return -1;
            }

            // Return Answer
            return cnt;
        }

        // Driver Code
        let A = [{ first: 1, second: 3 },
        { first: 2, second: 4 },
        { first: 2, second: 10 },
        { first: 2, second: 3 },
        { first: 1, second: 1 }
        ];
        let X = { first: 1, second: 10 };
        document.write(minimizeSegment(A, X));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(1)*