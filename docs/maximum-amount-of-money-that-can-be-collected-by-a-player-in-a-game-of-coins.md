# 玩家在硬币游戏中可以收取的最大金额

> 原文:[https://www . geeksforgeeks . org/游戏币玩家可收取的最高金额/](https://www.geeksforgeeks.org/maximum-amount-of-money-that-can-be-collected-by-a-player-in-a-game-of-coins/)

给定一个由 **N** 行和两个人 **A** 和 **B** 组成的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)**Arr【】【】】**按照以下规则进行轮流游戏:

*   随机选择一行，其中 **A** 只能拿最左边的剩余硬币，而 **B** 只能拿所选行中最右边的剩余硬币。
*   当没有硬币剩下时，游戏结束。

任务是确定 **A** 获得的最大金额。

**示例:**

> **输入:** N = 2，Arr[][] = {{ 5，2，3，4 }，{ 1，6 }}
> **输出:** 8
> **解释:**
> 行 1: 5，2，3，4
> 行 2: 1，6
> 操作:
> 
> 1.  a 拿走价值 5 的硬币
> 2.  乙拿走价值 4 的硬币
> 3.  a 拿走价值 2 的硬币
> 4.  乙拿走价值 3 的硬币
> 5.  a 拿走价值 1 的硬币
> 6.  乙拿走价值 6 的硬币
> 
> 最佳情况下，A 收的钱= 5+2+1 = 8
> B 收的钱= 3 + 4 + 6 = 13
> 
> **输入:** N = 1，Arr[] = {{ 1，2，3 }}
> 输出 : 3

**进场:**按照以下步骤解决问题

