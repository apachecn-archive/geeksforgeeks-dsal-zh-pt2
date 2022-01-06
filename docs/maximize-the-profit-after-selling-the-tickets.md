# 卖票后利润最大化

> 原文:[https://www . geesforgeks . org/卖票后利润最大化/](https://www.geeksforgeeks.org/maximize-the-profit-after-selling-the-tickets/)

给定阵列**座位【】**其中**座位【I】**是板球比赛体育场内 **i <sup>第</sup>** 排的空位数量。排队买票的人很多。每个座位的费用相当于它所属的那一排的空座位数。任务是把票卖给 **N** 人，利润最大化。

**示例:**

> **输入:**席[] = {2，1，1}，N = 3
> **输出:** 4
> 人 1:卖出有
> 2 个空位的那排座位，席= {1，1，1}
> 人 2:所有排各有 1 个空位
> 座，席[] = {0，1，1}
> 人 3:席[] = {0，0，1}
> 
> **输入:**席[] = {2，3，4，5，1}，N = 6
> T3】输出: 22

**进场:**为了利润最大化，该票必须是一排中空位最多的座位，并且该排中的空位数量将因其中一个座位刚刚售出而递减 1。所有的人都可以卖一张座位票，直到有空位为止。这可以在[优先级队列](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/)的帮助下有效计算。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized profit
int maxProfit(int seats[], int k, int n)
{

    // Push all the vacant seats
    // in a priority queue
    priority_queue<int> pq;
    for (int i = 0; i < k; i++)
        pq.push(seats[i]);

    // To store the maximized profit
    int profit = 0;

    // To count the people that
    // have been sold a ticket
    int c = 0;
    while (c < n) {

        // Get the maximimum number of
        // vacant seats for any row
        int top = pq.top();

        // Remove it from the queue
        pq.pop();

        // If there are no vacant seats
        if (top == 0)
            break;

        // Update the profit
        profit = profit + top;

        // Push the updated status of the
        // vacant seats in the current row
        pq.push(top - 1);

        // Update the count of persons
        c++;
    }
    return profit;
}

// Driver code
int main()
{
    int seats[] = { 2, 3, 4, 5, 1 };
    int k = sizeof(seats) / sizeof(int);
    int n = 6;

    cout << maxProfit(seats, k, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

// Function to return the maximized profit
static int maxProfit(int seats[], int k, int n)
{

    // Push all the vacant seats
    // in a priority queue
    PriorityQueue<Integer> pq;
    pq = new PriorityQueue<>(Collections.reverseOrder());

    for(int i = 0; i < k; i++)
       pq.add(seats[i]);

    // To store the maximized profit
    int profit = 0;

    // To count the people that
    // have been sold a ticket
    int c = 0;
    while (c < n)
    {

        // Get the maximimum number of
        // vacant seats for any row
        int top = pq.remove();

        // If there are no vacant seats
        if (top == 0)
            break;

        // Update the profit
        profit = profit + top;

        // Push the updated status of the
        // vacant seats in the current row
        pq.add(top - 1);

        // Update the count of persons
        c++;
    }

    return profit;
}

// Driver Code
public static void main(String args[])
{
    int seats[] = { 2, 3, 4, 5, 1 };
    int k = seats.length;
    int n = 6;

    System.out.println(maxProfit(seats, k ,n));
}
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximized profit
def maxProfit(seats, k, n) :

    # Push all the vacant seats
    # in a priority queue
    pq = [];
    for i in range(k) :
        pq.append(seats[i]);

    # for maintaining the property of max heap
    pq.sort(reverse = True);

    # To store the maximized profit
    profit = 0;

    # To count the people that
    # have been sold a ticket
    c = 0;
    while (c < n) :

        # for maintaining the property of max heap
        pq.sort(reverse = True);

        # Get the maximimum number of
        # vacant seats for any row
        top = pq[0];

        # Remove it from the queue
        pq.pop(0);

        # If there are no vacant seats
        if (top == 0) :
            break;

        # Update the profit
        profit = profit + top;

        # Push the updated status of the
        # vacant seats in the current row
        pq.append(top - 1);

        # Update the count of persons
        c += 1;

    return profit;

# Driver code
if __name__ == "__main__" :

    seats = [ 2, 3, 4, 5, 1 ];
    k = len(seats);
    n = 6;

    print(maxProfit(seats, k, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the maximized profit
static int maxProfit(int[] seats, int k, int n)
{

    // Push all the vacant seats
    // in a priority queue
    List<int> pq = new List<int>();
    for(int i = 0; i < k; i++)
        pq.Add(seats[i]);

    // To store the maximized profit
    int profit = 0;

    // To count the people that
    // have been sold a ticket
    int c = 0;

    while (c < n)
    {

        // Get the maximimum number of
        // vacant seats for any row
        pq.Sort();
        pq.Reverse();
        int top = pq[0];

        // Remove it from the queue
        pq.RemoveAt(0);

        // If there are no vacant seats
        if (top == 0)
            break;

        // Update the profit
        profit = profit + top;

        // Push the updated status of the
        // vacant seats in the current row
        pq.Add(top - 1);

        // Update the count of persons
        c++;
    }
    return profit;
}

// Driver Code
static void Main()
{
    int[] seats = { 2, 3, 4, 5, 1 };
    int k = seats.Length;
    int n = 6;

    Console.Write(maxProfit(seats, k, n));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to return the maximized profit
    function maxProfit(seats, k, n)
    {

        // Push all the vacant seats
        // in a priority queue
        let pq = [];
        for(let i = 0; i < k; i++)
            pq.push(seats[i]);

        // To store the maximized profit
        let profit = 0;

        // To count the people that
        // have been sold a ticket
        let c = 0;

        while (c < n)
        {

            // Get the maximimum number of
            // vacant seats for any row
            pq.sort(function(a, b){return a - b});
            pq.reverse();
            let top = pq[0];

            // Remove it from the queue
            pq.shift();

            // If there are no vacant seats
            if (top == 0)
                break;

            // Update the profit
            profit = profit + top;

            // Push the updated status of the
            // vacant seats in the current row
            pq.push(top - 1);

            // Update the count of persons
            c++;
        }
        return profit;
    }

    let seats = [ 2, 3, 4, 5, 1 ];
    let k = seats.length;
    let n = 6;

    document.write(maxProfit(seats, k, n));

</script>
```

**Output**

```
22
```

**滑窗进场:**

这个问题也可以使用滑动窗口技术来解决。

*   对于每个人，我们需要卖出最高价格的票，并将其价值减少 1。
*   对阵列座位进行排序。
*   保持两个指针指向当前最大座位数和下一个最大座位数。
*   我们迭代直到 n>0，数组中有第二大元素。
*   在每次迭代中，如果座位[i]>座位[j]，我们将座位[i]处的值加到我们的答案上，最小(n，i-j)次，并在第 I 个索引处递减该值，否则我们找到 j，使得座位[j]
*   如果在迭代结束时，我们的 n>0 并且座位[i]！=0 我们添加座位[i]直到 n>0，并添加座位[i]！=0.

## C++

```
#include <bits/stdc++.h>
using namespace std;
int maxProfit(int seats[],int k, int n)
{
    sort(seats,seats+k);
    int ans = 0;
    int i = k - 1;
    int j = k - 2;
    while (n > 0 && j >= 0) {
        if (seats[i] > seats[j]) {
            ans = ans + min(n, (i - j)) * seats[i];
            n = n - (i - j);
            seats[i]--;
        }
        else {
            while (j >= 0 && seats[j] == seats[i])
                j--;
            if (j < 0)
                break;
            ans = ans + min(n, (i - j)) * seats[i];
            n = n - (i - j);
            seats[i]--;
        }
    }
    while (n > 0 && seats[i] != 0) {
        ans = ans + min(n, k) * seats[i];
        n -= k;
        seats[i]--;
    }
    return ans;
}
int main()
{
    int seats[] = { 2, 3, 4, 5, 1 };
    int k = sizeof(seats) / sizeof(int);
    int n = 6;

    cout << maxProfit(seats, k, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.Arrays;

class GFG {

    static int maxProfit(int seats[], int k, int n)
    {
        Arrays.sort(seats, 0, k);
        int ans = 0;
        int i = k - 1;
        int j = k - 2;
        while (n > 0 && j >= 0) {
            if (seats[i] > seats[j]) {
                ans = ans + Math.min(n, (i - j)) * seats[i];
                n = n - (i - j);
                seats[i]--;
            }
            else {

                while (j >= 0 && seats[j] == seats[i])
                    j--;

                if (j < 0)
                    break;

                ans = ans + Math.min(n, (i - j)) * seats[i];
                n = n - (i - j);
                seats[i]--;
            }
        }
        while (n > 0 && seats[i] != 0) {
            ans = ans + Math.min(n, k) * seats[i];
            n -= k;
            seats[i]--;
        }
        return ans;
    }

    public static void main(String[] args)
    {
        int seats[] = { 2, 3, 4, 5, 1 };
        int k = seats.length;
        int n = 6;

        System.out.println(maxProfit(seats, k, n));
    }
}

// This code is contributed by rajsanghavi9.
```

## C#

```
// C# program for the above approach

using System;

class GFG {

    static int maxProfit(int []seats, int k, int n)
    {
        Array.Sort(seats, 0, k);
        int ans = 0;
        int i = k - 1;
        int j = k - 2;
        while (n > 0 && j >= 0) {
            if (seats[i] > seats[j]) {
                ans = ans + Math.Min(n, (i - j)) * seats[i];
                n = n - (i - j);
                seats[i]--;
            }
            else {

                while (j >= 0 && seats[j] == seats[i])
                    j--;

                if (j < 0)
                    break;

                ans = ans + Math.Min(n, (i - j)) * seats[i];
                n = n - (i - j);
                seats[i]--;
            }
        }
        while (n > 0 && seats[i] != 0) {
            ans = ans + Math.Min(n, k) * seats[i];
            n -= k;
            seats[i]--;
        }
        return ans;
    }

    public static void Main(String[] args)
    {
        int []seats = { 2, 3, 4, 5, 1 };
        int k = seats.Length;
        int n = 6;

        Console.Write(maxProfit(seats, k, n));
    }
}

// This code is contributed by shivanisinghss2110
```

## java 描述语言

```
<script>

function maxProfit(seats,k, n)
{
    seats.sort();

    var ans = 0;
    var i = k - 1;
    var j = k - 2;
    while (n > 0 && j >= 0) {
        if (seats[i] > seats[j]) {
            ans = ans + Math.min(n, (i - j)) * seats[i];
            n = n - (i - j);
            seats[i]--;
        }
        else {
            while (j >= 0 && seats[j] == seats[i])
                j--;
            if (j < 0)
                break;
            ans = ans + Math.min(n, (i - j)) * seats[i];
            n = n - (i - j);
            seats[i]--;
        }
    }
    while (n > 0 && seats[i] != 0) {
        ans = ans + Math.min(n, k) * seats[i];
        n -= k;
        seats[i]--;
    }
    return ans;
}

var seats = [2, 3, 4, 5, 1];
var k = seats.length;
var n = 6;
document.write(maxProfit(seats, k, n));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
22
```