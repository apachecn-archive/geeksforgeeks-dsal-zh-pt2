# 使用给定的操作最小化移动，将 N 减少到 0

> 原文:[https://www . geesforgeks . org/minimum-moves-reduce-n-to-0-使用给定操作/](https://www.geeksforgeeks.org/minimise-moves-to-reduce-n-to-0-using-given-operations/)

给定一个数字 **N、**和一些可以执行的操作，任务是找到最小的移动次数，将 **N** 转换为 0。在一次移动操作中，可以执行以下操作之一:

*   将 N 的值增加或减少 1。
*   将 N 的值乘以-1。
*   如果 N 为偶数，则将 N 的值除以 2。
*   如果 N 是一个完美的正方形，将 N 的值减少到√N。

**示例:**

> **输入:** N = 50
> **输出:** 6
> **说明:**执行的招式为:50(/2)-(T8)25(√)-(T9)5(-1)-(T10)4(/2)-(T11)2(-1)-(T12)1(-1)-(T13)0。因此，所需的移动次数是 6 次，这是可能的最小值。
> 
> **输入:**N = 75
> T3】输出: 8

**方法:**利用动态规划可以有效地解决给定的问题。想法是在 0 上使用[散列](http://www.geeksforgeeks.org/hashing-data-structure/)和[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，直到到达 **N** 。使用散列法是为了同一号码不会被访问两次。可以遵循以下步骤来解决问题:

*   使用 BFS，将从 0 到的所有可能的数字添加到队列和散列表中，这样它们就不会被再次访问
*   返回到达 **N** 后计算的移动次数。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

    class Node {
     public:
        int val, moves;

        // Constructor
        Node(int v, int m)
        {

            val = v;
            moves = m;
        }
    };

    // Function to calculate
    // minimum number of moves
    // required to convert N to 0
    int minMoves(int N)
    {

        // Initialize a hashset
        // to mark the visited numbers
        set<int> set;

        // Initialize a queue
        queue<Node*> q ;

        // Mark 0 as visited
        set.insert(0);

        // Add 0 into the queue
        q.push(new Node(0, 0));

        // while N is not reached
        while (!q.empty()) {

            // poll out current node
            Node *curr = q.front();
            q.pop();

            // If N is reached
            if (curr->val == N) {

                // Return the number of moves used
                return curr->moves;
            }

            if (set.find(curr->val - 1)==set.end()) {

                // Mark the number as visited
                set.insert(curr->val - 1);

                // Add the number in the queue
                q.push(new Node(curr->val - 1,
                               curr->moves + 1));
            }
            if (set.find(curr->val + 1)==set.end()) {

                // Mark the number as visited
                set.insert(curr->val + 1);

                // Add the number in the queue
                q.push(new Node(curr->val + 1,
                               curr->moves + 1));
            }
            if (set.find(curr->val * 2)==set.end()) {

                // Mark the number as visited
                set.insert(curr->val * 2);

                // Add the number in the queue
                q.push(new Node(curr->val * 2,
                               curr->moves + 1));
            }
            int sqr = curr->val * curr->val;
            if (set.find(sqr)==set.end()) {

                // Mark the number as visited
                set.insert(sqr);

                // Add the number in the queue
                q.push(new Node(sqr,
                               curr->moves + 1));
            }
            if (set.find(-curr->val)==set.end()) {

                // Mark the number as visited
                set.insert(-curr->val);

                // Add the number in the queue
                q.push(new Node(-curr->val,
                               curr->moves + 1));
            }
        }

        return -1;
    }

    // Driver code
     int main()
    {

        int N = 50;

        // Call the function
        // and print the answer
        cout<<(minMoves(N));
    }

// This code is contributed by Potta Lokesh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach

import java.io.*;
import java.util.*;

class GFG {

    static class Node {

        int val, moves;

        // Constructor
        public Node(int val, int moves)
        {

            this.val = val;
            this.moves = moves;
        }
    }

    // Function to calculate
    // minimum number of moves
    // required to convert N to 0
    public static int minMoves(int N)
    {

        // Initialize a hashset
        // to mark the visited numbers
        Set<Integer> set = new HashSet<>();

        // Initialize a queue
        Queue<Node> q = new LinkedList<>();

        // Mark 0 as visited
        set.add(0);

        // Add 0 into the queue
        q.add(new Node(0, 0));

        // while N is not reached
        while (!q.isEmpty()) {

            // poll out current node
            Node curr = q.poll();

            // If N is reached
            if (curr.val == N) {

                // Return the number of moves used
                return curr.moves;
            }

            if (!set.contains(curr.val - 1)) {

                // Mark the number as visited
                set.add(curr.val - 1);

                // Add the number in the queue
                q.add(new Node(curr.val - 1,
                               curr.moves + 1));
            }
            if (!set.contains(curr.val + 1)) {

                // Mark the number as visited
                set.add(curr.val + 1);

                // Add the number in the queue
                q.add(new Node(curr.val + 1,
                               curr.moves + 1));
            }
            if (!set.contains(curr.val * 2)) {

                // Mark the number as visited
                set.add(curr.val * 2);

                // Add the number in the queue
                q.add(new Node(curr.val * 2,
                               curr.moves + 1));
            }
            int sqr = curr.val * curr.val;
            if (!set.contains(sqr)) {

                // Mark the number as visited
                set.add(sqr);

                // Add the number in the queue
                q.add(new Node(sqr,
                               curr.moves + 1));
            }
            if (!set.contains(-curr.val)) {

                // Mark the number as visited
                set.add(-curr.val);

                // Add the number in the queue
                q.add(new Node(-curr.val,
                               curr.moves + 1));
            }
        }

        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {

        int N = 50;

        // Call the function
        // and print the answer
        System.out.println(minMoves(N));
    }
}
```

## 蟒蛇 3

```
# Python code for the above approach
from queue import Queue

class Node:

    # Constructor
    def __init__(self, v, m):
        self.val = v
        self.moves = m

# Function to calculate
# minimum number of moves
# required to convert N to 0
def minMoves(N):

    # Initialize a hashset
    # to mark the visited numbers
    _set = set()

    # Initialize a queue
    q = Queue()

    # Mark 0 as visited
    _set.add(0)

    # Add 0 into the queue
    q.put(Node(0, 0))

    # while N is not reached
    while (q.qsize):

        # poll out current node
        curr = q.queue[0]
        q.get()

        # If N is reached
        if (curr.val == N):

            # Return the number of moves used
            return curr.moves

        if (not (curr.val - 1) in _set):

            # Mark the number as visited
            _set.add(curr.val - 1)

            # Add the number in the queue
            q.put(Node(curr.val - 1, curr.moves + 1))

        if (not (curr.val + 1) in _set):

            # Mark the number as visited
            _set.add(curr.val + 1)

            # Add the number in the queue
            q.put(Node(curr.val + 1, curr.moves + 1))

        if (not (curr.val * 2) in _set):

            # Mark the number as visited
            _set.add(curr.val * 2)

            # Add the number in the queue
            q.put(Node(curr.val * 2, curr.moves + 1))

        sqr = curr.val * curr.val
        if (not sqr in _set):

            # Mark the number as visited
            _set.add(sqr)

            # Add the number in the queue
            q.put(Node(sqr, curr.moves + 1))

        if (not (-curr.val) in _set):

            # Mark the number as visited
            _set.add(-curr.val)

            # Add the number in the queue
            q.put(Node(-curr.val, curr.moves + 1))

    return -1

# Driver code
N = 50

# Call the function
# and print the answer
print((minMoves(N)))

# This code is contributed by gfgking
```

## java 描述语言

```
<script>
// Javascript code for the above approach
class Node {

  // Constructor
  constructor(v, m) {

    this.val = v;
    this.moves = m;
  }
};

// Function to calculate
// minimum number of moves
// required to convert N to 0
function minMoves(N) {

  // Initialize a hashset
  // to mark the visited numbers
  let set = new Set();

  // Initialize a queue
  let q = [];

  // Mark 0 as visited
  set.add(0);

  // Add 0 into the queue
  q.unshift(new Node(0, 0));

  // while N is not reached
  while (q.length) {

    // poll out current node
    let curr = q[q.length - 1];
    q.pop();

    // If N is reached
    if (curr.val == N) {

      // Return the number of moves used
      return curr.moves;
    }

    if (!set.has(curr.val - 1)) {

      // Mark the number as visited
      set.add(curr.val - 1);

      // Add the number in the queue
      q.unshift(new Node(curr.val - 1,
        curr.moves + 1));
    }
    if (!set.has(curr.val + 1)) {

      // Mark the number as visited
      set.add(curr.val + 1);

      // Add the number in the queue
      q.unshift(new Node(curr.val + 1,
        curr.moves + 1));
    }
    if (!set.has(curr.val * 2)) {

      // Mark the number as visited
      set.add(curr.val * 2);

      // Add the number in the queue
      q.unshift(new Node(curr.val * 2,
        curr.moves + 1));
    }
    let sqr = curr.val * curr.val;
    if (!set.has(sqr)) {

      // Mark the number as visited
      set.add(sqr);

      // Add the number in the queue
      q.unshift(new Node(sqr,
        curr.moves + 1));
    }
    if (!set.has(-curr.val)) {

      // Mark the number as visited
      set.add(-curr.val);

      // Add the number in the queue
      q.unshift(new Node(-curr.val,
        curr.moves + 1));
    }
  }

  return -1;
}

// Driver code
let N = 50;

// Call the function
// and print the answer
document.write((minMoves(N)));

// This code is contributed by gfgking
</script>
```

**Output**

```
6
```

***时间复杂度:** O(log N)*
***辅助空间:** O(K*log N)，其中 K 是允许的可能操作*