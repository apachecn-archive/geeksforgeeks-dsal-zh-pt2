# 计算沿着给定字符串指定的路径重新访问的点

> 原文:[https://www . geesforgeks . org/count-points-哪些是重新访问的-同时遵循给定字符串指定的路径/](https://www.geeksforgeeks.org/count-points-which-are-revisited-while-following-the-path-specified-by-a-given-string/)

给定一个表示一系列移动的[字符串](https://www.geeksforgeeks.org/string-data-structure/)**S**(**L**、 **R** 、 **U** 和 **D** )和两个表示起始坐标的整数 **X** 和 **Y** ，任务是根据以下规则找到在遵循给定字符串中指定的方向时被重新访问的位置数:

*   如果当前字符为 **L** ，则减量**x**-按 **1** 坐标。
*   如果当前字符为 **R** ，则按 **1** 增加**x**-坐标。
*   如果当前字符为 **U** ，则按 **1** 增加**y**-坐标。
*   如果当前字符为 **D** ，则递减**y**-按 **1** 坐标。

**示例:**

> **输入:** S = "RDDUDL "，X = 0，Y = 0
> **输出:** 2
> **说明:**初始坐标为(0，0)。坐标按照给定的遍历顺序变化如下:
> (0，0) - > (1，0) - > **(1，-1)** - > **(1，-2)** - > **(1，-1)** - > **(1，-2)** - > (0，-2)
> 因此，一个坐标被重访的次数为 2 次
> 
> **输入:** S = "RDDUDL "，X = 2，Y = 3
> T3】输出: 2

**方法:**按照给定的步骤解决问题:

*   初始化一个由[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)组成的[散列集合](https://www.geeksforgeeks.org/hashset-in-java/)，该集合存储遍历给定字符串时访问的坐标对和散列集合中的当前坐标。
*   [遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/) **S** ，并执行以下步骤:
    *   根据给定的规则更新坐标 **{X，Y}** 的值。
    *   检查更新的坐标是否存在于 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 中。如果发现**为真**，则按 **1** 递增**计数**。否则，[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。
*   完成上述步骤后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of times
// already visited position is revisited
// after starting traversal from {X, Y}
int count(string S, int X, int Y)
{
    int N = S.length();

    // Stores the x and y temporarily
    int temp_x = 0, temp_y = 0;

    // Stores the number of times an
    // already visited position
    // is revisited
    int count = 0;

    // Initialize hashset
    set<pair<int, int> > s;

    // Insert the starting coordinates
    s.insert({ X, Y });

    // Traverse over the string
    for (int i = 0; i < N; i++) {
        temp_x = X;
        temp_y = Y;

        // Update the coordinates according
        // to the current directions
        if (S[i] == 'U') {
            X++;
        }
        else if (S[i] == 'D') {
            X--;
        }
        else if (S[i] == 'R') {
            Y++;
        }
        else {
            Y--;
        }

        // If the new {X, Y} has been
        // visited before, then
        // increment the count by 1
        if (s.find({ temp_x + X, temp_y + Y })
            != s.end()) {
            count++;
        }

        // Otherwise
        else {

            // Insert new {x, y}
            s.insert({ temp_x + X,
                       temp_y + Y });
        }
    }

    return count;
}

// Driver Code
int main()
{
    string S = "RDDUDL";
    int X = 0, Y = 0;
    cout << count(S, X, Y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG
{

  // Function to find the number of times
  // already visited position is revisited
  // after starting traversal from {X, Y}
  static int count(String S, int X, int Y)
  {
    int N = S.length();

    // Stores the x and y temporarily
    int temp_x = 0, temp_y = 0;

    // Stores the number of times an
    // already visited position
    // is revisited
    int count = 0;

    // Initialize hashset
    HashSet<String> s = new HashSet<>();

    // Insert the starting coordinates
    s.add((X + "#" + Y));

    // Traverse over the string
    for (int i = 0; i < N; i++) {
      temp_x = X;
      temp_y = Y;

      // Update the coordinates according
      // to the current directions
      if (S.charAt(i) == 'U') {
        X++;
      }
      else if (S.charAt(i) == 'D') {
        X--;
      }
      else if (S.charAt(i) == 'R') {
        Y++;
      }
      else {
        Y--;
      }

      // If the new {X, Y} has been
      // visited before, then
      // increment the count by 1
      if (s.contains((temp_x + X) + "#"
                     + (temp_y + Y))) {
        count++;
      }

      // Otherwise
      else {

        // Insert new {x, y}
        s.add((temp_x + X) + "#" + (temp_y + Y));
      }
    }

    return count;
  }

  // Driver Code
  public static void main(String[] args)
  {

    String S = "RDDUDL";
    int X = 0, Y = 0;
    System.out.print(count(S, X, Y));
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of times
# already visited position is revisited
# after starting traversal from {X, Y}
def count(S, X, Y):
    N = len(S)

    # Stores the x and y temporarily
    temp_x, temp_y = 0, 0

    # Stores the number of times an
    # already visited position
    # is revisited
    count = 0

    # Initialize hashset
    s = {}

    # Insert the starting coordinates
    s[(X, Y)] = 1

    # Traverse over the string
    for i in range(N):
        temp_x = X
        temp_y = Y

        # Update the coordinates according
        # to the current directions
        if (S[i] == 'U'):
            X += 1
        elif (S[i] == 'D'):
            X -= 1
        elif (S[i] == 'R'):
            Y += 1
        else:
            Y -= 1

        # If the new {X, Y} has been
        # visited before, then
        # increment the count by 1
        if ((temp_x + X, temp_y + Y ) in s):
            count += 1
        # Otherwise
        else:
            # Insert new {x, y}
            s[(temp_x + X,temp_y + Y )] = 1
    return count

# Driver Code
if __name__ == '__main__':
    S = "RDDUDL"
    X,Y = 0, 0
    print (count(S, X, Y))

    # This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to find the number of times
  // already visited position is revisited
  // after starting traversal from {X, Y}
  static int count(String S, int X, int Y)
  {
    int N = S.Length;

    // Stores the x and y temporarily
    int temp_x = 0, temp_y = 0;

    // Stores the number of times an
    // already visited position
    // is revisited
    int count = 0;

    // Initialize hashset
    HashSet<String> s = new HashSet<String>();

    // Insert the starting coordinates
    s.Add((X + "#" + Y));

    // Traverse over the string
    for (int i = 0; i < N; i++) {
      temp_x = X;
      temp_y = Y;

      // Update the coordinates according
      // to the current directions
      if (S[i] == 'U') {
        X++;
      }
      else if (S[i] == 'D') {
        X--;
      }
      else if (S[i] == 'R') {
        Y++;
      }
      else {
        Y--;
      }

      // If the new {X, Y} has been
      // visited before, then
      // increment the count by 1
      if (s.Contains((temp_x + X) + "#"
                     + (temp_y + Y))) {
        count++;
      }

      // Otherwise
      else {

        // Insert new {x, y}
        s.Add((temp_x + X) + "#" + (temp_y + Y));
      }
    }
    return count;
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S = "RDDUDL";
    int X = 0, Y = 0;
    Console.Write(count(S, X, Y));
  }
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the number of times
// already visited position is revisited
// after starting traversal from {X, Y}
function count(S, X, Y){
    let N = S.length;

    // Stores the x and y temporarily
    let temp_x = 0, temp_y = 0;

    // Stores the number of times an
    // already visited position
    // is revisited
    let count = 0;

    // Initialize hashset
    let s = new Set();

    // Insert the starting coordinates
    s.add((X + "#" + Y));

    // Traverse over the string
    for (let i = 0; i < N; i++) {
      temp_x = X;
      temp_y = Y;

      // Update the coordinates according
      // to the current directions
      if (S[i] == 'U') {
        X++;
      }
      else if (S[i] == 'D') {
        X--;
      }
      else if (S[i] == 'R') {
        Y++;
      }
      else {
        Y--;
      }

      // If the new {X, Y} has been
      // visited before, then
      // increment the count by 1
      if (s.has((temp_x + X) + "#"
                     + (temp_y + Y))) {
        count++;
      }

      // Otherwise
      else {

        // Insert new {x, y}
        s.add((temp_x + X) + "#" + (temp_y + Y));
      }
    }

    return count;
}

// Driver Code

    let S = "RDDUDL";
    let X = 0, Y = 0;
    document.write(count(S, X, Y));

</script>       
```

**Output:** 

```
2
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*