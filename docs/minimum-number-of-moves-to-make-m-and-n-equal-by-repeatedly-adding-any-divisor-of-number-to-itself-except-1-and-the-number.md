# 通过重复将除 1 以外的任何除数与数字

相加，使 M 和 N 相等的最小移动次数

> 原文:[https://www . geeksforgeeks . org/最小移动次数通过重复将任意除数加到除 1 和数之外的自身上来使 m 和 n 相等/](https://www.geeksforgeeks.org/minimum-number-of-moves-to-make-m-and-n-equal-by-repeatedly-adding-any-divisor-of-number-to-itself-except-1-and-the-number/)

给定两个数字 **N** 和 **M，**任务是找到最小的移动次数，如果不可能的话把 **N** 改成 **M** 或者 **-1** 。在一次移动中，将任何不等于 1 的除数加到当前数和数本身。

**示例:**

> **输入:** N = 4，M = 24
> **输出:** 5
> **说明:**数字 24 可以从 4 开始用 5 个操作达到:4->6->8->12->18->24。
> 
> **输入:** N = 4，M = 576
> T3】输出: 14

**方法:**构建一个[图](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)，其中顶点是从 **N** 到 **M** 的数字，如果从 **v1** 只需要使用问题陈述中的一个操作就可以得到 **v2** ，那么从顶点 **v1** 到顶点 **v2** 之间就有一条[边](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)。为了解决这个问题，在这个图中找到从顶点 **N** 到顶点 **M** 的最短路径。这可以使用[广度优先搜索算法](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)来完成。按照以下步骤解决问题:

*   [初始化一个布尔数组](https://www.geeksforgeeks.org/a-boolean-array-puzzle/) **访问了[]** 来存储一个特定的数字是否被计数。
*   用值**假**填充布尔[数组](https://www.geeksforgeeks.org/array-data-structure/) **访问过的[]** 的所有指数，并将**访问过的【N】**的值设置为**真。**
*   [初始化一个队列对](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/) **q** 来存储访问的数量和完成的操作数量。
*   将[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{N，0}** 推入对对[队列 **q** 。](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)
*   [在一个范围](https://www.geeksforgeeks.org/different-types-of-range-based-for-loop-iterators-in-c/)内迭代，直到成对的[队列 **q** 不是空的](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)[。](https://www.geeksforgeeks.org/queueempty-queuesize-c-stl/)
    *   将变量 **aux** 初始化为[队列](https://www.geeksforgeeks.org/queue-data-structure/)的[前](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)T4 对 **q** 和 **cont** 的第一个值，作为[队列](https://www.geeksforgeeks.org/queue-data-structure/)**q**的[前](https://www.geeksforgeeks.org/queuefront-queueback-c-stl/)对的第二个值
    *   [从](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)[队列中弹出](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)最前面的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/)对对**问**
    *   如果 **aux** 等于 **M，**则返回 **cont 的值。**
    *   [在](https://www.geeksforgeeks.org/range-based-loop-c/)**【2】、辅助<sup>1/2</sup>**的范围内迭代，执行以下步骤。
        *   如果 **i** 是 **aux 的因子，**则采取以下步骤。
            *   如果 **aux+i** 小于等于 **M** ，**visitored【I+aux】**为 **false，**则将**visitored【aux+I】**的值设置为 **true** ，[将](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{aux+i，cont+1}** 推入到对 **q 的[队列中](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)**
            *   如果 **aux+aux/i** 小于等于 **M** ，**visitored【aux/I+aux】**为**假，**则将**visitored【aux+aux/I】**的值设置为**真**，[将](https://www.geeksforgeeks.org/queuepush-and-queuepop-in-cpp-stl/)的[对](https://www.geeksforgeeks.org/pair-in-cpp-stl/) **{aux+aux/i，cont+1}** 推入对的[队列](https://www.geeksforgeeks.org/queue-of-pairs-in-c-stl-with-examples/)
*   返回 **-1** ，因为不可能使 **N** 等于**m**

下面是上述方法的实现。

## C++

```
// C++ program for the above approach.
#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number
// of moves to make N and M equal.
int countOperations(int N, int M)
{
    // Array to maintain the numbers
    // included.
    bool visited[100001];
    fill(visited, visited + 100001, false);

    // pair of vertex, count
    queue<pair<int, int> > Q;
    Q.push(make_pair(N, 0));
    visited[N] = true;

    // run bfs from N
    while (!Q.empty()) {
        int aux = Q.front().first;
        int cont = Q.front().second;
        Q.pop();

        // if we reached goal
        if (aux == M)
            return cont;

        // Iterate in the range
        for (int i = 2; i * i <= aux; i++)
            // If i is a factor of aux
            if (aux % i == 0) {
                // If i is less than M-aux and
                // is not included earlier.
                if (aux + i <= M && !visited[aux + i]) {
                    Q.push(make_pair(aux + i, cont + 1));
                    visited[aux + i] = true;
                }
                // If aux/i is less than M-aux and
                // is not included earlier.
                if (aux + aux / i <= M
                    && !visited[aux + aux / i]) {
                    Q.push(
                        make_pair(aux + aux / i, cont + 1));
                    visited[aux + aux / i] = true;
                }
            }
    }

    // Not possible
    return -1;
}

// Driver Code
int main()
{

    int N = 4, M = 24;

    cout << countOperations(N, M);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.util.*;

class GFG{

static class pair<T, V>
{
    T first;
    V second;
}

static pair<Integer, Integer> make_pair(int f, int s)
{
    pair<Integer, Integer> p = new pair<>();
    p.first = f; p.second = s;
    return p;
}

// Function to find the minimum number
// of moves to make N and M equal.
static int countOperations(int N, int M)
{

    // Array to maintain the numbers
    // included.
    boolean[] visited = new boolean[100001];
    Arrays.fill(visited, false);

    // Pair of vertex, count
    Queue<pair<Integer, Integer>> Q = new LinkedList<>();
    Q.add(make_pair(N, 0));
    visited[N] = true;

    // Run bfs from N
    while (!Q.isEmpty())
    {
        int aux = Q.peek().first;
        int cont = Q.peek().second;
        Q.remove();

        // If we reached goal
        if (aux == M)
            return cont;

        // Iterate in the range
        for(int i = 2; i * i <= aux; i++)

            // If i is a factor of aux
            if (aux % i == 0)
            {

                // If i is less than M-aux and
                // is not included earlier.
                if (aux + i <= M && !visited[aux + i])
                {
                    Q.add(make_pair(aux + i, cont + 1));
                    visited[aux + i] = true;
                }

                // If aux/i is less than M-aux and
                // is not included earlier.
                if (aux + aux / i <= M &&
                    !visited[aux + aux / i])
                {
                    Q.add(make_pair(aux + aux / i,
                                   cont + 1));
                    visited[aux + aux / i] = true;
                }
            }
    }

    // Not possible
    return -1;
}

// Driver Code
public static void main(String[] args)
{
    int N = 4, M = 24;

    System.out.println(countOperations(N, M));
}
}

// This code is contributed by hritikrommie
```

## 蟒蛇 3

```
# Python3 program for the above approach.

# Function to find the minimum number
# of moves to make N and M equal.
def countOperations(N, M):

    # Array to maintain the numbers
    # included.
    visited = [False] * (100001)

    # Pair of vertex, count
    Q = []
    Q.append([N, 0])
    visited[N] = True

    # Run bfs from N
    while (len(Q) > 0):
        aux = Q[0][0]
        cont = Q[0][1]
        Q.pop(0)

        # If we reached goal
        if (aux == M):
            return cont

        # Iterate in the range
        i = 2

        while i * i <= aux:

            # If i is a factor of aux
            if (aux % i == 0):

                # If i is less than M-aux and
                # is not included earlier.
                if (aux + i <= M and not visited[aux + i]):
                    Q.append([aux + i, cont + 1])
                    visited[aux + i] = True

                # If aux/i is less than M-aux and
                # is not included earlier.
                if (aux + int(aux / i) <= M and not
                    visited[aux + int(aux / i)]):
                    Q.append([aux + int(aux / i), cont + 1])
                    visited[aux + int(aux / i)] = True

            i += 1

    # Not possible
    return -1

# Driver code
N, M = 4, 24

print(countOperations(N, M))

# This code is contributed by mukesh07
```

## C#

```
// C# program for the above approach.
using System;
using System.Collections;
class GFG
{

    // Function to find the minimum number
    // of moves to make N and M equal.
    static int countOperations(int N, int M)
    {
        // Array to maintain the numbers
        // included.
        bool[] visited = new bool[100001];

        // pair of vertex, count
        Queue Q = new Queue();
        Q.Enqueue(new Tuple<int, int>(N, 0));
        visited[N] = true;
        // run bfs from N
        while (Q.Count > 0) {
            int aux = ((Tuple<int,int>)(Q.Peek())).Item1;
            int cont = ((Tuple<int,int>)(Q.Peek())).Item2;
            Q.Dequeue();

            // if we reached goal
            if (aux == M)
                return cont;

            // Iterate in the range
            for (int i = 2; i * i <= aux; i++)

                // If i is a factor of aux
                if (aux % i == 0)
                {

                    // If i is less than M-aux and
                    // is not included earlier.
                    if (aux + i <= M && !visited[aux + i]) {
                        Q.Enqueue(new Tuple<int, int>(aux + i, cont + 1));
                        visited[aux + i] = true;
                    }

                    // If aux/i is less than M-aux and
                    // is not included earlier.
                    if (aux + aux / i <= M
                        && !visited[aux + aux / i]) {
                        Q.Enqueue(new Tuple<int, int>(aux + aux / i, cont + 1));
                        visited[aux + aux / i] = true;
                    }
                }
        }

        // Not possible
        return -1;
    }

  static void Main ()
  {
    int N = 4, M = 24;

    Console.WriteLine(countOperations(N, M));
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach.

    // Function to find the minimum number
    // of moves to make N and M equal.
    function countOperations(N, M)
    {

        // Array to maintain the numbers
        // included.
        let visited = new Array(100001);

        // pair of vertex, count
        let Q = [];
        Q.push([N, 0]);
        visited[N] = true;

        // run bfs from N
        while (Q.length > 0) {
            let aux = Q[0][0];
            let cont = Q[0][1];
            Q.shift();

            // if we reached goal
            if (aux == M)
                return cont;

            // Iterate in the range
            for (let i = 2; i * i <= aux; i++)

                // If i is a factor of aux
                if (aux % i == 0)
                {

                    // If i is less than M-aux and
                    // is not included earlier.
                    if (aux + i <= M && !visited[aux + i]) {
                        Q.push([aux + i, cont + 1]);
                        visited[aux + i] = true;
                    }

                    // If aux/i is less than M-aux and
                    // is not included earlier.
                    if (aux + parseInt(aux / i, 10) <= M
                        && !visited[aux + parseInt(aux / i, 10)]) {
                        Q.push([aux + parseInt(aux / i, 10), cont + 1]);
                        visited[aux + parseInt(aux / i, 10)] = true;
                    }
                }
        }

        // Not possible
        return -1;
    }

    let N = 4, M = 24;

    document.write(countOperations(N, M));

// This code is contributed by rameshtravel07.
</script>
```

**Output**

```
5
```

***时间复杂度:** O(N*sqrt(N))*
***辅助空间:** O(N)*