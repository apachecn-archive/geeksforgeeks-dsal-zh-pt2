# 水平放置的最大杆数，这样在 X 坐标上就不会有两根杆重叠

> 原文:[https://www . geeksforgeeks . org/最大水平放置杆数-这样-x 坐标上没有两个杆重叠/](https://www.geeksforgeeks.org/maximum-rods-to-put-horizontally-such-that-no-two-rods-overlap-on-x-coordinate/)

给定两个尺寸为 **N** 的[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/)**X【】**和**H【】**，其中**X【I】**表示**I<sup>th</sup>T15】垂直杆的 X 坐标**，而**H【I】**表示该杆的高度，并且还给定一个**I<sup>th</sup>T21 杆也可以 X[i]+H[i]]** 在 X 坐标上，任务是找到可以水平放置的杆的最大数量，以便在 X 坐标上没有两个杆重叠。

**示例:**

> ***输入:** N* = 3，X[] = {1，2，3}，H[] = {2，5，5}
> ***输出:** 2*
> **解释:**
> 放置棒的一种可能方式是:
> 
> 1.  将杆水平放置在 X[0]左侧的 X[0]( = 1)处，即线段[-1，1]上。
> 2.  让放置在位置 X[1]( = 2)的杆垂直。
> 3.  将杆水平放置在 X[2]右侧的 X[2]( = 3)处，即线段[3，8]上。
> 
> 因此，可以水平放置 2 根杆。这也是最大可能的计数。
> 
> ***输入:** N* = 3，X[] = {1，2，5}，H[] = {1，2，5}
> ***输出:*** 3

**方法:**使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。按照以下步骤解决问题:

*   初始化两个变量，比如说， **ans** 为 **0** 存储答案， **prev** 为 **INT_MIN** 存储 X 坐标上最后一个被占用的点。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**，并执行以下步骤:
    *   如果当前杆可以放在左边，即如果 **X[i]-H[i]** 大于 **prev** ，则将 **ans** 的值增加 **1** ，并将 **prev** 更新为 **X[i]。**
    *   否则，如果当前杆可以放在右边，即如果 **X[i]+H[i]** 小于 **X[i+1]** ，则将 **ans** 的值增加 **1** ，并将 **prev** 更新为 **X[i]+H[i]。**
    *   否则，将 **prev** 更新为**X【I】**。
*   最后，完成以上步骤后，打印 **ans 中得到的答案。**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>

using namespace std;

// Function to find the maximum number
// of rods that can be put horizontally
int findMaximumPoints(int N, int X[], int H[])
{

    // Stores the result
    int ans = 0;

    // Stores the last occupied point
    int prev = INT_MIN;

    // Traverse the array arr[]
    for (int i = 0; i < N; ++i) {

        // If the current point can be put on
        // the left side
        if (prev < (X[i] - H[i])) {

            // Increment the ans by 1
            ++ans;

            // Update prev
            prev = X[i];
        }

        // Else if the given point can be put
        // on the right side
        else if (i == N - 1
                 || (X[i] + H[i]) < X[i + 1]) {

            // Increment the ans by 1
            ++ans;

            // Update prev
            prev = X[i] + H[i];
        }

        // Otherwise,
        else {
            // Update prev
            prev = X[i];
        }
    }

    // Return the ans
    return ans;
}

