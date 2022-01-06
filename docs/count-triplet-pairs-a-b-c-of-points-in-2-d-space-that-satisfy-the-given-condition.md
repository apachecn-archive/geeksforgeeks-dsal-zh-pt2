# 计算二维空间中满足给定条件的点的三元组对(A，B，C)

> 原文:[https://www . geeksforgeeks . org/count-triple-pairs-a-B- c-of-in-2-d-space-满足给定条件/](https://www.geeksforgeeks.org/count-triplet-pairs-a-b-c-of-points-in-2-d-space-that-satisfy-the-given-condition/)

给定二维空间中的第 N 个点。任务是统计三胞胎对 **(A，B，C)** 的数量，使得点 **B** 是通过连接**点 A 和 C** 形成的线段的中点。
**举例:**

> **输入:**点= {{1，1}、{2，2}、{3，3}}
> **输出:** 1
> 点(2，2)是线段连接点(1，1)和(3，3)的中点。
> **输入:**点数= {{1，1}、{1，2}、{1，5}}
> **输出:** 0

**进场:**考虑一对点 **A** 和 **C** 。连接这些点的线段中点将是 **((A * X + C * X) / 2，(A * Y + C * Y) / 2))** 。如果该点存在于给定的点列表中，我们就找到了一个三元组。为了快速检查一个点是否在我们的点列表中，我们可以使用集合。对所有成对的点这样做将会给我们所需的计数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of possible triplets
int countTriplets(int n, vector<pair<int, int> > points)
{
    set<pair<int, int> > pts;
    int ct = 0;

    // Insert all the points in a set
    for (int i = 0; i < n; i++)
        pts.insert(points[i]);

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++) {
            int x = points[i].first + points[j].first;
            int y = points[i].second + points[j].second;

            // If the mid point exists in the set
            if (x % 2 == 0 && y % 2 == 0)
                if (pts.find(make_pair(x / 2, y / 2))
                    != pts.end())
                    ct++;
        }

    // Return the count of valid triplets
    return ct;
}

// Driver code
int main()
{
    vector<pair<int, int> > points
        = { { 1, 1 }, { 2, 2 }, { 3, 3 } };
    int n = points.size();
    cout << countTriplets(n, points);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

static class pair
{
    int first,second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }

}

// Function to return the count of possible triplets
static int countTriplets(int n, Vector<pair> points)
{
    Set<pair> pts = new HashSet<pair>();
    int ct = 0;

    // Insert all the points in a set
    for (int i = 0; i < n; i++)
        pts.add(points.get(i));

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
        {
            int x = points.get(i).first + points.get(j).first;
            int y = points.get(i).second + points.get(j).second;

            // If the mid point exists in the set
            if (x % 2 == 0 && y % 2 == 0)
                if (!pts.contains(new pair(x / 2, y / 2)))
                    ct++;
        }

    // Return the count of valid triplets
    return ct;
}

// Driver code
public static void main(String args[])
{
    Vector<pair> points = new Vector<>();
    points.add(new pair(1,1));
    points.add(new pair(2,2));
    points.add(new pair(3,3));
    int n = points.size();
    System.out.println(countTriplets(n, points));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of possible triplets
def countTriplets(n, points) :

    pts = []
    ct = 0;

    # Insert all the points in a set
    for i in range(n) :
        pts.append(points[i]);

    for i in range(n) :
        for j in range(i + 1, n) :
            x = points[i][0] + points[j][0];
            y = points[i][1] + points[j][1];

            # If the mid point exists in the set
            if (x % 2 == 0 and y % 2 == 0) :
                if [x // 2, y // 2] in pts :
                    ct += 1

    # Return the count of valid triplets
    return ct

# Driver code
if __name__ == "__main__" :

    points = [[ 1, 1 ], [ 2, 2 ], [ 3, 3 ]]
    n = len(points)
    print(countTriplets(n, points))

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

public class pair
{
    public int first,second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }

}

// Function to return the count of possible triplets
static int countTriplets(int n, List<pair> points)
{
    HashSet<pair> pts = new HashSet<pair>();
    int ct = 0;

    // Insert all the points in a set
    for (int i = 0; i < n; i++)
        pts.Add(points[i]);

    for (int i = 0; i < n; i++)
        for (int j = i + 1; j < n; j++)
        {
            int x = points[i].first + points[j].first;
            int y = points[i].second + points[j].second;

            // If the mid point exists in the set
            if (x % 2 == 0 && y % 2 == 0)
                if (!pts.Contains(new pair(x / 2, y / 2)))
                    ct++;
        }

    // Return the count of valid triplets
    return ct;
}

// Driver code
public static void Main(String []args)
{
    List<pair> points = new List<pair>();
    points.Add(new pair(1, 1));
    points.Add(new pair(2, 2));
    points.Add(new pair(3, 3));
    int n = points.Count;
    Console.WriteLine(countTriplets(n, points));
}
}

// This code is contributed by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count
// of possible triplets
function countTriplets($n, $points)
{
    $pts = array();
    $ct = 0;

    // Insert all the points in a set
    for ($i = 0; $i < count($points); $i++)
    {
        for ($j = 0;
             $j < count($points[$i]); $j++)
        {
            $pts[] = $points[$i][$j];
        }
    }

    for ($i = 0; $i < $n; $i++)
        for ($j = $i + 1; $j < $n; $j++)
        {
            $x = $points[$i][0] + $points[$j][0];
            $y = $points[$i][1] + $points[$j][1];

            // If the mid point exists in the set
            if ($x % 2 == 0 and $y % 2 == 0)
                if (in_array((int)($x / 2), $pts) and
                    in_array((int)($y / 2), $pts))
                    $ct += 1;
        }

    // Return the count of valid triplets
    return $ct;
}

// Driver code
$points = array(array( 1, 1 ),
                array( 2, 2 ),
                array( 3, 3 ));
$n = count($points);
print(countTriplets($n, $points));

// This code is contributed by chandan_jnu
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of possible triplets
function countTriplets(n, points)
{
    var pts = new Set();
    var ct = 0;

    // Insert all the points in a set
    for (var i = 0; i < n; i++)
        pts.add(points[i].toString());

    for (var i = 0; i < n; i++)
        for (var j = i + 1; j < n; j++) {
            var x = points[i][0] + points[j][0];
            var y = points[i][1] + points[j][1];

            // If the mid point exists in the set
            if (x % 2 == 0 && y % 2 == 0)
                if (pts.has([(x / 2), (y / 2)].toString()))
                    ct++;
        }

    // Return the count of valid triplets
    return ct;
}

// Driver code
var points
    = [ [ 1, 1 ], [ 2, 2 ], [ 3, 3 ] ];
var n = points.length;
document.write( countTriplets(n, points))

// This code is contributed by famously.
</script>
```

**Output:** 

```
1
```