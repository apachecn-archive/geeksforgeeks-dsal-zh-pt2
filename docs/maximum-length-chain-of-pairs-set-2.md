# 成对链的最大长度|组-2

> 原文:[https://www . geesforgeks . org/最大长度成对链-set-2/](https://www.geeksforgeeks.org/maximum-length-chain-of-pairs-set-2/)

给定一组大小为 **N** 的数对。在每对中，第一个数字总是小于第二个数字。如果 b < c，一对(c，d)可以跟在另一对(a，b)之后。成对的链可以以这种方式形成。任务是找出由给定的一组对组成的最长链的长度。

**示例:**

> **输入:** N = 5，arr={{5，24}、{39，60}、{15，28}、{27，40}、{50，90} }
> **输出:** 3
> 能形成的最长链长为 3，链长为{{5，24}、{27，40}、{50，90} }。
> 
> **输入:** N = 2，arr={{5，10}，{1，11 } }
> T3】输出: 1

**方法:**这个问题的动态规划方法已经讨论过了[这里](https://www.geeksforgeeks.org/maximum-length-chain-of-pairs-dp-20/)。
思路是用贪婪的方法解决问题，和[活动选择问题](https://www.geeksforgeeks.org/activity-selection-problem-greedy-algo-1/)一样。

*   按照每对的第二个数递增的顺序对所有对进行排序。
*   选择第一个“否”作为第一对链，并用第一对链的第二个值设置变量 s(比如说)。
*   从数组的第二对迭代到最后一对，如果当前对的第一个元素的值大于先前选择的对，则选择当前对并更新最大长度和变量 s 的值。
*   返回链的最大长度值。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator function which can compare
// the second element of the pair used to
// sort pairs in increasing order of second value.
const bool comparator(const pair<int,int>& p1, const pair<int,int>& p2)
{
    return (p1.second < p2.second);
}

// Function for finding max length chain
int maxChainLen(vector<pair<int,int> >p, int n)
{
    // Initialize length l = 1
    int l = 1;

    // Sort all pair in increasing order
    // according to second no of pair
    sort(p.begin(),p.end(),comparator);

    // Pick up the first pair and assign the
    // value of second element fo pair to a
    // temporary variable s
    int s = p[0].second;

    // Iterate from second pair (index of
    // the second pair is 1) to the last pair
    for (int i = 1; i < n; i++) {

        // If first of current pair is greater
        // than previously selected pair then
        // select current pair and update
        // value of l and s
        if (p[i].first > s) {
            l++;
            s = p[i].second;
        }
    }

    // Return maximum length
    return l;
}

// Driver Code
int main()
{

    // Declaration of vector of pairs
    vector<pair<int,int>> p = { { 5, 24 }, { 39, 60 },
              { 15, 28 }, { 27, 40 }, { 50, 90 } };

    int n = p.size();

    // Function call
    cout << maxChainLen(p, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

// Structure for storing pairs
// of first and second values.
class GFG{

// Class for storing pairs
// of first and second values.
static class Pair
{
    int first;
    int second;

    Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
};

// Function for finding max length chain
static int maxChainLen(Pair p[], int n)
{

    // Initialize length l = 1
    int l = 1;

    // Sort all pair in increasing order
    // according to second no of pair
    Arrays.sort(p, new Comparator<Pair>()
    {
        public int compare(Pair a, Pair b)
        {
            return a.second - b.second;
        }
    });

    // Pick up the first pair and assign the
    // value of second element fo pair to a
    // temporary variable s
    int s = p[0].second;

    // Iterate from second pair (index of
    // the second pair is 1) to the last pair
    for(int i = 1; i < n; i++)
    {

        // If first of current pair is greater
        // than previously selected pair then
        // select current pair and update
        // value of l and s
        if (p[i].first > s)
        {
            l++;
            s = p[i].second;
        }
    }

    // Return maximum length
    return l;
}

// Driver Code
public static void main(String args[])
{

    // Declaration of array of structure
    Pair p[] = new Pair[5];

    p[0] = new Pair(5, 24);
    p[1] = new Pair(39, 60);
    p[2] = new Pair(15, 28);
    p[3] = new Pair(27, 40);
    p[4] = new Pair(50, 90);

    int n = p.length;

    // Function call
    System.out.println(maxChainLen(p, n));
}
}

// This code is contributed by adityapande88
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;

// Structure for storing pairs
// of first and second values.
class GFG{

// Class for storing pairs
// of first and second values.
class Pair : IComparable<Pair>
{
    public int first, second;
    public Pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
    public int CompareTo(Pair p)
    {
        return this.second-p.second;
    }
}

// Function for finding max length chain
static int maxChainLen(Pair []p, int n)
{

    // Initialize length l = 1
    int l = 1;

    // Sort all pair in increasing order
    // according to second no of pair
    Array.Sort(p);

    // Pick up the first pair and assign the
    // value of second element fo pair to a
    // temporary variable s
    int s = p[0].second;

    // Iterate from second pair (index of
    // the second pair is 1) to the last pair
    for(int i = 1; i < n; i++)
    {

        // If first of current pair is greater
        // than previously selected pair then
        // select current pair and update
        // value of l and s
        if (p[i].first > s)
        {
            l++;
            s = p[i].second;
        }
    }

    // Return maximum length
    return l;
}

// Driver Code
public static void Main(String []args)
{

    // Declaration of array of structure
    Pair []p = new Pair[5];

    p[0] = new Pair(5, 24);
    p[1] = new Pair(39, 60);
    p[2] = new Pair(15, 28);
    p[3] = new Pair(27, 40);
    p[4] = new Pair(50, 90);

    int n = p.Length;

    // Function call
    Console.WriteLine(maxChainLen(p, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function for finding max length chain
def maxChainLen(p, n):
    # Initialize length l = 1
    l = 1

    # Sort all pair in increasing order
    # according to second no of pair
    p.sort(key=lambda x:x[1])

    # Pick up the first pair and assign the
    # value of second element fo pair to a
    # temporary variable s
    s = p[0][1]

    # Iterate from second pair (index of
    # the second pair is 1) to the last pair
    for i in range(n):

        # If first of current pair is greater
        # than previously selected pair then
        # select current pair and update
        # value of l and s
        if (p[i][0] > s) :
            l+=1
            s = p[i][1]

    # Return maximum length
    return l

# Driver Code
if __name__ == '__main__':

    # Declaration of vector of pairs
    p = [(5, 24) , (39, 60) ,
              (15, 28) , (27, 40) , (50, 90)] 

    n = len(p)

    # Function call
    print(maxChainLen(p, n))
```

**Output:** 

```
3
```

**时间复杂度:** O(N*log(N))
**辅助空间:** O(1)