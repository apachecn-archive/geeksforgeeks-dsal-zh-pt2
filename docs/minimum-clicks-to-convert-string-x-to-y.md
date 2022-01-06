# 将字符串 X 转换为 Y 的最少点击次数

> 原文:[https://www . geesforgeks . org/最小点击量-转换-字符串-x-y/](https://www.geeksforgeeks.org/minimum-clicks-to-convert-string-x-to-y/)

给定一个 3 个字符的起始字符串 **X** ，3 个字符的结束字符串 **Y** 和一个禁止字符串数组。任务是找到从 x 到达 Y 的最小点击次数。

**规则:**

*   3 个字符中的每一个都以循环方式变化，即每次点击时，您可以从 **a 转到 b** 或 **a 转到 z** ，并且禁止的单词从未显示过。
*   如果无法到达 Y **，**打印-1 **。**每次点击，只能更改一个字母。
*   每个禁用字符串的形式为:{**“S1”“S2”“S3”}**，其中每个字符串 S <sub>i</sub> 包含该字符的禁用字母。
*   Forbidden string = **{“ac” “bx” “lw”}** implies words **“abl”, “cxw”, “cbl”, “abw”, “cbw”, “axl”, “axw” and “cxl”** are forbidden and will never be displayed.

    **注意:**如果起始字符串 X 也是禁止字符的可能组合，那么结果也应该是-1。

    > **输入:**X =“znw”，Y =“lof”，N = 4(禁弦数)
    > 禁弦=
    > {“qlb”、“jcm”、“mhoq”}，
    > {“azn”、“piy”、“VJ”}，
    > {“by”、“oy”、“ubo”}，
    > {“jqm”、“f”， “EJ”}
    > **输出:**所需的最小点击次数为 22
    > **解释:**由于给定的禁止字符串中没有组合形成最终的字符串 Y，因此字符串 Y 变为有效。
    > 
    > 因此，所需的最小点击次数计算如下:
    > 向前方向 z–l 点击 12 次
    > 向后方向 z–l 点击 14 次
    > 向前方向 n–o 点击 1 次
    > 向后方向 n–o 点击 25 次
    > 向前方向 w–f 点击 9 次
    > 向后方向 w–f 点击 17 次
    > 
    > 总最少点击次数= 12 + 1 + 9 = 22。
    > 
    > **输入:**X =“BDB”，Y =“xxx”，N = 1(禁止字符串数)
    > 禁止= {“ax”、“acx”、“bxy”}
    > **输出:**所需的最小点击次数为-1
    > **解释:**由于“XXX”是禁止字符的可能组合，因此无法从 X 到达 Y

    **进场:**

    使用 [BFS(广度优先搜索)](https://www.geeksforgeeks.org/breadth-first-traversal-for-a-graph/)进行某些修改，以获得最小点击次数，绕过禁止的字符串。

    1.  由于 3 个位置中的每一个都可以包含字母，因此创建一个 26 * 26 * 26 维的 3D 访问数组，以便遍历单词状态。
    2.  要可视化每个受限单词，创建另一个 26 * 26 * 26 维的 3D 数组，以跟踪遍历中绝不能访问的单词。
    3.  由于 3 个字符中的每一个都以循环方式变化，即每次点击时字母将以循环方式变化，所以需要注意每次到达下一个字母时取模 26。
    4.  让单词的当前状态为**【X Y Z】**。然后，单击移动到以下 6 种状态是可能的:

        > **【X+1Y Z】【X-1Y Z】【X Y+1 Z】【X Y-1 Z】【X Y Z+1】【X Y Z-1】。**

    5.  因此创建 3 个实用程序数组 **dx，dy，dz** 来保持遍历过程的流线型。将每个单词状态存储在一个结构中，该结构有 4 个字段，即 a、b、c(3 个字符中的每一个)和距起始单词的距离。

    以下是上述方法的实现:

    ## C++

    ```
    // C++ code for above program.
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long int

    // each node represents a word state
    struct node {
        int a, b, c;
        // dist from starting word X
        int dist;
    };

    // 3D visited array
    bool visited[26][26][26];

    // 3D restricted array
    bool restricted[26][26][26];

    // utility arrays for single step
    // traversal in left and right
    int dx[6] = { 1, -1, 0, 0, 0, 0 };
    int dy[6] = { 0, 0, 1, -1, 0, 0 };
    int dz[6] = { 0, 0, 0, 0, 1, -1 };

    // function to find the
    // minimum clicks.
    void solve(string start,
               string end, int qx,
               const vector<vector<string> >& forbidden)
    {

        memset(visited, 0,
               sizeof(visited));
        memset(restricted, 0,
               sizeof(restricted));

        for (auto vec : forbidden) {

            string a = vec[0];
            string b = vec[1];
            string c = vec[2];

            for (auto x : a)
                for (auto y : b)
                    for (auto z : c) {

                        // each invalid word is
                        // decoded and marked as
                        // restricted = true.
                        restricted[x - 'a']
                                  [y - 'a']
                                  [z - 'a']
                            = true;
                    }
        }

        // starting and ending letter a
        int sa = start[0] - 'a';
        int ea = end[0] - 'a';

        // starting and ending letter b
        int sb = start[1] - 'a';
        int eb = end[1] - 'a';

        // starting and ending letter c
        int sc = start[2] - 'a';
        int ec = end[2] - 'a';

        if (restricted[sa][sb][sc]
            or restricted[ea][eb][ec]) {

            // check if starting word
            // or finishing word is
            // restricted or not
            cout << -1 << endl;

            return;
        }

        // queue of nodes for BFS
        queue<node> q;

        // initial starting word pushed in
        // queue. dist = 0 for starting word
        q.push({ sa, sb, sc, 0 });

        // mark as visited
        visited[sa][sb][sc] = true;

        while (!q.empty()) {
            node x = q.front();
            q.pop();

            // final destination reached condition
            if (x.a == (end[0] - 'a')
                and x.b == (end[1] - 'a')
                and x.c == (end[2] - 'a')) {

                cout << x.dist
                     << endl;
                return;
            }

            int DIST = x.dist;
            for (int i = 0; i < 6; i++) {

                // mod 26 for circular letter sequence

                // next letter for a
                int A = (x.a + dx[i] + 26) % 26;

                // next letter for b
                int B = (x.b + dy[i] + 26) % 26;

                // next letter for c
                int C = (x.c + dz[i] + 26) % 26;

                if (!restricted[A][B][C]
                    and !visited[A][B][C]) {

                    // if a valid word state,
                    // push into queue
                    q.push({ A, B, C, DIST + 1 });
                    visited[A][B][C] = true;
                }
            }
        }

        // reach here if not possible
        // to reach final word Y
        cout << -1 << endl;
    }

    // Driver Code
    signed main()
    {
        // starting string
        string X = "znw";

        // final string
        string Y = "lof";

        // no of restricting word vectors
        int N = 4;

        vector<vector<string> > forbidden
            = { { "qlb", "jcm", "mhoq" },
                { "azn", "piy", "vj" },
                { "by", "oy", "ubo" },
                { "jqm", "f", "ej" } };

        solve(X, Y, N, forbidden);
        return 0;
    }
    ```

    **Output:**

    ```
    22

    ```

     ***时间复杂度:** O(26 * 26 * 26)，既然在 max，可以有 26 * 26 * 26 个字的状态。
    **空间复杂度:** O(26 * 26 * 26)*