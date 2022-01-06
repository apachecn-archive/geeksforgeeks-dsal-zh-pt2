# 2D 平面上任意一对坐标的给定表达式的最大值

> 原文:[https://www . geeksforgeeks . org/2d 平面上任意坐标对给定表达式的最大值/](https://www.geeksforgeeks.org/maximum-the-value-of-a-given-expression-for-any-pair-of-coordinates-on-a-2d-plane/)

给定大小为 **N** 的排序后的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【2】**，使得 **(arr[i][0]，arr[i][1])** 表示笛卡尔平面中第 **i <sup>第</sup>点**的坐标和整数 **K** ，任务是找到表达式**(| arr[I][0]<sub>–arr[j]的最大值</sub>**

**示例:**

> **输入:** arr[][] = {{1，3}，{2，0}，{5，10}，{6，-10}}，K = 1
> **输出:** 4
> **解释:**
> 选对(0，1)。现在表达式的值由下式给出:
> value =(ABS(1–2)+3+0)= 4，为最大值，ABS(1–2)= 1(≤K)。
> 因此，打印 4。
> 
> **输入:** arr[][] = {{0，0}，{3，0}，{9，2}}，K = 3
> **输出:** 3

**方法:**给定的问题可以使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)来解决，该优先级队列基于以下观察:

*   将所有 **i > j** 的表达式重新排列为**(arr[I][0]<sub>–arr[I][1]<sub>+arr[j][0]<sub>+arr[j][1])</sub></sub></sub>**。
*   现在，将一对**{ arr[I]<sub>x</sub>–arr[I]<sub>y</sub>，arr[i] <sub>x</sub> }** 按排序顺序排列，就可以计算出索引 **j** 处每个数组元素的给定表达式的值。

按照以下步骤解决问题:

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)对，比如 **PQ** ，它存储一个点的坐标轴和该点的 **X** 坐标的一对差。
*   初始化一个变量，比如 **res** 为 [INT_MIN](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/) 来存储最大值。
*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】【】**并考虑 **{X，Y}** 是当前点执行以下操作:
    *   当 [**PQ** 不为空](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)和**(X–PQ . top()[1])**大于 **K** 时迭代，并从优先级队列 **PQ** 中移除[顶元素。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
    *   如果 **PQ** 不为空，则将 **res** 的值更新为 **res** 和**PQ . top()【0】+X+Y)**的最大值。
    *   将配对**{ Y–X，X}** 推入优先级队列 **PQ** 。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum value
// of the given expression possible
// for any pair of co-ordinates
void findMaxValueOfEquation(
    vector<vector<int> >& arr, int K)
{
    // Stores the differences between pairs
    priority_queue<vector<int> > pq;

    // Stores the maximum value
    int res = INT_MIN;

    // Traverse the array arr[][]
    for (auto point : arr) {

        // While pq is not empty and
        // difference between point[0]
        // and pq.top()[1] > K
        while (!pq.empty()
               && point[0] - pq.top()[1]
                      > K) {

            // Removes the top element
            pq.pop();
        }

        // If pq is not empty
        if (!pq.empty()) {

            // Update the value res
            res = max(res,
                      pq.top()[0] + point[0] + point[1]);
        }

        // Push pair {point[1] - point[0],
        // point[0]} in pq
        pq.push({ point[1] - point[0],
                  point[0] });
    }

    // Print the result
    cout << res;
}

// Driver Code
int main()
{
    vector<vector<int> > arr
        = { { 1, 3 }, { 2, 0 },
            { 5, 10 }, { 6, -10 } };
    int K = 1;
    findMaxValueOfEquation(arr, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

public class GFG
{

    // Function to find the maximum value
    // of the given expression possible
    // for any pair of co-ordinates
    static void findMaxValueOfEquation(int arr[][], int K)
    {

        // Stores the differences between pairs
        PriorityQueue<int[]> pq
            = new PriorityQueue<>((a, b) -> {
                  if (a[0] != b[0])
                      return b[0] - a[0];
                  return b[1] - a[1];
              });

        // Stores the maximum value
        int res = Integer.MIN_VALUE;

        // Traverse the array arr[][]
        for (int point[] : arr) {

            // While pq is not empty and
            // difference between point[0]
            // and pq.top()[1] > K
            while (!pq.isEmpty()
                   && point[0] - pq.peek()[1] > K) {

                // Removes the top element
                pq.poll();
            }

            // If pq is not empty
            if (!pq.isEmpty()) {

                // Update the value res
                res = Math.max(res, pq.peek()[0] + point[0]
                                        + point[1]);
            }

            // Push pair {point[1] - point[0],
            // point[0]} in pq
            pq.add(new int[] { point[1] - point[0],
                               point[0] });
        }

        // Print the result
        System.out.println(res);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[][] arr
            = { { 1, 3 }, { 2, 0 }, { 5, 10 }, { 6, -10 } };
        int K = 1;
        findMaxValueOfEquation(arr, K);
    }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the maximum value
# of the given expression possible
# for any pair of co-ordinates
def findMaxValueOfEquation(arr, K):

    # Stores the differences between pairs
    pq = []

    # Stores the maximum value
    res = -10**8

    # Traverse the array arr[][]
    for point in arr:

        # While pq is not empty and
        # difference between point[0]
        # and pq.top()[1] > K
        while (len(pq)>0 and point[0] - pq[-1][1] > K):

            # Removes the top element
            del pq[-1]

        # If pq is not empty
        if (len(pq) > 0):
            # Update the value res
            res = max(res, pq[-1][0] + point[0] + point[1])

        # Push pair {point[1] - point[0],
        # point[0]} in pq
        pq.append([point[1] - point[0], point[0]])
        pq = sorted(pq)

    # Prthe result
    print (res)

# Driver Code
if __name__ == '__main__':
    arr = [ [ 1, 3 ], [ 2, 0 ], [ 5, 10 ], [ 6, -10 ] ]
    K = 1
    findMaxValueOfEquation(arr, K)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the maximum value
    // of the given expression possible
    // for any pair of co-ordinates
function findMaxValueOfEquation(arr,K)
{

    // Stores the differences between pairs
        let pq=[];

        // Stores the maximum value
        let res = Number.MIN_VALUE;

        // Traverse the array arr[][]
        for (let point=0;point< arr.length;point++) {

            // While pq is not empty and
            // difference between point[0]
            // and pq.top()[1] > K
            while (pq.length!=0
                   && arr[point][0] - pq[0][1] > K) {

                // Removes the top element
                pq.shift();
            }

            // If pq is not empty
            if (pq.length!=0) {

                // Update the value res
                res = Math.max(res, pq[0][0] + arr[point][0]
                                        + arr[point][1]);
            }

            // Push pair {point[1] - point[0],
            // point[0]} in pq
            pq.push([ arr[point][1] - arr[point][0],
                               arr[point][0] ]);

            pq.sort(function(a,b){
                    if (a[0] != b[0])
                      return b[0] - a[0];
                  return b[1] - a[1];})
        }

        // Print the result
        document.write(res);
}

// Driver Code
let arr = [[ 1, 3 ], [ 2, 0 ], [ 5, 10 ], [ 6, -10 ]];
let K = 1;
findMaxValueOfEquation(arr, K);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N * log N)*
***辅助空间:** O(N)*