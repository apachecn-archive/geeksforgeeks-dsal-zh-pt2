# 从给定的数组中找出一对相交的范围

> 原文:[https://www . geeksforgeeks . org/从给定数组中查找一对相交范围/](https://www.geeksforgeeks.org/find-a-pair-of-intersecting-ranges-from-a-given-array/)

给定一个大小为 **N * 2** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **范围[][]** ，每行代表一个形式为**【L，R】**的范围，任务是找到两个范围，使第一个范围完全位于第二个范围内，并打印它们的索引。如果无法获得这样的范围对，打印 **-1。**如果存在多个这样的范围，打印其中任何一个。

> 如果 **L1 ≥ L2** 和 **R1 ≤ R2** ，线段**【R1 L1】**位于线段**【R2 L2】**内。

**示例:**

> **输入:** N = 5，范围[][] = {{1，5}，{2，10}，{3，10}，{2，2}，{2，15}}
> **输出:**4 1
> T6】解释:段[2，2]完全位于段[1，5]内，为 1 ≤ 2 和 2 ≤ 5。
> 
> **输入:** N = 4，范围[][] = {{2，10}，{1，9}，{1，8}，{1，7}}
> **输出:** -1
> **说明:**不存在这样的线段对。

**天真方法:**解决问题最简单的方法是[迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/)，对于每个范围，[遍历剩余的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查是否存在完全位于当前范围内的范围，反之亦然。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:*** O(1)

**有效方法:**为了优化上述方法，想法是使用[比较器功能](https://www.geeksforgeeks.org/comparator-function-of-qsort-in-c/)对范围数组进行[排序，并检查任何段是否位于任何其他段内。按照下面给出的步骤解决这个问题:](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)

*   [按照起点](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的递增顺序对线段进行排序。如果一对具有相等的起点，则按照终点的降序排序。
*   现在，[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并保持如此获得的最大结束点，并将其与当前段的结束点进行比较。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Store ranges and their
// corresponding array indices
vector<pair<pair<int, int>, int> > tup;

// Function to find a pair of intersecting ranges
void findIntersectingRange(int N, int ranges[][2])
{

    // Stores ending point
    // of every range
    int curr;

    // Stores the maximum
    // ending point obtained
    int currPos;

    // Iterate from 0 to N - 1
    for (int i = 0; i < N; i++) {

        int x, y;

        // Starting point of
        // the current range
        x = ranges[i][0];

        // End point of
        // the current range
        y = ranges[i][1];

        // Push pairs into tup
        tup.push_back({ { x, y }, i + 1 });
    }

    // Sort the tup vector
    sort(tup.begin(), tup.end());

    curr = tup[0].first.second;
    currPos = tup[0].second;

    // Iterate over the ranges
    for (int i = 1; i < N; i++) {

        int Q = tup[i - 1].first.first;
        int R = tup[i].first.first;

        // If starting points are equal
        if (Q == R) {
            if (tup[i - 1].first.second
                < tup[i].first.second)
                cout << tup[i - 1].second << ' '
                     << tup[i].second;

            else
                cout << tup[i].second << ' '
                     << tup[i - 1].second;

            return;
        }

        int T = tup[i].first.second;

        // Print the indices of the
        // intersecting ranges
        if (T <= curr) {
            cout << tup[i].second
                 << ' ' << currPos;
            return;
        }
        else {
            curr = T;
            currPos = tup[i].second;
        }
    }

    // If no such pair of segments exist
    cout << "-1 -1";
}

// Driver Code
int main()
{
    // Given N
    int N = 5;

    // Given 2d ranges[][] array
    int ranges[][2] = {
        { 1, 5 }, { 2, 10 },
        { 3, 10 }, { 2, 2 },
        { 2, 15 }};

    // Function call
    findIntersectingRange(N, ranges);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class GFG{

// Store ranges and their
// corresponding array indices
static ArrayList<int[]> tup = new ArrayList<>();

// Function to find a pair of intersecting ranges
static void findIntersectingRange(int N, int ranges[][])
{

    // Stores ending point
    // of every range
    int curr;

    // Stores the maximum
    // ending point obtained
    int currPos;

    // Iterate from 0 to N - 1
    for(int i = 0; i < N; i++)
    {
        int x, y;

        // Starting point of
        // the current range
        x = ranges[i][0];

        // End point of
        // the current range
        y = ranges[i][1];

        // Push pairs into tup
        int[] arr = { x, y, i + 1 };
        tup.add(arr);
    }

    // Sort the tup vector
    // sort(tup.begin(), tup.end());
    Collections.sort(tup, new Comparator<int[]>()
    {
        public int compare(int[] a, int[] b)
        {
            if (a[0] == b[0])
            {
                if (a[1] == b[1])
                {
                    return a[2] - b[2];
                }
                else
                {
                    return a[1] - b[1];
                }
            }
            return a[0] - b[0];
        }
    });

    curr = tup.get(0)[1];
    currPos = tup.get(0)[2];

    // Iterate over the ranges
    for(int i = 1; i < N; i++)
    {
        int Q = tup.get(i - 1)[0];
        int R = tup.get(i)[0];

        // If starting points are equal
        if (Q == R)
        {
            if (tup.get(i - 1)[1] < tup.get(i)[1])
                System.out.print(tup.get(i - 1)[2] + " " +
                                 tup.get(i)[2]);

            else
                System.out.print(tup.get(i)[2] + " " +
                                 tup.get(i - 1)[2]);
            return;
        }

        int T = tup.get(i)[1];

        // Print the indices of the
        // intersecting ranges
        if (T <= curr)
        {
            System.out.print(tup.get(i)[2] + " " +
                             currPos);
            return;
        }
        else
        {
            curr = T;
            currPos = tup.get(i)[2];
        }
    }

    // If no such pair of segments exist
    System.out.print("-1 -1");
}

// Driver Code
public static void main(String[] args)
{

    // Given N
    int N = 5;

    // Given 2d ranges[][] array
    int ranges[][] = { { 1, 5 }, { 2, 10 },
                       { 3, 10 }, { 2, 2 },
                       { 2, 15 } };

    // Function call
    findIntersectingRange(N, ranges);
}
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Store ranges and their
# corresponding array indices

# Function to find a pair of intersecting ranges
def findIntersectingRange(tup, N, ranges):

    # Stores ending po
    # of every range
    curr = 0

    # Stores the maximum
    # ending poobtained
    currPos = 0

    # Iterate from 0 to N - 1
    for i in range(N):

        # Starting point of
        # the current range
        x = ranges[i][0]

        # End point of
        # the current range
        y = ranges[i][1]

        # Push pairs into tup
        tup.append([ [ x, y ], i + 1 ])

    # Sort the tup vector
    tup = sorted(tup)

    curr = tup[0][0][1]
    currPos = tup[0][1]

    # Iterate over the ranges
    for i in range(1, N):

        Q = tup[i - 1][0][0]
        R = tup[i][0][0]

        #If starting points are equal
        if (Q == R):
            if (tup[i - 1][0][1] < tup[i][0][1]):
                print(tup[i - 1][1], tup[i][1])
            else:
                print(tup[i][1], tup[i - 1][1])
            return

        T = tup[i][0][1]

        # Prthe indices of the
        # intersecting ranges
        if (T <= curr):
            print(tup[i][1], currPos)
            return
        else:
            curr = T
            currPos = tup[i][1]

    # If no such pair of segments exist
    print("-1 -1")

# Driver Code
if __name__ == '__main__':
    # Given N
    N = 5

    # Given 2d ranges[][] array
    ranges= [[ 1, 5 ], [ 2, 10 ],
            [ 3, 10 ], [ 2, 2 ],
            [ 2, 15 ]]

    # Function call
    findIntersectingRange([], N, ranges)

    # This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Store ranges and their
// corresponding array indices
let tup = [];

// Function to find a pair of intersecting ranges
function findIntersectingRange(N,ranges)
{
    // Stores ending point
    // of every range
    let curr;

    // Stores the maximum
    // ending point obtained
    let currPos;

    // Iterate from 0 to N - 1
    for(let i = 0; i < N; i++)
    {
        let x, y;

        // Starting point of
        // the current range
        x = ranges[i][0];

        // End point of
        // the current range
        y = ranges[i][1];

        // Push pairs into tup
        let arr = [ x, y, i + 1 ];
        tup.push(arr);
    }

    // Sort the tup vector
    // sort(tup.begin(), tup.end());
    tup.sort(function(a,b)
    {
            if (a[0] == b[0])
            {
                if (a[1] == b[1])
                {
                    return a[2] - b[2];
                }
                else
                {
                    return a[1] - b[1];
                }
            }
            return a[0] - b[0];

    });

    curr = tup[0][1];
    currPos = tup[0][2];

    // Iterate over the ranges
    for(let i = 1; i < N; i++)
    {
        let Q = tup[i - 1][0];
        let R = tup[i][0];

        // If starting points are equal
        if (Q == R)
        {
            if (tup[i - 1][1] < tup[i][1])
                document.write(tup[i - 1][2] + " " +
                                 tup[i][2]);

            else
                document.write(tup[i][2] + " " +
                                 tup[i - 1][2]);
            return;
        }

        let T = tup[i][1];

        // Print the indices of the
        // intersecting ranges
        if (T <= curr)
        {
            document.write(tup[i][2] + " " +
                             currPos);
            return;
        }
        else
        {
            curr = T;
            currPos = tup[i][2];
        }
    }

    // If no such pair of segments exist
    document.write("-1 -1");
}

// Driver Code
let N = 5;

// Given 2d ranges[][] array
let ranges = [[ 1, 5 ], [ 2, 10 ],
[ 3, 10 ], [ 2, 2 ],
[ 2, 15 ]];

// Function call
findIntersectingRange(N, ranges);

// This code is contributed by patel2127

</script>
```

**Output:** 

```
4 1
```

***时间复杂度:** O(N LogN)*
***辅助空间:** O(N)*