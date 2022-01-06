# 最大化 K 个工人的速度和他们的最小效率的乘积

> 原文:[https://www . geeksforgeeks . org/速度之和最大化-o-k-工人及其最低效率/](https://www.geeksforgeeks.org/maximize-product-of-sum-of-speeds-o-k-workers-and-their-minimum-efficiency/)

给定一个整数 **N** ，代表工人数量，一个数组**速度【】**，其中**速度【I】**代表 i <sup>第</sup>名工人的速度，一个数组**效率【】**，其中**效率【I】**代表 i <sup>第</sup>名工人的效率，以及一个整数 **K** ，任务是选择 **K** 名工人

**示例:**

> **输入:** N = 6，速度[] = {2，10，3，1，5，8}，效率[] = {5，4，3，9，7，2}，K = 2
> **输出:** 60
> **说明:**
> 选择第 2 个工人(速度= 10，效率= 4)和第 5 个工人(速度= 5，效率= 7)。
> 因此，最大可能和= (10 + 5) * min(4，7) = 60
> 
> **输入:** N = 6，速度[] = {2，10，3，1，5，8}，效率[] = {5，4，3，9，7，2}，K = 3
> T3】输出: 68

**方法:按照以下步骤解决问题:**

*   初始化一对 **arr[ ]** 的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，其中 **arr[i]** 等于**{效率[i]，速度[i]}** 的大小 **N** 。
*   [将**中的 arr[ ]**](https://www.geeksforgeeks.org/sort-c-stl/) 按照效率递减的顺序排序。
*   初始化一个存储工人速度的 min [priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 。
*   初始化变量说， **SumOfSpeed** **= 0** 和 **Ans = 0** 。
*   迭代 **arr[ ]** 并执行以下操作:
    *   添加 **arr[i]。首先**到**的速度总和**
    *   在[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)中按**速度【I】**。
    *   如果[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)的大小超过 **K，**将弹出[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)的前面，并减去**速度总和**。
    *   更新 **Ans** 为 **Ans** 和**的**最大**sumof speed * efficiency【I】**。
*   最后，返回 **Ans** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate array of pairs
void generateArrayofPairs(int n, vector<int>& speed,
                          vector<int>& efficiency,
                          vector<pair<int, int> >& arr)
{

    for (int i = 0; i < n; i++) {

        arr[i] = { efficiency[i], speed[i] };
    }

    sort(arr.rbegin(), arr.rend());
}

// Function to find the maximum
// product of worker speeds and
// their minimum efficiency
int maximizePerformance(vector<int>& speed, int K,
                        vector<int>& efficiency)
{

    int n = speed.size();
    vector<pair<int, int> > arr(n);

    // Function to generate
    // sorted array of pairs
    generateArrayofPairs(n, speed,
                         efficiency, arr);

    // Initialize priority queue
    priority_queue<int, vector<int>,
                   greater<int> >
        pq;

    // Initialize ans and sumofspeed
    int ans = 0;
    int SumOfSpeed = 0;

    // Traversing the arr of pairs
    for (auto& it : arr) {

        int e = it.first;
        int s = it.second;

        // Updating sum of speed
        SumOfSpeed += s;

        // Pushing in priority queue
        pq.push(s);

        // If team consists of more than
        // K workers
        if (pq.size() > K) {

            int temp = pq.top();
            SumOfSpeed -= temp;
            pq.pop();
        }

        // Taking the maximum performance
        // that can be formed
        ans = max(ans, SumOfSpeed * e);
    }

    // Finally return the ans
    return ans;
}

// Driver Code
int main()
{
    // Given Input
    vector<int> speed = { 2, 10, 3, 1, 5, 8 };
    vector<int> efficiency = { 5, 4, 3, 9, 7, 2 };
    int K = 2;

    // Function Call
    cout << maximizePerformance(
        speed, K, efficiency);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

static class pair
{
    int first, second;

    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }  
}

// Function to generate array of pairs
static void generateArrayofPairs(int n, Vector<Integer> speed,
                          Vector<Integer> efficiency,
                          Vector<pair > arr)
{

    for (int i = 0; i < n; i++) {

        arr.insertElementAt(new pair(efficiency.elementAt(i), speed.elementAt(i)), i);
    }

    Collections.sort(arr, new Comparator<pair>() {
            @Override public int compare(pair p1, pair p2)
            {
                  if (p1.first != p2.first)
                    return (p2.first - p1.first);
                  return p2.second - p1.second;
            }
        });
}

// Function to find the maximum
// product of worker speeds and
// their minimum efficiency
static int maximizePerformance(Vector<Integer> speed, int K,
                        Vector<Integer> efficiency)
{

    int n = speed.size();
    Vector<pair > arr = new Vector<>();

    // Function to generate
    // sorted array of pairs
    generateArrayofPairs(n, speed,
                         efficiency, arr);

    // Initialize priority queue
      PriorityQueue<Integer> pq = new PriorityQueue<Integer>();

    // Initialize ans and sumofspeed
    int ans = 0;
    int SumOfSpeed = 0;

    // Traversing the arr of pairs
    for (int i = 0; i < arr.size(); i++) {

        int e = arr.elementAt(i).first;
        int s = arr.elementAt(i).second;

        // Updating sum of speed
        SumOfSpeed += s;

        // Pushing in priority queue
        pq.add(s);

        // If team consists of more than
        // K workers
        if (pq.size() > K) {

            int temp = pq.peek();
            SumOfSpeed -= temp;
            pq.poll();
        }

        // Taking the maximum performance
        // that can be formed
        ans = Math.max(ans, SumOfSpeed * e);
    }

    // Finally return the ans
    return ans;
}

// Driver Code
public static void main (String[] args) {

      // Given Input
    Vector<Integer> speed = new Vector<Integer>();
    speed.add(2);
      speed.add(10);
      speed.add(3);
      speed.add(1);
      speed.add(5);
      speed.add(8);

    Vector<Integer> efficiency = new Vector<Integer>();
      efficiency.add(5);
      efficiency.add(4);
      efficiency.add(3);
      efficiency.add(9);
      efficiency.add(7);
      efficiency.add(2);

      int K = 2;

    // Function Call
    System.out.println(maximizePerformance(
        speed, K, efficiency));
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to generate array of pairs
function generateArrayofPairs(n, speed, efficiency, arr)
{

    for (var i = 0; i < n; i++) {

        arr[i] = [ efficiency[i], speed[i] ];
    }

    arr.sort((a,b)=>{
        if(b[0] == a[0])
            return b[1] - a[1]
        return b[0] - a[0];
    });

    return arr;
}

// Function to find the maximum
// product of worker speeds and
// their minimum efficiency
function maximizePerformance(speed, K, efficiency)
{

    var n = speed.length;
    var arr = Array.from(Array(n),()=>new Array(2).fill(0));

    // Function to generate
    // sorted array of pairs
    arr = generateArrayofPairs(n, speed,
                         efficiency, arr);

    // Initialize priority queue
    var pq = [];

    // Initialize ans and sumofspeed
    var ans = 0;
    var SumOfSpeed = 0;

    // Traversing the arr of pairs
    for (var it of arr) {

        var e = it[0];
        var s = it[1];

        // Updating sum of speed
        SumOfSpeed += s;

        // Pushing in priority queue
        pq.push(s);

        pq.sort((a,b)=>b-a);

        // If team consists of more than
        // K workers
        if (pq.length > K) {

            var temp = pq[pq.length-1];
            SumOfSpeed -= temp;
            pq.pop();
        }

        // Taking the maximum performance
        // that can be formed
        ans = Math.max(ans, SumOfSpeed * e);
    }

    // Finally return the ans
    return ans;
}

// Driver Code
// Given Input
var speed = [2, 10, 3, 1, 5, 8 ];
var efficiency = [5, 4, 3, 9, 7, 2 ];
var K = 2;

// Function Call
document.write(maximizePerformance(speed, K, efficiency));

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
60
```

***时间复杂度:** O(NLogN)*
***辅助空间:** O(N)*