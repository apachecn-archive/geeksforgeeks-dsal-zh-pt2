# 计算向前或向后移动给定步数可以到达的唯一楼梯

> 原文:[https://www . geesforgeks . org/count-unique-通过向前或向后移动给定步数可以到达的楼梯/](https://www.geeksforgeeks.org/count-unique-stairs-that-can-be-reached-by-moving-given-number-of-steps-forward-or-backward/)

给定一个整数 **N** ，代表楼梯的数量，从 **1** 到 **N** 取值，以及一个起始位置 **S** ，任务是通过精确地移动 **A** 或 **B** 楼梯从任何位置向前或向后步进任何次数来计算可以到达的唯一楼梯的最大数量。

**示例:**

> **输入:** N = 10，S = 2，A = 5，B = 7
> **输出:** 4
> **说明:**
> 起始位置 S:楼梯 2
> 从楼梯 2 出发，有可能到达楼梯 7，即(S + A)，9，即(S + B)。
> 从 9 号楼梯可以到达 4 号楼梯，即(S–A)。
> 因此，唯一可到达的楼梯数量为 4 {2，4，7，9}。
> 
> **输入:** N = 10，S = 2，A = 3，B = 4
> T3】输出: 10

**方法:**给定的问题可以使用 [BFS 遍历](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)技术来解决。按照以下步骤解决问题:

*   初始化一个[队列](https://www.geeksforgeeks.org/queue-data-structure/)和一个大小为 **(N + 1)** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**，并将其初始化为**假**。**
*   **将起始节点 **S** 标记为已访问，即**vis【S】**标记为 **1** 。将 **S** 推入[队列](https://www.geeksforgeeks.org/queue-data-structure/) **Q** 。**
*   **现在[迭代直到 **Q** 不为空](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)并执行以下步骤:

    *   [弹出队列的前元素](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)并将其存储在变量中，比如 **currStair** 。
    *   考虑从 **currStair，**开始的所有 4 种可能的移动类型，即 **{+A，-A，+B，-B}** 。
    *   对于每一个新的楼梯，检查它是否是一个有效的和未访问的楼梯。如果发现是真的，那么[将其推入**Q**T3**。**将楼梯标记为已参观。否则，](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)[继续](https://www.geeksforgeeks.org/continue-statement-cpp/)。** 
*   **最后，使用数组**vis【】**统计到访楼梯的数量。**
*   **完成上述步骤后，打印已访问楼梯的数量作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number
// of unique stairs visited
void countStairs(int n, int x, int a, int b)
{
    // Checks whether the current
    // stair is visited or not
    int vis[n + 1] = { 0 };

    // Store the possible moves
    // from the current position
    int moves[] = { +a, -a, +b, -b };

    // Initialize a queue
    queue<int> q;

    /// Push the starting position
    q.push(x);

    // Mark the starting
    // position S as visited
    vis[x] = 1;

    // Iterate until queue is not empty
    while (!q.empty()) {

        // Store the current stair number
        int currentStair = q.front();

        // Pop it from the queue
        q.pop();

        // Check for all possible moves
        // from the current stair
        for (int j = 0; j < 4; j++) {

            // Store the new stair number
            int newStair = currentStair + moves[j];

            // If it is valid and unvisited
            if (newStair > 0 && newStair <= n
                && !vis[newStair]) {

                // Push it into queue
                q.push(newStair);

                // Mark the stair as visited
                vis[newStair] = 1;
            }
        }
    }

    // Store the result
    int cnt = 0;

    // Count the all visited stairs
    for (int i = 1; i <= n; i++)
        if (vis[i] == 1)
            cnt++;

    // Print the result
    cout << cnt;
}

// Driver Code
int main()
{
    int N = 10, S = 2, A = 5, B = 7;
    countStairs(N, S, A, B);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.LinkedList;
import java.util.Queue;

class GFG{

// Function to count the number
// of unique stairs visited
static void countStairs(int n, int x, int a, int b)
{

    // Checks whether the current
    // stair is visited or not
    int[] vis = new int[n + 1];

    // Store the possible moves
    // from the current position
    int[] moves = { +a, -a, +b, -b };

    // Initialize a queue
    Queue<Integer> q = new LinkedList<Integer>();

    /// Push the starting position
    q.add(x);

    // Mark the starting
    // position S as visited
    vis[x] = 1;

    // Iterate until queue is not empty
    while (!q.isEmpty())
    {

        // Store the current stair number
        int currentStair = q.peek();

        // Pop it from the queue
        q.remove();

        // Check for all possible moves
        // from the current stair
        for(int j = 0; j < 4; j++)
        {

            // Store the new stair number
            int newStair = currentStair + moves[j];

            // If it is valid and unvisited
            if (newStair > 0 && newStair <= n &&
                            vis[newStair] == 0)
            {

                // Push it into queue
                q.add(newStair);

                // Mark the stair as visited
                vis[newStair] = 1;
            }
        }
    }

    // Store the result
    int cnt = 0;

    // Count the all visited stairs
    for(int i = 1; i <= n; i++)
        if (vis[i] == 1)
            cnt++;

    // Print the result
    System.out.print(cnt);
}

// Driver Code
public static void main(String args[])
{
    int N = 10, S = 2, A = 5, B = 7;

    countStairs(N, S, A, B);
}
}

// This code is contributed by abhinavjain194
```

## **蟒蛇 3**

```
# Python3 program for the above approach
from collections import deque

# Function to count the number
# of unique stairs visited
def countStairs(n, x, a, b):

    # Checks whether the current
    # stair is visited or not
    vis = [0] * (n + 1)

    # Store the possible moves
    # from the current position
    moves = [+a, -a, +b, -b]

    # Initialize a queue
    q = deque()

    # Push the starting position
    q.append(x)

    # Mark the starting
    # position S as visited
    vis[x] = 1

    # Iterate until queue is not empty
    while (len(q) > 0):

        # Store the current stair number
        currentStair = q.popleft()

        # Pop it from the queue
        # q.pop()

        # Check for all possible moves
        # from the current stair
        for j in range(4):

            # Store the new stair number
            newStair = currentStair + moves[j]

            # If it is valid and unvisited
            if (newStair > 0 and newStair <= n and
               (not vis[newStair])):
                # Push it into queue
                q.append(newStair)

                # Mark the stair as visited
                vis[newStair] = 1

    # Store the result
    cnt = 0

    # Count the all visited stairs
    for i in range(1, n + 1):
        if (vis[i] == 1):
            cnt += 1

    # Print the result
    print (cnt)

# Driver Code
if __name__ == '__main__':

    N, S, A, B = 10, 2, 5, 7

    countStairs(N, S, A, B)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number
// of unique stairs visited
static void countStairs(int n, int x,
                        int a, int b)
{

    // Checks whether the current
    // stair is visited or not
    int []vis = new int[n + 1];
    Array.Clear(vis, 0, vis.Length);

    // Store the possible moves
    // from the current position
    int []moves = { +a, -a, +b, -b };

    // Initialize a queue
    Queue<int> q = new Queue<int>();

    /// Push the starting position
    q.Enqueue(x);

    // Mark the starting
    // position S as visited
    vis[x] = 1;

    // Iterate until queue is not empty
    while (q.Count > 0)
    {

        // Store the current stair number
        int currentStair = q.Peek();

        // Pop it from the queue
        q.Dequeue();

        // Check for all possible moves
        // from the current stair
        for(int j = 0; j < 4; j++)
        {

            // Store the new stair number
            int newStair = currentStair + moves[j];

            // If it is valid and unvisited
            if (newStair > 0 && newStair <= n &&
                            vis[newStair] == 0)
            {

                // Push it into queue
                q.Enqueue(newStair);

                // Mark the stair as visited
                vis[newStair] = 1;
            }
        }
    }

    // Store the result
    int cnt = 0;

    // Count the all visited stairs
    for(int i = 1; i <= n; i++)
        if (vis[i] == 1)
            cnt++;

    // Print the result
    Console.WriteLine(cnt);
}

// Driver Code
public static void Main()
{
    int N = 10, S = 2, A = 5, B = 7;

    countStairs(N, S, A, B);
}
}

// This code is contributed by ipg2016107
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

// Function to count the number
// of unique stairs visited
function countStairs(n, x, a, b)
{
    // Checks whether the current
    // stair is visited or not
    var vis = Array(n+1).fill(0);

    // Store the possible moves
    // from the current position
    var moves = [ +a, -a, +b, -b ];

    // Initialize a queue
    var q = [];

    /// Push the starting position
    q.push(x);

    // Mark the starting
    // position S as visited
    vis[x] = 1;

    // Iterate until queue is not empty
    while (q.length!=0) {

        // Store the current stair number
        var currentStair = q[0];

        // Pop it from the queue
        q.shift();

        // Check for all possible moves
        // from the current stair
        for (var j = 0; j < 4; j++) {

            // Store the new stair number
            var newStair = currentStair + moves[j];

            // If it is valid and unvisited
            if (newStair > 0 && newStair <= n
                && !vis[newStair]) {

                // Push it into queue
                q.push(newStair);

                // Mark the stair as visited
                vis[newStair] = 1;
            }
        }
    }

    // Store the result
    var cnt = 0;

    // Count the all visited stairs
    for (var i = 1; i <= n; i++)
        if (vis[i] == 1)
            cnt++;

    // Print the result
    document.write( cnt);
}

// Driver Code
var N = 10, S = 2, A = 5, B = 7;
countStairs(N, S, A, B);

</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**