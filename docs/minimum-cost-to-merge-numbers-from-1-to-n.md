# 从 1 到 N 合并数字的最小成本

> 原文:[https://www . geesforgeks . org/最小合并成本-数字-从-1 到-n/](https://www.geeksforgeeks.org/minimum-cost-to-merge-numbers-from-1-to-n/)

给定一个整数 **N** ，任务是找到**最小成本**来合并从 **1** 到 **N** 的所有数字，其中合并两组数字 A 和 B 的成本等于相应组中数字乘积的乘积。

**示例:**

> **输入:** N = 4
> **输出:** 32
> 合并{1}和{2}成本 1 * 2 = 2
> 合并{1，2}和{3}成本 2 * 3 = 6
> 合并{1，2，3}和{4}成本 6 * 4 = 24
> 因此，最小成本为 2 + 6 + 24 = 32
> 
> **输入:**N = 2
> T3】输出: 2

**进场:**

*   我们脑海中出现的第一个方法是[排序](https://www.geeksforgeeks.org/sorting-algorithms/)。我们取前两个**最小的**元素并添加它们，然后继续添加排序数组中的其余元素。但是当当前运行总和超过下一个数组中的下一个最小值时，它**失败。**

```
Take N = 5,
If we take the sorting approach, then-
Merge {1} and {2} - 1 * 2 = 2
Merge {1, 2} and {3} - 2 * 3 = 6
Merge{1, 2, 3} and {4} - 6 * 4 = 24
Merge{1, 2, 3, 4} and {5} - 24 * 5 = 120
Total sum = 152
```

```
But optimal way is,
Merge {1} and {2} - 1 * 2 = 2
Merge {1, 2} and {3} - 2 * 3 = 6
Merge {4} and {5} - 4 * 5 = 20
Merge {1, 2, 3} and {4, 5} - 6 * 20 = 120
Total sum = 148
This is the minimal answer.
```

*   所以，**解决这个问题的正确方法**是基于[的](https://www.geeksforgeeks.org/binary-heap/)方法。最初，我们将所有从 **1** 到 **N** 的数字推入最小堆。
*   在每次迭代中，我们从最小堆中提取**最小值**和**第二最小值**元素，并将它们的产品插入其中。这确保了产生的附加成本将是**最小的**。
*   我们继续重复上述步骤，直到最小堆中只剩下一个元素。在那之前计算出来的总数给了我们所需要的答案。

下面是上述方法的实现:

## C++

```
// C++ program to find the Minimum
// cost to merge numbers
// from 1 to N.
#include <bits/stdc++.h>
using namespace std;

// Function returns the
// minimum cost
int GetMinCost(int N)
{

    // Min Heap representation
    priority_queue<int, vector<int>,
                   greater<int> > pq;

    // Add all elements to heap
    for (int i = 1; i <= N; i++) {
        pq.push(i);
    }

    int cost = 0;

    while (pq.size() > 1)
    {
        // First minimum
        int mini = pq.top();
        pq.pop();

        // Second minimum
        int secondmini = pq.top();
        pq.pop();

        // Multiply them
        int current = mini * secondmini;

        // Add to the cost
        cost += current;

        // Push the product into the
        // heap again
        pq.push(current);
    }

    // Return the optimal cost
    return cost;
}

// Driver code
int main()
{
    int N = 5;
    cout << GetMinCost(N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

// Function returns the
// minimum cost
static int GetMinCost(int N)
{

    // Min Heap representation
    PriorityQueue<Integer> pq;
    pq = new PriorityQueue<>();

    // Add all elements to heap
    for(int i = 1; i <= N; i++)
    {
       pq.add(i);
    }

    int cost = 0;

    while (pq.size() > 1)
    {

        // First minimum
        int mini = pq.remove();

        // Second minimum
        int secondmini = pq.remove();

        // Multiply them
        int current = mini * secondmini;

        // Add to the cost
        cost += current;

        // Push the product into the
        // heap again
        pq.add(current);
    }

    // Return the optimal cost
    return cost;
}

// Driver Code
public static void main(String args[])
{
    int N = 5;

    // Function call
    System.out.println(GetMinCost(N));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# python3 program to find the Minimum
# cost to merge numbers
# from 1 to N.

# Function returns the
# minimum cost
def GetMinCost(N):

    # Min Heap representation
    pq = []

    # Add all elements to heap
    for i in range(1, N+1, 1):
        pq.append(i)

    pq.sort(reverse = False)

    cost = 0

    while (len(pq) > 1):

        # First minimum
        mini = pq[0]
        pq.remove(pq[0])

        # Second minimum
        secondmini = pq[0]
        pq.remove(pq[0])

        # Multiply them
        current = mini * secondmini

        # Add to the cost
        cost += current

        # Push the product into the
        # heap again
        pq.append(current)
        pq.sort(reverse = False)

    # Return the optimal cost
    return cost

# Driver code
if __name__ == '__main__':

    N = 5
    print(GetMinCost(N))

# This code is contributed by Bhupendra_Singh
```

## C#

```
// C# program to find the Minimum 
// cost to merge numbers 
// from 1 to N.
using System;
using System.Collections.Generic;

class GFG{

// Function returns the 
// minimum cost
static int GetMinCost(int N)
{

    // Min Heap representation
    List<int> pq = new List<int>();

    // Add all elements to heap
    for(int i = 1; i <= N; i++)
    {
        pq.Add(i);
    }

    int cost = 0;
    pq.Sort();

    while (pq.Count > 1)
    {

        // First minimum
        int mini = pq[0];
        pq.RemoveAt(0);

        // Second minimum
        int secondmini = pq[0];
        pq.RemoveAt(0);

        // Multiply them
        int current = mini * secondmini;

        // Add to the cost
        cost += current;

        // Push the product into the
        // heap again
        pq.Add(current);
        pq.Sort();
    }

    // Return the optimal cost
    return cost;
}

// Driver code
static void Main()
{
    int N = 5;

    Console.WriteLine(GetMinCost(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    // Function returns the
    // minimum cost
    function GetMinCost(N)
    {

        // Min Heap representation
        let pq = [];

        // Add all elements to heap
        for(let i = 1; i <= N; i++)
        {
           pq.push(i);
        }
        pq.sort(function(a, b){return a - b});

        let cost = 0;

        while (pq.length > 1)
        {

            // First minimum
            let mini = pq[0];
            pq.shift();

            // Second minimum
            let secondmini = pq[0];
            pq.shift();

            // Multiply them
            let current = mini * secondmini;

            // Add to the cost
            cost += current;

            // Push the product into the
            // heap again
            pq.push(current);
            pq.sort(function(a, b){return a - b});
        }

        // Return the optimal cost
        return cost;
    }

    let N = 5;

    // Function call
    document.write(GetMinCost(N));

  // This code is contributed by decode2207.
</script>
```

**Output:** 

```
148
```

**时间复杂度:***O(NlogN)*
T5】辅助空间: *O(N)*