# 在给定到达和离开时间的情况下，找出 k 个预订是否可能

> 原文:[https://www . geesforgeks . org/find-k-预订-可能-给定-到达-离开-时间/](https://www.geeksforgeeks.org/find-k-bookings-possible-given-arrival-departure-times/)

酒店经理必须为下一季度提前预订房间。他的酒店有 K 个房间。预订包含到达日期和离开日期。他想知道酒店是否有足够的房间来满足需求。

这个想法是对数组进行排序，并跟踪重叠。

**示例:**

```
Input :  Arrivals :   [1 3 5]
         Departures : [2 6 8]
         K: 1
Output: False
Hotel manager needs at least two
rooms as the second and third 
intervals overlap.
```

**方法 1**
想法是将到达和离开时间存储在一个辅助数组中，并带有一个额外的标记来指示时间是到达还是离开。现在对数组进行排序。为每个到达增量活动预订处理排序的数组。每次出发，减量。跟踪最大活跃预订量。如果任何时刻的有效预订数大于 k，则返回 false。否则返回真。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

bool areBookingsPossible(int arrival[],
                         int departure[], int n, int k)
{
    vector<pair<int, int> > ans;

    // create a common vector both arrivals
    // and departures.
    for (int i = 0; i < n; i++) {
        ans.push_back(make_pair(arrival[i], 1));
        ans.push_back(make_pair(departure[i], 0));
    }

    // sort the vector
    sort(ans.begin(), ans.end());

    int curr_active = 0, max_active = 0;

    for (int i = 0; i < ans.size(); i++) {

        // if new arrival, increment current
        // guests count and update max active
        // guests so far
        if (ans[i].second == 1) {
            curr_active++;
            max_active = max(max_active,
                             curr_active);
        }

        // if a guest departs, decrement
        // current guests count.
        else
            curr_active--;
    }

    // if max active guests at any instant
    // were more than the available rooms,
    // return false. Else return true.
    return (k >= max_active);
}

int main()
{
    int arrival[] = { 1, 3, 5 };
    int departure[] = { 2, 6, 8 };
    int n = sizeof(arrival) / sizeof(arrival[0]);
    cout << (areBookingsPossible(arrival,
                                 departure, n, 1)
                 ? "Yes\n"
                 : "No\n");
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

// User defined Pair class
class Pair {
  int x;
  int y;

  // Constructor
  public Pair(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

// class to define user defined conparator
class Compare {

  static void compare(Pair arr[], int n)
  {

    // Comparator to sort the pair according to second element
    Arrays.sort(arr, new Comparator<Pair>() {
      @Override public int compare(Pair p1, Pair p2)
      {
        return p1.x - p2.x;
      }
    });
  }
}

class GFG
{
  static boolean areBookingsPossible(int arrival[],
                                     int departure[],
                                     int n, int k)
  {
    Pair ans[] = new Pair[2*n];

    // create a common vector both arrivals
    // and departures.
    int j = 0;
    for (int i = 0; i < n; i++)
    {
      ans[i + j] = new Pair(arrival[i], 1);
      ans[i + j + 1] = new Pair(departure[i], 0);
      j++;
    }

    // sort the vector
    Compare obj = new Compare();
    obj.compare(ans, 2 * n);     
    int curr_active = 0, max_active = 0;    
    for (int i = 0; i < 2 * n; i++)
    {

      // if new arrival, increment current
      // guests count and update max active
      // guests so far
      if (ans[i].y == 1)
      {
        curr_active++;
        max_active = Math.max(max_active,
                              curr_active);
      }

      // if a guest departs, decrement
      // current guests count.
      else
        curr_active--;
    }

    // if max active guests at any instant
    // were more than the available rooms,
    // return false. Else return true.
    return (k >= max_active);
  }

  // Driver code
  public static void main(String[] args)
  {
    int arrival[] = { 1, 3, 5 };
    int departure[] = { 2, 6, 8 };
    int n = arrival.length;
    System.out.println(areBookingsPossible(arrival, departure, n, 1) ? "Yes" : "No");
  }
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 code for the above approach.
def areBookingsPossible(arrival, departure, n, k):

    ans = []

    # Create a common vector both arrivals
    # and departures.
    for i in range(0, n):
        ans.append((arrival[i], 1))
        ans.append((departure[i], 0))

    # Sort the vector
    ans.sort()
    curr_active, max_active = 0, 0

    for i in range(0, len(ans)):

        # If new arrival, increment current
        # guests count and update max active
        # guests so far
        if ans[i][1] == 1:
            curr_active += 1
            max_active = max(max_active,
                             curr_active)

        # if a guest departs, decrement
        # current guests count.
        else:
            curr_active -= 1

    # If max active guests at any instant
    # were more than the available rooms,
    # return false. Else return true.
    return k >= max_active

# Driver Code
if __name__ == "__main__":

    arrival = [1, 3, 5]
    departure = [2, 6, 8]
    n = len(arrival)

    if areBookingsPossible(arrival,
                           departure, n, 1):
        print("Yes")
    else:
        print("No")

# This code is contributed by Rituraj Jain
```

## java 描述语言

```
<script>

// JavaScript implementation of the above approach

function areBookingsPossible(arrival, departure, n, k)
{
    var ans = [];

    // create a common vector both arrivals
    // and departures.
    for (var i = 0; i < n; i++) {
        ans.push([arrival[i], 1]);
        ans.push([departure[i], 0]);
    }

    // sort the vector
    ans.sort();

    var curr_active = 0, max_active = 0;

    for (var i = 0; i < ans.length; i++) {

        // if new arrival, increment current
        // guests count and update max active
        // guests so far
        if (ans[i][1] == 1) {
            curr_active++;
            max_active = Math.max(max_active,
                             curr_active);
        }

        // if a guest departs, decrement
        // current guests count.
        else
            curr_active--;
    }

    // if max active guests at any instant
    // were more than the available rooms,
    // return false. Else return true.
    return (k >= max_active);
}

var arrival = [1, 3, 5];
var departure = [2, 6, 8];
var n = arrival.length;
document.write(areBookingsPossible(arrival,
                             departure, n, 1)
             ? "Yes"
             : "No");

</script>
```

**Output**

```
No
```

**时间复杂度:**O(n Log n)
T3】辅助空间: O(n)

**方法 2**
想法是先简单地对 2 个数组(到达日期数组和离开日期数组)进行排序。
现在，下一步是检查一个特定范围内存在多少重叠。如果重叠的数量大于房间的数量，我们可以说我们容纳客人的房间较少。

因此，对于一个特定的范围，其中到达日期(到达数组的第 I 个)是开始日期，离开日期(离开数组的第 I 个)是结束日期，只有下一个到达日期(从第 I+1 个)小于范围的结束日期并且大于或等于范围的开始日期，重叠才是可能的(因为这是一个排序的数组，我们不需要考虑后一个条件)。

考虑到我们已经对数组进行了排序，我们直接需要检查下一个 Kth (i+Kth)到达日期是否在范围内，如果在范围内，那么在那个到达日期之前的所有日期也将落在所采取的范围内，导致 K+1 与所讨论的范围重叠，从而超过房间的数量。

以下是上述方法的实施–

## C++

```
// C++ code implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

string areBookingsPossible(int A[], int B[],
                           int K, int N)
{
    sort(A, A + N);
    sort(B, B + N);

    for(int i = 0; i < N; i++)
    {
        if (i + K < N && A[i + K] < B[i])
        {
            return "No";
        }
    }
    return "Yes";
}

// Driver Code
int main()
{
    int arrival[] = { 1, 2, 3 };
    int departure[] = { 2, 3, 4 };
    int N = sizeof(arrival) / sizeof(arrival[0]);
    int K = 1;

    cout << (areBookingsPossible(
        arrival, departure, K, N));

    return 0;
}

// This code is contributed by rag2127
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code implementation of the above approach
import java.util.*;
class GFG
{

static String areBookingsPossible(int []A, int []B,
                                  int K)
{
    Arrays.sort(A);
    Arrays.sort(B);  
    for(int i = 0; i < A.length; i++)
    {
        if (i + K < A.length && A[i + K] < B[i])
        {
            return "No";
        }
    }
    return "Yes";
}

// Driver Code
public static void main(String []s)
{
    int []arrival = { 1, 2, 3 };
    int []departure = { 2, 3, 4 };
    int K = 1;    
    System.out.print(areBookingsPossible(
        arrival, departure, K));
}
}

// This code is contributed by Pratham76
```

## 计算机编程语言

```
# Python Code Implementation of the above approach
def areBookingsPossible(A, B, K):
        A.sort()
        B.sort()
        for i in range(len(A)):
            if i+K < len(A) and A[i+K] < B[i] :
                return "No"
        return "Yes"

if __name__ == "__main__":
    arrival = [1, 2, 3] 
    departure = [2, 3, 4]  
    K = 1
    print areBookingsPossible(arrival,departure,K)

# This code was contributed by Vidhi Modi
```

## C#

```
// C# code implementation of the above approach
using System;

class GFG{

static string areBookingsPossible(int []A, int []B,
                                  int K)
{
    Array.Sort(A);
    Array.Sort(B);

    for(int i = 0; i < A.Length; i++)
    {
        if (i + K < A.Length && A[i + K] < B[i])
        {
            return "No";
        }
    }
    return "Yes";
}

// Driver Code
static void Main()
{
    int []arrival = { 1, 2, 3 };
    int []departure = { 2, 3, 4 };
    int K = 1;

    Console.Write(areBookingsPossible(
        arrival, departure, K));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript code implementation of
// the above approach
function areBookingsPossible(A, B, K, N)
{
    A.sort();
    B.sort();

    for(let i = 0; i < N; i++)
    {
        if (i + K < N && A[i + K] < B[i])
        {
            return "No";
        }
    }
    return "Yes";
}

// Driver code
let arrival = [ 1, 2, 3 ];
let departure = [ 2, 3, 4 ];
let N = arrival.length;
let K = 1;

document.write(areBookingsPossible(
    arrival, departure, K, N));

// This code is contributed by suresh07

</script>
```

**Output**

```
Yes
```

**时间复杂度:**O(n Log n)
T3】辅助空间: O(n)被 Python 排序使用