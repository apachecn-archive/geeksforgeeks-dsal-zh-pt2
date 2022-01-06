# 最大化旅途中群体的幸福感

> 原文:[https://www . geesforgeks . org/最大化旅行中群体的幸福感/](https://www.geeksforgeeks.org/maximize-the-happiness-of-the-groups-on-the-trip/)

一次神秘土地之旅将在字节之城字节之地组织。可惜座位有限说 **A** 还有 **N** 人数组。每组可以有老人 **o** ，小孩 **c** ，男人 **m** ，女人 **w** 。组委会希望最大化旅行的快乐价值。旅行的幸福值是所有要去的群体的幸福值之和。如果每个成员都能得到一个座位，一个团体就会去旅行(打破一个团体不是一件好事)。

1.  孩子的幸福 **c = 4**
2.  女人的幸福 **w = 3**
3.  人的幸福 **m = 2**
4.  老人的幸福 **o = 1**

G 组的幸福，H(G) =(其中人的幸福之和)*(组内人数)。
群体的幸福感(‘coow’)=(4+1+1+3)* 4 = 36。
给定团体和总座位容量，任务是最大化快乐，打印旅行中团体的最大快乐。
**例:**

> **输入:**组[]= {“MMO”、“oo”、“cmw”、“cc”、“c”}，A = 5
> **输出:** 43
> 挑选这些组['cmw '、' cc']获得最大利润(4 + 2 + 3) * 3 + (4 + 4) * 2 = 43
> **输入:**组[]= {“CCC”、“oo”、“cm”、“mm”、“wwo”}，A = 10
> **输出:【T0**

**方法:**该问题可视为对 [0-1 背包](https://www.geeksforgeeks.org/0-1-knapsack-problem-dp-10/)问题的轻微修改。可用的座位总数可以被认为是背包的大小。每一组的快乐可以认为是每一项的利润，每一组的人数可以认为是每一项的权重。现在类似于 0-1 背包问题的动态规划方法，在这里应用动态规划来获得最大的快乐。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximized happiness
int MaxHappiness(int A, int N, vector<string> v)
{
    string str;

    // Two arrays similar to
    // 0 1 knapsack problem
    int val[N], wt[N], c = 0;
    for (int i = 0; i < N; i++) {
        str = v[i];

        // To store the happiness
        // of the current group
        c = 0;
        for (int j = 0; str[j]; j++) {

            // Current person is a child
            if (str[j] == 'c')
                c += 4;

            // Woman
            else if (str[j] == 'w')
                c += 3;

            // Man
            else if (str[j] == 'm')
                c += 2;

            // Old person
            else
                c++;
        }

        // Group's happiness is the sum of happiness
        // of the people in the group multiplied by
        // the number of people
        c *= str.length();
        val[i] = c;
        wt[i] = str.length();
    }

    // Solution using 0 1 knapsack
    int k[N + 1][A + 1];
    for (int i = 0; i <= N; i++) {
        for (int w = 0; w <= A; w++) {
            if (i == 0 || w == 0)
                k[i][w] = 0;
            else if (wt[i - 1] <= w)
                k[i][w] = max(val[i - 1]
                                  + k[i - 1][w - wt[i - 1]],
                              k[i - 1][w]);
            else
                k[i][w] = k[i - 1][w];
        }
    }
    return k[N][A];
}

// Driver code
int main()
{

    // Number of seats
    int A = 5;

    // Groups
    vector<string> v = { "mmo", "oo", "cmw", "cc", "c" };
    int N = v.size();
    cout << MaxHappiness(A, N, v);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
    // Function to return the maximized happiness
    static int maxHappiness(int A, int N, String[] v)
    {
        String str;

        // Two arrays similar to
        // 0 1 knapsack problem
        int[] val = new int[N];
        int[] wt = new int[N];
        int c = 0;
        for (int i = 0; i < N; i++)
        {
            str = v[i];

            // To store the happiness
            // of the current goup
            c = 0;
            for (int j = 0; j < str.length(); j++)
            {
                // Current person is a child
                if (str.charAt(j) == 'c')
                    c += 4;

                // Woman
                else if (str.charAt(j) == 'w')
                    c += 3;

                // Man
                else if (str.charAt(j) == 'm')
                    c += 2;

                // Old Person
                else
                    c++;
            }

            // Group's happiness is the sum of happiness
            // of the people in the group multiplie
            // the number of people
            c *= str.length();
            val[i] = c;
            wt[i] = str.length();
        }

        // Solution using 0 1 knapsack
        int[][] k = new int[N + 1][A + 1];
        for (int i = 0; i <= N; i++)
        {
            for (int w = 0; w <= A; w++)
            {
                if (i == 0 || w == 0)
                    k[i][w] = 0;
                else if (wt[i - 1] <= w)
                {
                    k[i][w] = Math.max(val[i - 1]+ k[i - 1][w - wt[i - 1]], k[i-1][w]);
                }
                else
                {
                    k[i][w] = k[i - 1][w];
                }
            }
        }
        return k[N][A];
    }

    // Driver code
    public static void main(String[] args)
    {
        // Number of seats
        int A = 5;

        // Groups
        String[] v = { "mmo", "oo", "cmw", "cc", "c" };
        int N = v.length;
        System.out.println(maxHappiness(A, N, v));
    }
}

// This code is contributed by Vivek Kumar Singh
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import numpy as np

# Function to return the maximized happiness
def MaxHappiness(A, N, v) :

    # Two arrays similar to
    # 0 1 knapsack problem
    val = [0] * N; wt = [0] * N; c = 0;

    for i in range(N) :
        string = v[i];

        # To store the happiness
        # of the current group
        c = 0;
        for j in range(len(string)) :

            # Current person is a child
            if (string[j] == 'c') :
                c += 4;

            # Woman
            elif (string[j] == 'w') :
                c += 3;

            # Man
            elif (string[j] == 'm') :
                c += 2;

            # Old person
            else :
                c += 1;

        # Group's happiness is the sum of happiness
        # of the people in the group multiplied by
        # the number of people
        c *= len(string);

        val[i] = c;

        wt[i] = len(string);

    # Solution using 0 1 knapsack
    k = np.zeros((N + 1, A + 1))

    for i in range(N + 1) :

        for w in range(A + 1) :
            if (i == 0 or w == 0) :
                k[i][w] = 0;
            elif (wt[i - 1] <= w) :
                k[i][w] = max(val[i - 1] +
                                k[i - 1][w - wt[i - 1]],
                                k[i - 1][w]);
            else :
                k[i][w] = k[i - 1][w];

    return k[N][A];

# Driver code
if __name__ == "__main__" :

    # Number of seats
    A = 5;

    # Groups
    v = [ "mmo", "oo", "cmw", "cc", "c" ];

    N = len(v);
    print(MaxHappiness(A, N, v));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the maximized happiness
    static int maxHappiness(int A, int N,
                              String[] v)
    {
        String str;

        // Two arrays similar to
        // 0 1 knapsack problem
        int[] val = new int[N];
        int[] wt = new int[N];
        int c = 0;
        for (int i = 0; i < N; i++)
        {
            str = v[i];

            // To store the happiness
            // of the current goup
            c = 0;
            for (int j = 0; j < str.Length; j++)
            {
                // Current person is a child
                if (str[j] == 'c')
                    c += 4;

                // Woman
                else if (str[j] == 'w')
                    c += 3;

                // Man
                else if (str[j] == 'm')
                    c += 2;

                // Old Person
                else
                    c++;
            }

            // Group's happiness is the sum of happiness
            // of the people in the group multiplie
            // the number of people
            c *= str.Length;
            val[i] = c;
            wt[i] = str.Length;
        }

        // Solution using 0 1 knapsack
        int[ , ] k = new int[N + 1, A + 1];
        for (int i = 0; i <= N; i++)
        {
            for (int w = 0; w <= A; w++)
            {
                if (i == 0 || w == 0)
                    k[i, w] = 0;
                else if (wt[i - 1] <= w)
                {
                    k[i, w] = Math.Max(val[i - 1]+
                                       k[i - 1, w - wt[i - 1]],
                                       k[i - 1, w]);
                }
                else
                {
                    k[i, w] = k[i - 1, w];
                }
            }
        }
        return k[N, A];
    }

    // Driver code
    public static void Main()
    {
        // Number of seats
        int A = 5;

        // Groups
        String[] v = { "mmo", "oo", "cmw", "cc", "c" };
        int N = v.Length;
        Console.WriteLine(maxHappiness(A, N, v));
    }
}

// This code is contributed by Mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to return the maximized happiness
    function maxHappiness(A, N, v) {

        let str;

        // Two arrays similar to
        // 0 1 knapsack problem
        let val = Array.from({length: N}, (_, i) => 0);
        let wt = Array.from({length: N}, (_, i) => 0);
        let c = 0;
        for (let i = 0; i < N; i++)
        {
            str = v[i];

            // To store the happiness
            // of the current goup
            c = 0;
            for (let j = 0; j < str.length; j++)
            {
                // Current person is a child
                if (str[j] == 'c')
                    c += 4;

                // Woman
                else if (str[j] == 'w')
                    c += 3;

                // Man
                else if (str[j] == 'm')
                    c += 2;

                // Old Person
                else
                    c++;
            }

            // Group's happiness is the sum of happiness
            // of the people in the group multiplie
            // the number of people
            c *= str.length;
            val[i] = c;
            wt[i] = str.length;
        }

        // Solution using 0 1 knapsack
        let k = new Array(N + 1);
        for (var i = 0; i < k.length; i++) {
            k[i] = new Array(2);
        }

        for (let i = 0; i <= N; i++)
        {
            for (let w = 0; w <= A; w++)
            {
                if (i == 0 || w == 0)
                    k[i][w] = 0;
                else if (wt[i - 1] <= w)
                {
                    k[i][w] = Math.max(val[i - 1]+ k[i - 1][w - wt[i - 1]], k[i-1][w]);
                }
                else
                {
                    k[i][w] = k[i - 1][w];
                }
            }
        }
        return k[N][A];
    }

// Driver Code

    // Number of seats
        let A = 5;

        // Groups
        let v = [ "mmo", "oo", "cmw", "cc", "c" ];
        let N = v.length;
        document.write(maxHappiness(A, N, v));

// This code is contributed by sanjoy_62.
</script>
```

**Output:** 

```
43
```