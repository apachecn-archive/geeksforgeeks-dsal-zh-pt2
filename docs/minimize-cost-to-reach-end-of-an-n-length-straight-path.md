# 最小化到达 N 长度直线路径末端的成本

> 原文:[https://www . geesforgeks . org/最小化到达 n 长度直线路径末端的成本/](https://www.geeksforgeeks.org/minimize-cost-to-reach-end-of-an-n-length-straight-path/)

给定整数 **K** 表示以 **1 升/地铁**为代价在长度为 **N** 米的直线路径上行驶的汽车的油箱容量，以及两个[阵列](https://www.geeksforgeeks.org/array-data-structure/)**a【】**和 **b【】，每个阵列的尺寸为 **M、**，其中**a【I】**表示 **i <sup>th</sup>** 站的位置任务是从 **0** 开始，找到到达线路终点所需的最小成本。如果无法到达终点，则打印 **-1** 。**

**示例:**

> **输入:** N = 10，K = 10，M = 2，a[] = {0，1}，b[] = {5，2}
> **输出:** 23
> **说明:**
> 在第 0 个位置，按成本 5 给汽车油箱加满 1 升燃油。然后，在第一个位置，以 18 美元的价格加注 9 升燃油。
> 因此，所需最低成本为 23。
> 
> **输入:** N = 10，K = 5，M = 3，a[] = {0，3，5}，b[] = {5，9，3}
> **输出:** 40

**方式:**思路是用[优先队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)和 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) 存放加油站，以最小的成本到达加油站。按照以下步骤解决问题:

*   初始化一个 [HashMap](https://www.geeksforgeeks.org/java-util-hashmap-in-java-with-examples/) ，比如说**地图，**来存储站点的索引和各自的燃油率。
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如 **pq，**来存储加油站的指数和燃油成本以及正在加油的升数。
*   初始化两个变量，说**成本，**存储所需的最小成本，设置**标志=假**检查是否有加油站。
*   迭代范围**【1，N】**:
    *   检查是否有车站。如果发现是真的，则[将其插入 **pq** 。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
    *   拆除所有无法加油的加油站。
    *   如果[**【pq】**为空](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)，则不可能到达线路终点。因此，设置**标志=真**。
    *   存储最低成本站，并更新成本和从该特定站泵出的升数。
    *   再次插入 **pq** 。
*   如果**标志**为真，则打印**“-1”。**表示没有加油站。因此，不可能到达行尾。
*   否则，打印到达行尾的最小成本。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// For priority_queue
struct Compare {
  bool operator()(array<int, 3> a, array<int, 3> b)
  {
    return a[1] > b[1];
  }
};

// Function to calculate the minimum cost
// required to reach the end of Line
void minCost(int N, int K, int M, int a[], int b[])
{
  // Checks if possible to
  // reach end or not
  bool flag = true;

  // Stores the stations and
  // respective rate of fuel
  unordered_map<int, int> map;
  for (int i = 0; i < M; i++) {
    map[a[i]] = b[i];
    if (i == M - 1 && K < N - a[i]) {
      flag = false;
      break;
    }
    else if (i < M - 1 && K < a[i + 1] - a[i]) {
      flag = false;
      break;
    }
  }

  if (!flag) {
    cout << -1;
    return;
  }

  // Stores the station index and cost of fuel and
  // litres of petrol which is being fueled
  priority_queue<array<int, 3>, vector<array<int, 3> >,
  Compare>
    pq;
  int cost = 0;
  flag = false;

  // Iterate through the entire line
  for (int i = 0; i < N; i++) {

    // Check if there is a station at current index
    if (map.find(i) != map.end()) {
      array<int, 3> arr = { i, map[i], 0 };
      pq.push(arr);
    }

    // Remove all the stations where
    // fuel cannot be pumped
    while (pq.size() > 0 && pq.top()[2] == K)
      pq.pop();

    // If there is no station left to fill fuel
    // in tank, it is not possible to reach end
    if (pq.size() == 0) {
      flag = true;
      break;
    }

    // Stores the best station
    // visited so far
    array<int, 3> best_bunk = pq.top();
    pq.pop();

    // Pump fuel from the best station
    cost += best_bunk[1];

    // Update the count of litres
    // taken from that station
    best_bunk[2]++;

    // Update the bunk in queue
    pq.push(best_bunk);
  }
  if (flag) {
    cout << -1 << "\n";
    return;
  }

  // Print the cost
  cout << cost << "\n";
}

// Driven Program
int main()
{

  // Given value of N, K & M
  int N = 10, K = 3, M = 4;

  // Given arrays
  int a[] = { 0, 1, 4, 6 };
  int b[] = { 5, 2, 2, 4 };

  // Function call to calculate minimum
  // cost to reach end of the line
  minCost(N, K, M, a, b);

  return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;
public class Main {

    // Function to calculate the minimum cost
    // required to reach the end of Line
    static void minCost(int N, int K, int M,
                        int[] a, int[] b)
    {
        // Checks if possible to
        // reach end or not
        boolean flag = true;

        // Stores the stations and
        // respective rate of fuel
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < M; i++) {
            map.put(a[i], b[i]);
            if (i == M - 1 && K < N - a[i]) {
                flag = false;
                break;
            }
            else if (i < M - 1 && K < a[i + 1] - a[i]) {
                flag = false;
                break;
            }
        }

        if (!flag) {
            System.out.println("-1");
            return;
        }

        // Stores the station index and cost of fuel and
        // litres of petrol which is being fueled
        PriorityQueue<int[]> pq
            = new PriorityQueue<>((c, d) -> c[1] - d[1]);
        int cost = 0;
        flag = false;

        // Iterate through the entire line
        for (int i = 0; i < N; i++) {

            // Check if there is a station at current index
            if (map.containsKey(i))
                pq.add(new int[] { i, map.get(i), 0 });

            // Remove all the stations where
            // fuel cannot be pumped
            while (pq.size() > 0 && pq.peek()[2] == K)
                pq.poll();

            // If there is no station left to fill fuel
            // in tank, it is not possible to reach end
            if (pq.size() == 0) {
                flag = true;
                break;
            }

            // Stores the best station
            // visited so far
            int best_bunk[] = pq.poll();

            // Pump fuel from the best station
            cost += best_bunk[1];

            // Update the count of litres
            // taken from that station
            best_bunk[2]++;

            // Update the bunk in queue
            pq.add(best_bunk);
        }
        if (flag) {
            System.out.println("-1");
            return;
        }

        // Print the cost
        System.out.println(cost);
    }

    // Driver Code
    public static void main(String args[])
    {
        // Given value of N, K & M
        int N = 10, K = 3, M = 4;

        // Given arrays
        int a[] = { 0, 1, 4, 6 };
        int b[] = { 5, 2, 2, 4 };

        // Function call to calculate minimum
        // cost to reach end of the line
        minCost(N, K, M, a, b);
    }
}
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to calculate the minimum cost
// required to reach the end of Line
function minCost(N, K, M, a, b)
{

  // Checks if possible to
  // reach end or not
  var flag = true;

  // Stores the stations and
  // respective rate of fuel
  var map = new Map();
  for (var i = 0; i < M; i++) {
    map.set(a[i] , b[i]);
    if (i == M - 1 && K < N - a[i]) {
      flag = false;
      break;
    }
    else if (i < M - 1 && K < a[i + 1] - a[i]) {
      flag = false;
      break;
    }
  }

  if (!flag) {
    document.write(-1);
    return;
  }

  // Stores the station index and cost of fuel and
  // litres of petrol which is being fueled
  var pq = [];
  var cost = 0;
  flag = false;

  // Iterate through the entire line
  for (var i = 0; i < N; i++) {

    // Check if there is a station at current index
    if (map.has(i)) {
      var arr = [ i, map.get(i), 0 ];
      pq.push(arr);
    }
    pq.sort();

    // Remove all the stations where
    // fuel cannot be pumped
    while (pq.length > 0 && pq[pq.length-1][2] == K)
      pq.pop();

    // If there is no station left to fill fuel
    // in tank, it is not possible to reach end
    if (pq.length == 0) {
      flag = true;
      break;
    }

    // Stores the best station
    // visited so far
    var best_bunk = pq[pq.length-1];
    pq.pop();

    // Pump fuel from the best station
    cost += best_bunk[1];

    // Update the count of litres
    // taken from that station
    best_bunk[2]++;

    // Update the bunk in queue
    pq.push(best_bunk);
    pq.sort();
  }
  if (flag) {
    document.write( -1 + "<br>");
    return;
  }

  // Print the cost
  document.write(cost + "<br>");
}

// Driven Program
// Given value of N, K & M
var N = 10, K = 3, M = 4;

// Given arrays
var a = [0, 1, 4, 6 ];
var b = [5, 2, 2, 4];

// Function call to calculate minimum
// cost to reach end of the line
minCost(N, K, M, a, b);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
-1
```

***时间复杂度:** O(N * logN)*
***辅助空间:** O(N)*