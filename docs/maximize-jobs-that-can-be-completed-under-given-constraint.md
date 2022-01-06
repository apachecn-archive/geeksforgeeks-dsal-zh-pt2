# 最大化在给定约束条件下可以完成的任务

> 原文:[https://www . geeksforgeeks . org/最大化在给定约束下可以完成的任务/](https://www.geeksforgeeks.org/maximize-jobs-that-can-be-completed-under-given-constraint/)

给定一个表示作业数量的整数 **N** 和一个矩阵**范围[]** ，该矩阵由需要完成的每个作业的范围**【开始日，结束日】**组成，任务是找到可以完成的最大可能作业。
**举例:**

> **输入:** N = 5，范围= {{1，5}，{1，5}，{1，5}，{2，3}，{2，3}}
> **输出:** 5
> **说明:**第 1 天的作业 1、第 2 天的作业 4、第 3 天的作业 5、第 4 天的作业 2、第 5 天的作业 3
> 
> **输入:** N=6，范围= {{1，3}、{1，3}、{2，3}、{2，3}、{1，4}、{2，5 } }
> T3】输出: 5

**方法:**使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)可以解决上述问题。按照以下步骤解决问题:

*   查找工作范围中的最小和最大日期。
*   按照**开始日**的递增顺序对所有作业进行排序。
*   从最小到最大的一天迭代，每第 I<sup>天，选择最少的**结束日**可以在该天完成的作业。</sup>
*   为了执行上述步骤，维护一个 **Min Heap** ，在每一个 i <sup>第</sup>天，将当天可以完成的作业插入到按**结束日** 排序的 **Min Heap** *中。如果有任何工作可以在第 I<sup>天完成，请考虑结束日期最低的工作，并增加已完成工作的数量。</sup>*
*   对所有日期重复此过程，最后打印已完成的作业数。

下面是上述方法的一个实现:

## C++

```
// C++ Program to implement the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find maxiumum
// number of jobs
int find_maximum_jobs(
    int N,
    vector<pair<int, int> > ranges)
{
    // Min Heap
    priority_queue<int, vector<int>,
                   greater<int> >
        queue;

    // Sort ranges by start day
    sort(ranges.begin(), ranges.end());

    // Stores the minimum and maximum
    // day in the ranges
    int min_day = ranges[0].first;
    int max_day = 0;

    for (int i = 0; i < N; i++)
        max_day
            = max(max_day,
                  ranges[i].second);

    int index = 0, count_jobs = 0;

    // Iterating from min_day to max_day
    for (int i = min_day; i <= max_day; i++) {

        // Insert the end day of the jobs
        // which can be completed on
        // i-th day in a priority queue
        while (index < ranges.size()
               && ranges[index].first <= i) {

            queue.push(ranges[index].second);
            index++;
        }

        // Pop all jobs whose end day
        // is less than current day
        while (!queue.empty()
               && queue.top() < i)
            queue.pop();

        // If queue is empty, no job
        // can be completed on
        // the i-th day
        if (queue.empty())
            continue;

        // Increment the count of
        // jobs completed
        count_jobs++;

        // Pop the job with
        // least end day
        queue.pop();
    }

    // Return the jobs
    // on the last day
    return count_jobs;
}

// Driver Code
int main()
{

    int N = 5;
    vector<pair<int, int> > ranges;
    ranges.push_back({ 1, 5 });
    ranges.push_back({ 1, 5 });
    ranges.push_back({ 1, 5 });
    ranges.push_back({ 2, 3 });
    ranges.push_back({ 2, 3 });

    cout << find_maximum_jobs(N, ranges);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to implement the
// above approach
import java.io.*;
import java.util.*;

class GFG {

  // Function to find maxiumum
  // number of jobs
  static int find_maximum_jobs(int N, ArrayList<ArrayList<Integer>> ranges)
  {
    // Min Heap
    ArrayList<Integer> queue = new ArrayList<Integer>();
    // Sort ranges by start day
    Collections.sort(ranges, new Comparator<ArrayList<Integer>>() {   
      @Override
      public int compare(ArrayList<Integer> o1, ArrayList<Integer> o2) {
        return o1.get(0).compareTo(o2.get(0));
      }              
    });

    // Stores the minimum and maximum
    // day in the ranges
    int min_day = ranges.get(0).get(0);
    int max_day = 0;
    for (int i = 0; i < N; i++)
      max_day = Math.max(max_day, ranges.get(i).get(1));
    int index = 0, count_jobs = 0;

    // Iterating from min_day to max_day
    for (int i = min_day; i <= max_day; i++)
    {
      // Insert the end day of the jobs
      // which can be completed on
      // i-th day in a priority queue
      while (index < ranges.size() && ranges.get(index).get(0) <= i)
      {
        queue.add(ranges.get(index).get(1));
        index++;
      }
      Collections.sort(queue);

      // Pop all jobs whose end day
      // is less than current day
      while (queue.size() > 0 && queue.get(0) < i)
        queue.remove(0);

      // If queue is empty, no job
      // can be completed on
      // the i-th day
      if (queue.size() == 0)
        continue;
      // Increment the count of
      // jobs completed
      count_jobs++;

      // Pop the job with
      // least end day
      queue.remove(0);
    }
    // Return the jobs
    // on the last day
    return count_jobs;

  }

  // Driver code
  public static void main (String[] args) {

    int N = 5;
    ArrayList<ArrayList<Integer>> ranges = new ArrayList<ArrayList<Integer>>();
    ranges.add(new ArrayList<Integer>(Arrays.asList(1, 5)));
    ranges.add(new ArrayList<Integer>(Arrays.asList(1, 5)));
    ranges.add(new ArrayList<Integer>(Arrays.asList(1, 5)));
    ranges.add(new ArrayList<Integer>(Arrays.asList(2, 3)));
    ranges.add(new ArrayList<Integer>(Arrays.asList(2, 3)));
    System.out.println(find_maximum_jobs(N, ranges));
  }
}
// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 Program to implement the
# above approach

# Function to find maxiumum
# number of jobs
def find_maximum_jobs(N, ranges) :

    # Min Heap
    queue = []

    # Sort ranges by start day
    ranges.sort()

    # Stores the minimum and maximum
    # day in the ranges
    min_day = ranges[0][0]
    max_day = 0
    for i in range(N) :
      max_day = max(max_day, ranges[i][1])
    index, count_jobs = 0, 0

    # Iterating from min_day to max_day
    for i in range(min_day, max_day + 1) :

      # Insert the end day of the jobs
      # which can be completed on
      # i-th day in a priority queue
      while (index < len(ranges) and ranges[index][0] <= i) :

        queue.append(ranges[index][1])
        index += 1

      queue.sort()

      # Pop all jobs whose end day
      # is less than current day
      while (len(queue) > 0 and queue[0] < i) :
        queue.pop(0)

      # If queue is empty, no job
      # can be completed on
      # the i-th day
      if (len(queue) == 0) :
        continue

      # Increment the count of
      # jobs completed
      count_jobs += 1

      # Pop the job with
      # least end day
      queue.pop(0)

    # Return the jobs
    # on the last day
    return count_jobs

    # Driver code
N = 5
ranges = []
ranges.append((1, 5))
ranges.append((1, 5))
ranges.append((1, 5))
ranges.append((2, 3))
ranges.append((2, 3))

print(find_maximum_jobs(N, ranges))

# This code is contributed by divyeshrabadiya07.
```

