# 以 M 为增量最大化 N 对比率的平均值

> 原文:[https://www . geesforgeks . org/最大化 n 对乘 m 增量的平均比率/](https://www.geeksforgeeks.org/maximize-average-of-the-ratios-of-n-pairs-by-m-increments/)

给定一个由 **N** 对和一个正整数 **M** 组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是通过将任意对的第一个和第二个元素精确地递增**1****M**次来最大化对比率的平均值。

**示例:**

> **输入:** arr[] = {{1，2}，{3，5}，{2，2}}，M = 2
> **输出:** 0.783333
> **解释:**
> 下面是执行的操作:
> **操作 1:** 将对{1，2}的第一个和第二个元素增加 1。现在，数组修改为{{2，3}，{3，5}，{2，2}}。
> **操作 2:** 将{2，3}对的第一个和第二个元素增加 1。现在，数组修改为{{3，4}，{3，5}，{2，2}}。
> 上述运算后，对比值的平均值为((3/4) + (3/5) + (2/2))/3 = 0.7833，这是最大可能值。
> 
> **输入:** arr[] = {{2，5}，{3，5}}，M = 3
> T3】输出: 0.619048

**方法:**通过使用 [Max-heap](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) 对配对进行运算，然后从[堆](https://www.geeksforgeeks.org/binary-heap/)中不断弹出数值 **M** 次，相加到总和中，从而存储比率的增加，就可以解决给定的问题。按照以下步骤解决问题:

*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如说 **PQ** 对，如果对其进行一次操作，存储相应的平均值变化和对的索引。
*   初始化一个变量，说**将**相加为 **0** 来存储对比率的最大平均值。
*   [遍历给定的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)对 **arr[]** ，在将 **1** 添加到对的两个值后，找到比率的增加，并将该值推送到[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **PQ** 。另外，将 **i <sup>第</sup>对**与变量**之和**的比值相加。
*   [迭代直到](https://www.geeksforgeeks.org/range-based-loop-c/)**M**的值为正，执行以下步骤:
    *   弹出优先队列 **PQ** 的[顶元素，将比例的增加添加到**总和**中。](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)
    *   更新该对的值，并在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/) **PQ** 中推动该对比率的新增加。
*   完成上述步骤后，打印**总和**除以 **N** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the change in the
// ratio in pair after applying operation
double change(int pass, int total)
{
    double currentPassRatio, newPassRatio;
    double increase;

    // Stores the current ratio
    currentPassRatio = ((double)pass)
                       / total;

    // Stores the new ratio
    newPassRatio = ((double)(pass + 1))
                   / (total + 1);

    // Stores the increase in ratio
    increase = newPassRatio
               - currentPassRatio;

    // Returns the change
    return increase;
}

// Function to find the maximum
// average of the ratio of the
// pairs by applying M increments
double maximumAverage(
    vector<vector<int> > v, int M,
    int N)
{
    // Stores the required result
    double sum = 0;

    double increase, average;

    // Declare a priority queue
    // for storing the increments
    priority_queue<pair<double, int> > pq;
    for (int i = 0; i < N; i++) {

        // Store the increase in the ratio
        // after applying one operation
        increase = change(v[i][0], v[i][1]);

        // Push the increased value and
        // index value in priority queue
        pq.push({ increase, i });

        // Store the ratio
        average = v[i][0] * 1.0 / v[i][1];

        // Update the value of sum
        sum += average;
    }

    // Iterate while M > 0
    while (M > 0) {

        // Add the maximum change
        // to the sum
        sum += pq.top().first;

        int i = pq.top().second;

        // Remove the element from
        // the priority queue
        pq.pop();

        // Increase the pairs elements
        // by 1 on which operation
        // is applied
        v[i][0] += 1;
        v[i][1] += 1;

        // Push the updated change of
        // the pair in priority queue
        pq.push({ change(v[i][0], v[i][1]), i });

        // Decrease the operation count
        M--;
    }

    // Update the value of the sum by
    // dividing it by N
    double ans = sum / N;

    // Return the result
    return ans;
}

// Driver Code
int main()
{
    vector<vector<int> > V
        = { { 1, 2 }, { 3, 5 }, { 2, 2 } };
    int M = 2;
    int N = V.size();
    cout << maximumAverage(V, M, N);

    return 0;
}
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the change in the
# ratio in pair after applying operation
def change(pas, total):

    # Stores the current ratio
    currentPassRatio = pas/ total

    # Stores the new ratio
    newPassRatio = (pas + 1) / (total + 1)

    # Stores the increase in ratio
    increase = newPassRatio - currentPassRatio

    # Returns the change
    return increase

# Function to find the maximum
# average of the ratio of the
# pairs by applying M increments
def maximumAverage(v, M, N):

    # Stores the required result
    sum = 0

    increase, average = 0, 0

    # Declare a priority queue
    # for storing the increments
    pq = []
    for i in range(N):
        # Store the increase in the ratio
        # after applying one operation
        increase = change(v[i][0], v[i][1])

        # Push the increased value and
        # index value in priority queue
        pq.append([increase, i ])

        # Store the ratio
        average = v[i][0] * 1.0 / v[i][1]

        # Update the value of sum
        sum += average
    pq = sorted(pq)

    # Iterate while M > 0
    while (M > 0):

        # Add the maximum change
        # to the sum
        sum += pq[-1][0]

        i = pq[-1][1]

        # Remove the element from
        # the priority queue
        del pq[-1]

        # Increase the pairs elements
        # by 1 on which operation
        # is applied
        v[i][0] += 1
        v[i][1] += 1

        # Push the updated change of
        # the pair in priority queue
        pq.append([change(v[i][0], v[i][1]), i])

        # Decrease the operation count
        M -= 1
        pq = sorted(pq)

    # Update the value of the sum by
    # dividing it by N
    ans = sum / N

    # Return the result
    return ans

# Driver Code
if __name__ == '__main__':
    V =  [[1, 2],  [3, 5],  [2, 2]]
    M = 2
    N = len(V)
    print (round(maximumAverage(V, M, N),6))

    # This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to find the change in the
// ratio in pair after applying operation
function change(pass,total)
{
    let currentPassRatio, newPassRatio;
    let increase;

    // Stores the current ratio
    currentPassRatio = (pass)
                       / total;

    // Stores the new ratio
    newPassRatio = ((pass + 1))
                   / (total + 1);

    // Stores the increase in ratio
    increase = newPassRatio
               - currentPassRatio;

    // Returns the change
    return increase;
}

// Function to find the maximum
// average of the ratio of the
// pairs by applying M increments
function maximumAverage(v,M,N)
{
    // Stores the required result
    let sum = 0;

    let increase, average;

    // Declare a priority queue
    // for storing the increments
    let pq=[];
    for (let i = 0; i < N; i++) {

        // Store the increase in the ratio
        // after applying one operation
        increase = change(v[i][0], v[i][1]);

        // Push the increased value and
        // index value in priority queue
        pq.push([ increase, i ]);

        // Store the ratio
        average = v[i][0] * 1.0 / v[i][1];

        // Update the value of sum
        sum += average;
    }

    pq.sort(function(a,b){return a[0]-b[0]});
    // Iterate while M > 0
    while (M > 0) {

        // Add the maximum change
        // to the sum
        sum += pq[pq.length-1][0];

        let i = pq[pq.length-1][1];

        // Remove the element from
        // the priority queue
        pq.pop();

        // Increase the pairs elements
        // by 1 on which operation
        // is applied
        v[i][0] += 1;
        v[i][1] += 1;

        // Push the updated change of
        // the pair in priority queue
        pq.push([ change(v[i][0], v[i][1]), i ]);

        // Decrease the operation count
        M--;
        pq.sort(function(a,b){return a[0]-b[0]});
    }

    // Update the value of the sum by
    // dividing it by N
    let ans = sum / N;

    // Return the result
    return ans;
}

// Driver Code
let V=[[ 1, 2 ], [ 3, 5 ], [ 2, 2 ] ];
let M = 2;
let N=V.length;
document.write( maximumAverage(V, M, N).toFixed(6));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
0.783333
```

***时间复杂度:** O(M*log N)*
***辅助空间:** O(N)*