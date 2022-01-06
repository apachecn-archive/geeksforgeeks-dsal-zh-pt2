# 根据给定的查询将数组划分为子数组后的最大子数组和

> 原文:[https://www . geeksforgeeks . org/最大子数组-将数组划分为子数组后求和-基于给定查询/](https://www.geeksforgeeks.org/maximum-sub-array-sum-after-dividing-array-into-sub-arrays-based-on-the-given-queries/)

给定一个数组 **arr[]** 和一个整数 **k** ，我们可以在 **k** 的不同位置切割这个数组，其中 **k[]** 存储所有需要切割的位置。任务是在每次切割后打印所有切割的最大总和。
每个切口都是整数 **x** 的形式，其中 **x** 表示 **arr[x]** 和 **arr[x + 1]** 之间的切口。

**示例:**

> **输入:** arr[] = {4，5，6，7，8}，k[] = {0，2，3，1}
> **输出:**
> 26
> 15
> 11
> 8
> **首切- >** {4}和{5，6，7，8}。最大可能和为 5 + 6 + 7 + 8 = 26
> **第二次切割- >** {4}、{5，6}和{7，8}。最大和= 15
> **第三次切割- >** {4}、{5，6}、{7}和{8}。最大和= 11
> **第四次切割- >** {4}、{5}、{6}、{7}和{8}。最大总和= 8
> 
> **输入:** arr[] = {1，2，3}，k[] = {1}
> **输出:**
> 3

**天真的方法:**将数组的结果存储在数组列表中，每次切割后线性计算最大可能和。但是这个方法需要 **O(n*k)** 时间来回答所有的问题。

**高效方法:**我们可以将数组的每个结果片段表示为一个具有数据成员的片段对象**开始**(该片段的开始索引)**结束**(该片段的结束索引)和**值**(该片段的和值)。我们可以将这些片段存储在[树集中](https://www.geeksforgeeks.org/treeset-in-java-with-examples/)和**中，并根据它们的和值**对它们进行排序。因此，在每次切割之后，我们可以得到在 O(log(n))中具有最大和值的块。

*   我们必须制作一个数组值的前缀和数组，以获得两个索引在恒定时间内的和。
*   我们必须用所有当前片段的开始索引来维护另一个树集，这样我们就可以找到要剪切的确切片段。例如，对于单件:
    1.  {1，8} ->开始= 1，结束= 2，值= 9 和{6，3，9} ->开始= 3，结束= 5，值= 18。
    2.  为了切割索引 4，我们需要将第二部分切割成两部分，分别为{6，3}和{9}。所以我们得到了从这个树集中切割哪一部分的开始索引。

下面是上述方法的实现:

```
// Java implementation of the approach
import java.io.IOException;
import java.io.InputStream;
import java.util.*;

// Comparator to sort the Pieces
// based on their sum values
class MyComp implements Comparator<Piece> {
    public int compare(Piece p1, Piece p2)
    {
        if (p2.val != p1.val)
            return p2.val - p1.val;
        if (p1.start != p2.start)
            return p2.start - p1.start;
        return 0;
    }
}
class Piece {
    int start;
    int end;
    int val;

    // Constructor to initialize each Piece
    Piece(int s, int e, int v)
    {
        start = s;
        end = e;
        val = v;
    }
}

class GFG {

    // Function to perform the given queries on the array
    static void solve(int n, int k, int cuts[], int A[])
    {

        // Prefix sum array
        int sum[] = new int[n];
        sum[0] = A[0];
        for (int i = 1; i < n; i++)
            sum[i] = sum[i - 1] + A[i];

        // TreeSet storing all the starts
        TreeSet<Integer> t = new TreeSet<>();

        // TreeSet storing the actual pieces
        TreeSet<Piece> pq = new TreeSet<>(new MyComp());
        Piece temp[] = new Piece[n];
        temp[0] = new Piece(0, n - 1, sum[n - 1]);

        // Added the whole array or Piece of array
        // as there is no cuts yet
        pq.add(temp[0]);
        t.add(0);

        for (int i = 0; i < k; i++) {

            // curr is the piece to be cut
            int curr = t.floor(cuts[i]);
            pq.remove(temp[curr]);
            int end = temp[curr].end;

            // When a piece with start = s and end = e
            // is cut at index i, two pieces are created with
            // start = s, end = i and start = i + 1 and end = e
            // We remove the previous piece and add
            // this one to the TreeSet
            temp[curr]
                = new Piece(curr, cuts[i],
                            sum[cuts[i]]
                                - (curr == 0 ? 0 : sum[curr - 1]));
            pq.add(temp[curr]);

            temp[cuts[i] + 1]
                = new Piece(cuts[i] + 1,
                            end, sum[end] - sum[cuts[i]]);
            pq.add(temp[cuts[i] + 1]);

            t.add(curr);
            t.add(cuts[i] + 1);

            System.out.println(pq.first().val);
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        int A[] = { 4, 5, 6, 7, 8 };
        int n = A.length;
        int cuts[] = { 0, 2, 3, 1 };
        int k = cuts.length;

        solve(n, k, cuts, A);
    }
}
```

**Output:**

```
26
15
11
8

```

时间复杂度 O(n + k 对数 n)