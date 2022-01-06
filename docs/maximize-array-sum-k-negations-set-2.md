# K 次否定后最大化数组和|集合 2

> 原文:[https://www . geesforgeks . org/maximize-array-sum-k-negations-set-2/](https://www.geeksforgeeks.org/maximize-array-sum-k-negations-set-2/)

给定一个大小为 n 的数组和一个数字 K，我们必须修改数组 K 的次数。这里修改数组意味着在每个操作中，我们可以用-arr[i]替换任意数组元素 arr[i]。我们需要以这样一种方式执行这个操作，即在 K 次操作之后，数组的和必须是最大的？

示例:

```
Input : arr[] = {-2, 0, 5, -1, 2} 
        K = 4
Output: 10
// Replace (-2) by -(-2), array becomes {2, 0, 5, -1, 2}
// Replace (-1) by -(-1), array becomes {2, 0, 5, 1, 2}
// Replace (0) by -(0), array becomes {2, 0, 5, 1, 2}
// Replace (0) by -(0), array becomes {2, 0, 5, 1, 2}

Input : arr[] = {9, 8, 8, 5} 
        K = 3
Output: 20
```

## [我们强烈建议您点击此处进行练习，然后再进入解决方案。](https://practice.geeksforgeeks.org/problems/maximize-sum-after-k-negations1149/1)

我们在下面的帖子中讨论了一个 O(nk)解决方案。
[K 次否定后最大化数组和|集合 1](https://www.geeksforgeeks.org/maximize-array-sun-after-k-negation-operations/)
上文中使用的思路是用 arr[i]代替数组中的最小元素 arr[i]进行当前操作。这样我们就可以在 K 次运算后使数组的和最大。一旦有趣的情况是，一旦最小元素变成 0，我们就不需要再做任何改变。
上述解决方案中使用的实现使用线性搜索来寻找最小元素。上面讨论的解决方案的时间复杂度是 O(nk)
在这篇文章中，实现了一个优化的解决方案，它使用优先级队列(或[二进制堆](https://www.geeksforgeeks.org/binary-heap/))来快速找到最小元素。

下面是这个想法的实现。它使用 Java 中的 [PriorityQueue 类](https://www.geeksforgeeks.org/priority-queue-class-in-java-2/)。

## C++

```
// A PriorityQueue based C++ program to
// maximize array sum after k negations.
#include <bits/stdc++.h>
using namespace std;

// Function to find Maximum sum
// after K negations
int MaxSum(int a[], int n, int k)
{
    int sum = 0;

    // Create a min heap for priority queue
    priority_queue<int, vector<int>, greater<int>> pq;

    // Insert all elements in f array in priority_queue
    for(int i = 0; i < n; i++)
    {
        pq.push(a[i]);
    }

    while (k--)
    {

        // Retrieve and remove min element
        int temp = pq.top();

        pq.pop();

        // Modify the minimum element and
        // add back to priority queue
        temp = (temp) * -1;
        pq.push(temp);
    }

    // Calculate the sum
    while (!pq.empty())
    {
        sum = sum + pq.top();
        pq.pop();
    }
    return sum;
}

// Driver Code
int main()
{
    int a[] = { -2, 0, 5, -1, 2 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 4;

    cout << MaxSum(a, n, k);
    return 0;
}

// This code is contributed by Harshit Srivastava
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A PriorityQueue based Java program to maximize array
// sum after k negations.
import java.util.*;

class maximizeSum
{
    public static int maxSum(int[] a, int k)
    {
        // Create a priority queue and insert all array elements
        // int
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int x : a)
            pq.add(x);

        // Do k negations by removing a minimum element k times
        while (k-- > 0)
        {
            // Retrieve and remove min element
            int temp = pq.poll();

            // Modify the minimum element and add back
            // to priority queue
            temp *= -1;
            pq.add(temp);
        }

        // Compute sum of all elements in priority queue.
        int sum = 0;
        for (int x : pq)
            sum += x;
        return sum;
    }

    // Driver code
    public static void main (String[] args)
    {
        int[] arr = {-2, 0, 5, -1, 2};
        int k = 4;
        System.out.println(maxSum(arr, k));
    }
}
```

**输出:**

```
10
```

本文由**普拉哈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。