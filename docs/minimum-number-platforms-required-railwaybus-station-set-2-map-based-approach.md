# 铁路/公交车站所需的最小站台数|第 2 组(基于集合的方法)

> 原文:[https://www . geesforgeks . org/最小数量-平台-必需-铁路巴士-车站-集合-2-基于地图的方法/](https://www.geeksforgeeks.org/minimum-number-platforms-required-railwaybus-station-set-2-map-based-approach/)

给定到达火车站的所有列车的到达和离开时间，找到火车站所需的最小站台数，以便没有列车等待。给我们两个数组，分别代表停站列车的到达和离开时间。

示例:

```
Input:  arr[]  = {9:00,  9:40, 9:50,  11:00, 15:00, 18:00}
        dep[]  = {9:10, 12:00, 11:20, 11:30, 19:00, 20:00}
Output: 3
There are at-most three trains at a time 
(time between 11:00 to 11:20)
```

我们已经在下面的帖子中讨论了它的简单和基于排序的解决方案。
[铁路/公交车站所需的最小站台数](https://www.geeksforgeeks.org/minimum-number-platforms-required-railwaybus-station/)。
在这篇文章中，我们将所有的到达和离开时间插入一个[多集](https://www.geeksforgeeks.org/multiset-in-cpp-stl/)中。multiset 中元素的第一个值表示到达/离开时间，第二个值表示它是到达还是离开，分别用“a”或“d”表示。
如果到达，则增加 1，否则减少 1。如果我们从 STDIN 获取输入，那么我们可以直接将时间插入多集，而不需要将时间存储在数组中。

## C++

```
// C++ program to find minimum number of platforms
// required on a railway station
#include <bits/stdc++.h>
using namespace std;

int findPlatform(int arr[], int dep[], int n)
{
    // Insert all the times (arr. and dep.)
    // in the multiset.
    multiset<pair<int, char> > order;
    for (int i = 0; i < n; i++) {

        // If its arrival then second value
        // of pair is 'a' else 'd'
        order.insert(make_pair(arr[i], 'a'));
        order.insert(make_pair(dep[i], 'd'));
    }

    int result = 0;
    int plat_needed = 0;

    // Start iterating the multiset.
    for (auto it : order) {

        // If its 'a' then add 1 to plat_needed
        // else minus 1 from plat_needed.
        if (it.second == 'a')
            plat_needed++;
        else
            plat_needed--;

        if (plat_needed > result)
            result = plat_needed;
    }
    return result;
}

// Driver code
int main()
{
    int arr[] = { 900, 940, 950, 1100, 1500, 1800 };
    int dep[] = { 910, 1200, 1120, 1130, 1900, 2000 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum Number of Platforms Required = "
         << findPlatform(arr, dep, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of platforms required on a railway station
import java.io.*;
import java.util.*;

class pair
{
    int first;
    char second;

    pair(int key1, char key2)
    {
        this.first = key1;
        this.second = key2;
    }
}

class GFG{

public static int findPlatform(int arr[], int dep[],
                               int n)
{

    // Insert all the times (arr. and dep.)
    // in the ArrayList of pairs.
    ArrayList<pair> order = new ArrayList<>();
    for(int i = 0; i < n; i++)
    {
        order.add(new pair(arr[i], 'a'));
        order.add(new pair(dep[i], 'd'));
    }

    // Custom sort order ArrayList, first
    // by time than by arrival or departure
    Collections.sort(order, new Comparator<pair>()
    {
        public int compare(pair p1, pair p2)
        {
            if (p1.first == p2.first)
                return new Character(p1.second)
                    .compareTo(
                        new Character(p2.second));

            return p1.first - p2.first;
        }
    });

    int result = 1;
    int plat_needed = 0;

    for(int i = 0; i < order.size(); i++)
    {
        pair p = order.get(i);

        // If its 'a' then add 1 to plat_needed
        // else minus 1 from plat_needed.
        if (p.second == 'a')
            plat_needed++;
        else
            plat_needed--;

        if (plat_needed > result)
            result = plat_needed;
    }
    return result;
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 900, 940, 950, 1100, 1500, 1800 };
    int dep[] = { 910, 1200, 1120, 1130, 1900, 2000 };
    int n = 6;

    System.out.println("Minimum Number of " +
                       "Platforms Required = " +
                       findPlatform(arr, dep, n));
}
}

// This code is contributed by RohitOberoi
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of platforms required on a railway station
def findPlatform(arr, dep, n):

    # Inserting all the arr. and dep. times
    # in the array times
    times = []
    for i in range(n):
        times.append([dep[i], 'd'])
        times.append([arr[i], 'a'])

    # Sort the array
    times = sorted(times, key = lambda x: x[1])
    times = sorted(times, key = lambda x: x[0])

    result, plat_needed = 0, 0

    for i in range(2 * n):

        # If its 'a' then add 1 to plat_needed
        # else minus 1 from plat_needed.
        if times[i][1] == 'a':
            plat_needed += 1
            result = max(plat_needed, result)
        else:
            plat_needed -= 1

    return result

# Driver code
arr = [ 900, 940, 950, 1100, 1500, 1800 ]
dep = [ 910, 1200, 1120, 1130, 1900, 2000 ]
n = len(arr)

print("Minimum Number of Platforms Required =",
      findPlatform(arr, dep, n))

# This code is contributed by Tharun Reddy
```

**输出:**

```
Minimum Number of Platforms Required = 3
```

**复杂度分析:**

*   **时间复杂度:** O( N* LogN)。

因为我们插入了多集，并且它保持元素的排序顺序。所以多集合中的 N 个插入操作需要 N*LogN 的时间复杂度。

*   **空间复杂度:** O(N)。**T3】**

我们正在使用多集，它将有 2*N 个元素。

## C++

```
// C++ program to find minimum number of platforms
// required on a railway station
#include <bits/stdc++.h>
using namespace std;

int minPlatform(int arrival[], int departure[], int n)
{

    // as time range from 0 to 2359 in 24 hour clock,
    // we declare an array for values from 0 to 2360
    int platform[2361] = {0};
    int requiredPlatform = 1;
    for (int i = 0; i < n; i++) {

        // increment the platforms for arrival
        ++platform[arrival[i]];

         // once train departs we decrease the platform count
        --platform[departure[i] + 1];
    }

    // We are running loop till 2361 because maximum time value
    // in a day can be 23:60
    for (int i = 1; i < 2361; i++) {

        // taking cumulative sum of platform give us required
        // number of platform fro every minute
        platform[i] = platform[i] + platform[i - 1];
        requiredPlatform = max(requiredPlatform, platform[i]);
    }
    return requiredPlatform;
}

// Driver code
int main()
{
    int arr[] = { 900, 940, 950, 1100, 1500, 1800 };
    int dep[] = { 910, 1200, 1120, 1130, 1900, 2000 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << "Minimum Number of Platforms Required = "
         << minPlatform(arr, dep, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number
// of platforms required on a railway
// station
import java.util.*;
import java.lang.*;

class GFG{

static int minPlatform(int arrival[],
                       int departure[],
                       int n)
{

    // As time range from 0 to 2359 in
    // 24 hour clock, we declare an array
    // for values from 0 to 2360
    int[] platform = new int[2361];
    int requiredPlatform = 1;

    for(int i = 0; i < n; i++)
    {

        // Increment the platforms for arrival
        ++platform[arrival[i]];

         // Once train departs we decrease
         // the platform count
        --platform[departure[i] + 1];
    }

    // We are running loop till 2361 because
    // maximum time value in a day can be 23:60
    for(int i = 1; i < 2361; i++)
    {

        // Taking cumulative sum of platform
        // give us required number of
        // platform fro every minute
        platform[i] = platform[i] +
                      platform[i - 1];
        requiredPlatform = Math.max(requiredPlatform,
                                    platform[i]);
    }
    return requiredPlatform;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 900, 940, 950, 1100, 1500, 1800 };
    int dep[] = { 910, 1200, 1120, 1130, 1900, 2000 };
    int n = arr.length;

    System.out.println("Minimum Number of " +
                       "Platforms Required = " +
                       minPlatform(arr, dep, n));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find minimum number
# of platforms required on a railway station
def minPlatform(arrival, departure, n):

    # As time range from 0 to 2359 in
    # 24 hour clock, we declare an array
    # for values from 0 to 2360
    platform = [0] * 2631
    requiredPlatform = 1

    for i in range(n):

        # Increment the platforms for arrival
        platform[arrival[i]] += 1

        # Once train departs we decrease the
        # platform count
        platform[departure[i] + 1] -= 1

    # We are running loop till 2361 because
    # maximum time value in a day can be 23:60
    for i in range(1, 2631):

        # Taking cumulative sum of
        # platform give us required
        # number of platform fro every minute
        platform[i] = platform[i] + platform[i - 1]
        requiredPlatform = max(requiredPlatform,
                               platform[i])

    return requiredPlatform

# Driver code
arr = [ 900, 940, 950, 1100, 1500, 1800 ]
dep = [ 910, 1200, 1120, 1130, 1900, 2000 ]
n = len(arr)

print("Minimum Number of Platforms Required = ",
       minPlatform(arr, dep, n))

# This code is contributed by PawanJain1
```

## C#

```
// C# program to find minimum number
// of platforms required on a railway
// station
using System;
class GFG {

    static int minPlatform(int[] arrival, int[] departure, int n)
    {
        // As time range from 0 to 2359 in
        // 24 hour clock, we declare an array
        // for values from 0 to 2360
        int[] platform = new int[2361];
        int requiredPlatform = 1;

        for(int i = 0; i < n; i++)
        {

            // Increment the platforms for arrival
            ++platform[arrival[i]];

             // Once train departs we decrease
             // the platform count
            --platform[departure[i] + 1];
        }

        // We are running loop till 2361 because
        // maximum time value in a day can be 23:60
        for(int i = 1; i < 2361; i++)
        {

            // Taking cumulative sum of platform
            // give us required number of
            // platform fro every minute
            platform[i] = platform[i] +
                          platform[i - 1];
            requiredPlatform = Math.Max(requiredPlatform,
                                        platform[i]);
        }
        return requiredPlatform;
    }

  static void Main() {
    int[] arr = { 900, 940, 950, 1100, 1500, 1800 };
    int[] dep = { 910, 1200, 1120, 1130, 1900, 2000 };
    int n = arr.Length;

    Console.Write("Minimum Number of " +
                       "Platforms Required = " +
                       minPlatform(arr, dep, n));
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        function minPlatform(arrival, departure, n) {

            // as time range from 0 to 2359 in 24 hour clock,
            // we declare an array for values from 0 to 2360
            let platform = new Array(2361).fill(0);
            let requiredPlatform = 1;
            for (let i = 0; i < n; i++) {

                // increment the platforms for arrival
                ++platform[arrival[i]];

                // once train departs we
                // decrease the platform count
                --platform[departure[i] + 1];
            }

            // We are running loop till 2361
            // because maximum time value
            // in a day can be 23:60
            for (let i = 1; i < 2361; i++) {

                // taking cumulative sum of
                // platform give us required
                // number of platform fro every minute
                platform[i] =
                platform[i] + platform[i - 1];

                requiredPlatform =
                Math.max(requiredPlatform, platform[i]);
            }
            return requiredPlatform;
        }

        // Driver code

        let arr = [900, 940, 950, 1100, 1500, 1800];
        let dep = [910, 1200, 1120, 1130, 1900, 2000];
        let n = arr.length;
        document.write("Minimum Number of Platforms Required = "
            + minPlatform(arr, dep, n));

    // This code is contributed by Potta Lokesh

    </script>
```

**输出:**

```
Minimum Number of Platforms Required = 3
```

**复杂度分析:**

*   **时间复杂度:** O(N)。
*   **空间复杂度:** O(1)。**T3】**

本文由**贾丁·戈亚尔**和**阿比纳夫·库马尔·辛格**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。