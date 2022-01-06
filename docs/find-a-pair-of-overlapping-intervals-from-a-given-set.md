# 从给定的集合中找出一对重叠的间隔

> 原文:[https://www . geeksforgeeks . org/find-一对来自给定集合的重叠间隔/](https://www.geeksforgeeks.org/find-a-pair-of-overlapping-intervals-from-a-given-set/)

给定一个具有表格每一行 **{l，r}** 的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/) **arr[][]** ，任务是找到一对 **(i，j)** ，使得 **i <sup>第</sup>T11】区间位于 **j <sup>第</sup>T15】区间内。如果存在多个解决方案，则打印其中的任何一个。否则，打印 **-1** 。****

**示例:**

> **输入:** N = 5，arr[][] = { { 1，5 }，{2，10}，{ 3，10 }，{2，2}，{ 2，15}}
> **输出:**3 0
> T6】解释:【2，2】位于【1，5】内部。
> 
> **输入:** N = 4，arr[][] = { { 2，10 }，{ 1，9 }，{ 1，8 }，{ 1，7 } }
> **输出:** -1
> **说明:**不存在这样的区间对。

**原生方法:**解决这个问题最简单的方法是[生成数组中所有可能的对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)。对于每对 **(i，j)** ，检查 **i <sup>第</sup>T9】间隔是否在 **j <sup>第</sup>T13】间隔内。如果发现是真的，那么打印成对。否则，打印 **-1** 。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*****

