# 求 2 的幂次且和为 N 的 k 个数|集合 1

> 原文:[https://www . geeksforgeeks . org/find-k-numbers-这是 2 的幂，并且有-sum-n/](https://www.geeksforgeeks.org/find-k-numbers-which-are-powers-of-2-and-have-sum-n/)

给定两个数字 N 和 K。任务是打印 K 个 2 的幂，并且它们的和是 N。如果不可能，打印-1。

**示例:**

```
Input: N = 9, K = 4
Output: 4 2 2 1
4 + 2 + 2 + 1 = 9 

Input: N = 4, K = 5
Output: -1 

```

**逼近**:可以按照下面的算法来解决上面的问题:

*   如果 K 小于 N 中的设置位数或大于 N，则不可能。
*   将两个 at 位的幂插入[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)。
*   在优先级队列中迭代，直到我们得到 K 个元素， *pop()* 最顶端的元素
*   push()

    元素/2 再次进入优先级队列。

*   一旦达到 K 个元素，就打印出来。

下面是上述方法的实现:

## C++

```
// CPP program to find k numbers that 
// are power of 2 and have sum equal 
// to N
#include <bits/stdc++.h>
using namespace std;

// function to print numbers
void printNum(int n, int k)
{
    // Count the number of set bits
    int x = __builtin_popcount(n);

    // Not-possible condition
    if (k < x || k > n) {
        cout << "-1";
        return;
    }

    // Stores the number
    priority_queue<int> pq;

    // Get the set bits
    int two = 1;
    while (n) {
        if (n & 1) {
            pq.push(two);
        }

        two = two * 2;
        n = n >> 1;
    }

    // Iterate till we get K elements
    while (pq.size() < k) {

        // Get the topmost element
        int el = pq.top();
        pq.pop();

        // Push the elements/2 into 
        // priority queue
        pq.push(el / 2);
        pq.push(el / 2);
    }

    // Print all elements
    int ind = 0;
    while (ind < k) {
        cout << pq.top() << " ";
        pq.pop();
        ind++;
    }
}

// Driver Code
int main()
{
    int n = 9, k = 4;
    printNum(n, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find k numbers that 
// are power of 2 and have sum equal 
// to N 
import java.io.*;
import java.util.*;

class GFG 
{

    // function to print numbers
    static void printNum(int n, int k)
    {

        // Count the number of set bits
        String str = Integer.toBinaryString(n);
        int x = 0;
        for (int i = 0; i < str.length(); i++)
            if (str.charAt(i) == '1')
                x++;

        // Not-possible condition
        if (k < x || k > n)
        {
            System.out.println("-1");
            return;
        }

        // Stores the number
        PriorityQueue<Integer> pq = 
        new PriorityQueue<>(Comparator.reverseOrder());

        // Get the set bits
        int two = 1;
        while (n > 0) 
        {
            if ((n & 1) == 1)
                pq.add(two);
            two *= 2;
            n = n >> 1;
        }

        // Iterate till we get K elements
        while (pq.size() < k)
        {

            // Get the topmost element
            int el = pq.poll();

            // Push the elements/2 into
            // priority queue
            pq.add(el / 2);
            pq.add(el / 2);
        }

        // Print all elements
        int ind = 0;
        while (ind < k) 
        {
            System.out.print(pq.poll() + " ");
            ind++;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        int n = 9, k = 4;
        printNum(n, k);
    }
}

// This code is contributed by
// sanjeev2552
```

## 计算机编程语言

```
# Python program to find k numbers that 
# are power of 2 and have sum equal 
# to N 

# function to prnumbers 
def printNum(n, k):

    # Count the number of set bits 
    x = 0
    m = n
    while (m): 
        x += m & 1
        m >>= 1

    # Not-possible condition 
    if k < x or k > n:
        print("-1")
        return

    # Stores the number 
    pq = []

    # Get the set bits 
    two = 1
    while (n):
        if (n & 1):
            pq.append(two) 

        two = two * 2
        n = n >> 1

    # Iterate till we get K elements 
    while (len(pq) < k):

        # Get the topmost element 
        el = pq[-1]
        pq.pop()

        # append the elements/2 into 
        # priority queue 
        pq.append(el // 2) 
        pq.append(el // 2)

    # Prall elements 
    ind = 0
    pq.sort()
    while (ind < k):
        print(pq[-1], end = " ")
        pq.pop()
        ind += 1

# Driver Code 
n = 9
k = 4
printNum(n, k) 

# This code is contributed by SHUBHAMSINGH10
```

**Output:**

```
4 2 2 1

```

[将 n 表示为 2 的 k 次幂之和|集合 2](https://www.geeksforgeeks.org/represent-n-as-the-sum-of-exactly-k-powers-of-two-set-2/)