## C#

```
// C# Program to implement the
// above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to find maxiumum
  // number of jobs
  static int find_maximum_jobs(int N, List<Tuple<int, int>> ranges)
  {
    // Min Heap
    List<int> queue = new List<int>();

    // Sort ranges by start day
    ranges.Sort();

    // Stores the minimum and maximum
    // day in the ranges
    int min_day = ranges[0].Item1;
    int max_day = 0;
    for (int i = 0; i < N; i++)
      max_day = Math.Max(max_day, ranges[i].Item2);
    int index = 0, count_jobs = 0;

    // Iterating from min_day to max_day
    for (int i = min_day; i <= max_day; i++)
    {

      // Insert the end day of the jobs
      // which can be completed on
      // i-th day in a priority queue
      while (index < ranges.Count && ranges[index].Item1 <= i)
      {
        queue.Add(ranges[index].Item2);
        index++;
      }
      queue.Sort();

      // Pop all jobs whose end day
      // is less than current day
      while (queue.Count > 0 && queue[0] < i)
        queue.RemoveAt(0);

      // If queue is empty, no job
      // can be completed on
      // the i-th day
      if (queue.Count == 0)
        continue;

      // Increment the count of
      // jobs completed
      count_jobs++;

      // Pop the job with
      // least end day
      queue.RemoveAt(0);
    }

    // Return the jobs
    // on the last day
    return count_jobs;
  }

  // Driver code
  static void Main()
  {
    int N = 5;
    List<Tuple<int, int>> ranges = new List<Tuple<int, int>>();
    ranges.Add(new Tuple<int,int>(1, 5));
    ranges.Add(new Tuple<int,int>(1, 5));
    ranges.Add(new Tuple<int,int>(1, 5));
    ranges.Add(new Tuple<int,int>(2, 3));
    ranges.Add(new Tuple<int,int>(2, 3));

    Console.Write(find_maximum_jobs(N, ranges));
  }
}

// This code is contributed by divyesh072019.
```

**Output:** 

```
5
```

***时间复杂度:** O(Xlog(N))，其中 X 为最大和最小日差，N 为作业数。*
***辅助空间:** O(N <sup>2</sup> )*