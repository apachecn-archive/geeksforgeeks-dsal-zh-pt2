# 最长单调递增子序列大小(N log N):简单实现

> 原文:[https://www . geesforgeks . org/最长-单调递增-子序列-size-n-log-n-simple-implementation/](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n-simple-implementation/)

给定一个随机数数组，找出数组中最长的单调递增子序列。
如果你想理解 O(NlogN)方法，这里解释的很清楚。
在这篇文章中，我们讨论了一种使用 stl 实现 O(NlogN)方法的简单且省时的方法。下面是 LIS O(NlogN)的代码:

## C++

```
// C++ implementation
// to find LIS
#include<iostream>
#include<algorithm>
#include<set>
using namespace std;

// Return length of LIS in arr[] of size N
int lis(int arr[], int N)
{
    int i;
    set<int> s;
    set<int>::iterator k;
    for (i=0; i<N; i++)
    {
        // Check if the element was actually inserted
        // An element in set is not inserted if it is
        // already present. Please see
        // https://www.geeksforgeeks.org/set-insert-function-in-c-stl/
        if (s.insert(arr[i]).second)
        {
            // Find the position of inserted element in iterator k
            k = s.find(arr[i]);

            k++;  // Find the next greater element in set

            // If the new element is not inserted at the end, then
            // remove the greater element next to it (This is tricky)
            if (k!=s.end()) s.erase(k);
        }
    }

    // Note that set s may not contain actual LIS, but its size gives
    // us the length of LIS
    return s.size();
}

int main()
{
    int arr[] = {8, 9, 12, 10, 11};
    int n = sizeof(arr)/sizeof(arr[0]);
    cout << lis(arr, n)<< endl;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// to find LIS
import java.util.*;
class GFG{

// Return length of LIS
// in arr[] of size N
static int lis(int arr[],
               int N)
{
  int i;
  HashSet<Integer> s = new HashSet<>();
  for (i = 0; i < N; i++)
  {
    // Check if the element
    // was actually inserted
    // An element in set is
    // not inserted if it is
    // already present. Please see
    // https://www.geeksforgeeks.
    // org/set-insert-function-in-c-stl/
    int k = 0;
    int size = s.size();
    if (s.add(arr[i]))
    {
      // Find the position of
      // inserted element in iterator k
      if(s.contains(arr[i]))
        k++; 

      // Find the next
      // greater element in set
      // If the new element is not
      // inserted at the end, then
      // remove the greater element
      // next to it.
      if (size == s.size())
        s.remove(k + 1);
    }
  }

  // Note that set s may not contain
  // actual LIS, but its size gives
  // us the length of LIS
  return s.size();
}

public static void main(String[] args)
{
  int arr[] = {8, 9, 12, 10, 11};
  int n = arr.length;
  System.out.print(lis(arr, n) + "\n");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python implementation
# to find LIS

# Return length of LIS
# in arr of size N
def lis(arr, N):
    s = set();
    for i in range(N):

        # Check if the element
        # was actually inserted
        # An element in set is
        # not inserted if it is
        # already present. Please see
        # https:#www.geeksforgeeks.
        # org/set-insert-function-in-c-stl/
        k = 0;
        size = len(s);
        if (s.add(arr[i])):

            # Find the position of
            # inserted element in iterator k
            if arr[i] in s:
                k += 1;

            # Find the next
            # greater element in set
            # If the new element is not
            # inserted at the end, then
            # remove the greater element
            # next to it.
            if (size == len(s)):
                s.remove(k + 1);

    # Note that set s may not contain
    # actual LIS, but its size gives
    # us the length of LIS
    return len(s);

# Driver code
if __name__ == '__main__':
    arr = [ 8, 9, 12, 10, 11 ];
    n = len(arr);
    print(lis(arr, n) ,"");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation
// to find LIS
using System;
using System.Collections.Generic;

class GFG{

// Return length of LIS
// in arr[] of size N
static int lis(int[] arr, int N)
{
    int i;
    HashSet<int> s = new HashSet<int>();
    for(i = 0; i < N; i++)
    {

        // Check if the element was actually inserted
        // An element in set is not inserted if it is
        // already present. Please see
        // https://www.geeksforgeeks.org/set-insert-function-in-c-stl/
        int k = 0;
        int size = s.Count;

        if (s.Add(arr[i]))
        {

            // Find the position of inserted
            // element in iterator k
            if (s.Contains(arr[i]))
                k++;

            // Find the next greater element in set
            // If the new element is not inserted at
            // the end, then remove the greater element
            // next to it.
            if (size == s.Count)
                s.Remove(k + 1);
        }
    }

    // Note that set s may not contain
    // actual LIS, but its size gives
    // us the length of LIS
    return s.Count;
}

// Driver code
static public void Main()
{
    int[]    arr = { 8, 9, 12, 10, 11 };
    int n = arr.Length;

    Console.Write(lis(arr, n) + "\n");
}
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// Javascript implementation
// to find LIS

// Return length of LIS
// in arr[] of size N
function lis(arr,N)
{
    let i;
  let s = new Set();
  for (i = 0; i < N; i++)
  {
    // Check if the element
    // was actually inserted
    // An element in set is
    // not inserted if it is
    // already present. Please see
    // https://www.geeksforgeeks.
    // org/set-insert-function-in-c-stl/
    let k = 0;
    let size = s.size;
    if (s.add(arr[i]))
    {
      // Find the position of
      // inserted element in iterator k
      if(s.has(arr[i]))
        k++;

      // Find the next
      // greater element in set
      // If the new element is not
      // inserted at the end, then
      // remove the greater element
      // next to it.
      if (size == s.size)
        s.delete(k + 1);
    }
  }

  // Note that set s may not contain
  // actual LIS, but its size gives
  // us the length of LIS
  return s.size;
}

let arr=[8, 9, 12, 10, 11];
let n = arr.length;
document.write(lis(arr, n) + "<br>");

// This code is contributed by unknown2108

</script>
```

**Output**

```
4

```

本文由**拉杰·库马尔**供稿。如果你发现任何不正确的地方，请写评论，或者你想分享更多关于上面讨论的话题的信息