**有效方法:**思路是[先按左边框升序对线段](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序，在左边框相等的情况下，按右边框降序对线段进行排序。然后，只需通过跟踪最大右边界来找到相交间隔。

按照以下步骤解决问题:

1.  [根据间隔的左边框对间隔的给定数组](https://www.geeksforgeeks.org/sorting-a-vector-in-c/)进行排序，如果任意两个左边框相等，则按照右边框的降序对它们进行排序。
2.  现在，从左向右遍历，保留已处理线段的最大右边界，并将其与当前线段进行比较。
3.  如果线段重叠，打印它们的索引。
4.  否则，遍历后，如果没有发现重叠段，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find a pair(i, j) such that
// i-th interval lies within the j-th interval
void findOverlapSegement(int N, int a[], int b[])
{

    // Store interval and index of the interval
    // in the form of { {l, r}, index }
    vector<pair<pair<int, int>, int> > tup;

    // Traverse the array, arr[][]
    for (int i = 0; i < N; i++) {

        int x, y;

        // Stores l-value of
        // the interval
        x = a[i];

        // Stores r-value of
        // the interval
        y = b[i];

        // Push current interval and index into tup
        tup.push_back(pair<pair<int, int>, int>(
            pair<int, int>(x, y), i));
    }

    // Sort the vector based on l-value
    // of the intervals
    sort(tup.begin(), tup.end());

    // Stores r-value of current interval
    int curr = tup[0].first.second;

    // Stores index of current interval
    int currPos = tup[0].second;

    // Traverse the vector, tup[]
    for (int i = 1; i < N; i++) {

        // Stores l-value of previous interval
        int Q = tup[i - 1].first.first;

        // Stores l-value of current interval
        int R = tup[i].first.first;

        // If Q and R are equal
        if (Q == R) {

            // Print the index of interval
            if (tup[i - 1].first.second
                < tup[i].first.second)
                cout << tup[i - 1].second << ' '
                     << tup[i].second;

            else
                cout << tup[i].second << ' '
                     << tup[i - 1].second;

            return;
        }

        // Stores r-value of current interval
        int T = tup[i].first.second;

        // If T is less than or equal to curr
        if (T <= curr) {
            cout << tup[i].second << ' ' << currPos;
            return;
        }
        else {

            // Update curr
            curr = T;

            // Update currPos
            currPos = tup[i].second;
        }
    }

    // If such intervals found
    cout << "-1 -1";
}

// Driver Code
int main()
{

    // Given l-value of segments
    int a[] = { 1, 2, 3, 2, 2 };

    // Given r-value of segments
    int b[] = { 5, 10, 10, 2, 15 };

    // Given size
    int N = sizeof(a) / sizeof(int);

    // Function Call
    findOverlapSegement(N, a, b);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class pair{
  int l,r,index;

  pair(int l, int r, int index){
    this.l = l;
    this.r = r;
    this.index=index;
  }
}
class GFG {

  // Function to find a pair(i, j) such that
  // i-th interval lies within the j-th interval
  static void findOverlapSegement(int N, int[] a, int[] b)
  {

    // Store interval and index of the interval
    // in the form of { {l, r}, index }
    ArrayList<pair> tup = new ArrayList<>();

    // Traverse the array, arr[][]
    for (int i = 0; i < N; i++) {

      int x, y;

      // Stores l-value of
      // the interval
      x = a[i];

      // Stores r-value of
      // the interval
      y = b[i];

      // Push current interval and index into tup
      tup.add(new pair(x, y, i));
    }

    // Sort the vector based on l-value
    // of the intervals
    Collections.sort(tup,(aa,bb)->(aa.l!=bb.l)?aa.l-bb.l:aa.r-bb.r);

    // Stores r-value of current interval
    int curr = tup.get(0).r;

    // Stores index of current interval
    int currPos = tup.get(0).index;

    // Traverse the vector, tup[]
    for (int i = 1; i < N; i++) {

      // Stores l-value of previous interval
      int Q = tup.get(i - 1).l;

      // Stores l-value of current interval
      int R = tup.get(i).l;

      // If Q and R are equal
      if (Q == R) {

        // Print the index of interval
        if (tup.get(i - 1).r < tup.get(i).r)
          System.out.print(tup.get(i - 1).index + " " + tup.get(i).index);

        else
          System.out.print(tup.get(i).index + " " + tup.get(i - 1).index);

        return;
      }

      // Stores r-value of current interval
      int T = tup.get(i).r;

      // If T is less than or equal to curr
      if (T <= curr) {
        System.out.print(tup.get(i).index + " " + currPos);
        return;
      }
      else {

        // Update curr
        curr = T;

        // Update currPos
        currPos = tup.get(i).index;
      }
    }

    // If such intervals found
    System.out.print("-1 -1");
  }    

  // Driver code
  public static void main (String[] args)
  {

    // Given l-value of segments
    int[] a = { 1, 2, 3, 2, 2 };

    // Given r-value of segments
    int[] b = { 5, 10, 10, 2, 15 };

    // Given size
    int N = a.length;

    // Function Call
    findOverlapSegement(N, a, b);
  }
}

// This code is contributed by offbeat.
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find a pair(i, j) such that
# i-th interval lies within the j-th interval
def findOverlapSegement(N, a, b) :

    # Store interval and index of the interval
    # in the form of { {l, r}, index }
    tup = []

    # Traverse the array, arr[][]
    for i in range(N) :

        # Stores l-value of
        # the interval
        x = a[i]

        # Stores r-value of
        # the interval
        y = b[i]

        # Push current interval and index into tup
        tup.append(((x,y),i))

    # Sort the vector based on l-value
    # of the intervals
    tup.sort()

    # Stores r-value of current interval
    curr = tup[0][0][1]

    # Stores index of current interval
    currPos = tup[0][1]

    # Traverse the vector, tup[]
    for i in range(1,N) :

        # Stores l-value of previous interval
        Q = tup[i - 1][0][0]

        # Stores l-value of current interval
        R = tup[i][0][0]

        # If Q and R are equal
        if Q == R :

            # Print the index of interval
            if tup[i - 1][0][1] < tup[i][0][1] :

                print(tup[i - 1][1], tup[i][1])

            else :

                print(tup[i][1], tup[i - 1][1])

            return

        # Stores r-value of current interval
        T = tup[i][0][1]

        # If T is less than or equal to curr
        if (T <= curr) :

            print(tup[i][1], currPos)

            return
        else :

            # Update curr
            curr = T

            # Update currPos
            currPos = tup[i][1]

    # If such intervals found
    print("-1", "-1", end = "")

# Given l-value of segments
a = [ 1, 2, 3, 2, 2 ]

# Given r-value of segments
b = [ 5, 10, 10, 2, 15 ]

# Given size
N = len(a)

# Function Call
findOverlapSegement(N, a, b)

# This code is contributed by divyesh072019
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find a pair(i, j) such that
  // i-th interval lies within the j-th interval
  static void findOverlapSegement(int N, int[] a, int[] b)
  {

    // Store interval and index of the interval
    // in the form of { {l, r}, index }
    List<Tuple<Tuple<int,int>, int>> tup = new List<Tuple<Tuple<int,int>, int>>();

    // Traverse the array, arr[][]
    for (int i = 0; i < N; i++) {

      int x, y;

      // Stores l-value of
      // the interval
      x = a[i];

      // Stores r-value of
      // the interval
      y = b[i];

      // Push current interval and index into tup
      tup.Add(new Tuple<Tuple<int,int>, int>(new Tuple<int, int>(x, y), i));
    }

    // Sort the vector based on l-value
    // of the intervals
    tup.Sort();

    // Stores r-value of current interval
    int curr = tup[0].Item1.Item2;

    // Stores index of current interval
    int currPos = tup[0].Item2;

    // Traverse the vector, tup[]
    for (int i = 1; i < N; i++) {

      // Stores l-value of previous interval
      int Q = tup[i - 1].Item1.Item1;

      // Stores l-value of current interval
      int R = tup[i].Item1.Item1;

      // If Q and R are equal
      if (Q == R) {

        // Print the index of interval
        if (tup[i - 1].Item1.Item2 < tup[i].Item1.Item2)
          Console.Write(tup[i - 1].Item2 + " " + tup[i].Item2);

        else
          Console.Write(tup[i].Item2 + " " + tup[i - 1].Item2);

        return;
      }

      // Stores r-value of current interval
      int T = tup[i].Item1.Item2;

      // If T is less than or equal to curr
      if (T <= curr) {
        Console.Write(tup[i].Item2 + " " + currPos);
        return;
      }
      else {

        // Update curr
        curr = T;

        // Update currPos
        currPos = tup[i].Item2;
      }
    }

    // If such intervals found
    Console.Write("-1 -1");
  }    

  // Driver code
  static void Main()
  {

    // Given l-value of segments
    int[] a = { 1, 2, 3, 2, 2 };

    // Given r-value of segments
    int[] b = { 5, 10, 10, 2, 15 };

    // Given size
    int N = a.Length;

    // Function Call
    findOverlapSegement(N, a, b);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find a pair(i, j) such that
// i-th interval lies within the j-th interval
function findOverlapSegement(N, a, b)
{

    // Store interval and index of the interval
    // in the form of { {l, r}, index }
    var tup = [];

    // Traverse the array, arr[][]
    for (var i = 0; i < N; i++) {

          var x, y;

          // Stores l-value of
         // the interval
          x = a[i];

          // Stores r-value of
          // the interval
          y = b[i];

          // Push current interval and index into tup
        tup.push([[x, y], i]);
    }

    // Sort the vector based on l-value
    // of the intervals
    tup.sort((a,b) =>
    {
       if(a[0][0] == b[0][0])
       {
           return a[0][1] - b[0][1];
       }

       var tmp = (a[0][0] - b[0][0]);
       console.log(tmp);

       return (a[0][0] - b[0][0])
    });

    // Stores r-value of current interval
    var curr = tup[0][0][1];

    // Stores index of current interval
    var currPos = tup[0][1];

    // Traverse the vector, tup[]
    for (var i = 1; i < N; i++) {

        // Stores l-value of previous interval
        var Q = tup[i - 1][0][0];

        // Stores l-value of current interval
        var R = tup[i][0][0];

        // If Q and R equal
        if (Q == R) {

            // If Y value of immediate previous
            // interval is less than Y value of
            // current interval
            if (tup[i - 1][0][1]
                < tup[i][0][1]) {

                // Print the index of interval
                document.write(tup[i - 1][1] + " " + tup[i][1]);
                return;
            }

            else {
                document.write(tup[i][1] + " " + tup[i - 1][1]);
                return;
            }
        }

         // Stores r-value of current interval
        var T = tup[i][0][1];

        // T is less than or equal to curr
        if (T <= curr) {
             document.write(tup[i][1] + " " + currPos);
             return;
        }
        else {

            // Update curr
            curr = T;

            // Update currPos
            currPos = tup[i][1];
        }
    }

    // If such intervals found
    document.write("-1 -1");
}

// Driver Code
// Given l-value of segments
    let a = [ 1, 2, 3, 2, 2 ];

    // Given r-value of segments
    let b = [ 5, 10, 10, 2, 15 ];

    // Given size
    let N = a.length;

    // Function Call
    findOverlapSegement(N, a, b);

// This code is contributed by Dharanendra L V.
</script>
```

**Output:** 

```
3 0
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*