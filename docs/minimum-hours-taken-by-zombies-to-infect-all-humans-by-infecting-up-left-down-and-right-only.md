# 僵尸通过只感染上、左、下和右感染所有人类所需的最短时间

> 原文:[https://www . geeksforgeeks . org/僵尸感染全人类的最短时间-只感染上-左-下-右/](https://www.geeksforgeeks.org/minimum-hours-taken-by-zombies-to-infect-all-humans-by-infecting-up-left-down-and-right-only/)

给定一个 **2D** 网格，每个细胞要么是一个**僵尸**T4【1】要么是人类 **0** 。丧尸每小时可以将相邻**水平或垂直** **(上/下/左/右)**人类变成丧尸。任务是找出感染所有人需要多少小时。

**示例:**

> **输入:** arr[][] = { { 0，1，0，1 }，
> { 0，0，0，0 }，
> { 0，0，0，1 } }；
> **输出:** 3
> **说明:**在时间= 3 小时内所有人类都会转化为丧尸。
> 
> **输入:** arr[][] = {{ 0，1，0 }，
> { 0，0，0 }，
> { 0，0，0 } }；
> T5】输出: 3

**途径:**这个问题可以用[多源 BFS](https://www.geeksforgeeks.org/multi-source-shortest-path-in-unweighted-graph/) 解决。按照以下步骤解决给定的问题。

*   因为所有的丧尸都在同时扩张所以**多源 BFS** 需要使用。
*   最初将所有**僵尸位置**推入**队列**。
*   当队列不空时，尝试访问每个僵尸的所有**四个方向**，因为每个僵尸的效果将在所有四个方向。
*   每套僵尸后增加 **1** 的时间。
*   在检查是否有任何细胞留给人类，这意味着最初**网格中没有僵尸**，所以**返回-1** 。
*   否则返回**感染所有人类所花费的总时间**。

下面是上述方法的实现:

## C++14

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// To check if current coordinate
// lies inside the grid or not
bool isValid(int i, int j, int n, int m)
{
    if (i < n and i >= 0 and j < m and j >= 0)
        return 1;
    else
        return 0;
}

// Function to find out minimum time required
// to infect all humans into zombies
int zombieInfection(vector<vector<int> >& grid)
{
    // Queue to store coordinates for BFS
    queue<pair<int, int> > q;

    // Number of rows
    int n = grid.size();

    // Number of columns
    int m = grid[0].size();

    int cur = 0, next = 0;

    // Initially pushing coordinates of all the
    // zombies into the queue
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {

            // If cell is zombie
            if (grid[i][j] == 1) {
                q.push({ i, j });
                cur++;
            }
        }
    }

    // To keep track of the time
    int t = 0;

    // While any zombie is left
    while (!q.empty()) {
        for (int i = 0; i < cur; i++) {
            auto use = q.front();
            q.pop();
            int x = use.first, y = use.second;

            // Checking for all the four directons
            // horizontally and vertically
            if (isValid(x + 1, y, n, m)
                and grid[x + 1][y] == 0) {
                grid[x + 1][y] = 1;
                q.push({ x + 1, y });
                next++;
            }
            if (isValid(x - 1, y, n, m)
                and grid[x - 1][y] == 0) {
                grid[x - 1][y] = 1;
                q.push({ x - 1, y });
                next++;
            }
            if (isValid(x, y + 1, n, m)
                and grid[x][y + 1] == 0) {
                grid[x][y + 1] = 1;
                q.push({ x, y + 1 });
                next++;
            }
            if (isValid(x, y - 1, n, m)
                and grid[x][y - 1] == 0) {
                grid[x][y - 1] = 1;
                q.push({ x, y - 1 });
                next++;
            }
        }
        if (next == 0)
            break;
        cur = next;
        next = 0;

        // Increment time
        t++;
    }

    // If no zombie was there in the grid
    // Then it is not possible to convert all
    // the humans to zombie so return -1
    for (int i = 0; i < n; i++)
        for (int j = 0; j < m; j++)
            if (grid[i][j] == 0)
                return -1;

    // Return the total time elapsed
    return t;
}

// Driver Code
int main()
{
    int N = 3, M = 4;

    // Given grid
    vector<vector<int> > grid = { { 0, 1, 0, 1 },
                                  { 0, 0, 0, 0 },
                                  { 0, 0, 0, 1 } };

    // Function Call
    cout << zombieInfection(grid);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;
class GFG
{

  // To check if current coordinate
  // lies inside the grid or not
  static boolean isValid(int i, int j, int n, int m)
  {
    if (i < n && i >= 0 && j < m && j >= 0)
      return true;
    else
      return false;
  }
  static class pair
  {
    int first, second;
    public pair(int first, int second) 
    {
      this.first = first;
      this.second = second;
    }   
  }

  // Function to find out minimum time required
  // to infect all humans into zombies
  static int zombieInfection(int [][]grid)
  {

    // Queue to store coordinates for BFS
    Queue<pair > q = new LinkedList<GFG.pair>();

    // Number of rows
    int n = grid.length;

    // Number of columns
    int m = grid[0].length;

    int cur = 0, next = 0;

    // Initially pushing coordinates of all the
    // zombies into the queue
    for (int i = 0; i < n; i++) {
      for (int j = 0; j < m; j++) {

        // If cell is zombie
        if (grid[i][j] == 1) {
          q.add(new pair( i, j ));
          cur++;
        }
      }
    }

    // To keep track of the time
    int t = 0;

    // While any zombie is left
    while (!q.isEmpty()) {
      for (int i = 0; i < cur; i++) {
        pair use = q.peek();
        q.remove();
        int x = use.first, y = use.second;

        // Checking for all the four directons
        // horizontally and vertically
        if (isValid(x + 1, y, n, m)
            && grid[x + 1][y] == 0) {
          grid[x + 1][y] = 1;
          q.add(new pair(  x + 1, y ));
          next++;
        }
        if (isValid(x - 1, y, n, m)
            && grid[x - 1][y] == 0) {
          grid[x - 1][y] = 1;
          q.add(new pair(  x - 1, y ));
          next++;
        }
        if (isValid(x, y + 1, n, m)
            && grid[x][y + 1] == 0) {
          grid[x][y + 1] = 1;
          q.add(new pair(  x, y + 1 ));
          next++;
        }
        if (isValid(x, y - 1, n, m)
            && grid[x][y - 1] == 0) {
          grid[x][y - 1] = 1;
          q.add(new pair(  x, y - 1 ));
          next++;
        }
      }
      if (next == 0)
        break;
      cur = next;
      next = 0;

      // Increment time
      t++;
    }

    // If no zombie was there in the grid
    // Then it is not possible to convert all
    // the humans to zombie so return -1
    for (int i = 0; i < n; i++)
      for (int j = 0; j < m; j++)
        if (grid[i][j] == 0)
          return -1;

    // Return the total time elapsed
    return t;
  }

  // Driver Code
  public static void main(String[] args)
  {
    int N = 3, M = 4;

    // Given grid
    int [][]grid = { { 0, 1, 0, 1 },
                    { 0, 0, 0, 0 },
                    { 0, 0, 0, 1 } };

    // Function Call
    System.out.print(zombieInfection(grid));

  }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# python program for above approach
from queue import Queue

# To check if current coordinate
# lies inside the grid or not
def isValid(i, j, n, m):

    if (i < n and i >= 0 and j < m and j >= 0):
        return 1
    else:
        return 0

# Function to find out minimum time required
# to infect all humans into zombies
def zombieInfection(grid):

    # Queue to store coordinates for BFS
    q = Queue()

    # Number of rows
    n = len(grid)

    # Number of columns
    m = len(grid[0])

    cur = 0
    next = 0

    # Initially pushing coordinates of all the
    # zombies into the queue

    for i in range(0, n):
        for j in range(0, m):

                        # If cell is zombie
            if (grid[i][j] == 1):
                q.put([i, j])
                cur += 1

        # To keep track of the time
    t = 0

    # While any zombie is left
    while (not q.empty()):
        for i in range(0, cur):
            use = q.get()
            x = use[0]
            y = use[1]

            # Checking for all the four directons
            # horizontally and vertically
            if (isValid(x + 1, y, n, m)
                    and grid[x + 1][y] == 0):
                grid[x + 1][y] = 1
                q.put([x + 1, y])
                next += 1

            if (isValid(x - 1, y, n, m)
                    and grid[x - 1][y] == 0):
                grid[x - 1][y] = 1
                q.put([x - 1, y])
                next += 1

            if (isValid(x, y + 1, n, m)
                    and grid[x][y + 1] == 0):
                grid[x][y + 1] = 1
                q.put([x, y + 1])
                next += 1

            if (isValid(x, y - 1, n, m)
                    and grid[x][y - 1] == 0):
                grid[x][y - 1] = 1
                q.put([x, y - 1])
                next += 1

        if (next == 0):
            break

        cur = next
        next = 0

        # Increment time
        t += 1

        # If no zombie was there in the grid
        # Then it is not possible to convert all
        # the humans to zombie so return -1
    for i in range(0, n):
        for j in range(0, m):
            if (grid[i][j] == 0):
                return -1

        # Return the total time elapsed
    return t

# Driver Code
if __name__ == "__main__":

    N = 3
    M = 4

    # Given grid
    grid = [[0, 1, 0, 1],
            [0, 0, 0, 0],
            [0, 0, 0, 1]]

    # Function Call
    print(zombieInfection(grid))

    # This code is contributed by rakeshsahni
```

## java 描述语言

```
<script>
   // JavaScript code for the above approach

   // To check if current coordinate
   // lies inside the grid or not
   function isValid(i, j, n, m) {
     if (i < n && i >= 0 && j < m && j >= 0)
       return 1;
     else
       return 0;
   }

   // Function to find out minimum time required
   // to infect all humans into zombies
   function zombieInfection(grid)
   {

     // Queue to store coordinates for BFS
     let q = [];

     // Number of rows
     let n = grid.length;

     // Number of columns
     let m = grid[0].length;

     let cur = 0, next = 0;

     // Initially pushing coordinates of all the
     // zombies into the queue
     for (let i = 0; i < n; i++) {
       for (let j = 0; j < m; j++) {

         // If cell is zombie
         if (grid[i][j] == 1) {
           q.push({ first: i, second: j });
           cur++;
         }
       }
     }

     // To keep track of the time
     let t = 0;

     // While any zombie is left
     while (q.length != 0) {
       for (let i = 0; i < cur; i++) {
         let use = q[0];
         q.shift();
         let x = use.first, y = use.second;

         // Checking for all the four directons
         // horizontally and vertically
         if (isValid(x + 1, y, n, m)
           && grid[x + 1][y] == 0) {
           grid[x + 1][y] = 1;
           q.push({ first: x + 1, second: y });
           next++;
         }
         if (isValid(x - 1, y, n, m)
           && grid[x - 1][y] == 0) {
           grid[x - 1][y] = 1;
           q.push({ first: x - 1, second: y });
           next++;
         }
         if (isValid(x, y + 1, n, m)
           && grid[x][y + 1] == 0) {
           grid[x][y + 1] = 1;
           q.push({ first: x, second: y + 1 });
           next++;
         }
         if (isValid(x, y - 1, n, m)
           && grid[x][y - 1] == 0) {
           grid[x][y - 1] = 1;
           q.push({ first: x, second: y - 1 });
           next++;
         }
       }
       if (next == 0)
         break;
       cur = next;
       next = 0;

       // Increment time
       t++;
     }

     // If no zombie was there in the grid
     // Then it is not possible to convert all
     // the humans to zombie so return -1
     for (let i = 0; i < n; i++)
       for (let j = 0; j < m; j++)
         if (grid[i][j] == 0)
           return -1;

     // Return the total time elapsed
     return t;
   }

   // Driver Code

   let N = 3, M = 4;

   // Given grid
   let grid = [[0, 1, 0, 1],
   [0, 0, 0, 0],
   [0, 0, 0, 1]];

   // Function Call
   document.write(zombieInfection(grid));

 // This code is contributed by Potta Lokesh
 </script>
```

**Output**

```
3
```

**时间复杂度:**O(N * M)
T3】辅助空间: O(N*M)