1.  在用最优策略玩的游戏中
2.  初始化一个变量，比如**金额**，存储 **A** 得到的钱。
3.  如果 **N** 为偶数， **A** 将收取前半枚硬币
4.  否则，首先 **(N / 2)** 硬币由 **A** 收集，最后 **(N / 2)** 硬币由 **B** 收集
5.  如果 N 是奇数，中间的硬币可以由 **A** 或 **B** 收集，这取决于移动的顺序。
6.  将硬币存储在变量中所有奇数行的中间，比如 **mid_odd[]。**
7.  [按降序排列数组**中奇数[]** 。](https://www.geeksforgeeks.org/how-to-sort-an-array-in-descending-order-using-stl-in-c/)
8.  最佳情况下， **A** 将在**min _ odd【】**的**偶数指数**收集所有硬币
9.  最后打印 **A** 的分数。

下面是上述方法的实现:

## C++

```
// CPP Program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

// Function to calculate the
// maximum amount collected by A
void find(int N,  vector<vector<int>>Arr)
{

    // Stores the money
    // obtained by A
    int amount = 0;

    // Stores mid elements
    // of odd sized rows
    vector<int> mid_odd;
    for(int i = 0; i < N; i++)
    {

        // Size of current row
        int siz = Arr[i].size();

        // Increase money collected by A
        for (int j = 0; j < siz / 2; j++)
            amount = amount + Arr[i][j];

        if(siz % 2 == 1)
            mid_odd.push_back(Arr[i][siz/2]);
    }

    // Add coins at even indices
    // to the amount collected by A
    sort(mid_odd.begin(),mid_odd.end());

    for(int i = 0; i < mid_odd.size(); i++)
        if (i % 2 == 0)
         amount = amount + mid_odd[i];

    // Print the amount
    cout<<amount<<endl;

}

// Driver Code
int main()
{
   int N = 2;
   vector<vector<int>>Arr{{5, 2, 3, 4}, {1, 6}};

   // Function call to calculate the
   // amount of coins collected by A
   find(N, Arr);
}

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG
{

// Function to calculate the
// maximum amount collected by A
static void find(int N, int[][] Arr)
{

    // Stores the money
    // obtained by A
    int amount = 0;

    // Stores mid elements
    // of odd sized rows
    ArrayList<Integer> mid_odd
            = new ArrayList<Integer>();
    for(int i = 0; i < N; i++)
    {

        // Size of current row
        int siz = Arr[i].length;

        // Increase money collected by A
        for (int j = 0; j < siz / 2; j++)
            amount = amount + Arr[i][j];

        if(siz % 2 == 1)
            mid_odd.add(Arr[i][siz/2]);
    }

    // Add coins at even indices
    // to the amount collected by A
    Collections.sort(mid_odd);

    for(int i = 0; i < mid_odd.size(); i++){
        if (i % 2 == 0)
         amount = amount + mid_odd.get(i);
    }

    // Print the amount
    System.out.println(amount);
}

// Driver Code
public static void main(String[] args)
{
    int N = 2;
   int[][] Arr = {{5, 2, 3, 4}, {1, 6}};

   // Function call to calculate the
   // amount of coins collected by A
   find(N, Arr);
}
}

// This code is contributed by splevel62.
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to calculate the
# maximum amount collected by A

def find(N, Arr):

    # Stores the money
    # obtained by A
    amount = 0

    # Stores mid elements
    # of odd sized rows
    mid_odd = []

    for i in range(N):

        # Size of current row
        siz = len(Arr[i])

        # Increase money collected by A
        for j in range(0, siz // 2):
            amount = amount + Arr[i][j]

        if(siz % 2 == 1):
            mid_odd.append(Arr[i][siz // 2])

    # Add coins at even indices
    # to the amount collected by A
    mid_odd.sort(reverse=True)

    for i in range(len(mid_odd)):
        if i % 2 == 0:
            amount = amount + mid_odd[i]

    # Print the amount
    print(amount)

# Driver Code

N = 2
Arr = [[5, 2, 3, 4], [1, 6]]

# Function call to calculate the
# amount of coins collected by A
find(N, Arr)
```

## C#

```
// C# Program to implement
// the above approach
using System;
using System.Collections.Generic;
class GFG {

  // Function to calculate the
  // maximum amount collected by A
  static void find(int N, List<List<int>> Arr)
  {

    // Stores the money
    // obtained by A
    int amount = 0;

    // Stores mid elements
    // of odd sized rows
    List<int> mid_odd = new List<int>();
    for(int i = 0; i < N; i++)
    {

      // Size of current row
      int siz = Arr[i].Count;

      // Increase money collected by A
      for (int j = 0; j < siz / 2; j++)
        amount = amount + Arr[i][j];

      if(siz % 2 == 1)
        mid_odd.Add(Arr[i][siz/2]);
    }

    // Add coins at even indices
    // to the amount collected by A
    mid_odd.Sort();

    for(int i = 0; i < mid_odd.Count; i++)
      if (i % 2 == 0)
        amount = amount + mid_odd[i];

    // Print the amount
    Console.WriteLine(amount);

  }

  // Driver code
  static void Main()
  {
    int N = 2;
    List<List<int>> Arr = new List<List<int>>();
    Arr.Add(new List<int>());
    Arr[0].Add(5);
    Arr[0].Add(2);
    Arr[0].Add(3);
    Arr[0].Add(4);
    Arr.Add(new List<int>());
    Arr[1].Add(1);
    Arr[1].Add(6);

    // Function call to calculate the
    // amount of coins collected by A
    find(N, Arr);
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>

// Javascript Program to implement
// the above approach

// Function to calculate the
// maximum amount collected by A
function find(N,  Arr)
{

    // Stores the money
    // obtained by A
    var amount = 0;

    // Stores mid elements
    // of odd sized rows
    var mid_odd = [];
    for(var i = 0; i < N; i++)
    {

        // Size of current row
        var siz = Arr[i].length;

        // Increase money collected by A
        for (var j = 0; j < siz / 2; j++)
            amount = amount + Arr[i][j];

        if(siz % 2 == 1)
            mid_odd.push(Arr[i][siz/2]);
    }

    // Add coins at even indices
    // to the amount collected by A
    mid_odd.sort((a,b)=>a-b)

    for(var i = 0; i < mid_odd.length; i++)
        if (i % 2 == 0)
         amount = amount + mid_odd[i];

    // Print the amount
    document.write( amount + "<br>");

}

// Driver Code
var N = 2;
var Arr = [[5, 2, 3, 4], [1, 6]];

// Function call to calculate the
// amount of coins collected by A
find(N, Arr);

// This code is contributed by importantly.
</script>
```

**Output:** 

```
8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)