# 避开给定障碍物阵列的最小跳跃长度

> 原文:[https://www . geesforgeks . org/最小跳跃长度以避开给定的障碍物阵列/](https://www.geeksforgeeks.org/minimum-length-of-jumps-to-avoid-given-array-of-obstacles/)

给我们直线上障碍物的坐标。我们从 0 点开始跳跃，我们需要到达终点，避开一切障碍。每次跳跃的长度必须相同(例如，如果我们从 0 跳到 4，那么我们必须从 4 跳到 8)。我们需要找到跳跃的最小长度，这样我们就可以到达终点，避免所有的障碍。

**示例:**

```
Input : obs[] = [5, 3, 6, 7, 9]
Output : 4
Obstacles are at points 3, 5, 6, 7 and 9
We jump from 0 to 4, then 4 to 8, then 4
to 12\. This is how we reach end with jumps
of length 4\. If we try lower jump lengths,
we cannot avoid all obstacles.

Input : obs[] = [5, 8, 9, 13, 14]
Output : 6 
```

我们在散列表中插入所有障碍物的位置。我们也找到了障碍的最大值。然后我们尝试了从 1 到最大的所有可能的跳跃大小。如果任何跳跃的大小导致障碍，我们不考虑那个跳跃。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to find length of a jump
// to reach end avoiding all obstacles
#include <bits/stdc++.h>
#define mod 1000000007
using namespace std;

int avoidObstacles(unordered_set<int> obs)
{

    // set jump distance to 1
    int jump_dist = 1;

    // flag to check if current jump distance
    // hits an obstacle
    bool obstacle_hit = true;

    while(obstacle_hit)
    {

        obstacle_hit = false;
        jump_dist += 1;

        // checking if jumping with current length
        // hits an obstacle
        for (auto i:obs)
        {
            if (i % jump_dist == 0)
            {

                // if obstacle is hit repeat process
                // after increasing jump distance
                obstacle_hit = true;
                break;
            }
            }
        }

    return jump_dist;
}

// Driver Code
int main()
{
    unordered_set<int> a = {5, 3, 6, 7, 9};
    int b = avoidObstacles(a);
    cout << b;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find length of a jump
// to reach end avoiding all obstacles
import java.util.*;

public class obstacle {
    static int avoidObstacles(int[] obs)
    {
        // Insert all array elements in a hash table
        // and find the maximum value in the array
        HashSet<Integer> hs = new HashSet<Integer>();
        int max = obs[0];
        for (int i=0; i<obs.length; i++)
        {
            hs.add(obs[i]);
            max = Math.max(max, obs[i]);
        }

        // checking for every possible length which
        // yield us solution
        for (int i = 1; i <= max; i++) {
            int j;
            for (j = i; j <= max; j = j + i) {

                // if there is obstacle, break the loop.
                if (hs.contains(j))
                    break;
            }

            // If above loop did not break
            if (j > max)
                return i;        
        }

        return max+1;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int a[] = new int[] { 5, 3, 6, 7, 9 };
        int b = avoidObstacles(a);
        System.out.println(b);
    }
}
```

## 蟒蛇 3

```
# Python3 program to find length of a jump
# to reach end avoiding all obstacles
def avoidObstacles(obs):

    # sort the list in ascending order
    obs = sorted(obs)

    # set jump distance to 1
    jump_dist = 1

    # flag to check if current jump distance
    # hits an obstacle
    obstacle_hit = True

    while(obstacle_hit):

        obstacle_hit = False
        jump_dist += 1

        # checking if jumping with current length
        # hits an obstacle
        for i in range(0, len(obs)):
            if obs[i] % jump_dist == 0:

                # if obstacle is hit repeat process
                # after increasing jump distance
                obstacle_hit = True
                break

    return jump_dist

# Driver Code
a = [5, 3, 6, 7, 9]
b = avoidObstacles(a)
print(b)

# This code is contributed by ViratJoshi
```

## C#

```
// C# program to find length of a jump
// to reach end avoiding all obstacles
using System;
using System.Collections.Generic;

public class obstacle
{
    static int avoidObstacles(int[] obs)
    {
        // Insert all array elements in a hash table
        // and find the maximum value in the array
        HashSet<int> hs = new HashSet<int>();
        int max = obs[0];
        for (int i = 0; i < obs.Length; i++)
        {
            hs.Add(obs[i]);
            max = Math.Max(max, obs[i]);
        }

        // checking for every possible length which
        // yield us solution
        for (int i = 1; i <= max; i++)
        {
            int j;
            for (j = i; j <= max; j = j + i)
            {

                // if there is obstacle, break the loop.
                if (hs.Contains(j))
                    break;
            }

            // If above loop did not break
            if (j > max)
                return i;        
        }
        return max+1;
    }

    // Driver Code
    public static void Main()
    {
        int []a = new int[] { 5, 3, 6, 7, 9 };
        int b = avoidObstacles(a);
        Console.WriteLine(b);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to find length of a jump
// to reach end avoiding all obstacles

    function avoidObstacles(obs)
    {
        // Insert all array elements in a hash table
        // and find the maximum value in the array
        let hs = new Set();
        let max = obs[0];
        for (let i=0; i<obs.length; i++)
        {
            hs.add(obs[i]);
            max = Math.max(max, obs[i]);
        }

        // checking for every possible length which
        // yield us solution
        for (let i = 1; i <= max; i++) {
            let j;
            for (j = i; j <= max; j = j + i) {

                // if there is obstacle, break the loop.
                if (hs.has(j))
                    break;
            }

            // If above loop did not break
            if (j > max)
                return i;        
        }

        return max+1;
    }

    // Driver Code
    let a=[5, 3, 6, 7, 9 ];
    let b = avoidObstacles(a);
    document.write(b);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
4
```