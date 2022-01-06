# 从给定的一组间隔中找出最少的不重叠的数

> 原文:[https://www . geeksforgeeks . org/从给定的一组间隔中找到最小非重叠数/](https://www.geeksforgeeks.org/find-least-non-overlapping-number-from-a-given-set-of-intervals/)

给定一个整数对的数组**区间**，代表大小区间 **N** 的起点和终点。任务是从给定的一组区间中找到最小的非负整数，它是一个不重叠的数。

**输入约束:**

![1 \le N \le 10^{5}0 \le interval[i] \le 10^{9}             ](img/87248d14a57ccc9383dfa6edb8316f26.png "Rendered by QuickLaTeX.com")

**示例:**

> **输入:**区间= {{0，4}、{6，8}、{2，3}、{9，18}}
> **输出:** 5
> **解释:**
> 与所有区间集不重叠的最小非负整数为 5。
> 
> **输入:**间隔= {{0，14}、{86，108}、{22，30}、{5，17}}
> **输出:** 18

**天真方法:**

*   创建一个大小为 **MAX** 的访问数组，对于每个间隔，从**开始**到**结束**标记所有值为真。
*   最后从 **1** 迭代到 **MAX** ，找到未被访问的最小值。

但是，如果间隔坐标达到 10 <sup>9</sup> ，这种方法将不起作用。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O (MAX)*

**有效方法:**

1.  与其从头到尾迭代，不如创建一个访问过的数组，对于每个范围，标记 **vis[start] = 1** 和 **vis[end+1] = -1** 。
2.  取数组的前缀和。
3.  然后遍历数组，找到第一个值为 **0** 的整数。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// least non-overlapping number
// from a given set intervals

#include <bits/stdc++.h>
using namespace std;
const int MAX = 1e5 + 5;

// function to find the smallest
// non-overlapping number
void find_missing(
    vector<pair<int, int> > interval)
{
    // create a visited array
    vector<int> vis(MAX);

    for (int i = 0; i < interval.size(); ++i) {
        int start = interval[i].first;
        int end = interval[i].second;
        vis[start]++;
        vis[end + 1]--;
    }

    // find the first missing value
    for (int i = 1; i < MAX; i++) {
        vis[i] += vis[i - 1];
        if (!vis[i]) {
            cout << i << endl;
            return;
        }
    }
}
// Driver function
int main()
{

    vector<pair<int, int> > interval
        = { { 0, 14 }, { 86, 108 },
            { 22, 30 }, { 5, 17 } };
    find_missing(interval);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// least non-overlapping number
// from a given set intervals
class GFG{

static int MAX = (int) (1e5 + 5);
static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}
// function to find the smallest
// non-overlapping number
static void find_missing(
    pair[] interval)
{
    // create a visited array
    int [] vis = new int[MAX];

    for (int i = 0; i < interval.length; ++i)
    {
        int start = interval[i].first;
        int end = interval[i].second;
        vis[start]++;
        vis[end + 1]--;
    }

    // find the first missing value
    for (int i = 1; i < MAX; i++) {
        vis[i] += vis[i - 1];
        if (vis[i]==0) {
            System.out.print(i +"\n");
            return;
        }
    }
}
// Driver function
public static void main(String[] args)
{

    pair []interval = {new pair( 0, 14 ),
                       new pair( 86, 108 ),
                       new pair( 22, 30 ),
                       new pair( 5, 17 )};
    find_missing(interval);
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to find the
# least non-overlapping number
# from a given set intervals
MAX = int(1e5 + 5)

# Function to find the smallest
# non-overlapping number
def find_missing(interval):

    # Create a visited array
    vis = [0] * (MAX)

    for i in range(len(interval)):
        start = interval[i][0]
        end = interval[i][1]
        vis[start] += 1
        vis[end + 1] -= 1

    # Find the first missing value
    for i in range(1, MAX):
        vis[i] += vis[i - 1]

        if (vis[i] == 0):
            print(i)
            return

# Driver code
interval = [ [ 0, 14 ], [ 86, 108 ],
             [ 22, 30 ], [ 5, 17 ] ]

find_missing(interval)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to find the
// least non-overlapping number
// from a given set intervals
using System;

class GFG{

static int MAX = (int)(1e5 + 5);
class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to find the smallest
// non-overlapping number
static void find_missing(pair[] interval)
{

    // Create a visited array
    int [] vis = new int[MAX];

    for(int i = 0; i < interval.Length; ++i)
    {
        int start = interval[i].first;
        int end = interval[i].second;

        vis[start]++;
        vis[end + 1]--;
    }

    // Find the first missing value
    for(int i = 1; i < MAX; i++)
    {
        vis[i] += vis[i - 1];
        if (vis[i] == 0)
        {
            Console.Write(i + "\n");
            return;
        }
    }
}

// Driver code
public static void Main(String[] args)
{
    pair []interval = { new pair(0, 14),
                        new pair(86, 108),
                        new pair(22, 30),
                        new pair(5, 17) };

    find_missing(interval);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Javascript program to find the
// least non-overlapping number
// from a given set intervals
var MAX = 100005;

// function to find the smallest
// non-overlapping number
function find_missing(  interval)
{
    // create a visited array
    var vis = Array(MAX).fill(0);

    for (var i = 0; i < interval.length; ++i) {
        var start = interval[i][0];
        var end = interval[i][1];
        vis[start]++;
        vis[end + 1]--;
    }

    // find the first missing value
    for (var i = 1; i < MAX; i++) {
        vis[i] += vis[i - 1];
        if (!vis[i]) {
            document.write( i + "<br>");
            return;
        }
    }
}
// Driver function
var interval
    = [ [ 0, 14 ], [ 86, 108 ],
        [ 22, 30 ], [ 5, 17 ] ];
find_missing(interval);

</script>
```

**Output:** 

```
18
```

***时间复杂度:** O (N)*
***辅助空间:** O (MAX)*
不过，如果区间坐标达到 10 <sup>9</sup> 的话，这种方法也行不通。

**有效方法:**

1.  根据范围的起始坐标和每个下一个范围对范围进行排序。
2.  检查起点是否大于目前为止遇到的最大终点坐标，那么可以找到一个缺失的数字，它将是 **previous_max + 1** 。

> **图解:**
> 考虑以下例子:
> 区间[][] = { { 0，14 }，{ 86，108 }，{ 22，30 }，{ 5，17 } }；
> 排序后，区间[][] = { { 0，14 }，{ 5，17 }，{ 22，30 }，{ 86，108 } }；
> 初始 mx = 0 且在考虑第一间隔 mx = max(0，15) = 15 后
> 由于 mx = 15 和 15 > 5 所以在考虑第二间隔 mx = max(15，18) = 18 后
> 现在 18 < 22 所以 18 是最少不重叠的数。

下面是上述方法的实现:

## C++

```
// C++ program to find the
// least non-overlapping number
// from a given set intervals

#include <bits/stdc++.h>
using namespace std;

// function to find the smallest
// non-overlapping number
void find_missing(
    vector<pair<int, int> > interval)
{
    // Sort the intervals based on their
    // starting value
    sort(interval.begin(), interval.end());

    int mx = 0;

    for (int i = 0; i < (int)interval.size(); ++i) {

        // check if any missing value exist
        if (interval[i].first > mx) {
            cout << mx;
            return;
        }

        else
            mx = max(mx, interval[i].second + 1);
    }
    // finally print the missing value
    cout << mx;
}
// Driver function
int main()
{

    vector<pair<int, int> > interval
        = { { 0, 14 }, { 86, 108 },
            { 22, 30 }, { 5, 17 } };
    find_missing(interval);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the
// least non-overlapping number
// from a given set intervals
import java.util.*;
import java.io.*;

class GFG{

static class Pair implements Comparable<Pair>
{
    int start,end;
    Pair(int s, int e)
    {
        start = s;
        end = e;
    }

    public int compareTo(Pair p)
    {
        return this.start - p.start;
    }
}

// Function to find the smallest
// non-overlapping number
static void findMissing(ArrayList<Pair> interval)
{

    // Sort the intervals based on their
    // starting value
    Collections.sort(interval);

    int mx = 0;

    for(int i = 0; i < interval.size(); ++i)
    {

        // Check if any missing value exist
        if (interval.get(i).start > mx)
        {
            System.out.println(mx);
            return;
        }
        else
            mx = Math.max(mx, interval.get(i).end + 1);
    }

    // Finally print the missing value
    System.out.println(mx);
}

// Driver code
public static void main(String []args)
{
    ArrayList<Pair> interval = new ArrayList<>();
    interval.add(new Pair(0, 14));
    interval.add(new Pair(86, 108));
    interval.add(new Pair(22, 30));
    interval.add(new Pair(5, 17));

    findMissing(interval);
}
}

// This code is contributed by Ganeshchowdharysadanala
```

## 蟒蛇 3

```
# Python3 program to find the
# least non-overlapping number
# from a given set intervals

# function to find the smallest
# non-overlapping number
def find_missing(interval):

    # Sort the intervals based 
    # on their starting value
    interval.sort()

    mx = 0

    for i in range (len(interval)):

        # Check if any missing
        # value exist
        if (interval[i][0] > mx):
            print (mx)
            return

        else:
            mx = max(mx,
                     interval[i][1] + 1)

    # Finally print the missing value
    print (mx)

# Driver code
if __name__ == "__main__":

    interval = [[0, 14], [86, 108],
                [22, 30], [5, 17]]
    find_missing(interval);

# This code is contributed by Chitranayal
```

## C#

```
// C# program to find the
// least non-overlapping number
// from a given set intervals
using System;
using System.Collections.Generic;
class GFG{

class Pair : IComparable<Pair>
{
    public int start,end;
    public Pair(int s, int e)
    {
        start = s;
        end = e;
    }

    public int CompareTo(Pair p)
    {
        return this.start - p.start;
    }
}

// Function to find the smallest
// non-overlapping number
static void findMissing(List<Pair> interval)
{

    // Sort the intervals based on their
    // starting value
    interval.Sort();
    int mx = 0;
    for(int i = 0; i < interval.Count; ++i)
    {

        // Check if any missing value exist
        if (interval[i].start > mx)
        {
            Console.WriteLine(mx);
            return;
        }
        else
            mx = Math.Max(mx, interval[i].end + 1);
    }

    // Finally print the missing value
    Console.WriteLine(mx);
}

// Driver code
public static void Main(String []args)
{
    List<Pair> interval = new List<Pair>();
    interval.Add(new Pair(0, 14));
    interval.Add(new Pair(86, 108));
    interval.Add(new Pair(22, 30));
    interval.Add(new Pair(5, 17));

    findMissing(interval);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// Javascript program to find the
// least non-overlapping number
// from a given set intervals

// Function to find the smallest
// non-overlapping number
function findMissing(interval)
{

    // Sort the intervals based on their
    // starting value
    interval.sort(function(a,b){return a[0]-b[0];});
    let mx = 0;
    for(let i = 0; i < interval.length; ++i)
    {

        // Check if any missing value exist
        if (interval[i][0] > mx)
        {
            document.write(mx+"<br>");
            return;
        }
        else
            mx = Math.max(mx, interval[i][1] + 1);
    }

    // Finally print the missing value
    document.write(mx);
}

// Driver code
let interval = [[0, 14], [86, 108],
                [22, 30], [5, 17]];

findMissing(interval);

// This code is contributed by avanitrachhadiya2155.
</script>
```

**输出:**

```
18
```

***时间复杂度:** O (N * logN)*
***辅助空间:** O (1)*