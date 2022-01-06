# 最大化 N 个项目的利润总和，使得每个项目的利润是其重量和不同选择值计数的乘积

> 原文:[https://www . geeksforgeeks . org/n 件物品利润总额最大化，以至于每件物品的利润都是其重量和独特选择价值的乘积/](https://www.geeksforgeeks.org/maximize-sum-of-profits-for-n-items-such-that-profit-for-ith-item-is-product-of-its-weight-and-count-of-distinct-chosen-values/)

给定一个由 **N** 对项目组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**作为 **{value，weight}** ，任务是通过选择所有给定的 **N 个项目**来找到利润的最大和，从而选择 **i <sup>th</sup> 项目**的利润被计算为其重量和已经取得的不同值的数量的乘积。

**示例:**

> **输入:** arr[] = {(1，4)，(2，3)，(1，2)，(3，2)}
> **输出:** 27
> **说明:**
> 以下是选择物品使利润最大化的顺序:
> 
> *   选择第二项，即 arr[2] = (1，2)。当前所选项目的利润为 2 * 1 = 2。
> *   选择第三项，即 arr[3] = (3，2)。当前所选项目的利润为 2 * 2 = 4。
> *   选择第一项，即 arr[1] = (2，3)。当前所选项目的利润为 3 * 3 = 9。
> *   选择第 0 项，即 arr[0] = (1，4)。当前所选项目的利润为 4 * 3 = 12。
> 
> 因此，总利润为 2 + 4 + 9 + 12 = 27，这是所选 N 对的所有可能组合中最大的。
> 
> **输入:** arr[] = {(2，2)，(1，2)，(3，2)}
> T3】输出: 12

**方法:**给定的问题可以用[贪婪方法](https://www.geeksforgeeks.org/greedy-algorithms/)解决。其思想是[根据物品的重量对给定的数组**arr【】**](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)进行排序，并且首先选择所有不同的物品，然后选择剩余的物品。按照以下步骤解决给定的问题:

*   初始化一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，比如说**物品**，来存储所有唯一的物品。
*   初始化一个变量，比如 **uniqCnt = 0** ，来存储唯一项目的计数。
*   初始化一个变量，比如**最大利润= 0** ，存储总最大利润。
*   初始化一个变量，比如**总重量= 0** ，来存储非唯一项目的总重量。
*   [遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并将所有独有物品存储到集合**物品**中。
*   [按照权重的升序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)对数组 **arr[]** 进行排序。
*   将唯一元素的计数存储为 **uniqCnt = items.size()** 并从项目中移除所有元素。
*   遍历给定数组 **arr[]** 并检查以下条件:
    *   **如果(！项目数。首先)如果发现这是真的，则插入 **arr[i]。首先将**元素放入设置的**项目**中，计算利润，并通过**最大利润+= items.size() * arr[i]将其更新为**最大利润**。第二**。**
    *   否则，将**总重量**更新为**总重量+= arr[i]。第二**。
*   计算非唯一项目的利润，并将**最大利润**更新为**最大利润+=总重量*唯一性**。
*   完成以上步骤后，打印**最大利润**的值作为最终最大利润。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Comparator function to sort vector
// with respect to the second value
bool comp(pair<int, int> a, pair<int, int> b)
{
    if (a.second > b.second)
        return false;

    return true;
}

// Function to maximize the total profit
// by choosing  the array of items in a
// particular order
int maxProfit(vector<pair<int, int> >& arr,
              int N)
{

    // Stores the unique items
    set<int> items;

    for (int i = 0; i < N; i++) {

        // Store all the unique items
        items.insert(arr[i].first);
    }

    // Sort the arr with respect to
    // the weights
    sort(arr.begin(), arr.end(), comp);

    // Stores the number of unique
    // items count
    int uniqCnt = items.size();

    // Clear the set items
    items.clear();

    // Stores the maximum profit
    int maxProfit = 0;

    // Stores the total weight of items
    // which are not unique
    int totWeight = 0;

    for (int i = 0; i < N; i++) {

        // Check the current item is unique
        if (!items.count(arr[i].first)) {

            // Insert the current item
            // into the items set
            items.insert(arr[i].first);

            // Calculate the profit for
            // the current item and
            // update the maxProfit
            maxProfit += items.size() * arr[i].second;
        }
        else
            // Update the totWeight by
            // adding current item weight
            totWeight += arr[i].second;
    }

    // Update the maxProfit by calculating
    // the profit for items which are not
    // unique and adding it to maxProfit
    maxProfit += totWeight * uniqCnt;

    // Return maxProfit
    return maxProfit;
}

// Driver Code
int main()
{
    vector<pair<int, int> > arr{
        { 1, 4 }, { 2, 3 }, { 1, 2 }, { 3, 2 }
    };
    int N = arr.size();
    cout << maxProfit(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{
    static class pair
    {
        int first, second;
        public pair(int first, int second) 
        {
            this.first = first;
            this.second = second;
        }   
    }
// Comparator function to sort vector
// with respect to the second value
boolean comp(pair a, pair b)
{
    if (a.second > b.second)
        return false;

    return true;
}

// Function to maximize the total profit
// by choosing  the array of items in a
// particular order
static int maxProfit(pair[] arr,
              int N)
{

    // Stores the unique items
    HashSet<Integer> items = new HashSet<Integer>();

    for (int i = 0; i < N; i++) {

        // Store all the unique items
        items.add(arr[i].first);
    }

    // Sort the arr with respect to
    // the weights
    Arrays.sort(arr,(a,b)->a.second-b.second);

    // Stores the number of unique
    // items count
    int uniqCnt = items.size();

    // Clear the set items
    items.clear();

    // Stores the maximum profit
    int maxProfit = 0;

    // Stores the total weight of items
    // which are not unique
    int totWeight = 0;

    for (int i = 0; i < N; i++) {

        // Check the current item is unique
        if (!items.contains(arr[i].first)) {

            // Insert the current item
            // into the items set
            items.add(arr[i].first);

            // Calculate the profit for
            // the current item and
            // update the maxProfit
            maxProfit += items.size() * arr[i].second;
        }
        else
            // Update the totWeight by
            // adding current item weight
            totWeight += arr[i].second;
    }

    // Update the maxProfit by calculating
    // the profit for items which are not
    // unique and adding it to maxProfit
    maxProfit += totWeight * uniqCnt;

    // Return maxProfit
    return maxProfit;
}

// Driver Code
public static void main(String[] args)
{
    pair[] arr = {
            new pair( 1, 4 ), new pair( 2, 3 ), new pair( 1, 2 ), new pair( 3, 2 )
    };
    int N = arr.length;
    System.out.print(maxProfit(arr, N));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python Program to implement
# the above approach

# Function to maximize the total profit
# by choosing  the array of items in a
# particular order
def maxProfit(arr, N):

    # Stores the unique items
    items = set()

    for i in range(N):

        # Store all the unique items
        items.add(arr[i]["first"])

    # Sort the arr with respect to
    # the weights

    arr = sorted(arr, key=lambda i: i['second'])

    # Stores the number of unique
    # items count
    uniqCnt = len(items)

    # Clear the set items
    items.clear()

    # Stores the maximum profit
    maxProfit = 0

    # Stores the total weight of items
    # which are not unique
    totWeight = 0

    for i in range(0, N):

        # Check the current item is unique
        if (not (arr[i]['first']) in items):

            # Insert the current item
            # into the items set
            items.add(arr[i]['first'])

            # Calculate the profit for
            # the current item and
            # update the maxProfit
            maxProfit += len(items) * arr[i]['second']

        else:
            # Update the totWeight by
            # adding current item weight
            totWeight += arr[i]['second']

    # Update the maxProfit by calculating
    # the profit for items which are not
    # unique and adding it to maxProfit
    maxProfit += totWeight * uniqCnt

    # Return maxProfit
    return maxProfit

# Driver Code
arr = [
    {"first": 1, "second": 4},
    {"first": 2, "second": 3},
    {"first": 1, "second": 2},
    {"first": 3, "second": 2}
]
N = len(arr)
print(maxProfit(arr, N))

# This code is contributed by gfgking
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{
    public class pair : IComparable<pair>
    {
        public int first,second;
        public pair(int first, int second)
        {
            this.first = first;
            this.second = second; 
        }

        // Comparator function to sort vector
        // with respect to the second value
        public int CompareTo(pair p)
        {
            return this.second - p.second;
        }
    }

// Function to maximize the total profit
// by choosing  the array of items in a
// particular order
static int maxProfit(pair[] arr,
              int N)
{

    // Stores the unique items
    HashSet<int> items = new HashSet<int>();

    for (int i = 0; i < N; i++) {

        // Store all the unique items
        items.Add(arr[i].first);
    }   

    // Sort the arr with respect to
    // the weights
    Array.Sort(arr);

    // Stores the number of unique
    // items count
    int uniqCnt = items.Count;

    // Clear the set items
    items.Clear();

    // Stores the maximum profit
    int maxProfit = 0;

    // Stores the total weight of items
    // which are not unique
    int totWeight = 0;

    for (int i = 0; i < N; i++) {

        // Check the current item is unique
        if (!items.Contains(arr[i].first)) {

            // Insert the current item
            // into the items set
            items.Add(arr[i].first);

            // Calculate the profit for
            // the current item and
            // update the maxProfit
            maxProfit += items.Count * arr[i].second;
        }
        else
            // Update the totWeight by
            // adding current item weight
            totWeight += arr[i].second;
    }

    // Update the maxProfit by calculating
    // the profit for items which are not
    // unique and adding it to maxProfit
    maxProfit += totWeight * uniqCnt;

    // Return maxProfit
    return maxProfit;
}

// Driver Code
public static void Main(String[] args)
{
    pair[] arr = {
            new pair( 1, 4 ), new pair( 2, 3 ), new pair( 1, 2 ), new pair( 3, 2 )
    };
    int N = arr.Length;
    Console.Write(maxProfit(arr, N));

}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
        // JavaScript Program to implement
        // the above approach

        // Function to maximize the total profit
        // by choosing  the array of items in a
        // particular order
        function maxProfit(arr,
            N) {

            // Stores the unique items
            let items = new Set();

            for (let i = 0; i < N; i++) {

                // Store all the unique items
                items.add(arr[i].first);
            }

            // Sort the arr with respect to
            // the weights
            arr.sort(function (a, b) { return a.second - b.second })
            // Stores the number of unique
            // items count
            let uniqCnt = items.size;

            // Clear the set items
            items.clear();

            // Stores the maximum profit
            let maxProfit = 0;

            // Stores the total weight of items
            // which are not unique
            let totWeight = 0;

            for (let i = 0; i < N; i++) {

                // Check the current item is unique
                if (!items.has(arr[i].first)) {

                    // Insert the current item
                    // into the items set
                    items.add(arr[i].first);

                    // Calculate the profit for
                    // the current item and
                    // update the maxProfit
                    maxProfit += items.size * arr[i].second;
                }
                else
                    // Update the totWeight by
                    // adding current item weight
                    totWeight += arr[i].second;
            }

            // Update the maxProfit by calculating
            // the profit for items which are not
            // unique and adding it to maxProfit
            maxProfit += totWeight * uniqCnt;

            // Return maxProfit
            return maxProfit;
        }

        // Driver Code
        let arr = [
            { "first": 1, "second": 4 },
            { "first": 2, "second": 3 },
            { "first": 1, "second": 2 },
            { "first": 3, "second": 2 }
        ]
        let N = arr.length;
        document.write(maxProfit(arr, N));

     // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
27
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*