# 最大化相交线段的数量

> 原文:[https://www . geeksforgeeks . org/最大化相交线段数/](https://www.geeksforgeeks.org/maximize-count-of-intersecting-line-segments/)

给定两个[数组](https://www.geeksforgeeks.org/array-data-structure/)**X【】**和**Y【】**，分别代表 **X** 和 **Y** 上的点，使得每个相似索引数组元素形成一个线段，即 **X[i]** 和 **Y[i]** 形成一个线段，任务是找到可以从给定数组中选择的最大线段数。

**示例:**

> **输入:** X[] = {0，3，4，1，2}，Y[] = {3，2，0，1，4}
> **输出:** 3
> **说明:**线段集为{{1，1}，{4，0}，{0，3}}。
> 
> **输入:** X[] = {1，2，0}，Y[] = {2，0，1}
> **输出:** 2
> **说明:**线段集为{{1，2}，{2，0}}。

**方法:**通过观察发现只有当 **X[i] < X[j]** 和 **Y[i] > Y[j]** 或**时，两个线段(I，j)才会相交，反之亦然**可以解决这个问题。因此，使用[排序](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)和[二分搜索法](https://www.geeksforgeeks.org/binary-search/)可以解决这个问题，使用[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)可以找到这样的线段。

按照以下步骤解决给定的问题:

1.  初始化一个[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，说 **p** 来存储对 **{X[i]，Y[i]}** 作为一个元素。
2.  [按照 X 数线上点的升序对成对的向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/) **p** 进行排序，使每一条线段 **i** 满足相交的第一个条件，即**X【k】<X【I】**其中 **k < i** 。
3.  初始化一个[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如 **s** ，以降序存储**Y【I】**的值。
4.  从 **p** 的第一个元素开始，推 Y 坐标(即**p【0】)。第二次**)进入设定。
5.  迭代 **p** 的所有元素，对于每个元素:
    *   执行一个[二分搜索法](https://www.geeksforgeeks.org/binary-search/)找到**p【I】的[下界](https://www.geeksforgeeks.org/set-lower_bound-function-in-c-stl/)。第二**。
    *   如果没有得到[下界](https://www.geeksforgeeks.org/lower_bound-in-cpp/)，那就意味着 **p[i]。第二个**小于集合中的所有[元素。这就满足了第二个条件 **Y[i] < Y[k]** 其中 **k < i** ，所以推 **p[i]。第二次**进入**设定**。](https://www.geeksforgeeks.org/set-find-function-in-c-stl/)
    *   如果找到下限，则将其移除并按下 **p[i]。第二次**进入[设定](https://www.geeksforgeeks.org/set-in-cpp-stl/)。
6.  最后，返回作为结果的设置的[大小。](https://www.geeksforgeeks.org/setsize-c-stl/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum number of
// intersecting line segments possible
int solve(int N, int X[], int Y[])
{
    // Stores pairs of line
    // segments {X[i], Y[i])
    vector<pair<int, int> > p;

    for (int i = 0; i < N; i++) {
        // Push {X[i], Y[i]} into p
        p.push_back({ X[i], Y[i] });
    }

    // Sort p in ascending order
    // of points on X number line
    sort(p.begin(), p.end());

    // Stores the points on Y number
    // line in descending order
    set<int, greater<int> > s;

    // Insert the first Y point from p
    s.insert(p[0].second);

    for (int i = 0; i < N; i++) {

        // Binary search to find the
        // lower bound of p[i].second
        auto it = s.lower_bound(p[i].second);

        // If lower_bound doesn't exist
        if (it == s.end()) {

            // Insert p[i].second into the set
            s.insert(p[i].second);
        }
        else {

            // Erase the next lower
            //_bound from the set
            s.erase(*it);

            // Insert p[i].second
            // into the set
            s.insert(p[i].second);
        }
    }

    // Return the size of the set
    // as the final result
    return s.size();
}

// Driver Code
int main()
{
    // Given Input
    int N = 3;
    int X[] = { 1, 2, 0 };
    int Y[] = { 2, 0, 1 };

    // Function call to find the maximum
    // number of intersecting line segments
    int maxintersection = solve(N, X, Y);
    cout << maxintersection;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

// Function to find the maximum number of
// intersecting line segments possible
static int solve(int N, int X[], int Y[])
{

    // Stores pairs of line
    // segments {X[i], Y[i])
    ArrayList<int[]> p = new ArrayList<>();

    for(int i = 0; i < N; i++)
    {

        // Add {X[i], Y[i]} into p
        p.add(new int[] { X[i], Y[i] });
    }

    // Sort p in ascending order
    // of points on X number line
    Collections.sort(p, (p1, p2) -> {
        if (p1[0] != p2[0])
            return p1[0] - p2[0];

        return p1[1] - p2[1];
    });

    // Stores the points on Y number
    // line in ascending order
    TreeSet<Integer> s = new TreeSet<>();

    // Insert the first Y point from p
    s.add(p.get(0)[1]);

    for(int i = 0; i < N; i++)
    {

        // Binary search to find the
        // floor value of p.get(i)[1]
        Integer it = s.floor(p.get(i)[1]);

        // If floor value doesn't exist
        if (it == null)
        {

            // Insert p.get(i)[1] into the set
            s.add(p.get(i)[1]);
        }
        else
        {

            // Erase the next floor
            // value from the set
            s.remove(it);

            // Insert p.get(i)[1]
            // into the set
            s.add(p.get(i)[1]);
        }
    }

    // Return the size of the set
    // as the final result
    return s.size();
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int N = 3;
    int X[] = { 1, 2, 0 };
    int Y[] = { 2, 0, 1 };

    // Function call to find the maximum
    // number of intersecting line segments
    int maxintersection = solve(N, X, Y);
    System.out.println(maxintersection);
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
from bisect import bisect_left

# Function to find the maximum number of
# intersecting line segments possible
def solve(N, X, Y):

    # Stores pairs of line
    # segments {X[i], Y[i])
    p = []

    for i in range(N):

        # Push {X[i], Y[i]} into p
        p.append([X[i], Y[i]])

    # Sort p in ascending order
    # of points on X number line
    p = sorted(p)

    # Stores the points on Y number
    # line in descending order
    s = {}

    # Insert the first Y pofrom p
    s[p[0][1]] = 1

    for i in range(N):

        # Binary search to find the
        # lower bound of p[i][1]
        arr = list(s.keys())

        it = bisect_left(arr, p[i][1])

        # If lower_bound doesn't exist
        if (it == len(s)):

            # Insert p[i][1] into the set
            s[p[i][1]] = 1
        else:

            # Erase the next lower
            # _bound from the set
            del s[arr[it]]

            # Insert p[i][1]
            # into the set
            s[p[i][1]] = 1

    # Return the size of the set
    # as the final result
    return len(s)

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 3
    X = [1, 2, 0]
    Y = [2, 0, 1]

    # Function call to find the maximum
    # number of intersecting line segments
    maxintersection = solve(N, X, Y)

    print (maxintersection)

# This code is contributed by mohit kumar 29
```

**Output:** 

```
2
```

***时间复杂度:** O(N log N)*
***辅助空间:** O(N)*