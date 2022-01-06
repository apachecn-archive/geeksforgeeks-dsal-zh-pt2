# 与 3 个给定单元之间的最小路径相连的最小单元数

> 原文:[https://www . geeksforgeeks . org/用 3 个给定单元之间的最小路径连接的最小单元数/](https://www.geeksforgeeks.org/minimum-numbers-of-cells-that-are-connected-with-the-smallest-path-between-3-given-cells/)

给定一个矩阵的 3 个单元 **(X1，Y1)** 、 **(X2，Y2)** 和 **(X3，Y3)** 的坐标。任务是找到连接所有这三个单元格的最小路径，并打印通过该路径连接的所有单元格的计数。
**注意:**只有上、下、左、右可能的招式。
**举例:**

> **输入:** X1 = 0，Y1 = 0，X2 = 1，Y2 = 1，X3 = 2，Y3 = 2
> **输出:** 5
> (0，0)，(1，0)，(1，1)，(1，2)，(2，2)为所需单元格。
> **输入:** X1 = 0，Y1 = 0，X2 = 2，Y2 = 0，X3 = 1，Y3 = 1
> **输出:** 4

**方法:**首先对单元格进行排序，从最开始行数最小的到最后行数最大的。另外，将这三个单元格中的最小列数和最大列数分别存储在变量 **MinCol** 和 **MaxCol** 中。
之后，将中间单元格的行号(从已排序的单元格中)存储在变量**中行**中，并将该**中行**的所有单元格从 **MinCol** 标记为 **MaxCol** 。
现在我们的最后一步是标记第一个和第三个单元格的所有列号，直到它们到达**中间行**。
这里，标记是指我们将所需的单元格坐标存储在[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)中。因此，我们的答案将是这个集合的大小。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum cells that are
// connected via the minimum length path
int Minimum_Cells(vector<pair<int, int> > v)
{
    int col[3], i, j;
    for (i = 0; i < 3; i++) {
        int column_number = v[i].second;

        // Array to store column number
        // of the given cells
        col[i] = column_number;
    }

    sort(col, col + 3);

    // Sort cells in ascending
    // order of row number
    sort(v.begin(), v.end());

    // Middle row number
    int MidRow = v[1].first;

    // Set pair to store required cells
    set<pair<int, int> > s;

    // Range of column number
    int Maxcol = col[2], MinCol = col[0];

    // Store all cells of middle row
    // within column number range
    for (i = MinCol; i <= Maxcol; i++) {
        s.insert({ MidRow, i });
    }

    for (i = 0; i < 3; i++) {
        if (v[i].first == MidRow)
            continue;

        // Final step to store all the column number
        // of 1st and 3rd cell upto MidRow
        for (j = min(v[i].first, MidRow);
             j <= max(v[i].first, MidRow); j++) {
            s.insert({ j, v[i].second });
        }
    }

    return s.size();
}

// Driver Function
int main()
{
    // vector pair to store X, Y, Z
    vector<pair<int, int> > v = { { 0, 0 }, { 1, 1 }, { 2, 2 } };

    cout << Minimum_Cells(v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
import java.awt.Point;
public class Main
{
    // Function to return the minimum cells that are
    // connected via the minimum length path
    static int Minimum_Cells(Vector<Point> v)
    {
        int[] col = new int[3];
        int i, j;
        for (i = 0; i < 3; i++) {
            int column_number = v.get(i).y;

            // Array to store column number
            // of the given cells
            col[i] = column_number;
        }

        Arrays.sort(col);

        // Middle row number
        int MidRow = v.get(1).x;

        // Set pair to store required cells
        Set<Point> s = new HashSet<Point>();

        // Range of column number
        int Maxcol = col[2], MinCol = col[0];

        // Store all cells of middle row
        // within column number range
        for (i = MinCol; i <= Maxcol; i++) {
            s.add(new Point(MidRow, i));
        }

        for (i = 0; i < 3; i++) {
            if (v.get(i).x == MidRow)
                continue;

            // Final step to store all the column number
            // of 1st and 3rd cell upto MidRow
            for (j = Math.min(v.get(i).x, MidRow);
                 j <= Math.max(v.get(i).x, MidRow); j++) {
                s.add(new Point(j, v.get(i).x));
            }
        }

        return s.size();
    }

  // Driver code
    public static void main(String[] args)
    {

        // vector pair to store X, Y, Z
        Vector<Point> v = new Vector<Point>();
        v.add(new Point(0, 0));
        v.add(new Point(1, 1));
        v.add(new Point(2, 2));

        System.out.print(Minimum_Cells(v));
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum cells that
# are connected via the minimum length path
def Minimum_Cells(v) :

    col = [0] * 3
    for i in range(3) :
        column_number = v[i][1]

        # Array to store column number
        # of the given cells
        col[i] = column_number

    col.sort()

    # Sort cells in ascending order
    # of row number
    v.sort()

    # Middle row number
    MidRow = v[1][0]

    # Set pair to store required cells
    s = set()

    # Range of column number
    Maxcol = col[2]
    MinCol = col[0]

    # Store all cells of middle row
    # within column number range
    for i in range(MinCol, int(Maxcol) + 1) :
        s.add((MidRow, i))

    for i in range(3) :
        if (v[i][0] == MidRow) :
            continue;

        # Final step to store all the column
        # number of 1st and 3rd cell upto MidRow
        for j in range(min(v[i][0], MidRow),
                       max(v[i][0], MidRow) + 1) :
            s.add((j, v[i][1]));

    return len(s)

# Driver Code
if __name__ == "__main__" :

    # vector pair to store X, Y, Z
    v = [(0, 0 ), ( 1, 1 ), ( 2, 2 )]

    print(Minimum_Cells(v))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to return the minimum cells that are
    // connected via the minimum length path
    static int Minimum_Cells(List<Tuple<int, int>> v)
    {
        int[] col = new int[3];
        int i, j;
        for (i = 0; i < 3; i++) {
            int column_number = v[i].Item2;

            // Array to store column number
            // of the given cells
            col[i] = column_number;
        }

        Array.Sort(col);

        // Sort cells in ascending
        // order of row number
        v.Sort();

        // Middle row number
        int MidRow = v[1].Item1;

        // Set pair to store required cells
        HashSet<Tuple<int, int>> s = new HashSet<Tuple<int, int>>();

        // Range of column number
        int Maxcol = col[2], MinCol = col[0];

        // Store all cells of middle row
        // within column number range
        for (i = MinCol; i <= Maxcol; i++) {
            s.Add(new Tuple<int,int>(MidRow, i));
        }

        for (i = 0; i < 3; i++) {
            if (v[i].Item1 == MidRow)
                continue;

            // Final step to store all the column number
            // of 1st and 3rd cell upto MidRow
            for (j = Math.Min(v[i].Item1, MidRow);
                 j <= Math.Max(v[i].Item1, MidRow); j++) {
                s.Add(new Tuple<int,int>(j, v[i].Item1));
            }
        }

        return s.Count;
    }

  static void Main()
  {

    // vector pair to store X, Y, Z
    List<Tuple<int, int>> v = new List<Tuple<int, int>>();
    v.Add(new Tuple<int,int>(0, 0));
    v.Add(new Tuple<int,int>(1, 1));
    v.Add(new Tuple<int,int>(2, 2));

    Console.Write(Minimum_Cells(v));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the minimum cells that are
    // connected via the minimum length path
    function Minimum_Cells(v)
    {
        let col = new Array(3);
        let i, j;
        for (i = 0; i < 3; i++) {
            let column_number = v[i][1];

            // Array to store column number
            // of the given cells
            col[i] = column_number;
        }

        col.sort(function(a, b){return a - b});

        // Sort cells in ascending
        // order of row number
        v.sort();

        // Middle row number
        let MidRow = v[1][0];

        // Set pair to store required cells
        let s = new Set();

        // Range of column number
        let Maxcol = col[2], MinCol = col[0];

        // Store all cells of middle row
        // within column number range
        for (i = MinCol; i <= Maxcol; i++) {
            s.add([MidRow, i]);
        }

        for (i = 0; i < 3; i++) {
            if (v[i][0] == MidRow)
                continue;

            // Final step to store all the column number
            // of 1st and 3rd cell upto MidRow
            for (j = Math.min(v[i][0], MidRow);
                 j <= Math.max(v[i][0], MidRow); j++) {
                s.add([j, v[i][0]]);
            }
        }

        return s.size-2;
    }

    // vector pair to store X, Y, Z
    let v = [];
    v.push([0, 0]);
    v.push([1, 1]);
    v.push([2, 2]);

    document.write(Minimum_Cells(v));

    // This code is contributed by decode2207.
</script>
```

**Output:** 

```
5
```