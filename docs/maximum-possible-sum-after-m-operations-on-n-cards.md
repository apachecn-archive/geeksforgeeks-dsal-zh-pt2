# N 张卡片 M 次运算后的最大可能和

> 原文:[https://www . geeksforgeeks . org/n-cards 上 m-after-operations 最大可能金额/](https://www.geeksforgeeks.org/maximum-possible-sum-after-m-operations-on-n-cards/)

给定一个大小为 **N** 的数组**arr【】**，它代表每张牌上的初始号码，给定一个大小为 **M** 的二维数组**B【】【】**，其中 **M** 代表需要执行的操作数。每次操作时，最多选择 **B[j][0]** 张卡片(可能为零)，并用 **B[j][1]** 替换每张选中卡片上写的整数。任务是找到 **M** 次运算后的最大可能和。

**示例:**

> **输入:** arr[] = {5，1，4}，B[][] = {{2，3}，{1，5}}
> **输出:** 14
> 用 5 代替 1，总和变为
> 5 + 5 + 4 = 14，这是最大可能。
> 
> **输入:** arr[] = {100，100}，B[][] = {{2，99}}
> **输出:** 200

**进场:** A [贪婪](https://www.geeksforgeeks.org/greedy-algorithms/)进场适用于此。[按照递增的顺序对数组](https://www.geeksforgeeks.org/merge-sort/)进行排序**arr【】**按照要替换的数字的递减顺序对数组**B【】【】**进行排序。然后尝试用 **B[][]** 的一张未使用过的卡片替换 **arr[]** 的最后一张未被替换的卡片。最后，打印最大化总和。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the maximum
// possible sum after M operations
int max_sum(int a[], int n, int b[][2], int m)
{

    // Sort the array a in
    // increasing order
    sort(a, a + n);

    // Place all replacable cards in B
    vector<pair<int, int> > B;
    for (int i = 0; i < m; i++)
        B.push_back({ b[i][1], b[i][0] });

    // Sort vector B in decreasing order
    sort(B.rbegin(), B.rend());

    // To store last unused card of a
    int left = 0;

    // Try to apply all m operations
    for (int i = 0; i < m; i++) {
        int x = B[i].first, y = B[i].second;

        // Try for all applicable cards
        for (int j = 0; j < y; j++) {

            // If current number on card is
            // less than applicable card
            if (a[left] < x) {
                a[left] = x;
                left++;

                if (left == n)
                    break;
            }
            else
                break;
        }
    }

    // To store the maximum
    // possible sum
    int ans = 0;

    // Calculate the maximum
    // possible sum
    for (int i = 0; i < n; i++)
        ans += a[i];

    // Return the required answer
    return ans;
}

// Driver code
int main()
{
    int a[] = { 5, 1, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    int b[][2] = { { 2, 3 }, { 1, 5 } };
    int m = sizeof(b) / sizeof(b[0]);

    cout << max_sum(a, n, b, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

// User defined Pair class
class Pair {
  int x;
  int y;

  // Constructor
  public Pair(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

// class to define user defined conparator
class Sort {

  static void sort(Pair arr[], int n)
  {
    // Comparator to sort the pair according to second element
    Arrays.sort(arr, new Comparator<Pair>() {
      @Override public int compare(Pair p1, Pair p2)
      {
        return p1.x - p2.x;
      }
    });
  }
}

public class Main
{
  // Function to return the maximum
  // possible sum after M operations
  static int max_sum(int[] a, int n,
                     int[][] b, int m)
  {

    // Sort the array a in
    // increasing order
    Arrays.sort(a);

    // Place all replacable cards in B
    Pair B[] = new Pair[m];

    for(int i = 0; i < m; i++)
      B[i] = new Pair(b[i][1], b[i][0]);

    // Sort vector B in decreasing order
    Sort obj = new Sort();
    obj.sort(B, m);

    // To store last unused card of a
    int left = 0;

    // Try to apply all m operations
    for(int i = m-1; i >= 0; i--)
    {
      int x = B[i].x, y = B[i].y;

      // Try for all applicable cards
      for(int j = 0; j < y; j++)
      {

        // If current number on card is
        // less than applicable card
        if (a[left] < x)
        {
          a[left] = x;
          left++;

          if (left == n)
            break;
        }
        else
          break;
      }
    }

    // To store the maximum
    // possible sum
    int ans = 0;

    // Calculate the maximum
    // possible sum
    for(int i = 0; i < n; i++)
      ans += a[i];

    // Return the required answer
    return ans;
  }

  // Driver code
  public static void main(String[] args) {
    int[] a = { 5, 1, 4 };
    int n = a.length;
    int[][] b = { { 2, 3 }, { 1, 5 } };
    int m = 2;

    System.out.println(max_sum(a, n, b, m));
  }
}

// This code is contributed by divyesh072019.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the maximum
# possible sum after M operations
def max_sum(a, n, b, m) :

    # Sort the array a in
    # increasing order
    a.sort();

    # Place all replacable cards in B
    B = [];
    for i in range(m) :
        B.append([b[i][1], b[i][0]]);

    # Sort vector B in decreasing order
    B.sort(reverse = True)

    # To store last unused card of a
    left = 0;

    # Try to apply all m operations
    for i in range(m) :
        x = B[i][0];
        y = B[i][1];

        # Try for all applicable cards
        for j in range(y) :

            # If current number on card is
            # less than applicable card
            if (a[left] < x) :
                a[left] = x;
                left += 1;

                if (left == n) :
                    break;
            else :
                break;

    # To store the maximum
    # possible sum
    ans = 0;

    # Calculate the maximum
    # possible sum
    for i in range(n) :
        ans += a[i];

    # Return the required answer
    return ans;

# Driver code
if __name__ == "__main__" :

    a = [5, 1, 4];
    n = len(a);
    b = [[2, 3], [1, 5]];
    m = len(b);

    print(max_sum(a, n, b, m));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG{

// Function to return the maximum
// possible sum after M operations
static int max_sum(int[] a, int n,
                   int[,] b, int m)
{

    // Sort the array a in
    // increasing order
    Array.Sort(a);

    // Place all replacable cards in B
    List<Tuple<int,
               int>> B = new List<Tuple<int,
                                        int>>();
    for(int i = 0; i < m; i++)
        B.Add(new Tuple<int, int>(b[i, 1], b[i, 0]));

    // Sort vector B in decreasing order
    B.Sort();
    B.Reverse();

    // To store last unused card of a
    int left = 0;

    // Try to apply all m operations
    for(int i = 0; i < m; i++)
    {
        int x = B[i].Item1, y = B[i].Item2;

        // Try for all applicable cards
        for(int j = 0; j < y; j++)
        {

            // If current number on card is
            // less than applicable card
            if (a[left] < x)
            {
                a[left] = x;
                left++;

                if (left == n)
                    break;
            }
            else
                break;
        }
    }

    // To store the maximum
    // possible sum
    int ans = 0;

    // Calculate the maximum
    // possible sum
    for(int i = 0; i < n; i++)
        ans += a[i];

    // Return the required answer
    return ans;
}

// Driver code
static void Main()
{
    int[] a = { 5, 1, 4 };
    int n = a.Length;
    int[,] b = { { 2, 3 }, { 1, 5 } };
    int m = 2;

    Console.WriteLine(max_sum(a, n, b, m));
}
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the maximum
// possible sum after M operations
function max_sum(a, n, b, m) {

    // Sort the array a in
    // increasing order
    a.sort();

    // Place all replacable cards in B
    let B = new Array();
    for (let i = 0; i < m; i++)
        B.push([b[i][1], b[i][0]]);

    // Sort vector B in decreasing order
    B.sort().reverse();

    // To store last unused card of a
    let left = 0;

    // Try to apply all m operations
    for (let i = 0; i < m; i++) {
        let x = B[i][0], y = B[i][1];

        // Try for all applicable cards
        for (let j = 0; j < y; j++) {

            // If current number on card is
            // less than applicable card
            if (a[left] < x) {
                a[left] = x;
                left++;

                if (left == n)
                    break;
            }
            else
                break;
        }
    }

    // To store the maximum
    // possible sum
    let ans = 0;

    // Calculate the maximum
    // possible sum
    for (let i = 0; i < n; i++)
        ans += a[i];

    // Return the required answer
    return ans;
}

// Driver code

let a = [5, 1, 4];
let n = a.length;
let b = [[2, 3], [1, 5]];
let m = b.length;

document.write(max_sum(a, n, b, m));

</script>
```

**Output:** 

```
14
```