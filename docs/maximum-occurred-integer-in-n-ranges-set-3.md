# n 个范围内出现的最大整数| Set-3

> 原文:[https://www . geesforgeks . org/maximum-increated-整数 in-n-ranges-set-3/](https://www.geeksforgeeks.org/maximum-occurred-integer-in-n-ranges-set-3/)

给定从 **L** 到 **R** 的 **N** 范围，任务是找出所有范围内出现的最大整数。如果存在多个这样的整数，打印最小的一个。

**示例:**

> **输入:**点[] = { {1，6}，{2，3}，{2，5}，{3，8} }
> 输出: 3
> 说明:
> 1 出现在 1 范围{1，6}
> 2 出现在 3 范围{1，6}，{2，3}，{2，5}
> 3 出现在 4 范围{1，6}，{2，3}，{2，5}，{3，8 }
> 3 出现在 4 范围{1，6}，{ 4 {2，5}、{3，8}
> 6 在 2 个范围{1，6}中出现 2 个，{3，8}
> 7 在 1 个范围{3，8}
> 8 在 1 个范围{3，8}
> 中出现 1 个。因此，出现次数最多的整数是 3。
> 
> **输入:**点[] = { {1，4}，{1，9}，{1，2 } }；
> T3】输出: 1

**进场:**这是[最大出现整数 n 范围](https://www.geeksforgeeks.org/maximum-occurred-integer-in-n-ranges-set-2/)的临时进场。主要思想是使用坐标压缩使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。因此，没有必要创建一个频率阵列，这将超过大范围的内存限制。下面是解决这个问题的分步算法:

1.  初始化一个[有序地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)名称**点**，以跟踪给定范围的起点和终点。
2.  对于给定范围的每个起始指数，将 ***点【L】**的值增加 1* 。
3.  对于给定范围的每个结束指数，将 ***点【R+1】**的值减少 1，*。
4.  按照点的值的递增顺序迭代地图。注意**频率【当前点】=频率【上一点】+点【当前点】**。在变量**中保持当前点的频率值。**
5.  最大值为 **cur_freq** 的点就是答案。
6.  存储索引并返回。

下面是上述方法的实现:

## C++

```
// C++ program of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the most
// occurred element in given ranges
void maxOccurring(int range[][2], int n)
{
    // STL map for storing start
    // and end points
    map<int, int> points;

    for (int i = 0; i < n; i++) {
        int l = range[i][0];
        int r = range[i][1];

        // Increment at starting point
        points[l]++;

        // Decrement at ending point
        points[r + 1]--;
    }

    // Stores current frequency
    int cur_freq = 0;

    // Store element with maximum frequency
    int ans = 0;

    // Frequency of the current ans
    int freq_ans = 0;

    for (auto x : points) {
        // x.first denotes the current
        // point and x.second denotes
        // points[x.first]
        cur_freq += x.second;

        // If frequency of x.first is
        // greater that freq_ans
        if (cur_freq > freq_ans) {
            freq_ans = cur_freq;
            ans = x.first;
        }
    }

    // Print Answer
    cout << ans;
}

// Driver code
int main()
{
    int range[][2]
        = { { 1, 6 }, { 2, 3 }, { 2, 5 }, { 3, 8 } };
    int n = sizeof(range) / sizeof(range[0]);

    // Function call
    maxOccurring(range, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program of the above approach
import java.util.*;

class GFG{

// Function to print the most
// occurred element in given ranges
static void maxOccurring(int range[][], int n)
{
    // STL map for storing start
    // and end points
    HashMap<Integer,Integer> points = new HashMap<Integer,Integer>();

    for (int i = 0; i < n; i++) {
        int l = range[i][0];
        int r = range[i][1];

        // Increment at starting point
        if(points.containsKey(l)){
            points.put(l, points.get(l)+1);
        }
        else{
            points.put(l, 1);

        // Decrement at ending point
            if(points.containsKey(r + 1)){
                points.put(r + 1, points.get(r + 1)-1);
            }
    }
    }
    // Stores current frequency
    int cur_freq = 0;

    // Store element with maximum frequency
    int ans = 0;

    // Frequency of the current ans
    int freq_ans = 0;

    for (Map.Entry<Integer,Integer> entry :points.entrySet()) {
        // x.first denotes the current
        // point and x.second denotes
        // points[x.first]
        cur_freq += entry.getValue();

        // If frequency of x.first is
        // greater that freq_ans
        if (cur_freq > freq_ans) {
            freq_ans = cur_freq;
            ans = entry.getKey();
        }
    }

    // Print Answer
    System.out.print(ans);
}

// Driver code
public static void main(String[] args)
{
    int range[][]
        = { { 1, 6 }, { 2, 3 }, { 2, 5 }, { 3, 8 } };
    int n = range.length;

    // Function call
    maxOccurring(range, n);

}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program of the above approach

# Function to print the most
# occurred element in given ranges
def maxOccurring(range1, n):

    # STL map for storing start
    # and end points
    points = {}

    for i in range(n):
        l = range1[i][0]
        r = range1[i][1]

        # Increment at starting point
        if l in points:
            points[l] += 1
        else:
            points[l] = 1

        # Decrement at ending point
        if r+1 in points:
            points[r + 1] -= 1
        else:
            points[r+1] = 0

    # Stores current frequency
    cur_freq = 0

    # Store element with maximum frequency
    ans = 0

    # Frequency of the current ans
    freq_ans = 0

    for key,value in points.items():
        # x.first denotes the current
        # point and x.second denotes
        # points[x.first]
        cur_freq += value

        # If frequency of x.first is
        # greater that freq_ans
        if (cur_freq > freq_ans):
            freq_ans = cur_freq
            ans = key

    # Print Answer
    print(ans)

# Driver code
if __name__ == '__main__':
    range1 = [[1, 6],[2, 3],[2, 5],[3, 8]]
    n = len(range1)

    # Function call
    maxOccurring(range1, n)

    # This code is contributed by ipg2016107.
```

## C#

```
// C# program of the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to print the most
// occurred element in given ranges
static void maxOccurring(int [,]range, int n)
{
    // STL map for storing start
    // and end points
    Dictionary<int, int> points = new Dictionary<int,int>();

    for (int i = 0; i < n; i++) {
        int l = range[i,0];
        int r = range[i,1];

        // Increment at starting point
      if(points.ContainsKey(l))
        points[l]++;

      else
        points.Add(l,1);

        // Decrement at ending point
        if(points.ContainsKey(r+1))
          points[r + 1]--;
        else
          points.Add(r+1,0);
    }

    // Stores current frequency
    int cur_freq = 0;

    // Store element with maximum frequency
    int ans = 0;

    // Frequency of the current ans
    int freq_ans = 0;

    foreach(KeyValuePair<int,int> entry in points) {
        // x.first denotes the current
        // point and x.second denotes
        // points[x.first]
        cur_freq += entry.Value;

        // If frequency of x.first is
        // greater that freq_ans
        if (cur_freq > freq_ans) {
            freq_ans = cur_freq;
            ans = entry.Key;
        }
    }

    // Print Answer
    Console.Write(ans);
}

// Driver code
public static void Main()
{
    int [,]range = {{1, 6 }, { 2, 3 }, { 2, 5 }, { 3, 8 } };
    int n = 4;

    // Function call
    maxOccurring(range, n);
}
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to print the most
        // occurred element in given ranges
        function maxOccurring(range, n)
        {

            // STL map for storing start
            // and end points
            let points = new Map();

            for (let i = 0; i < n; i++) {
                let l = range[i][0];
                let r = range[i][1];

                // Increment at starting point
                if (points.has(l))
                    points.set(points.get(l), points.get(l) + 1);
                else
                    points.set(l, 1);

                // Decrement at ending point
                if (points.has(r + 1)) {
                    points.set(points.get(r + 1), points.get(r + 1) - 1);
                }

            }

            // Stores current frequency
            let cur_freq = 0;

            // Store element with maximum frequency
            let ans = 0;

            // Frequency of the current ans
            let freq_ans = 0;

            for (let [key, value] of points)
            {

                // x.first denotes the current
                // point and x.second denotes
                // points[x.first]
                cur_freq = cur_freq + value;

                // If frequency of x.first is
                // greater that freq_ans
                if (cur_freq > freq_ans) {
                    freq_ans = cur_freq;
                    ans = key;
                }
            }

            // Print Answer
            document.write(ans);
        }

        // Driver code
        let range
            = [[1, 6], [2, 3], [2, 5], [3, 8]];
        let n = range.length;

        // Function call
        maxOccurring(range, n);

// This code is contributed by Potta Lokesh
    </script>
```

**Output**

```
3
```

**时间复杂度:***O(n Logn)*
T5】空间复杂度: *O(n)*