// Driver Code
int main()
{

    int X[] = { 1, 2, 3 };
    int H[] = { 2, 5, 5 };
    int N = sizeof(X) / sizeof(X[0]);

    cout << findMaximumPoints(N, X, H);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to find the maximum number
    // of rods that can be put horizontally
    public static int findMaximumPoints(int N, int X[], int H[]) {

        // Stores the result
        int ans = 0;

        // Stores the last occupied point
        int prev = Integer.MIN_VALUE;

        // Traverse the array arr[]
        for (int i = 0; i < N; ++i) {

            // If the current point can be put on
            // the left side
            if (prev < (X[i] - H[i])) {

                // Increment the ans by 1
                ++ans;

                // Update prev
                prev = X[i];
            }

            // Else if the given point can be put
            // on the right side
            else if (i == N - 1 || (X[i] + H[i]) < X[i + 1]) {

                // Increment the ans by 1
                ++ans;

                // Update prev
                prev = X[i] + H[i];
            }

            // Otherwise,
            else {
                // Update prev
                prev = X[i];
            }
        }

        // Return the ans
        return ans;
    }

    // Driver Code
    public static void main(String args[]) {

        int X[] = { 1, 2, 3 };
        int H[] = { 2, 5, 5 };
        int N = X.length;

        System.out.println(findMaximumPoints(N, X, H));
    }
}

// This code is contributed by _saurabh_jaiswal.
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function to find the maximum number
# of rods that can be put horizontally
def findMaximumPoints(N, X, H):
    # Stores the result
    ans = 0

    # Stores the last occupied point
    prev = -sys.maxsize-1

    # Traverse the array arr[]
    for i in range(N):

        # If the current point can be put on
        # the left side
        if (prev < (X[i] - H[i])):

            # Increment the ans by 1
            ans += 1

            # Update prev
            prev = X[i]

        # Else if the given point can be put
        # on the right side
        elif(i == N - 1 or (X[i] + H[i]) < X[i + 1]):

            # Increment the ans by 1
            ans += 1

            # Update prev
            prev = X[i] + H[i]

        # Otherwise,
        else:
            # Update prev
            prev = X[i]

    # Return the ans
    return ans

# Driver Code
if __name__ == '__main__':
    X = [1, 2, 3]
    H = [2, 5, 5]
    N = len(X)

    print(findMaximumPoints(N, X, H))

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to find the maximum number
    // of rods that can be put horizontally
    public static int findMaximumPoints(int N, int[] X, int[] H) {

        // Stores the result
        int ans = 0;

        // Stores the last occupied point
        int prev = Int32.MinValue;

        // Traverse the array arr[]
        for (int i = 0; i < N; ++i) {

            // If the current point can be put on
            // the left side
            if (prev < (X[i] - H[i])) {

                // Increment the ans by 1
                ++ans;

                // Update prev
                prev = X[i];
            }

            // Else if the given point can be put
            // on the right side
            else if (i == N - 1 || (X[i] + H[i]) < X[i + 1]) {

                // Increment the ans by 1
                ++ans;

                // Update prev
                prev = X[i] + H[i];
            }

            // Otherwise,
            else {
                // Update prev
                prev = X[i];
            }
        }

        // Return the ans
        return ans;
    }

// Driver code
static public void Main()
{
    int[] X = { 1, 2, 3 };
        int[] H = { 2, 5, 5 };
        int N = X.Length;

        Console.WriteLine(findMaximumPoints(N, X, H));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to find the maximum number
        // of rods that can be put horizontally
        function findMaximumPoints(N, X, H)
        {

            // Stores the result
            let ans = 0;

            // Stores the last occupied point
            let prev = Number.MIN_VALUE;

            // Traverse the array arr[]
            for (let i = 0; i < N; ++i) {

                // If the current point can be put on
                // the left side
                if (prev < (X[i] - H[i])) {

                    // Increment the ans by 1
                    ++ans;

                    // Update prev
                    prev = X[i];
                }

                // Else if the given point can be put
                // on the right side
                else if (i == N - 1
                    || (X[i] + H[i]) < X[i + 1]) {

                    // Increment the ans by 1
                    ++ans;

                    // Update prev
                    prev = X[i] + H[i];
                }

                // Otherwise,
                else
                {

                    // Update prev
                    prev = X[i];
                }
            }
            ans++;
            // Return the ans
            return ans;
        }

        // Driver Code
        let X = [1, 2, 3];
        let H = [2, 5, 5];
        let N = X.length;

        document.write(findMaximumPoints(N, X, H));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)