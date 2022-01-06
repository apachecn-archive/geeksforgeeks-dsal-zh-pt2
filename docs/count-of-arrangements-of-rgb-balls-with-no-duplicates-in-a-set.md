# 一组中没有重复的 RGB 球排列计数

> 原文:[https://www . geeksforgeeks . org/不重复排列的 rgb 球的排列计数/](https://www.geeksforgeeks.org/count-of-arrangements-of-rgb-balls-with-no-duplicates-in-a-set/)

给定 **R** 红球、 **G** 绿球、 **B** 蓝球。一套可以有 **1** 、 **2** 或 **3** 球。此外，一套可以有所有相同颜色的球或所有不同颜色的球。所有其他可能的集合都不被认为是有效的。任务是计算放置所有球所需的**最小**可能集合。

**示例:**

> **输入:** R = 4，G = 2，B = 4
> **输出:** 4
> **说明:**可以有 4 个集合满足上述所有条件{R，R，R}、{B，B，B}、{G，R}、{G，B}。
> 所以，答案是 4。
> 
> **输入:** R = 1，G = 7，B = 1
> **输出:** 3
> **说明:**有 3 个有效集{R，G，B}，{G，G，G}，{G，G，G}

**方法:**这个问题是基于分析的。按照以下步骤解决给定的问题。

*   问题陈述可以通过仔细的案例分析来解决。
*   不失一般性地假设**R<= G<= b**
*   所以至少会形成 R 个集合。从 G 和 b 中减去 R。由这一步形成的所有集合中会有不同的球。
*   剩下的球将是 **0，G–R，B–R**。对于其余的球，形成相同的球组。
*   完成上述步骤后，剩余的球将为 **0，(G–R)% 3，(B–R)% 3。**
*   现在可以有 3 种情况:
*   第二项为 0，第三项为零。不需要额外的设置。
*   (第二项为 1，第三项为 1)或(第二项为 0，第三项为 2，反之亦然)。需要 1 套额外的。
*   在所有其他情况下，还需要 2 套。
*   仔细检查以上所有条件，打印答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate minimum sets
// required with given conditions
int minimumSetBalls(int R, int G, int B)
{
    // Push values R, G, B
    // in a vector and sort them
    vector<int> balls;
    balls.push_back(R);
    balls.push_back(G);
    balls.push_back(B);

    // Sort the vector
    sort(balls.begin(), balls.end());

    // Store the answer
    int ans = 0;
    ans += balls[0];
    balls[1] -= balls[0];
    balls[2] -= balls[0];
    balls[0] = 0;

    // Check all mentioned conditions
    ans += balls[1] / 3;
    balls[1] %= 3;
    ans += balls[2] / 3;
    balls[2] %= 3;

    if (balls[1] == 0
        && balls[2] == 0) {
        // No extra set requried
    }
    else if (balls[1] == 1
             && balls[2] == 1) {
        ans++;
        // 1 extra set is required
    }
    else if ((balls[1] == 2
              && balls[2] == 0)
             || (balls[1] == 0
                 && balls[2] == 2)) {
        ans++;
        // 1 extra set is required
    }
    else {
        // 2 extra sets will be required
        ans += 2;
    }
    return ans;
}

// Driver Code
int main()
{
    int R = 4, G = 2, B = 4;
    cout << minimumSetBalls(R, G, B);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

public class GFG{

// Function to calculate minimum sets
// required with given conditions
static int minimumSetBalls(int R, int G, int B)
{

    // Push values R, G, B
    // in a vector and sort them
    ArrayList<Integer> balls = new ArrayList<Integer>();
    balls.add(R);
    balls.add(G);
    balls.add(B);

    // Sort the vector
    Collections.sort(balls);   ;

    // Store the answer
    int ans = 0;
    ans += balls.get(0);
    balls.set(1,balls.get(1) - balls.get(0));
    balls.set(2,balls.get(2) - balls.get(0));
    balls.set(0,0);

    // Check all mentioned conditions
    ans += balls.get(1) / 3;
    balls.set(1, balls.get(1) % 3);
    ans += balls.get(2) / 3;
    balls.set(2,balls.get(2) % 3);

    if (balls.get(1) == 0
        && balls.get(2) == 0)
    {

        // No extra set requried
    }
    else if (balls.get(1) == 1
             && balls.get(2) == 1) {
        ans++;
        // 1 extra set is required
    }
    else if ((balls.get(1) == 2
              && balls.get(2) == 0)
             || (balls.get(1) == 0
                 && balls.get(2) == 2)) {
        ans++;
        // 1 extra set is required
    }
    else {
        // 2 extra sets will be required
        ans += 2;
    }
    return ans;
}

// Driver Code
public static void main(String []args)
{
    int R = 4, G = 2, B = 4;
    System.out.println( minimumSetBalls(R, G, B));
}
}

// This code is contributed by AnkThon
```

## 蟒蛇 3

```
# Python3 Program to implement the above approach

# Function to calculate minimum sets
# required with given conditions
def minimumSetBalls(R, G, B) :

    # Push values R, G, B
    # in a vector and sort them
    balls = [];
    balls.append(R);
    balls.append(G);
    balls.append(B);

    # Sort the vector
    balls.sort();

    # Store the answer
    ans = 0;
    ans += balls[0];
    balls[1] -= balls[0];
    balls[2] -= balls[0];
    balls[0] = 0;

    # Check all mentioned conditions
    ans += balls[1] // 3;
    balls[1] %= 3;
    ans += balls[2] // 3;
    balls[2] %= 3;

    if (balls[1] == 0 and balls[2] == 0) :
        pass

    elif (balls[1] == 1 and balls[2] == 1) :
        ans += 1;
        # 1 extra set is required

    elif ((balls[1] == 2 and balls[2] == 0) or (balls[1] == 0 and balls[2] == 2)) :
        ans += 1;
        # 1 extra set is required
    else :
        # 2 extra sets will be required
        ans += 2;

    return ans;

# Driver Code
if __name__ == "__main__" :

    R = 4; G = 2; B = 4;
    print(minimumSetBalls(R, G, B));

    # This code is contributed by AnkThon
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate minimum sets
// required with given conditions
static int minimumSetBalls(int R, int G, int B)
{

    // Push values R, G, B
    // in a vector and sort them
    List<int> balls = new List<int>();
    balls.Add(R);
    balls.Add(G);
    balls.Add(B);

    // Sort the vector
    balls.Sort();

    // Store the answer
    int ans = 0;
    ans += balls[0];
    balls[1] -= balls[0];
    balls[2] -= balls[0];
    balls[0] = 0;

    // Check all mentioned conditions
    ans += balls[1] / 3;
    balls[1] %= 3;
    ans += balls[2] / 3;
    balls[2] %= 3;

    if (balls[1] == 0
        && balls[2] == 0)
    {

        // No extra set requried
    }
    else if (balls[1] == 1
             && balls[2] == 1) {
        ans++;
        // 1 extra set is required
    }
    else if ((balls[1] == 2
              && balls[2] == 0)
             || (balls[1] == 0
                 && balls[2] == 2)) {
        ans++;
        // 1 extra set is required
    }
    else {
        // 2 extra sets will be required
        ans += 2;
    }
    return ans;
}

// Driver Code
public static void Main()
{
    int R = 4, G = 2, B = 4;
    Console.WriteLine( minimumSetBalls(R, G, B));
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

        // JavaScript Program to implement
        // the above approach

        // Function to calculate minimum sets
        // required with given conditions
        function minimumSetBalls(R, G, B)
        {

            // Push values R, G, B
            // in a vector and sort them
            let balls = [];
            balls.push(R);
            balls.push(G);
            balls.push(B);

            // Sort the vector
            balls.sort(function (a, b) { return a - b })

            // Store the answer
            let ans = 0;
            ans += balls[0];
            balls[1] -= balls[0];
            balls[2] -= balls[0];
            balls[0] = 0;

            // Check all mentioned conditions
            ans += Math.floor(balls[1] / 3);
            balls[1] %= 3;
            ans += Math.floor(balls[2] / 3);
            balls[2] %= 3;

            if (balls[1] == 0
                && balls[2] == 0) {
                // No extra set requried
            }
            else if (balls[1] == 1
                && balls[2] == 1) {
                ans++;
                // 1 extra set is required
            }
            else if ((balls[1] == 2
                && balls[2] == 0)
                || (balls[1] == 0
                    && balls[2] == 2)) {
                ans++;
                // 1 extra set is required
            }
            else {
                // 2 extra sets will be required
                ans += 2;
            }
            return ans;
        }

        // Driver Code
        let R = 4, G = 2, B = 4;
        document.write(minimumSetBalls(R, G, B));

    // This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
4
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)