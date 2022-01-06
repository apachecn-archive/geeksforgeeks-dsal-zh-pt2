# 计算由斜率在[-K，K]

范围内的直线连接的坐标对

> 原文:[https://www . geeksforgeeks . org/count-坐标对-通过范围内斜率直线连接-k-k/](https://www.geeksforgeeks.org/count-pairs-of-coordinates-connected-by-a-line-with-slope-in-the-range-k-k/)

给定一个整数 **K** ，以及两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**X【】**和**Y【】**均由 **N** 个整数组成，其中 **(X[i]，Y[i])** 是一个平面中的坐标，任务是找出点对的总数，使得通过它们的直线具有在**【-K，K】**范围内的斜率。

**示例:**

> **输入:** X[] = {2，1，0}，Y[] = {1，2，0}，K = 1
> **输出:** 2
> **说明:**
> 满足给定条件的对集合为[(0，0)，(2，1)]和[(1，2)，(2，1)]。
> 
> **输入:** X[] = {2，4}，Y[][] = {5，6}，K = 1
> T3】输出: 1

**进场:**思路是遍历所有对点，检查其斜率是否在**【-K，K】**范围内。按照以下步骤解决问题:

*   初始化一个变量，说 **ans** 到 **0** 来存储结果对的计数。
*   现在，[生成所有可能的坐标对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)，如果 2 个点 **(X[i]，Y[i])** 和 **(X[j]，Y[j])** 的[斜率位于范围**【-K，K】**内，那么将 **ans** 增加 **1** 。](https://www.geeksforgeeks.org/program-find-slope-line/)
*   完成上述步骤后，打印和的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of pairs
// of points such that the line passing
// through them has a slope in the range[-k, k]
void findPairs(vector<int> x, vector<int> y,
               int K)
{
    int n = x.size();

    // Store the result
    int ans = 0;

    // Traverse through all the
    // combination of points
    for (int i = 0; i < n; ++i) {

        for (int j = i + 1; j < n; ++j) {

            // If pair satisfies
            // the given condition
            if (K * abs(x[i] - x[j])
                >= abs(y[i] - y[j])) {

                // Increment ans by 1
                ++ans;
            }
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    vector<int> X = { 2, 1, 0 },
                Y = { 1, 2, 0 };
    int K = 1;

    // Function Call
    findPairs(X, Y, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Function to find the number of pairs
// of points such that the line passing
// through them has a slope in the range[-k, k]
static void findPairs(int[] x, int[] y,
               int K)
{
    int n = x.length;

    // Store the result
    int ans = 0;

    // Traverse through all the
    // combination of points
    for (int i = 0; i < n; ++i) {

        for (int j = i + 1; j < n; ++j) {

            // If pair satisfies
            // the given condition
            if (K * Math.abs(x[i] - x[j])
                >= Math.abs(y[i] - y[j])) {

                // Increment ans by 1
                ++ans;
            }
        }
    }

    // Print the result
    System.out.print(ans);
}

// Driven Code
public static void main(String[] args)
{
    int[] X = { 2, 1, 0 };
    int[] Y = { 1, 2, 0 };
    int K = 1;

    // Function Call
    findPairs(X, Y, K);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of pairs
# of points such that the line passing
# through them has a slope in the range[-k, k]
def findPairs(x, y, K):
    n = len(x)

    # Store the result
    ans = 0

    # Traverse through all the
    # combination of points
    for i in range(n):
        for j in range(i + 1, n):

            # If pair satisfies
            # the given condition
            if (K * abs(x[i] - x[j]) >= abs(y[i] - y[j])):

                # Increment ans by 1
                ans += 1

    # Print the result
    print (ans)

# Driver Code
if __name__ == '__main__':
    X = [2, 1, 0]
    Y = [1, 2, 0]
    K = 1

    # Function Call
    findPairs(X, Y, K)

 # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the number of pairs
// of points such that the line passing
// through them has a slope in the range[-k, k]
static void findPairs(int[] x, int[] y,
                      int K)
{
    int n = x.Length;

    // Store the result
    int ans = 0;

    // Traverse through all the
    // combination of points
    for(int i = 0; i < n; ++i)
    {
        for(int j = i + 1; j < n; ++j)
        {

            // If pair satisfies
            // the given condition
            if (K * Math.Abs(x[i] - x[j]) >=
                    Math.Abs(y[i] - y[j]))
            {

                // Increment ans by 1
                ++ans;
            }
        }
    }

    // Print the result
    Console.WriteLine(ans);
}

// Driver Code
public static void Main(String []args)
{
    int[] X = { 2, 1, 0 };
    int[] Y = { 1, 2, 0 };
    int K = 1;

    // Function Call
    findPairs(X, Y, K);
}
}

// This code is contributed by souravghosh0416
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function to find the number of pairs
    // of points such that the line passing
    // through them has a slope in the range[-k, k]
    function findPairs(x, y, K)
    {
        let n = x.length;

        // Store the result
        let ans = 0;

        // Traverse through all the
        // combination of points
        for (let i = 0; i < n; ++i) {

            for (let j = i + 1; j < n; ++j) {

                // If pair satisfies
                // the given condition
                if (K * Math.abs(x[i] - x[j])
                    >= Math.abs(y[i] - y[j])) {

                    // Increment ans by 1
                    ++ans;
                }
            }
        }

        // Print the result
        document.write(ans);
    }

  // Driver code
    let X = [ 2, 1, 0 ], Y = [ 1, 2, 0 ];
    let K = 1;

    // Function Call
    findPairs(X, Y, K);

    // This code is contributed by divyesh072019.
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*