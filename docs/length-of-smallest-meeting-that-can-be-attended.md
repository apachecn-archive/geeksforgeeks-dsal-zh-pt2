# 可参加的最小会议长度

> 原文:[https://www . geeksforgeeks . org/可参加的最小会议长度/](https://www.geeksforgeeks.org/length-of-smallest-meeting-that-can-be-attended/)

给定一个代表 **N** 会议开始和结束时间的**{开始，结束}** 形式的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-c-cpp/)**arr【】【】【】**，还给定了两个[数组](https://www.geeksforgeeks.org/array-data-structure/) **入口【】**和**存在【】**分别代表会议室的开放和关闭时间，任务是找到可以参加会议的最小时间。如果不能参加任何会议，则打印 **-1** 。

**示例:**

> **输入:** arr[][] = {{15，19}，{5，10}，{7，25}}，入口[] = {4，13，25，2}，存在[] = {10，21 }
> T3】输出:6
> T6】说明:
> **会议 1:** 时间 13 进入，间隔(15，19)参加会议，时间 21 退出。因此，会议总时间= 21–13 = 8。
> **会议 2:** 在时间 4 进入，在(5，10)参加会议，在时间 10 退出。因此，会议总时间= 10–4 = 6。
> **会议 3:** 时间 4 进入，间隔(7、25)参加会议。但是在时间 25 之后没有关闭时间。因此，花费的总时间是无限的。
> 因此，参加会议可以花费的最小时间单位是 6。
> 
> **输入:** arr[][] = {{1，2}}，入口[] = {1，2}，存在[] = {3，4 }
> T3】输出: 2

**天真法:**解决这个问题最简单的方法就是[遍历**arr【】【】**T5】对于每个区间 **{start <sub>i</sub> ，end <sub>i</sub> }** ，在数组**入口【】**中找到刚好小于或等于**arr【I】【0】**的值。另外，在数组**exist【】**中找到刚好大于或等于 **arr[i][1]** 的值。最后，打印恰好参加一次会议的最短时间。](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)

***时间复杂度:** O(N*max(P，M))，其中 M 和 P 是入口[]的大小，存在[]数组。*
***辅助空间:** O(1)*

**高效方法:**优化上述方法的思路是使用[排序算法](https://www.geeksforgeeks.org/sorting-algorithms/)和[二分搜索法技术](https://www.geeksforgeeks.org/binary-search/)。
按照以下步骤解决问题:

1.  [将](https://www.geeksforgeeks.org/sort-c-stl/) **入口【】**和**存在的数组【】**按递增顺序排序。
2.  初始化一个变量**和**来存储恰好参加一次会议的最短时间。
3.  遍历数组，对于会议的每个间隔，使用[上限](https://www.geeksforgeeks.org/upper_bound-in-cpp/)在**入口【】**数组中找到刚好小于或等于**起始<sub>I</sub>T3 的值，使用[下限](https://www.geeksforgeeks.org/lower_bound-in-cpp/)在**存在【】**数组中找到刚好大于或等于**结束<sub>I</sub>T11 的值。****
4.  最后，打印恰好参加一次会议的最短时间。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum time to
// attend exactly one meeting
int minTime(int meeting[][2], int n,
          vector<int> entrance, int m,
             vector<int> &exit, int p)
{

    // Stores minimum time to attend
    // exactly one meeting
    int ans = INT_MAX;

    // Sort entrance[] array
    sort(entrance.begin(), entrance.end());

    // Sort exit[] time
    sort(exit.begin(), exit.end());

    // Traverse meeting[][]
    for (int i = 0; i < n; i++) {

        // Stores start time of
        // current meeting
        int u = meeting[i][0];

        // Stores end time of
        // current meeting
        int v = meeting[i][1];

        // Find just greater value of
        // u in entrance[]
        auto it1
          = upper_bound(entrance.begin(),
                     entrance.end(), u);

        // Find just greater or equal value
        //  of u in entrance[]
        auto it2
            = lower_bound(exit.begin(),
                         exit.end(), v);

        // Stores enter time to attend
        // the current meeting
        int start = it1
              - entrance.begin() - 1;

        // Stores exist time after
        // attending the meeting   
        int end = it2 - exit.begin();

        // Update start lies in range [0, m -1]
        // and end lies in the range [0, p - 1]
        if (start >= 0 && start < m &&
                          end >= 0 && end < p)

            // Update ans             
            ans = min(ans,
                  exit[end] - entrance[start]);
    }

    // Return answer
    return ans >= INT_MAX ? -1 : ans;
}

// Driver Code
int main()
{

    // Stores interval of meeting
    int meeting[][2]
        = { { 15, 19 }, { 5, 10 }, { 7, 25 } };

    // Stores entrance timings
    vector<int> entrance = { 4, 13, 25, 2 };

    // Stores exit timings
    vector<int> exit = { 10, 25 };

    // Stores total count of  meetings
    int n = (sizeof(meeting))
               / sizeof(meeting[0]);

    // Stores total entrance timings
    int m = entrance.size();

    // Stores total exit timings
    int p = exit.size();

    // Minimum time
    cout << minTime(meeting, n, entrance,
                               m, exit, p)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG{

static Vector<Integer> exit =
       new Vector<>();

// Function to find the
// minimum time to attend
// exactly one meeting
static int minTime(int meeting[][], int n,
                   int[] entrance, int m,
                   int p)
{
  // Stores minimum time to attend
  // exactly one meeting
  int ans = Integer.MAX_VALUE;

  // Sort entrance[] array
  Arrays.sort(entrance);

  // Sort exit[] time
  Collections.sort(exit);

  // Traverse meeting[][]
  for (int i = 0; i < n; i++)
  {
    // Stores start time of
    // current meeting
    int u = meeting[i][0];

    // Stores end time of
    // current meeting
    int v = meeting[i][1];

    // Find just greater value of
    // u in entrance[]
    int it1 = upper_bound(entrance, 0,
                          entrance.length, u);

    // Find just greater or equal
    // value of u in entrance[]
    int it2 = lowerBound(exit, 0,
                         exit.size(), v);

    // System.out.println(exit.size());
    // Stores enter time to attend
    // the current meeting
    int start = it1 - 1  ;

    // Stores exist time after
    // attending the meeting   
    int end = it2 ;

    // Update start lies in range [0, m -1]
    // and end lies in the range [0, p - 1]
    if (start >= 0 && start < m &&
        end >= 0 && end < p)

      // Update ans   
      ans = Math.min(ans,
                     exit.get(end) -
                     entrance[start]);
  }

  // Return answer
  return ans >= Integer.MAX_VALUE ?
         -1 : ans;
}

static int upper_bound(int[] a, int low,
                       int high, int element)
{
  while(low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if(a[middle] > element)
      high = middle;
    else
      low = middle + 1;
  }
  return low;
}

static int lowerBound(Vector<Integer> vec,
                      int low, int high,
                      int element)
{
  int [] array =
         new int[vec.size()];
  int k = 0;

  for(Integer val : vec)
  {
    array[k] = val;
    k++;
  }

  // vec.clear();
  while (low < high)
  {
    int middle = low +
                 (high - low) / 2;

    if (element > array[middle])
    {
      low = middle + 1;
    } else
    {
      high = middle;
    }
  }
  return low;
}

// Driver Code
public static void main(String[] args)
{
  // Stores interval of meeting
  int meeting[][] = {{15, 19},
                     {5, 10},
                     {7, 25}};

  // Stores entrance timings
  int []entrance = {4, 13, 25, 2};

  // Stores exit timings
  exit.add(10);
  exit.add(25);

  // Stores total count of
  // meetings
  int n = meeting.length;

  // Stores total entrance
  // timings
  int m = entrance.length;

  // Stores total exit
  // timings
  int p = exit.size();

  // Minimum time
  System.out.print(minTime(meeting, n,
                           entrance, m,
                           p) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from bisect import bisect_left, bisect_right
import sys

# Function to find the minimum time to
# attend exactly one meeting
def minTime(meeting, n, entrance, m, exit, p):

    # Stores minimum time to attend
    # exactly one meeting
    ans = sys.maxsize

    # Sort entrance[] array
    entrance = sorted(entrance)

    # Sort exit[] time
    exit = sorted(exit)

    # Traverse meeting[][]
    for i in range(n):

        # Stores start time of
        # current meeting
        u = meeting[i][0]

        # Stores end time of
        # current meeting
        v = meeting[i][1]

        # Find just greater value of
        # u in entrance[]
        it1 = bisect_right(entrance, u)

        # Find just greater or equal value
        # of u in entrance[]
        it2 = bisect_left(exit, v)

        # Stores enter time to attend
        # the current meeting
        start = it1 - 1

        # Stores exist time after
        # attending the meeting
        end = it2

        # Update start lies in range [0, m -1]
        # and end lies in the range [0, p - 1]
        if (start >= 0 and start < m and
              end >= 0 and end < p):

            # Update ans
            ans = min(ans, exit[end] -
                       entrance[start])

    if ans >= sys.maxsize:
        ans = -1

    # Return answer
    return ans

# Driver Code
if __name__ == '__main__':

    # Stores interval of meeting
    meeting = [ [ 15, 19 ], [ 5, 10 ], [ 7, 25 ] ]

    # Stores entrance timings
    entrance = [ 4, 13, 25, 2 ]

    # Stores exit timings
    exit = [ 10, 25 ]

    # Stores total count of  meetings
    n = len(meeting)

    # Stores total entrance timings
    m = len(entrance)

    # Stores total exit timings
    p = len(exit)

    # Minimum time
    print(minTime(meeting, n, entrance,
                  m, exit, p))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static List<int> exit = new List<int>();

// Function to find the
// minimum time to attend
// exactly one meeting
static int minTime(int [,]meeting, int n,
                   int[] entrance, int m,
                   int p)
{

  // Stores minimum time to attend
  // exactly one meeting
  int ans = int.MaxValue;

  // Sort entrance[] array
  Array.Sort(entrance);

  // Sort exit[] time
  exit.Sort();

  // Traverse meeting[,]
  for(int i = 0; i < n; i++)
  {

    // Stores start time of
    // current meeting
    int u = meeting[i, 0];

    // Stores end time of
    // current meeting
    int v = meeting[i, 1];

    // Find just greater value of
    // u in entrance[]
    int it1 = upper_bound(entrance, 0,
                          entrance.Length, u);

    // Find just greater or equal
    // value of u in entrance[]
    int it2 = lowerBound(exit, 0,
                         exit.Count, v);

    // Console.WriteLine(exit.Count);
    // Stores enter time to attend
    // the current meeting
    int start = it1 - 1;

    // Stores exist time after
    // attending the meeting   
    int end = it2;

    // Update start lies in range [0, m -1]
    // and end lies in the range [0, p - 1]
    if (start >= 0 && start < m &&
          end >= 0 && end < p)

      // Update ans   
      ans = Math.Min(ans,
                     exit[end] -
                     entrance[start]);
  }

  // Return answer
  return ans >= int.MaxValue ?
          -1 : ans;
}

static int upper_bound(int[] a, int low,
                       int high, int element)
{
  while (low < high)
  {
    int middle = low + (high - low) / 2;

    if (a[middle] > element)
      high = middle;
    else
      low = middle + 1;
  }
  return low;
}

static int lowerBound(List<int> vec,
                      int low, int high,
                      int element)
{
  int [] array = new int[vec.Count];
  int k = 0;

  foreach(int val in vec)
  {
    array[k] = val;
    k++;
  }

  // vec.Clear();
  while (low < high)
  {
    int middle = low + (high - low) / 2;

    if (element > array[middle])
    {
      low = middle + 1;
    }
    else
    {
      high = middle;
    }
  }
  return low;
}

// Driver Code
public static void Main(String[] args)
{

  // Stores interval of meeting
  int [,]meeting = { { 15, 19 },
                     { 5, 10 },
                     { 7, 25 } };

  // Stores entrance timings
  int []entrance = { 4, 13, 25, 2 };

  // Stores exit timings
  exit.Add(10);
  exit.Add(25);

  // Stores total count of
  // meetings
  int n = meeting.GetLength(0);

  // Stores total entrance
  // timings
  int m = entrance.Length;

  // Stores total exit
  // timings
  int p = exit.Count;

  // Minimum time
  Console.Write(minTime(meeting, n,
                        entrance, m,
                        p) + "\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach
let exit = [];

// Function to find the
// minimum time to attend
// exactly one meeting
function minTime(meeting, n, entrance, m, p)
{

    // Stores minimum time to attend
    // exactly one meeting
    let ans = Number.MAX_VALUE;

    // Sort entrance[] array
    (entrance).sort(function(a, b){return a - b;});

    // Sort exit[] time
    (exit).sort(function(a, b){return a - b;});

    // Traverse meeting[][]
    for(let i = 0; i < n; i++)
    {

        // Stores start time of
        // current meeting
        let u = meeting[i][0];

        // Stores end time of
        // current meeting
        let v = meeting[i][1];

        // Find just greater value of
        // u in entrance[]
        let it1 = upper_bound(entrance, 0,
                              entrance.length, u);

        // Find just greater or equal
        // value of u in entrance[]
        let it2 = lowerBound(exit, 0,
                             exit.length, v);

        // System.out.println(exit.size());
        // Stores enter time to attend
        // the current meeting
        let start = it1 - 1;

        // Stores exist time after
        // attending the meeting  
        let end = it2;

        // Update start lies in range [0, m -1]
        // and end lies in the range [0, p - 1]
        if (start >= 0 && start < m &&
            end >= 0 && end < p)

          // Update ans  
          ans = Math.min(ans,
                         exit[end] -
                         entrance[start]);
    }

    // Return answer
    return ans >= Number.MAX_VALUE ?
            -1 : ans;
}

function upper_bound(a, low, high, element)
{
    while(low < high)
    {
        let middle = low +
             Math.floor((high - low) / 2);

        if (a[middle] > element)
            high = middle;
        else
            low = middle + 1;
    }
    return low;
}

function lowerBound(vec, low, high, element)
{
    let array = new Array(vec.length);
    let k = 0;

    for(let val = 0; val < vec.length; val++)
    {
        array[k] = vec[val];
        k++;
    }

    // vec.clear();
    while (low < high)
    {
        let middle = low +
        Math.floor((high - low) / 2);

        if (element > array[middle])
        {
            low = middle + 1;
        }
        else
        {
            high = middle;
        }
    }
    return low;
}

// Driver Code   

// Stores interval of meeting
let meeting = [ [ 15, 19 ],
                [ 5, 10 ],
                [ 7, 25 ] ];

// Stores entrance timings
let entrance = [ 4, 13, 25, 2 ];

// Stores exit timings
exit.push(10);
exit.push(25);

// Stores total count of
// meetings
let n = meeting.length;

// Stores total entrance
// timings
let m = entrance.length;

// Stores total exit
// timings
let p = exit.length;

// Minimum time
document.write(minTime(meeting, n, entrance,
                       m, p) + "<br>");

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
6
```

***时间复杂度:** O(N * max(logP，logM))其中 M 和 P 是入口[]和存在[]数组的长度。*
***辅助空间:** O(1)*