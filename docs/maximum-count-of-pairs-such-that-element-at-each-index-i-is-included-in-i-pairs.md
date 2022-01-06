# 配对的最大数量，使得每个索引 I 处的元素包含在 I 对中

> 原文:[https://www . geeksforgeeks . org/最大成对计数-每个索引中的元素都包含在 I 对中/](https://www.geeksforgeeks.org/maximum-count-of-pairs-such-that-element-at-each-index-i-is-included-in-i-pairs/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) arr[]和一个整数 **N** ，任务是找到可以形成的最大对数，使得**I<sup>th</sup>T7】索引包含在几乎 **arr[i]** 对中。**

**示例:**

> **输入** : arr[] = {2，2，3，4}
> **输出**:
> 5
> 1 3
> 2 4
> 2 4
> 3 4
> 3 4
> **说明:**对于给定的数组，最多可以创建 5 对，其中第一个索引包含在 1 对中，第二个索引包含在 2 对中，第三个索引包含在 3 对中，第四个索引包含在 4 对中，如上所示。
> 
> **输入** : arr[] = {8，2，0，1，1}
> **输出**:
> 4
> 1 2
> 1 5
> 1 4
> 1 2

**方法:**给定的问题可以用[贪婪的方法](https://www.geeksforgeeks.org/greedy-algorithms/)来解决。可以观察到，每一步的最优选择都是选择价值最大的元素，创建各自的对。利用这个观察，按照以下步骤解决这个问题:

*   创建一个[最大优先级队列](https://www.geeksforgeeks.org/priority-queue-using-binary-heap/)，该队列按照给定数组值的降序存储给定数组的索引。
*   创建一个循环来迭代优先级队列，直到其中有两个以上的元素，然后按照以下步骤操作:
    *   在优先级队列中选择[顶部的](https://www.geeksforgeeks.org/priority_queuetop-c-stl/)两个索引，将它们的配对添加到答案[数组](https://www.geeksforgeeks.org/array-data-structure/)中。
    *   如果它们的值大于 0，则在递减它们各自的数组值后，将它们重新插入优先级队列。
*   打印答案数组中的所有对。

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of above appraoch
import java.io.*;
import java.util.*;
class GFG {
    public static void maxPairs(int arr[])
    {
        // Stores the final list
        // of pairs required
        List<Integer> matchList = new ArrayList<>();

        // Max Priority Queue to
        // store indiced in order
        // of their array value
        PriorityQueue<Integer> pq = new PriorityQueue<>(
            (x, y) -> arr[y] - arr[x]);

        // Loop to iterate arr[]
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] > 0)
                pq.add(i);
        }

        // Loop to iterate pq
        // till it has more
        // than 2 elements
        while (pq.size() >= 2) {

            // Stores the maximum
            int top = pq.poll();

            // Stores the second
            // maximum
            int cur = pq.poll();

            // Insert pair into the
            // final list
            matchList.add(top + 1);
            matchList.add(cur + 1);
            arr[top]--;
            arr[cur]--;

            if (arr[top] > 0)
                pq.add(top);

            if (arr[cur] > 0)
                pq.add(cur);
        }

        // Print Answer
        System.out.println(matchList.size() / 2);
        for (int i = 0; i < matchList.size(); i += 2) {
            System.out.println(matchList.get(i) + " "
                               + matchList.get(i + 1));
        }
    }
    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4 };
        maxPairs(arr);
    }
}
```

**Output**

```
5
4 3
4 3
2 4
3 4
2 1
```

***时间复杂度:** O(M*log M)，其中 M 表示所有数组元素之和*
***辅助空间:** O(N)*