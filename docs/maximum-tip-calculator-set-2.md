# 最大小费计算器|设置 2

> 原文:[https://www.geeksforgeeks.org/maximum-tip-calculator-set-2/](https://www.geeksforgeeks.org/maximum-tip-calculator-set-2/)

Rahul 和 Ankit 是皇家餐厅仅有的两个服务员。今天餐厅收到 **N** 订单。当由不同的服务员处理并以[阵列](https://www.geeksforgeeks.org/introduction-to-arrays/)**A【】**和**B【】**的形式给出时，小费的金额可能会有所不同，因此如果**拉胡尔**接受**I<sup>th</sup>T13】订单，他将会得到小费**A【I】**卢比，如果**安基特**接受该订单，小费将会是**B【I】**卢比。为了最大化总小费价值，他们决定在他们之间分配订单。一个订单将由一个人**处理。此外，由于时间限制，拉胡尔不能接受超过 **X** 的订单，安基特不能接受超过 **Y** 的订单。保证 **X + Y** 大于等于 **N** ，意味着所有订单都可以由 Rahul 或者 Ankit 处理。任务是在处理完所有订单后，找出最大可能的小费总额。

**示例:**

> **输入:** N = 5，X = 3，Y = 3，A[] = {1，2，3，4，5}，B[] = {5，4，3，2， 1}
> **输出:** 21
> **说明:**
> 步骤 1: 5 包含在安基特的数组中
> 步骤 2: 4 包含在安基特的数组中
> 步骤 3:由于两者具有相同的值 3，则选择其中任意一个
> 步骤 4: 4 包含在拉胡尔的数组中
> 步骤 5: 5 包含在拉胡尔的数组中
> 因此，小费总额的最大可能金额合计为 20
> 
> **输入:** N = 7，X = 3，Y = 4，A[] = {8，7，15，19，16，16，18}，B[] = {1，7，15，11，12，31，9}
> **输出:** 110

**天真方法:**解决本文的天真方法在上一篇文章中讨论过。

**高效途径:**思路是用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)解决问题。根据拉胡尔小费和安基特小费的不同，将 **N** 订单按[递减顺序](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)排序。然后，遍历所有订单，如果可能的话，取 **i <sup>th</sup>** 订单的最大提示。按照以下步骤解决问题:

*   将**和**初始化为 0，以存储最大可能的提示。
*   创建一对整数的[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，大小为 **N** 的 **V** ，使得**V【I】**的**第一**和**第二**元素分别存储拉胡尔和安基特的 **i <sup>第</sup>和**顺序的尖端。
*   [根据叶尖之间的差异，按降序排列矢量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)、**和**。
*   [使用变量 **i** 遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/)、 **V**
    *   如果 **Y** 的值为**0**T4】或条件**V【I】。第一≥ V[i]。第二个**成立，那么加上 **V[i]的值。先将**改为 **ans** ，再将 **X** 递减 **1** 。
    *   否则，加上 **V[i]的值。第二个**到 **ans** 和减量 **Y** 到 **1** 。
*   完成以上步骤后，打印 **ans** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility Compare function 
// for sorting the array
bool compare(pair<int, int> p1, pair<int, int> p2)
{
    return abs(p1.first - p1.second)
           > abs(p2.first - p2.second);
}

// Function to find the maximum possible amount of total
// tip money after processing all the orders
void maxTip(int A[], int B[], int X, int Y, int N)
{
    // Store all the N orders
    vector<pair<int, int> > tips(N);

    // Traverse all the orders and add them
    // to the vector, V
    for (int i = 0; i < N; i++) {
        tips[i].first = A[i];
        tips[i].second = B[i];
    }

    // Sort the vector in decreasing
      // order of absolute
    // difference of the tips value
    sort(tips.begin(), tips.end(), compare);

    // Store the required result
    int ans = 0;

    // Traverse all the orders
    for (int i = 0; i < N; i++) {

        // Check if Y is 0 or Rahul's tip value
        // is greater than or equal to that of Ankit
        if (Y == 0
            || (X > 0 && tips[i].first >= tips[i].second)) {

            // Update the overall result and
            // decrement X by 1
            ans += tips[i].first;
            X--;
        }

        else {

            // Update the overall result and
            // decrement Y by 1
            ans += tips[i].second;
            Y--;
        }
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given input
    int N = 5, X = 3, Y = 3;
    int A[] = { 1, 2, 3, 4, 5 };
    int B[] = { 5, 4, 3, 2, 1 };

    // Function Call
    maxTip(A, B, X, Y, N);

    return 0;
}
```

**Output**

```
21
```

***时间复杂度:** O(N * log(N))*
***辅助空间:** O(N)*