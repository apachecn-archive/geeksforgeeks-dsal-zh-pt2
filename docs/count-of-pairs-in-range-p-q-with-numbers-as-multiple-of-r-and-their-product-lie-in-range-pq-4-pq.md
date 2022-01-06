# 范围[P，Q]内的对的计数，其数为 R 的倍数，其乘积位于范围[P*Q/4，P*Q]

内

> 原文:[https://www . geeksforgeeks . org/范围内成对计数-p-q-带数字的倍数-r-及其乘积-范围内-pq-4-pq/](https://www.geeksforgeeks.org/count-of-pairs-in-range-p-q-with-numbers-as-multiple-of-r-and-their-product-lie-in-range-pq-4-pq/)

给定 **3** 正整数 **P** 、 **Q** 和 **R** ，任务是找到配对数，使得两个元素都在**【P，Q】**的范围内，并且数应该是 **R** 的倍数，数的乘积应该在**【P×Q/4，P×Q】**的范围内。如果不存在这样的配对，打印 **-1。**

**示例:**

> **输入:** P = 14，Q = 30，R = 5
> **输出:** 15 20
> 15 25
> **说明:**
> P&Q 之间 R 的倍数为{15，20，25，30}。
> P × Q = 420，P × Q / 4 = 105
> 所以满足上述条件的对是 15，20 和 15，25。
> 
> **输入:** P = 10，Q = 20，R = 7
> T3】输出: 7 14

**处理方法:**要先解决这个问题，先找到可以存在的对的最小和最大范围，然后找到满足上述条件的对。按照以下步骤解决问题:

*   初始化[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)说， **v** 来存储范围**【P，Q】**内的所有数字，并且是 **R** 的倍数和配对的[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)说， **ans** 来存储符合上述条件的配对。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【P，Q】**中迭代，检查 **i** 是否可以被 **R** 整除，然后在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **v** 中插入 **i** 。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，v . size()-1】**中迭代，并执行以下步骤:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I+1，v . size()-1】**中迭代，检查**v【j】* v【I】<= P * Q**和**v【j】* v【I】>= P * Q/4**，然后将配对插入 **ans** 。
*   如果 **ans.size()** 等于 **0** ，则打印 **-1。**
*   否则，在**和**中打印配对。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// pairs such that both the elements
// are in the range [P, Q] and the
// numbers should be multiple of R,
// and the product of numbers should
// lie in the range [P*Q/4, P*Q]
void findPairs(int p, int q, int r)
{
    // Store multiple of r
    // in range of [P, Q]
    vector<int> v;

    // Iterate in the range [p, q]
    for (int i = p; i <= q; i++) {
        if (i % r == 0) {
            v.push_back(i);
        }
    }

    // Vector to store pair of answer
    vector<pair<int, int> > ans;

    // Iterate through the vector v
    for (int i = 0; i < v.size(); i++) {

        // Iterate in the range [i+1, v.size()-1]
        for (int j = i + 1; j < v.size(); j++) {

            // If pair follow this condition
            // insert the pair in vector ans
            if (v[i] * v[j] >= p * q / 4
                && v[i] * v[j] <= p * q) {
                ans.push_back({ v[i], v[j] });
            }
        }
    }

    // If no pair satisfy the conditions, print -1
    if (ans.size() == 0) {
        cout << -1 << endl;
    }
    else {

        // Print the pairs
        // which satisfy the given condition
        for (int i = 0; i < ans.size(); i++) {

            cout << ans[i].first << " "
                 << ans[i].second << endl;
        }
    }
}

// Driver Code
int main()
{

    // Given Input
    int p = 14, q = 30, r = 5;

    // Function Call
    findPairs(p, q, r);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java program for above approach
import java.awt.*;
import java.util.*;
class GFG{
    static class pair< T, V>{
        T first;
        V second;
    }

    // Function to find the number of
    // pairs such that both the elements
    // are in the range [P, Q] and the
    // numbers should be multiple of R,
    // and the product of numbers should
    // lie in the range [P*Q/4, P*Q]
    static void findPairs(int p, int q, int r)
    {

        // Store multiple of r
        // in range of [P, Q]
        ArrayList<Integer> v = new ArrayList<>();

        // Iterate in the range [p, q]
        for (int i = p; i <= q; i++) {
            if (i % r == 0) {
                v.add(i);
            }
        }

        // Vector to store pair of answer
        ArrayList<pair<Integer, Integer> > ans = new ArrayList<>();

        // Iterate through the vector v
        for (int i = 0; i < v.size(); i++) {

            // Iterate in the range [i+1, v.size()-1]
            for (int j = i + 1; j < v.size(); j++) {

                // If pair follow this condition
                // insert the pair in vector ans
                if (v.get(i) * v.get(j) >= p * q / 4
                        && v.get(i) * v.get(j) <= p * q) {
                    pair<Integer,Integer> x = new pair<>();
                    x.first = v.get(i);
                    x.second = v.get(j);
                    ans.add(x);
                }
            }
        }

        // If no pair satisfy the conditions, print -1
        if (ans.size() == 0) {
            System.out.println(-1);
        }
        else {

            // Print the pairs
            // which satisfy the given condition
            for (int i = 0; i < ans.size(); i++) {
                System.out.println(ans.get(i).first +
                        " " + ans.get(i).second);
            }
        }
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int p = 14, q = 30, r = 5;

        // Function Call
        findPairs(p, q, r);
    }
}

// This code is contributed by hritikrommie.
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of
# pairs such that both the elements
# are in the range [P, Q] and the
# numbers should be multiple of R,
# and the product of numbers should
# lie in the range [P*Q/4, P*Q]
def findPairs(p, q, r):

    # Store multiple of r
    # in range of [P, Q]
    v = []

    # Iterate in the range [p, q]
    for i in range(p, q + 1):
        if (i % r == 0):
            v.append(i)

    # Vector to store pair of answer
    ans = []

    # Iterate through the vector v
    for i in range(len(v)):

        # Iterate in the range [i+1, v.size()-1]
        for j in range(i + 1, len(v)):

            # If pair follow this condition
            # insert the pair in vector ans
            if (v[i] * v[j] >= p * q // 4 and
                v[i] * v[j] <= p * q):
                ans.append([v[i], v[j]])

    # If no pair satisfy the conditions, pr-1
    if (len(ans) == 0):
        print (-1)
    else:

        # Print the pairs
        # which satisfy the given condition
        for i in range(len(ans)):
            print(ans[i][0], ans[i][1])

# Driver Code
if __name__ == '__main__':

    # Given Input
    p = 14
    q = 30
    r = 5

    # Function Call
    findPairs(p, q, r)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach

using System;
using System.Collections.Generic;

class GFG{

// Function to find the number of
// pairs such that both the elements
// are in the range [P, Q] and the
// numbers should be multiple of R,
// and the product of numbers should
// lie in the range [P*Q/4, P*Q]
static void findPairs(int p, int q, int r)
{
    // Store multiple of r
    // in range of [P, Q]
    List<int> v = new List<int>();

    // Iterate in the range [p, q]
    for (int i = p; i <= q; i++) {
        if (i % r == 0) {
            v.Add(i);
        }
    }

    // Vector to store pair of answer
    List<List<int>> ans = new List<List<int>>();

    // Iterate through the vector v
    for(int i = 0; i < v.Count; i++) {

        // Iterate in the range [i+1, v.size()-1]
        for (int j = i + 1; j < v.Count; j++) {

            // If pair follow this condition
            // insert the pair in vector ans
            if (v[i] * v[j] >= p * q / 4
                && v[i] * v[j] <= p * q) {
                List<int> temp = new List<int>();
                temp.Add(v[i]);
                temp.Add(v[j]);
                ans.Add(temp);
            }
        }
    }

    // If no pair satisfy the conditions, print -1
    if (ans.Count == 0) {
        Console.Write(-1);
    }
    else {

         foreach (List<int> subList in ans)
        {
            foreach (int item in subList)
            {
                Console.Write(item + " ");
            }
            Console.WriteLine();
        }
        // Print the pairs
        // which satisfy the given condition
    }
}

// Driver Code
public static void Main()
{

    // Given Input
    int p = 14, q = 30, r = 5;

    // Function Call
    findPairs(p, q, r);

}

}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the number of
// pairs such that both the elements
// are in the range [P, Q] and the
// numbers should be multiple of R,
// and the product of numbers should
// lie in the range [P*Q/4, P*Q]
function findPairs(p, q, r) {
    // Store multiple of r
    // in range of [P, Q]
    let v = [];

    // Iterate in the range [p, q]
    for (let i = p; i <= q; i++) {
        if (i % r == 0) {
            v.push(i);
        }
    }

    // Vector to store pair of answer
    let ans = [];

    // Iterate through the vector v
    for (let i = 0; i < v.length; i++) {

        // Iterate in the range [i+1, v.size()-1]
        for (let j = i + 1; j < v.length; j++) {

            // If pair follow this condition
            // insert the pair in vector ans
            if (v[i] * v[j] >= p * q / 4
                && v[i] * v[j] <= p * q) {
                ans.push([v[i], v[j]]);
            }
        }
    }

    // If no pair satisfy the conditions, print -1
    if (ans.length == 0) {
        document.write(-1 + "<br>");
    }
    else {

        // Print the pairs
        // which satisfy the given condition
        for (let i = 0; i < ans.length; i++) {

            document.write(ans[i][0] + " "
                + ans[i][1] + "<br>");
        }
    }
}

// Driver Code

// Given Input
let p = 14, q = 30, r = 5;

// Function Call
findPairs(p, q, r);

// This code is contributed by _saurabh_jaiswal.
</script>
```

**Output:** 

```
15 20
15 25
```

***时间复杂度:** O(N <sup>2</sup> ，其中 **N** 为**Q–P+1。***
***辅助空间:** O(N)*