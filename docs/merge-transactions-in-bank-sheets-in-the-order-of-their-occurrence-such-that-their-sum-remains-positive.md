# 按照发生的顺序合并银行表中的交易，使其总和保持正

> 原文:[https://www . geesforgeks . org/merge-transactions-in-bank-sheets-按发生顺序排列-这样-它们的总和保持正/](https://www.geeksforgeeks.org/merge-transactions-in-bank-sheets-in-the-order-of-their-occurrence-such-that-their-sum-remains-positive/)

给定一个由代表 **N** 事务的 **N** 列表组成的数组 **arr[][]** ，任务是按照事务出现的顺序合并给定的[事务列表](https://www.geeksforgeeks.org/list-cpp-stl/)，这样在任何时间点，已经执行的事务的总和都是非负数。如果发现为负，则打印**-1”**。否则，打印合并的交易列表。

**示例:**

> **输入:**arr[][]= { { 100→400 →- 1000 →- 500 }、{-300 → 2000 → -500}}
> **输出:**100→400 →- 300→2000 →- 500 →- 1000 →- 500
> **解释:**上述交易列表每一瞬间的总和由{ T0
> 
> **输入:** arr[][] = [[100 → 400]]
> **输出:** 100 400

**方法:**给定的问题可以被可视化为[合并 **K** 排序的链表](https://www.geeksforgeeks.org/merge-k-sorted-linked-lists-set-2-using-min-heap/)的变体，其标准是在任何时刻合并的事务列表的总和应该是非负的。
按照以下步骤解决问题:

*   初始化一个新节点，比如说 **P** ，表示构造的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的头。
*   初始化一个[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)，比如说 **PQ** ，大小为 **N** ，实现一个 [**最大堆**](https://www.geeksforgeeks.org/heap-data-structure/) 。
*   [将第一个 **N** 交易作为节点插入**PQ**T5。](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)
*   迭代直到 [**PQ** 非空](https://www.geeksforgeeks.org/priority_queueempty-priority_queuesize-c-stl/)并执行以下步骤:
    *   [弹出**优先级队列**的顶部节点](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)，[将该节点插入列表](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的末尾，头部为 **P** 。
    *   如果弹出节点的下一个节点存在，则[在 **PQ** 中插入弹出节点的下一个节点](https://www.geeksforgeeks.org/priority_queuepush-priority_queuepop-c-stl/)。
*   完成上述步骤后，打印形成的**链表**有头 **P** 。

以下是上述方法的实施情况

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.*;

// Structure of a Node
// in the Linked List
class Node {

    int val;
    Node next;

    // Constructor
    Node(int val)
    {
        this.val = val;
        this.next = null;
    }
}

class GFG {

    // Function to merge the Bank sheets
    public static void mergeSheets(
        Node lists[])
    {
        // Initialize Max_Heap
        PriorityQueue<Node> pq

            = new PriorityQueue<>(
                new Comparator<Node>() {

                    // Comparator Function
                    // to make it maxHeap
                    public int compare(Node a, Node b)
                    {
                        return b.val - a.val;
                    }

                });

        // Stores the output list
        Node p, head = new Node(0);
        p = head;

        // Insert the first element
        // of each list
        for (int i = 0;
             i < lists.length; i++) {

            // If the list is not NULL
            if (lists[i] != null) {

                // Insert element in
                // the priority queue
                pq.add(lists[i]);
            }
        }

        // Iterate until PQ is non-empty
        while (!pq.isEmpty()) {
            p.next = pq.poll();
            p = p.next;

            if (p.next != null)
                pq.add(p.next);
        }

        p = head.next;

        // Print the output list
        while (p.next != null) {
            System.out.print(p.val + " ");
            p = p.next;
        }

        System.out.print(p.val);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 2;

        Node arr[] = new Node[N];

        arr[0] = new Node(100);
        arr[0].next = new Node(400);
        arr[0].next.next = new Node(-1000);
        arr[0].next.next.next = new Node(-500);

        arr[1] = new Node(-300);
        arr[1].next = new Node(2000);
        arr[1].next.next = new Node(-500);

        // Function Call
        mergeSheets(arr);
    }
}
```

**Output:** 

```
100 400 -300 2000 -500 -1000 -500
```

***时间复杂度:** O(N * log K)*
***辅助空间:** O(K)*