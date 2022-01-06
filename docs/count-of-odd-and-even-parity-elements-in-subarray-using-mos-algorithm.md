# 使用 MO 的算法对子阵列中的奇偶校验元素进行计数

> 原文:[https://www . geesforgeks . org/使用 mos 算法计算子阵列中奇偶校验元素的数量/](https://www.geeksforgeeks.org/count-of-odd-and-even-parity-elements-in-subarray-using-mos-algorithm/)

给定由表示范围的 **L** 和 **R** 表示的 **N** 元素和 **Q** 查询组成的数组 **arr** ，任务是打印子数组**【L，R】**中奇偶校验元素的计数。

**示例:**

> **输入:**
> arr[]=[5，2，3，1，4，8，10]
> Q=2
> 1 3
> 0 4
> **输出:**
> 2 1
> 3 2
> 
> **解释** :
> 在查询 1 中，子阵【1:3】中的奇数奇偶元素为 2 和 1，偶数奇偶元素为 3。
> 在查询 2 中，子阵[0:4]中奇数奇偶元素为 2、1 和 4，偶数奇偶元素为 5 和 3。
> 
> **输入:**
> arr[] = { 13，17，12，10，18，19，15，7，9，6 }
> Q = 3
> 1 5
> 0 7
> 2 9
> **输出:**
> 1 4
> 3 5
> 2 6
> **解释** :
> 在查询 1 中，子数组【1:4】中的奇偶性元素为 19
> 在查询 2 中，子阵[0:7]中奇数奇偶元素为 13、19 和 7，偶数奇偶元素为 17、12、10、18 和 15。
> 在查询 3 中，子阵[2:6]中奇数奇偶元素为 19 和 7，偶数奇偶元素为 12、10、18、15、9 和 6。

**方法:**
MO 算法的思想是对所有查询进行预处理，使得一个查询的结果可以用于下一个查询。

1.  对所有查询进行排序，将从 **0 到√n–1**的 **L** 值的查询放在一起，然后是从 **√n 到 2×√n–1**的查询，依此类推。一个块内的所有查询按照 **R** 值的递增顺序排序。
2.  计算**奇偶性**元素，然后计算**偶奇偶性**元素为 **(R-L+1-奇偶性元素)**
3.  逐个处理所有查询，增加奇数奇偶校验元素的数量，并将结果存储在结构中。
    *   让 **count_oddP** 存储上一次查询中奇数奇偶校验元素的计数。
    *   移除先前查询的额外元素，并为当前查询添加新元素。例如，如果以前的查询是[0，8]，而当前的查询是[3，9]，那么删除元素 arr[0]，arr[1]和 arr[2]并添加 arr[9]。
4.  为了显示结果，请按照提供的顺序对查询进行排序。

**添加元素()**

*   如果当前元素具有奇数奇偶校验，则增加 **count_oddP** 的计数。

    **去除元素()**

    *   如果当前元素具有奇偶性，则减少 **count_oddP** 的计数。

        下面的代码是上述方法的实现:

        ## C++

        ```
        // C++ program to count odd and
        // even parity elements in subarray
        // using MO's algorithm

        #include <bits/stdc++.h>
        using namespace std;

        #define MAX 100000

        // Variable to represent block size.
        // This is made global so compare()
        // of sort can use it.
        int block;

        // Structure to represent a query range 
        struct Query {
            // Starting index
            int L; 
            // Ending index
            int R;
            // Index of query
            int index;
            // Count of odd
            // parity elements
            int odd;
            // Count of even
            // parity elements
            int even;
        };

        // To store the count of
        // odd parity elements
        int count_oddP;

        // Function used to sort all queries so that
        // all queries of the same block are arranged
        // together and within a block, queries are
        // sorted in increasing order of R values.
        bool compare(Query x, Query y)
        {
            // Different blocks, sort by block.
            if (x.L / block != y.L / block)
                return x.L / block < y.L / block;

            // Same block, sort by R value
            return x.R < y.R;
        }

        // Function used to sort all queries in order of their
        // index value so that results of queries can be printed
        // in same order as of input
        bool compare1(Query x, Query y)
        {
            return x.index < y.index;
        }

        // Function to Add elements
        // of current range
        void add(int currL, int a[])
        {
            // _builtin_parity(x)returns true(1)
            // if the number has odd parity else
            // it returns false(0) for even parity.
            if (__builtin_parity(a[currL]))
                count_oddP++;
        }

        // Function to remove elements
        // of previous range
        void remove(int currR, int a[])
        {
            // _builtin_parity(x)returns true(1)
            // if the number has odd parity else
            // it returns false(0) for even parity.
            if (__builtin_parity(a[currR]))
                count_oddP--;
        }

        // Function to generate the result of queries
        void queryResults(int a[], int n, Query q[],
                        int m)
        {

            // Initialize number of odd parity
            // elements to 0
            count_oddP = 0;

            // Find block size
            block = (int)sqrt(n);

            // Sort all queries so that queries of
            // same blocks are arranged together.
            sort(q, q + m, compare);

            // Initialize current L, current R and
            // current result
            int currL = 0, currR = 0;

            for (int i = 0; i < m; i++) {
                // L and R values of current range
                int L = q[i].L, R = q[i].R;

                // Add Elements of current range
                while (currR <= R) {
                    add(currR, a);
                    currR++;
                }
                while (currL > L) {
                    add(currL - 1, a);
                    currL--;
                }

                // Remove element of previous range
                while (currR > R + 1)

                {
                    remove(currR - 1, a);
                    currR--;
                }
                while (currL < L) {
                    remove(currL, a);
                    currL++;
                }

                q[i].odd = count_oddP;
                q[i].even = R - L + 1 - count_oddP;
            }
        }
        // Function to display the results of
        // queries in their initial order
        void printResults(Query q[], int m)
        {
            sort(q, q + m, compare1);
            for (int i = 0; i < m; i++) {
                cout << q[i].odd << " " 
                       << q[i].even << endl;
            }
        }

        // Driver Code
        int main()
        {

            int arr[] = { 5, 2, 3, 1, 4, 8, 10, 12 };
            int n = sizeof(arr) / sizeof(arr[0]);

            Query q[] = { { 1, 3, 0, 0, 0 }, 
                          { 0, 4, 1, 0, 0 }, 
                          { 4, 7, 2, 0, 0 } };

            int m = sizeof(q) / sizeof(q[0]);

            queryResults(arr, n, q, m);

            printResults(q, m);

            return 0;
        }
        ```

        **Output:**

        ```
        2 1
        3 2
        2 2

        ```

        **时间复杂度:** O(Q × √n)