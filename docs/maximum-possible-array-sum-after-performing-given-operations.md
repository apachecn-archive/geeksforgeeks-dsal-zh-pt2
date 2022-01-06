# 执行给定操作后的最大可能数组和

> 原文:[https://www . geeksforgeeks . org/执行给定操作后最大可能数组求和/](https://www.geeksforgeeks.org/maximum-possible-array-sum-after-performing-given-operations/)

给定正整数数组 **arr[]** ，整数 **Q** ，以及大小为 **Q** 的数组 **X[]** 和 **Y[]** 。对于数组 **X[]** 和 **Y[]** 中的每个元素，我们可以执行以下操作:

*   对于数组 X[]和 Y[]中的每个查询，从数组 **arr[]** 中最多选择**X[I]个元素，并用整数 **Y[i]** 替换所有选择的元素。**
*   **执行 Q 运算后，任务是从数组**arr【】**中获取最大和。**

****示例:****

> ****输入:** arr[] = {5，2，6，3，8，5，4，7，9，10}，Q = 3，X[] = {2，4，1}，Y[] = {4，3，10}
> **输出:** 68
> **解释:**
> 对于 i = 1，
> 我们可以用整数 4 替换 arr[]中的 atmost 2 元素。这里 arr[]数组 2 个元素小于 4，所以我们将 arr[]中的元素 2 和 3 替换为 4，arr[]变成{5，4，6，4，8，5，4，7，9，10}。
> 对于 i = 2，
> 我们最多可以用整数 3 替换数组 ar[]中的 4 个元素，但是数组 arr[]中没有小于 3 的元素。所以我们不会取代任何东西。
> 对于 i = 3，
> 我们最多可以用整数 10 替换 arr[]中的 1 个元素，arr[]中的 9 个元素小于 10。为了得到最大和，我们将数组 arr[]中的最小元素替换为 10。第三次运算后的 arr[]= { 5，10，6，4，8，5，10，7，9，10 }。最大可能总和是 68。**
> 
> ****输入:** ar[] = {200，100，200，300}，Q = 2，X[] = {2，3}，Y[] = {100，90}
> **输出:** 800
> **解释:**
> 对于 i = 1，
> 我们可以用整数 100 替换 arr[]中的 atmost 2 元素，arr[]的任何元素都不能小于 100。所以我们将替换 0 个元素。
> 对于 i = 2，
> 我们最多可以用整数 90 替换 arr[]数组中的 3 个元素，arr[]数组中没有小于 90 的元素。所以我们将替换 0 个元素。所以 q 运算后我们能得到的最大和是 800。**

****天真方法:**天真的想法是从数组**arr【】**中挑选**X【I】**个数字元素。如果数组中的元素少于 **Y[i]** ，则更新这些元素的 **X[i]** 。** 

*****时间复杂度:** (N <sup>2</sup> )***

 ******Auxiliary Space:** O(1)*

**高效方法:**思路是使用[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)在较低值元素之前获取值较高的元素，精确的优先级队列对以其频率存储值。以下是步骤:

*   将数组 **arr[]** 的每个元素插入优先级队列中。
*   对于数组**中的每个元素(比如 **X[i]** )执行以下操作:**
    1.  从优先级队列中最多选择 **X[i]** 个最小元素。
    2.  如果选择元素小于 Y[i]，则替换为 **Y[i]** 。
    3.  将被替换的元素插入优先级队列，并给出相应的频率。
*   在上述操作之后，数组 **arr[]** 将具有所有元素之和最大的元素。打印总和。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// maximum possible sum of array
// after performing given operations
#include <bits/stdc++.h>
using namespace std;

// Function to get maximum
// sum after q operations
void max_sum(int ar[], int n,
             int q, int x[], int y[])
{
    int ans = 0, i;

    // priority queue to
    // get maximum sum
    priority_queue<pair<int, int> > pq;

    // Push pair, value and 1
    // in the priority queue
    for (i = 0; i < n; i++)
        pq.push({ ar[i], 1 });

    // Push pair, value (to be replaced)
    // and number of elements (to be replaced)
    for (i = 0; i < q; i++)
        pq.push({ y[i], x[i] });

    // Add top n elements from
    // the priority queue
    // to get max sum
    while (n > 0) {

        // pr is the pair
        // pr.first is the value and
        // pr.second is the occurrence
        auto pr = pq.top();

        // pop from the priority queue
        pq.pop();

        // Add value to answer
        ans += pr.first * min(n, pr.second);

        // Update n
        n -= pr.second;
    }

    cout << ans << "\n";
}

// Driver code
int main()
{
    int ar[] = { 200, 100, 200, 300 };
    int n = (sizeof ar) / (sizeof ar[0]);
    int q = 2;
    int x[] = { 2, 3 };
    int y[] = { 100, 90 };
    max_sum(ar, n, q, x, y);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the 
// maximum possible sum of array 
// after performing given operations 
import java.util.*;
import java.lang.*;

class GFG{

static class pair
{
    int first, second;
    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// Function to get maximum 
// sum after q operations 
static void max_sum(int ar[], int n, int q,
                    int x[], int y[]) 
{ 
    int ans = 0, i; 

    // priority queue to 
    // get maximum sum 
    PriorityQueue<pair> pq = new PriorityQueue<>(
        (a, b) -> Integer.compare(a.second, b.second)); 

    // Push pair, value and 1 
    // in the priority queue 
    for(i = 0; i < n; i++) 
        pq.add(new pair(ar[i], 1 )); 

    // Push pair, value (to be replaced) 
    // and number of elements (to be replaced) 
    for(i = 0; i < q; i++) 
        pq.add(new pair(y[i], x[i])); 

    // Add top n elements from 
    // the priority queue 
    // to get max sum 
    while (n > 0)
    { 

        // pr is the pair 
        // pr.first is the value and 
        // pr.second is the occurrence 
        pair pr = pq.peek(); 

        // pop from the priority queue 
        pq.poll(); 

        // Add value to answer 
        ans += pr.first * Math.min(n, pr.second); 

        // Update n 
        n -= pr.second; 
    } 
    System.out.println(ans); 
} 

// Driver Code
public static void main (String[] args)
{
    int ar[] = { 200, 100, 200, 300 }; 
    int n = ar.length; 
    int q = 2; 
    int x[] = { 2, 3 }; 
    int y[] = { 100, 90 };

    max_sum(ar, n, q, x, y); 
}
}

// This code is contributed by offbeat
```

**Output:** 

```
800

```

***时间复杂度:**O(N * log<sub>2</sub>N)*
***辅助空间:** O(N)****