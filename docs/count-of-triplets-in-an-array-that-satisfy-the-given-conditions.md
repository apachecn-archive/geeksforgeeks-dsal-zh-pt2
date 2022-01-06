# 满足给定条件的数组中三元组的计数

> 原文:[https://www . geesforgeks . org/满足给定条件的数组中三元组的计数/](https://www.geeksforgeeks.org/count-of-triplets-in-an-array-that-satisfy-the-given-conditions/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找到三元组 **(arr[i]、arr[j]、arr[k])** 的计数，使得 **(arr[i] + arr[j] + arr[k] = L)** 和**(L % arr[I]= L % arr[j]= L % arr[k]= 0**。
**举例:**

> **输入:** arr[] = {2，4，5，6，7}
> **输出:** 1
> 唯一可能的三元组是{2，4，6}
> **输入:** arr[] = {4，4，4，4，4}
> **输出:** 10

**进场:**

*   考虑以下等式:

> **L = a * arr[i]** 、 **L = b * arr[j]** 和 **L = c * arr[k]** 。
> 因此， **arr[i] = L / a** ， **arr[j] = L / b** 和 **arr[k] = L / c** 。
> 所以，在**中使用这个，arr[i] + arr[j] + arr[k] = L** 给出 **L / a + L / b + L / c = L**
> 或 **1 / a + 1 / b + 1 / c = 1** 。
> 现在，上述方程只能有 10 种可能的解，分别是
> {2，3，6}
> {2，4，4}
> {2，6，3}
> {3，2，6}
> {3，3，3}
> {3，6，2}
> {4，2，4}
> {4，4，2}
> {6，2，3}
> {6，4}所以，所有这些解决方案都可以存储在一个 2D 数组中，比如 **test[][3]** 。所以，所有满足这些解决方案的三元组都可以找到。

*   所有**我**从 **1** 到 **N** 。考虑 **arr[i]** 作为三元组的中间元素。并为方程**的所有可能解找到对应的三元组的第一和第三元素 1 / a + 1 / b + 1 / c = 1** 。找到所有案例的答案，并将其添加到最终答案中。
*   维护数组中出现**arr【I】**的索引。对于给定的方程的可能解 **X** 和每个数**arr【I】**，保持该数为三元组的中间元素，并找到第一个和第三个元素。将[二分搜索法](https://www.geeksforgeeks.org/binary-search/)应用于第一个和第三个元素的可用索引集，找出第一个元素从 **1** 到**I–1**的出现次数，以及第三个元素从 **i + 1** 到 **N** 的出现次数。将两个值相乘，并将其添加到最终答案中。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int
#define MAX 100001
#define ROW 10
#define COl 3

vector<int> indices[MAX];

// All possible solutions of the
// equation 1/a + 1/b + 1/c = 1
int test[ROW][COl] = { { 2, 3, 6 },
                       { 2, 4, 4 },
                       { 2, 6, 3 },
                       { 3, 2, 6 },
                       { 3, 3, 3 },
                       { 3, 6, 2 },
                       { 4, 2, 4 },
                       { 4, 4, 2 },
                       { 6, 2, 3 },
                       { 6, 3, 2 } };

// Function to find the triplets
int find_triplet(int array[], int n)
{
    int answer = 0;

    // Storing indices of the elements
    for (int i = 0; i < n; i++) {
        indices[array[i]].push_back(i);
    }

    for (int i = 0; i < n; i++) {
        int y = array[i];

        for (int j = 0; j < ROW; j++) {
            int s = test[j][1] * y;

            // Check if y can act as the middle
            // element of triplet with the given
            // solution of 1/a + 1/b + 1/c = 1
            if (s % test[j][0] != 0)
                continue;
            if (s % test[j][2] != 0)
                continue;

            int x = s / test[j][0];
            ll z = s / test[j][2];
            if (x > MAX || z > MAX)
                continue;

            int l = 0;
            int r = indices[x].size() - 1;

            int first = -1;

            // Binary search to find the number of
            // possible values of the first element
            while (l <= r) {
                int m = (l + r) / 2;

                if (indices[x][m] < i) {
                    first = m;
                    l = m + 1;
                }
                else {
                    r = m - 1;
                }
            }

            l = 0;
            r = indices[z].size() - 1;

            int third = -1;

            // Binary search to find the number of
            // possible values of the third element
            while (l <= r) {
                int m = (l + r) / 2;

                if (indices[z][m] > i) {
                    third = m;
                    r = m - 1;
                }
                else {
                    l = m + 1;
                }
            }

            if (first != -1 && third != -1) {

                // Contribution to the answer would
                // be the multiplication of the possible
                // values for the first and the third element
                answer += (first + 1) * (indices[z].size() - third);
            }
        }
    }

    return answer;
}

// Driver code
int main()
{
    int array[] = { 2, 4, 5, 6, 7 };
    int n = sizeof(array) / sizeof(array[0]);

    cout << find_triplet(array, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static int MAX = 100001;
static int ROW = 10;
static int COl = 3;

static Vector<Integer> []indices = new Vector[MAX];

// All possible solutions of the
// equation 1/a + 1/b + 1/c = 1
static int test[][] = { { 2, 3, 6 }, { 2, 4, 4 },
                        { 2, 6, 3 }, { 3, 2, 6 },
                        { 3, 3, 3 }, { 3, 6, 2 },
                        { 4, 2, 4 }, { 4, 4, 2 },
                        { 6, 2, 3 }, { 6, 3, 2 } };

// Function to find the triplets
static int find_triplet(int array[], int n)
{
    int answer = 0;
    for (int i = 0; i < MAX; i++)
    {
        indices[i] = new Vector<>();
    }

    // Storing indices of the elements
    for (int i = 0; i < n; i++)
    {
        indices[array[i]].add(i);
    }

    for (int i = 0; i < n; i++)
    {
        int y = array[i];

        for (int j = 0; j < ROW; j++)
        {
            int s = test[j][1] * y;

            // Check if y can act as the middle
            // element of triplet with the given
            // solution of 1/a + 1/b + 1/c = 1
            if (s % test[j][0] != 0)
                continue;
            if (s % test[j][2] != 0)
                continue;

            int x = s / test[j][0];
            int z = s / test[j][2];
            if (x > MAX || z > MAX)
                continue;

            int l = 0;
            int r = indices[x].size() - 1;

            int first = -1;

            // Binary search to find the number of
            // possible values of the first element
            while (l <= r)
            {
                int m = (l + r) / 2;

                if (indices[x].get(m) < i)
                {
                    first = m;
                    l = m + 1;
                }
                else
                {
                    r = m - 1;
                }
            }

            l = 0;
            r = indices[z].size() - 1;

            int third = -1;

            // Binary search to find the number of
            // possible values of the third element
            while (l <= r)
            {
                int m = (l + r) / 2;

                if (indices[z].get(m) > i)
                {
                    third = m;
                    r = m - 1;
                }
                else
                {
                    l = m + 1;
                }
            }

            if (first != -1 && third != -1)
            {

                // Contribution to the answer would
                // be the multiplication of the possible
                // values for the first and the third element
                answer += (first + 1) * (indices[z].size() - third);
            }
        }
    }
    return answer;
}

// Driver code
public static void main(String []args)
{
    int array[] = { 2, 4, 5, 6, 7 };
    int n = array.length;

    System.out.println(find_triplet(array, n));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MAX = 100001
ROW = 10
COL = 3

indices = [0] * MAX

# All possible solutions of the
# equation 1/a + 1/b + 1/c = 1
test = [[2, 3, 6], [2, 4, 4],
        [2, 6, 3], [3, 2, 6],
        [3, 3, 3], [3, 6, 2],
        [4, 2, 4], [4, 4, 2],
        [6, 2, 3], [6, 3, 2]]

# Function to find the triplets
def find_triplet(array, n):
    answer = 0

    for i in range(MAX):
        indices[i] = []

    # Storing indices of the elements
    for i in range(n):
        indices[array[i]].append(i)

    for i in range(n):
        y = array[i]

        for j in range(ROW):
            s = test[j][1] * y

            # Check if y can act as the middle
            # element of triplet with the given
            # solution of 1/a + 1/b + 1/c = 1
            if s % test[j][0] != 0:
                continue
            if s % test[j][2] != 0:
                continue

            x = s // test[j][0]
            z = s // test[j][2]
            if x > MAX or z > MAX:
                continue

            l = 0
            r = len(indices[x]) - 1
            first = -1

            # Binary search to find the number of
            # possible values of the first element
            while l <= r:
                m = (l + r) // 2

                if indices[x][m] < i:
                    first = m
                    l = m + 1
                else:
                    r = m - 1

            l = 0
            r = len(indices[z]) - 1
            third = -1

            # Binary search to find the number of
            # possible values of the third element
            while l <= r:
                m = (l + r) // 2

                if indices[z][m] > i:
                    third = m
                    r = m - 1
                else:
                    l = m + 1

            if first != -1 and third != -1:

                # Contribution to the answer would
                # be the multiplication of the possible
                # values for the first and the third element
                answer += (first + 1) * (len(indices[z]) - third)
    return answer

# Driver Code
if __name__ == "__main__":
    array = [2, 4, 5, 6, 7]
    n = len(array)

    print(find_triplet(array, n))

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

static int MAX = 100001;
static int ROW = 10;
static int COl = 3;

static List<int> []indices = new List<int>[MAX];

// All possible solutions of the
// equation 1/a + 1/b + 1/c = 1
static int [,]test = { { 2, 3, 6 }, { 2, 4, 4 },
                       { 2, 6, 3 }, { 3, 2, 6 },
                       { 3, 3, 3 }, { 3, 6, 2 },
                       { 4, 2, 4 }, { 4, 4, 2 },
                       { 6, 2, 3 }, { 6, 3, 2 } };

// Function to find the triplets
static int find_triplet(int []array, int n)
{
    int answer = 0;
    for (int i = 0; i < MAX; i++)
    {
        indices[i] = new List<int>();
    }

    // Storing indices of the elements
    for (int i = 0; i < n; i++)
    {
        indices[array[i]].Add(i);
    }

    for (int i = 0; i < n; i++)
    {
        int y = array[i];

        for (int j = 0; j < ROW; j++)
        {
            int s = test[j, 1] * y;

            // Check if y can act as the middle
            // element of triplet with the given
            // solution of 1/a + 1/b + 1/c = 1
            if (s % test[j, 0] != 0)
                continue;
            if (s % test[j, 2] != 0)
                continue;

            int x = s / test[j, 0];
            int z = s / test[j, 2];
            if (x > MAX || z > MAX)
                continue;

            int l = 0;
            int r = indices[x].Count - 1;

            int first = -1;

            // Binary search to find the number of
            // possible values of the first element
            while (l <= r)
            {
                int m = (l + r) / 2;

                if (indices[x][m] < i)
                {
                    first = m;
                    l = m + 1;
                }
                else
                {
                    r = m - 1;
                }
            }

            l = 0;
            r = indices[z].Count - 1;

            int third = -1;

            // Binary search to find the number of
            // possible values of the third element
            while (l <= r)
            {
                int m = (l + r) / 2;

                if (indices[z][m] > i)
                {
                    third = m;
                    r = m - 1;
                }
                else
                {
                    l = m + 1;
                }
            }

            if (first != -1 && third != -1)
            {

                // Contribution to the answer would
                // be the multiplication of the possible
                // values for the first and the third element
                answer += (first + 1) * (indices[z].Count - third);
            }
        }
    }
    return answer;
}

// Driver code
public static void Main(String []args)
{
    int []array = { 2, 4, 5, 6, 7 };
    int n = array.Length;

    Console.WriteLine(find_triplet(array, n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

var MAX = 100001
var ROW = 10
var COl = 3

var indices = Array.from(Array(MAX), ()=>new Array());

// All possible solutions of the
// equation 1/a + 1/b + 1/c = 1
var test = [ [ 2, 3, 6 ],
                       [ 2, 4, 4 ],
                       [ 2, 6, 3 ],
                       [ 3, 2, 6 ],
                       [ 3, 3, 3 ],
                       [ 3, 6, 2 ],
                       [ 4, 2, 4 ],
                       [ 4, 4, 2 ],
                       [ 6, 2, 3 ],
                       [ 6, 3, 2 ] ];

// Function to find the triplets
function find_triplet(array, n)
{
    var answer = 0;

    // Storing indices of the elements
    for (var i = 0; i < n; i++) {
        indices[array[i]].push(i);
    }

    for (var i = 0; i < n; i++) {
        var y = array[i];

        for (var j = 0; j < ROW; j++) {
            var s = test[j][1] * y;

            // Check if y can act as the middle
            // element of triplet with the given
            // solution of 1/a + 1/b + 1/c = 1
            if (s % test[j][0] != 0)
                continue;
            if (s % test[j][2] != 0)
                continue;

            var x = s / test[j][0];
            var z = s / test[j][2];
            if (x > MAX || z > MAX)
                continue;

            var l = 0;
            var r = indices[x].length - 1;

            var first = -1;

            // Binary search to find the number of
            // possible values of the first element
            while (l <= r) {
                var m = (l + r) / 2;

                if (indices[x][m] < i) {
                    first = m;
                    l = m + 1;
                }
                else {
                    r = m - 1;
                }
            }

            l = 0;
            r = indices[z].length - 1;

            var third = -1;

            // Binary search to find the number of
            // possible values of the third element
            while (l <= r) {
                var m = (l + r) / 2;

                if (indices[z][m] > i) {
                    third = m;
                    r = m - 1;
                }
                else {
                    l = m + 1;
                }
            }

            if (first != -1 && third != -1) {

                // Contribution to the answer would
                // be the multiplication of the possible
                // values for the first and the third element
                answer += (first + 1) * (indices[z].length - third);
            }
        }
    }

    return answer;
}

// Driver code
var array = [2, 4, 5, 6, 7];
var n = array.length;
document.write( find_triplet(array, n));

</script>
```

**Output:** 

```
1
```