# 找出任意两对(a，b)和(c，d ),使得 a 和 d

> 原文:[https://www . geesforgeks . org/find-any-two-pair-ab-and-CD-so-a-c-and-B- d/](https://www.geeksforgeeks.org/find-any-two-pairs-ab-and-cd-such-that-a-c-and-b-d/)

给定一组大小为 **N** 的[对**arr【】**，任务是找到任意两对 **(a，b)** 和 **(c，d)** ，使得 **a < c** 和 **b > d** 始终保持。如果存在这样的配对，打印这些配对。否则，打印“*不存在这样的配对*”。](https://www.geeksforgeeks.org/array-data-structure/)

***例:***

> **输入:** arr[] = {(3，7)，(21，23)，(4，13)，(1，2)，(7，-1)}
> **输出:**必选对为(3，7)，(7，-1)
> **解释:** (a，b) = (3，7)
> (c，d) = (7，-1)
> 显然，a < c 和 b > d。
> 
> **输入:** arr[]={(1，6)，(-5，4)，(10，13)}
> **输出:**不存在这样的配对

**天真方法:**解决这个问题最简单的方法是检查数组中的每一对是否存在满足给定条件的其他对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
void findPair(pair<int, int>* arr, int N)
{
    for (int i = 0; i < N; i++) {

        int a = arr[i].first, b = arr[i].second;

        for (int j = i + 1; j < N; j++) {

            int c = arr[j].first, d = arr[j].second;

            if (a < c && b > d) {

                cout << "(" << a << " " << b << "), ("
                     << c << " " << d << ")\n";
                return;
            }
        }
    }

    // If no such pair is found
    cout << "NO SUCH PAIR EXIST\n";
}

// Driver Code
int main()
{
    pair<int, int> arr[] = {
        { 3, 7 }, { 21, 23 },
        { 4, 13 }, { 1, 2 },
        { 7, -1 }
    };

    findPair(arr, 5);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to sort the
// array of points by its distance
// from the given point
import java.util.*;
class GFG
{

static class pair
{ 
    int first, second; 
    public pair(int first, int second) 
    { 
        this.first = first; 
        this.second = second; 
    } 
}

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
static void findPair(pair arr[], int N)
{
    for (int i = 0; i < N; i++)
    {
        int a = arr[i].first, b = arr[i].second;
        for (int j = i + 1; j < N; j++)
        {
            int c = arr[j].first, d = arr[j].second;
            if (a < c && b > d)
            {
                System.out.println( "(" + a + " " + b + "), ("
                    + c + " " + d + ")");
                return;
            }
        }
    }

    // If no such pair is found
    System.out.println("NO SUCH PAIR EXIST");
}

// Driver code
public static void main(String[] args)
{
    pair arr[] = {new pair( 3, 7 ), new pair( 21, 23 ), 
                new pair( 4, 13 ), new pair( 1, 2 ), 
                new pair( 7, -1 )};
    findPair(arr, 5);
}
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find two pairs (a, b) and
# (c, d) such that a < c and b > d
def findPair(arr, N):
    for i in range(N):
        a, b = arr[i][0], arr[i][1]
        for j in range(i + 1, N):
            c, d = arr[j][0], arr[j][1]
            if (a < c and b > d):
                print("(", a, b, "), (", c, d, ")")
                return

    # If no such pair is found
    print("NO SUCH PAIR EXIST")

# Driver Code
if __name__ == '__main__':
    arr = [
        [ 3, 7 ], [ 21, 23 ],
        [ 4, 13 ], [ 1, 2 ],
        [ 7, -1 ]
    ]

    findPair(arr, 5)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation to sort the
// array of points by its distance
// from the given point
using System;

public class GFG
{

  class pair
  { 
    public int first, second; 
    public pair(int first, int second) 
    { 
      this.first = first; 
      this.second = second; 
    } 
  }

  // Function to find two pairs (a, b) and
  // (c, d) such that a < c and b > d
  static void findPair(pair []arr, int N)
  {
    for (int i = 0; i < N; i++)
    {
      int a = arr[i].first, b = arr[i].second;
      for (int j = i + 1; j < N; j++)
      {
        int c = arr[j].first, d = arr[j].second;
        if (a < c && b > d)
        {
          Console.WriteLine( "(" + a + " " + b + "), ("
                            + c + " " + d + ")");
          return;
        }
      }
    }

    // If no such pair is found
    Console.WriteLine("NO SUCH PAIR EXIST");
  }

  // Driver code
  public static void Main(String[] args)
  {
    pair []arr = {new pair( 3, 7 ), new pair( 21, 23 ), 
                  new pair( 4, 13 ), new pair( 1, 2 ), 
                  new pair( 7, -1 )};
    findPair(arr, 5);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to sort the
// array of points by its distance
// from the given point

class pair
{
    constructor(first,second)
    {
        this.first=first;
        this.second = second;
    }
}

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
function findPair(arr,N)
{
    for (let i = 0; i < N; i++)
    {
        let a = arr[i].first, b = arr[i].second;
        for (let j = i + 1; j < N; j++)
        {
            let c = arr[j].first, d = arr[j].second;
            if (a < c && b > d)
            {
                document.write( "(" + a + " " + b + "), ("
                    + c + " " + d + ")<br>");
                return;
            }
        }
    }

    // If no such pair is found
    document.write("NO SUCH PAIR EXIST<br>");
}

// Driver code
let arr=[new pair( 3, 7 ), new pair( 21, 23 ),
                new pair( 4, 13 ), new pair( 1, 2 ),
                new pair( 7, -1 )];
findPair(arr, 5);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
(3 7), (7 -1)
```

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(1)

**高效方法:**优化上述方法，解决问题的思路 si:

*   [根据每对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的第一个元素对给定的数组进行排序。
*   现在，任务简化为检查 **arr[]** 中是否存在任何对，其中 **arr[i]。第二<arr[I–1]。第二个**作为每对的第一个元素已经排序。
*   所以，简单的[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)检查是否存在这样的一对。
    *   如果发现是真的，就打印一对。
    *   否则，打印“不存在这样的配对”。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
void findPair(pair<int, int>* arr, int N)
{
    // Sort the array in increasing
    // order of first element of pairs
    sort(arr, arr + N);

    // Traverse the array
    for (int i = 1; i < N; i++) {

        int b = arr[i - 1].second;
        int d = arr[i].second;

        if (b > d) {
            cout << "(" << arr[i - 1].first << " " << b
                 << "), (" << arr[i].first << " " << d << ")";
            return;
        }
    }

    // If no such pair found
    cout << "NO SUCH PAIR EXIST\n";
}

// Driver Code
int main()
{
    pair<int, int> arr[] = {
        { 3, 7 }, { 21, 23 },
        { 4, 13 }, { 1, 2 },
        { 7, -1 }
    };
    findPair(arr, 5);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{
static class pair implements Comparable<pair>
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }

    public int compareTo(pair p)
    {
        return this.first - p.first;
    }
}

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
static void findpair(pair []arr, int N)
{

    // Sort the array in increasing
    // order of first element of pairs
    Arrays.sort(arr);

    // Traverse the array
    for (int i = 1; i < N; i++)
    {
        int b = arr[i - 1].second;
        int d = arr[i].second;
        if (b > d)
        {
            System.out.print("(" +  arr[i - 1].first + " " +  b
                + "), (" +  arr[i].first + " " +  d + ")");
            return;
        }
    }

    // If no such pair found
    System.out.print("NO SUCH PAIR EXIST\n");
}

// Driver Code
public static void main(String[] args)
{
    pair arr[] = { new pair( 3, 7 ),  new pair( 21, 23 ),
            new pair( 4, 13 ),  new pair( 1, 2 ),
            new pair( 7, -1 ) };
    findpair(arr, 5);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find two pairs (a, b) and
# (c, d) such that a < c and b > d
def findPair(arr, N):

    # Sort the array in increasing
    # order of first element of pairs
    arr.sort(key = lambda x: x[0])

    # Traverse the array
    for i in range(1, N):

        b = arr[i - 1][1]
        d = arr[i][1]

        if (b > d):
            print("(", arr[i - 1][0], b, "), (", arr[i][0], d, ")")
            return

    #If no such pair found
    print("NO SUCH PAIR EXIST\n");

# Driver Code
arr = [
        [ 3, 7 ], [ 21, 23 ],
        [ 4, 13 ], [ 1, 2 ],
        [ 7, -1 ]]
findPair(arr, 5)

# This code is contributed by Dharanendra L V
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{
  class pair : IComparable<pair>
  {
    public int first, second;
    public pair(int first, int second) 
    {
      this.first = first;
      this.second = second;
    }

    public int CompareTo(pair p)
    {
      return this.first - p.first;
    }
  }

  // Function to find two pairs (a, b) and
  // (c, d) such that a < c and b > d
  static void findpair(pair []arr, int N)
  {

    // Sort the array in increasing
    // order of first element of pairs
    Array.Sort(arr);

    // Traverse the array
    for (int i = 1; i < N; i++)
    {
      int b = arr[i - 1].second;
      int d = arr[i].second;
      if (b > d)
      {
        Console.Write("(" +  arr[i - 1].first + " " +  b
                      + "), (" +  arr[i].first + " " +  d + ")");
        return;
      }
    }

    // If no such pair found
    Console.Write("NO SUCH PAIR EXIST\n");
  }

  // Driver Code
  public static void Main(String[] args)
  {
    pair []arr = { new pair( 3, 7 ),  new pair( 21, 23 ),
                  new pair( 4, 13 ),  new pair( 1, 2 ),
                  new pair( 7, -1 ) };
    findpair(arr, 5);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// JavaScript program for the above approach

// Function to find two pairs (a, b) and
// (c, d) such that a < c and b > d
function findPair(arr, N)
{
    // Sort the array in increasing
    // order of first element of pairs

    arr.sort( function(a, b) {
  return (a[0] - b[0]) || (a[1] - b[1]);
});

    // Traverse the array
    for (let i = 1; i < N; i++) {

        let b = arr[i - 1][1];
        let d = arr[i][1];

        if (b > d) {
            console.log( "(" + arr[i - 1][0] + " " + b
                 + "), (" + arr[i][0] + " " +d + ")");
            return;
        }
    }

    // If no such pair found
    console.log( "NO SUCH PAIR EXIST");
}

// Driver Code

var arr = [
        [ 3, 7 ], [ 21, 23 ],
        [ 4, 13 ], [ 1, 2 ],
        [ 7, -1 ]
    ]
findPair(arr, 5);

// Thiss code is contributed by ukasp.
</script>
```

**Output:** 

```
(4 13), (7 -1)
```

***时间复杂度:*** O(N*logN)
***辅助空间:*** O(1)