# 分数背包问题的 C++程序

> 原文:[https://www . geesforgeks . org/c-分数背包问题程序/](https://www.geeksforgeeks.org/c-program-for-the-fractional-knapsack-problem/)

**先决条件:** [分数背包问题](https://www.geeksforgeeks.org/fractional-knapsack-problem/)

给定两个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **权重[]** 和**利润[]***权重* 和利润的 **N** 物品，我们需要将这些物品放入一个容量为 **W** 的背包中，得到背包中 *最大* 的总价值。
**注:** 与 0/1 背包不同，允许你破开物品。

**示例:**

> **输入:**权重[] = {10，20，30}，利润[] = {60，100，120}，N= 50
> **输出:**赚取的最大利润= 240
> **解释:**
> 递减的市盈率[] = {6，5，4}
> 取权重值 10，20，(2 / 3) * 30
> 利润= 60+100+120 *(t)
> 
> **输入:**权重[] = {10，40，20，24}，利润[] = {100，280，120，120}，N = 60
> **输出:**赚取的最大利润= 440
> **解释:**
> 降低 p/w 比[] = {10，7，6，5}
> 取权重值 10，40，(1 / 2) * 120
> 利润=

**方法 1–不使用 [STL](https://www.geeksforgeeks.org/the-c-standard-template-library-stl/) :** 想法是使用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)。以下是步骤:

1.  找出每个项目的**值/重量**的比值，[根据该比值对](https://www.geeksforgeeks.org/sorting-algorithms/)项目进行排序。
2.  选择比例最高的项目并添加它们，直到我们无法将下一个项目作为一个整体添加。
3.  最后，尽可能多地添加下一项。
4.  打印上述步骤后的最大利润。

下面是的执行情况上面的做法:T4】

## C++

```
// C++ program to solve fractional
// Knapsack Problem
#include <bits/stdc++.h>

using namespace std;

// Structure for an item which stores
// weight & corresponding value of Item
struct Item {
    int value, weight;

    // Constructor
    Item(int value, int weight)
        : value(value), weight(weight)
    {
    }
};

// Comparison function to sort Item
// according to val/weight ratio
bool cmp(struct Item a, struct Item b)
{
    double r1 = (double)a.value / a.weight;
    double r2 = (double)b.value / b.weight;
    return r1 > r2;
}

// Main greedy function to solve problem
double fractionalKnapsack(struct Item arr[],
                          int N, int size)
{
    // Sort Item on basis of ratio
    sort(arr, arr + size, cmp);

    // Current weight in knapsack
    int curWeight = 0;

    // Result (value in Knapsack)
    double finalvalue = 0.0;

    // Looping through all Items
    for (int i = 0; i < size; i++) {

        // If adding Item won't overflow,
        // add it completely
        if (curWeight + arr[i].weight <= N) {
            curWeight += arr[i].weight;
            finalvalue += arr[i].value;
        }

        // If we can't add current Item,
        // add fractional part of it
        else {
            int remain = N - curWeight;
            finalvalue += arr[i].value
                          * ((double)remain
                             / arr[i].weight);

            break;
        }
    }

    // Returning final value
    return finalvalue;
}

// Driver Code
int main()
{
    // Weight of knapsack
    int N = 60;

    // Given weights and values as a pairs
    Item arr[] = { { 100, 10 },
                   { 280, 40 },
                   { 120, 20 },
                   { 120, 24 } };

    int size = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << "Maximum profit earned = "
         << fractionalKnapsack(arr, N, size);
    return 0;
}
```

**Output:**

```
Maximum profit earned = 440

```

**时间复杂度:***O(N * log<sub>2</sub>N)*
**辅助空间:** *O(1)*

**方法 2–使用 STL:**

1.  为每个元素创建一个以**利润【I/权重【I】**为第一元素，I 为第二元素的[地图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)。
2.  定义一个变量**最大利润= 0** 。
3.  以相反的方式遍历地图:
    *   创建一个名为 fraction 的变量，该变量的值等于 restrict _ weight/weight[I]。
    *   如果**剩余重量**大于或等于零，且其值大于**重量【I】**，则将当前利润加到**最大利润**上，并将剩余重量减少**重量【I】**。
    *   否则，如果剩余重量小于重量[i]，将**分数*利润[i]** 加到**最大 _ 利润**上并断开。
4.  打印**最大利润**。

以下是上述方式的实施:

## C++

```
// C++ program to Fractional Knapsack
// Problem using STL
#include <bits/stdc++.h>
using namespace std;

// Function to find maximum profit
void maxProfit(vector<int> profit,
               vector<int> weight, int N)
{

    // Number of total weights present
    int numOfElements = profit.size();
    int i;

    // Multimap container to store
    // ratio and index
    multimap<double, int> ratio;

    // Variable to store maximum profit
    double max_profit = 0;
    for (i = 0; i < numOfElements; i++) {

        // Insert ratio profit[i] / weight[i]
        // and corresponding index
        ratio.insert(make_pair(
            (double)profit[i] / weight[i], i));
    }

    // Declare a reverse iterator
    // for Multimap
    multimap<double, int>::reverse_iterator it;

    // Traverse the map in reverse order
    for (it = ratio.rbegin(); it != ratio.rend();
         it++) {

        // Fraction of weight of i'th item
        // that can be kept in knapsack
        double fraction = (double)N / weight[it->second];

        // if remaining_weight is greater
        // than the weight of i'th item
        if (N >= 0
            && N >= weight[it->second]) {

            // increase max_profit by i'th
            // profit value
            max_profit += profit[it->second];

            // decrement knapsack to form
            // new remaining_weight
            N -= weight[it->second];
        }

        // remaining_weight less than
        // weight of i'th item
        else if (N < weight[it->second]) {
            max_profit += fraction
                          * profit[it->second];
            break;
        }
    }

    // Print the maximum profit earned
    cout << "Maximum profit earned is:"
         << max_profit;
}

// Driver Code
int main()
{
    // Size of list
    int size = 4;

    // Given profit and weight
    vector<int> profit(size), weight(size);

    // Profit of items
    profit[0] = 100, profit[1] = 280,
    profit[2] = 120, profit[3] = 120;

    // Weight of items
    weight[0] = 10, weight[1] = 40,
    weight[2] = 20, weight[3] = 24;

    // Capacity of knapsack
    int N = 60;

    // Function Call
    maxProfit(profit, weight, N);
}
```

**Output:**

```
Maximum profit earned is:440

```

**时间复杂度:***O(N)*
T5】辅助空间: *O(N)*