# 最大不相交间隔

> 原文:[https://www.geeksforgeeks.org/maximal-disjoint-intervals/](https://www.geeksforgeeks.org/maximal-disjoint-intervals/)

给定一组 **N** 区间，任务是找到最大的互不相交区间集。如果两个区间**【I，j】**&**【k，l】**没有任何共同点，则称为不相交。

**示例:**

> **输入:**间隔[][] = {{1，4}、{2，3}、{4，6}、{8，9}}
> **输出:**
> 【2，3】
> 【4，6】
> 【8，9】
> 间隔以 w.r.t .结束点= {{2，3}、{1，4}、{4，6}、{8，9}}
> 间隔[2，3]和[1，4]
> 我们必须包含[2，3]，因为如果包含[1，4]，那么
> 就不能包含[4，6]。
> **输入:**间隔[][] = {{1，9}，{2，3}，{5，7}}
> **输出:**
> 【2，3】
> 【5，7】

**进场:**

1.  [根据间隔的终点对间隔进行排序](https://www.geeksforgeeks.org/sort-algorithms-the-c-standard-template-library-stl/)。
2.  现在，遍历所有的区间，如果我们得到两个重叠的区间，那么贪婪地选择具有较低端点的区间，因为，选择它将确保区间可以进一步被容纳而没有任何重叠。
3.  对所有间隔应用相同的程序，并打印满足上述标准的所有间隔。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;
#define ll long long int

// Function to sort the vector elements
// by second element of pairs
bool sortbysec(const pair<int, int>& a,
               const pair<int, int>& b)
{
    return (a.second < b.second);
}

// Function to find maximal disjoint set
void maxDisjointIntervals(vector<pair<int, int> > list)
{

    // Sort the list of intervals
    sort(list.begin(), list.end(), sortbysec);

    // First Interval will always be
    // included in set
    cout << "[" << list[0].first << ", "
         << list[0].second << "]" << endl;

    // End point of first interval
    int r1 = list[0].second;

    for (int i = 1; i < list.size(); i++) {
        int l1 = list[i].first;
        int r2 = list[i].second;

        // Check if given interval overlap with
        // previously included interval, if not
        // then include this interval and update
        // the end point of last added interval
        if (l1 > r1) {
            cout << "[" << l1 << ", "
                 << r2 << "]" << endl;
            r1 = r2;
        }
    }
}

// Driver code
int main()
{
    int N = 4;
    vector<pair<int, int> > intervals = { { 1, 4 },
                                          { 2, 3 },
                                          { 4, 6 },
                                          { 8, 9 } };
    maxDisjointIntervals(intervals);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;
class GFG
{
    static class Pair implements Comparable<Pair>
    {
        int first, second;

        Pair(int f, int s)
        {
            first = f;
            second = s;
        }

        @Override

     // Function to sort the vector elements
     // by second element of Pairs
        public int compareTo(Pair o)
        {
            if(this.second > o.second)
                return 1;
            else if(this.second == o.second)
                return 0;
            return -1;
        }
    }

// Function to find maximal disjoint set
static void maxDisjointIntervals(Pair []list)
{

    // Sort the list of intervals
    Collections.sort(Arrays.asList(list));

    // First Interval will always be
    // included in set
    System.out.print("[" +  list[0].first+ ", "
         + list[0].second+ "]" +"\n");

    // End point of first interval
    int r1 = list[0].second;

    for (int i = 1; i < list.length; i++) {
        int l1 = list[i].first;
        int r2 = list[i].second;

        // Check if given interval overlap with
        // previously included interval, if not
        // then include this interval and update
        // the end point of last added interval
        if (l1 > r1) {
            System.out.print("[" +  l1+ ", "
                 + r2+ "]" +"\n");
            r1 = r2;
        }
    }
}

// Driver code
public static void main(String[] args)
{
    int N = 4;
    Pair []intervals = { new Pair(1, 4 ),
            new Pair( 2, 3 ),
            new Pair( 4, 6 ),
            new Pair( 8, 9 ) };
    maxDisjointIntervals(intervals);
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find maximal disjoint set
def maxDisjointIntervals(list_):

    # Lambda function to sort the list 
    # elements by second element of pairs
    list_.sort(key = lambda x: x[1])

    # First interval will always be
    # included in set
    print("[", list_[0][0], ", ", list_[0][1], "]")

    # End point of first interval
    r1 = list_[0][1]

    for i in range(1, len(list_)):
        l1 = list_[i][0]
        r2 = list_[i][1]

        # Check if given interval overlap with
        # previously included interval, if not
        # then include this interval and update
        # the end point of last added interval
        if l1 > r1:
            print("[", l1, ", ", r2, "]")
            r1 = r2

# Driver code
if __name__ == "__main__":

    N = 4
    intervals = [ [ 1, 4 ], [ 2, 3 ],
                  [ 4, 6 ], [ 8, 9 ] ]

    # Call the function
    maxDisjointIntervals(intervals)

# This code is contributed by Tokir Manva
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to find maximal disjoint set
function maxDisjointIntervals(list)
{

    // Sort the list of intervals
    list.sort((a,b)=> a[1]-b[1]);

    // First Interval will always be
    // included in set
    document.write( "[" + list[0][0] + ", "
         + list[0][1] + "]" + "<br>");

    // End point of first interval
    var r1 = list[0][1];

    for (var i = 1; i < list.length; i++) {
        var l1 = list[i][0];
        var r2 = list[i][1];

        // Check if given interval overlap with
        // previously included interval, if not
        // then include this interval and update
        // the end point of last added interval
        if (l1 > r1) {
            document.write( "[" + l1 + ", "
                 + r2 + "]" + "<br>");
            r1 = r2;
        }
    }
}

// Driver code
var N = 4;
var intervals = [ [ 1, 4 ],
                                      [ 2, 3 ],
                                      [ 4, 6 ],
                                      [ 8, 9 ] ];
maxDisjointIntervals(intervals);

</script>
```

**Output:** 

```
[2, 3]
[4, 6]
[8, 9]
```