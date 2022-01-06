# 给定数量可满足的最大客户数量

> 原文:[https://www . geesforgeks . org/最大客户数量-可满足-给定数量/](https://www.geeksforgeeks.org/maximum-number-customers-can-satisfied-given-quantity/)

超市里引进了一种新品种的大米，这种大米首次上市，但数量有限。每位顾客都需要 a 号和 b 号两种不同包装的大米。a 号和 b 号由工作人员根据需求决定。
给定包 a 和包 b 的大小，可用大米的总量 d 和顾客数量 n，找出对给定大米数量满意的最大顾客数量。
显示可满足的客户总数和可满足的客户指数。

**注:**如果客户订购 2 个 3，他需要 2 包 a 号和 3 包 b 号，假设客户的索引从 1 开始。

**输入:**
第一行输入包含两个整数 n 和 d；下一行包含两个整数 a 和 b。接下来的 n 行包含每个客户的两个整数，表示客户需要的 a 号和 b 号袋子的总数。

**输出:**
打印可满足的最大客户数，在下一行打印满意客户的空格分隔索引。

**示例:**

```
Input : n = 5, d = 5
        a = 1, b = 1
        2 0
        3 2
        4 4
        10 0
        0 1
Output : 2
         5 1 

Input : n = 6, d = 1000000000
       a = 9999, b = 10000
       10000 9998
       10000 10000
       10000 10000
       70000 70000
       10000 10000
       10000 10000
Output : 5
         1 2 3 5 6 

```

**说明:**
在第一个例子中，客户根据需求的顺序是:

```
Customer ID   Demand
   5            1
   1            2
   2            5
   3            8
   4            10
```

由此很容易得出结论，对于 1 + 2 = 3 的总需求，只能满足客户 5 和客户 1。剩余的顾客不能购买剩余的大米，因为他们的需求大于可用的数量。

**方法:**
为了满足最大客户数量的需求，我们必须从需求最小的客户开始，这样我们就有最大的剩余大米量来满足剩余的客户。因此，根据需求的递增顺序对客户进行排序，以便满足最大数量的客户。

以下是上述方法的实现:

## C++

```
// CPP program to find maximum number 
// of customers that can be satisfied
#include <bits/stdc++.h>
using namespace std;

vector<pair<long long, int> > v;

// print maximum number of satisfied
// customers and their indexes 
void solve(int n, int d, int a, int b, 
                        int arr[][2])
{
    // Creating an vector of pair of 
    // total demand and customer number
    for (int i = 0; i < n; i++) {
        int m = arr[i][0], t = arr[i][1];
        v.push_back(make_pair((a * m + b * t),
                                     i + 1));
    }

    // Sorting the customers according
    // to their total demand
    sort(v.begin(), v.end());

    vector<int> ans;

    // Taking the first k customers that
    // can be satisfied by total amount d
    for (int i = 0; i < n; i++) {
        if (v[i].first <= d) {
            ans.push_back(v[i].second);
            d -= v[i].first;
        }
    }

    cout << ans.size() << endl;    
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver program
int main()
{
    // Initializing variables
    int n = 5;
    long d = 5;
    int a = 1, b = 1;
    int arr[][2] = {{2, 0},
                    {3, 2},
                    {4, 4},
                    {10, 0},
                    {0, 1}};

    solve(n, d, a, b, arr);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find maximum number 
# of customers that can be satisfied 
v = []

# print maximum number of satisfied 
# customers and their indexes 
def solve(n, d, a, b, arr):
    first, second = 0, 1

    # Creating an vector of pair of 
    # total demand and customer number 
    for i in range(n):
        m = arr[i][0]
        t = arr[i][1] 
        v.append([a * m + b * t, i + 1])

    # Sorting the customers according 
    # to their total demand 
    v.sort()

    ans = [] 

    # Taking the first k customers that 
    # can be satisfied by total amount d 
    for i in range(n):
        if v[i][first] <= d: 
            ans.append(v[i][second]) 
            d -= v[i][first]

    print(len(ans))
    for i in range(len(ans)):
        print(ans[i], end = " ")

# Driver Code
if __name__ == '__main__': 

    # Initializing variables 
    n = 5
    d = 5
    a = 1
    b = 1
    arr = [[2, 0], [3, 2],  
           [4, 4], [10, 0], 
           [0, 1]] 

    solve(n, d, a, b, arr)

# This code is contributed by PranchalK
```

**Output:**

```
2
5 1

```