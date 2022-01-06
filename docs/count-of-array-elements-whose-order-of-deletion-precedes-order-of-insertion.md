# 删除顺序先于插入顺序的数组元素的计数

> 原文:[https://www . geesforgeks . org/数组元素计数-其删除顺序在插入顺序之前/](https://www.geeksforgeeks.org/count-of-array-elements-whose-order-of-deletion-precedes-order-of-insertion/)

给定一个初始数组 **A[]** 和一个最终数组 **B[]** ,两个数组的大小均为 **N** ,包含范围为**【1，N】**的整数，其中 **A[]** 表示元素插入的顺序， **B[]** 表示移除元素的顺序，任务是找出位于比其在 **A 中的相应位置更早的索引处的 **B[]** 中的元素数量**

**示例:**

> **输入:** A[ ] = {1，2，4，3}，B[ ] = {2，3，4，1}
> **输出:** 3
> **解释:**
> 元素 2 在 1 之后插入，但在 1 之前移除。
> 元素 3 在 4 之后插入，但在 4 之前移除。
> 元素 4 在 1 之后插入，但在 1 之前移除。
> 因此，总共有 3 个元素向前移动。
> 
> **输入:** A[ ] = {1，2，3，4} B[ ] = {1，2，4，3}
> **输出:** 1
> **解释:**
> 元素 4 在 3 之后插入，但在 3 之前移除。
> 因此，只有 1 个元素前进。

**天真的做法:**解决这个问题最简单的方法就是将**B【】**中每个元素的位置与**A【】**中每个其他元素的位置进行比较，检查它是否插入在**A【】**中的某个元素之后，但之前在**B【】**中被移除。如果是，则增加计数。最后，打印总计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**解决这个问题的更好方法是维护一个队列，将 **B[]** 的元素插入到这个[队列](https://www.geeksforgeeks.org/queue-data-structure/)中，同时将所有元素插入到一个[无序集合](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)中。无序集用于有效检查特定元素是否已被处理。遍历 **A[]** 并从队列中弹出元素，直到当前元素 **A[i]** 出现在队列顶部，同时不断增加计数并将出现在队列顶部的元素标记为已处理。最后，总计数将给出在 **B[]** 中向前移动的元素数量。

按照以下步骤解决问题:

*   维护一个 [**队列**](https://www.geeksforgeeks.org/queue-data-structure/) 和**无序集**，并在两者中存储数组 **B[]** 的值。
*   现在，迭代数组 **A[]** 。
*   如果当前元素不在无序集中，则意味着它已经被移除。
*   初始化变量**计数**。如果在队列中没有找到任何第 **i <sup>第</sup>T5】个元素，则从队列中移除所有在**A【I】**之前存在于队列中的元素，并且无序集继续增加**计数**。**
*   从队列和无序集中删除 **A[i]** 。
*   最后，打印总计**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function returns maximum number
// of required elements
int maximumCount(int A[], int B[], int n)
{

    queue<int> q;
    unordered_set<int> s;

    // Insert the elements of array B
    // in the queue and set
    for (int i = 0; i < n; i++) {

        s.insert(B[i]);
        q.push(B[i]);
    }

    // Stores the answer
    int count = 0;

    for (int i = 0; i < n; i++) {

        // If A[i] is already processed
        if (s.find(A[i]) == s.end())
            continue;

        // Until we find A[i] in the queue
        while (!q.empty() && q.front() != A[i]) {

            // Remove elements from the queue
            s.erase(q.front());
            q.pop();

            // Increment the count
            count++;
        }

        // Remove the current element A[i]
        // from the queue and set.
        if (A[i] == q.front()) {

            q.pop();
            s.erase(A[i]);
        }

        if (q.empty())
            break;
    }

    // Return total count
    cout << count << endl;
}

// Driver Code
int main()
{
    int N = 4;
    int A[] = { 1, 2, 3, 4 };
    int B[] = { 1, 2, 4, 3 };

    maximumCount(A, B, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function returns maximum number
// of required elements
static void maximumCount(int A[], int B[], int n)
{
    Queue<Integer> q = new LinkedList<>();
    HashSet<Integer> s = new HashSet<>();

    // Insert the elements of array B
    // in the queue and set
    for(int i = 0; i < n; i++)
    {
        s.add(B[i]);
        q.add(B[i]);
    }

    // Stores the answer
    int count = 0;

    for(int i = 0; i < n; i++)
    {

        // If A[i] is already processed
        if (!s.contains(A[i]))
            continue;

        // Until we find A[i] in the queue
        while (!q.isEmpty() && q.peek() != A[i])
        {

            // Remove elements from the queue
            s.remove(q.peek());
            q.remove();

            // Increment the count
            count++;
        }

        // Remove the current element A[i]
        // from the queue and set.
        if (A[i] == q.peek())
        {
            q.remove();
            s.remove(A[i]);
        }

        if (q.isEmpty())
            break;
    }

    // Return total count
    System.out.print(count + "\n");
}

// Driver Code
public static void main(String[] args)
{
    int N = 4;
    int A[] = { 1, 2, 3, 4 };
    int B[] = { 1, 2, 4, 3 };

    maximumCount(A, B, N);
}
}

// This code is contributed by princi singh
```

## 蟒蛇 3

```
# Python3 Program to implement
# the above approach
import queue

# Function returns maximum number
# of required elements
def maximumCount(A, B, n):

    q = queue.Queue() 
    s = set()

    # Insert the elements of
    # array B in the queue
    # and set
    for i in range(n):
        s.add(B[i])
        q.put(B[i])

    # Stores the answer
    count = 0

    for i in range(n):

        # If A[i] is already
        # processed
        if (A[i] not in s):
            continue

        # Until we find A[i]
        # in the queue
        while (q.qsize() > 0 and
               q.queue[0] != A[i]):

            # Remove elements from
            # the queue
            s.remove(q.queue[0]);
            q.get()

            # Increment the count
            count += 1

        # Remove the current element A[i]
        # from the queue and set.
        if (A[i] == q.queue[0]):
            q.get()
            s.remove(A[i])

        if (q.qsize() == 0):
            break

    # Return total count
    print(count)

# Driver code
N = 4
A = [1, 2, 3, 4]
B = [1, 2, 4, 3]
maximumCount(A, B, N)

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function returns maximum number
// of required elements
static void maximumCount(int []A, int []B, int n)
{
    Queue<int> q = new Queue<int>();
    HashSet<int> s = new HashSet<int>();

    // Insert the elements of array B
    // in the queue and set
    for(int i = 0; i < n; i++)
    {
        s.Add(B[i]);
        q.Enqueue(B[i]);
    }

    // Stores the answer
    int count = 0;

    for(int i = 0; i < n; i++)
    {

        // If A[i] is already processed
        if (!s.Contains(A[i]))
            continue;

        // Until we find A[i] in the queue
        while (q.Count != 0 && q.Peek() != A[i])
        {

            // Remove elements from the queue
            s.Remove(q.Peek());
            q.Dequeue();

            // Increment the count
            count++;
        }

        // Remove the current element A[i]
        // from the queue and set.
        if (A[i] == q.Peek())
        {
            q.Dequeue();
            s.Remove(A[i]);
        }
        if (q.Count == 0)
            break;
    }

    // Return total count
    Console.Write(count + "\n");
}

// Driver Code
public static void Main(String[] args)
{
    int N = 4;
    int []A = { 1, 2, 3, 4 };
    int []B = { 1, 2, 4, 3 };

    maximumCount(A, B, N);
}
}

// This code is contributed by princi singh
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function returns maximum number
// of required elements
function maximumCount(A, B, n)
{

    var q = [];
    var s = new Set();

    // Insert the elements of array B
    // in the queue and set
    for (var i = 0; i < n; i++) {

        s.add(B[i]);
        q.push(B[i]);
    }

    // Stores the answer
    var count = 0;

    for (var i = 0; i < n; i++) {

        // If A[i] is already processed
        if (s.has(A[i]))
        {

        // Until we find A[i] in the queue
        while(q.length!=0 && q[0] != A[i]) {

            // Remove elements from the queue
            s.delete(q[0]);
            q.shift();

            // Increment the count
            count++;
        }

        // Remove the current element A[i]
        // from the queue and set.
        if (A[i] == q[0]) {

            q.shift();
            s.delete(A[i]);
        }

        if (q.length==0)
            break;
        }
    }

    // Return total count
    document.write( count );
}

// Driver Code
var N = 4;
var A = [1, 2, 3, 4];
var B = [1, 2, 4, 3];
maximumCount(A, B, N);

</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)