# 放置在 N*N 棋盘上的 K 个车中可以互相攻击的车数

> 原文:[https://www . geeksforgeeks . org/可攻击对方的车数-k 车外-放置在-nn-棋盘上/](https://www.geeksforgeeks.org/count-of-rooks-that-can-attack-each-other-out-of-k-rooks-placed-on-a-nn-chessboard/)

给定一个 **N X N** 棋盘上 **K** 车的一对坐标，任务是**计算**可以**互相攻击**的**车**的数量。注:**1<= K<= N * N**
**示例**:

> **输入** : K = 2，arr[][] = { {2，2}，{2，3} }，N = 8
> **输出** : 2
> **解释**:两个车都可以互相攻击，因为它们在同一排。因此，可以互相攻击的车数为 2
> 
> **输入** : K = 1，arr[][] = { {4，5} }，N = 4
> T3】输出 : 0

**接近**:利用 **2 车**可以**互相攻击**的事实就可以轻松解决任务，如果他们不是在**同排**就是在**同列**的话，否则他们**就不能**互相攻击。

下面是上述代码的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of attacking rooks
int willAttack(vector<vector<int> >& arr, int k, int N)
{
    int ans = 0;

    for (int i = 0; i < k; i++) {
        for (int j = 0; j < k; j++) {

            if (i != j) {

                // Check if rooks are in same row
                // or same column
                if ((arr[i][0] == arr[j][0])
                    || (arr[i][1] == arr[j][1]))
                    ans++;
            }
        }
    }

    return ans;
}

// Driver Code
int main()
{
    vector<vector<int> > arr = { { 2, 2 }, { 2, 3 } };
    int K = 2, N = 8;
    cout << willAttack(arr, K, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.io.*;
import java.util.*;

class Solution {
  static int willAttack(int arr[][], int k, int N)
  {
    int ans = 0;

    for (int i = 0; i < k; i++) {
      for (int j = 0; j < k; j++) {

        if (i != j) {

          // Check if rooks are in same row
          // or same column
          if ((arr[i][0] == arr[j][0])
              || (arr[i][1] == arr[j][1]))
            ans++;
        }
      }
    }

    return ans;
  }

  // Driver code
  public static void main(String[] args)
  {
    int[][] arr = { { 2, 2 }, { 2, 3 } };
    int K = 2, N = 8;
    System.out.println(willAttack(arr, K, N));
  }
}

// This code is contributed by dwivediyash.
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to count the number of attacking rooks
      function willAttack(arr, k, N) {
          let ans = 0;

          for (let i = 0; i < k; i++) {
              for (let j = 0; j < k; j++) {

                  if (i != j) {

                      // Check if rooks are in same row
                      // or same column
                      if ((arr[i][0] == arr[j][0])
                          || (arr[i][1] == arr[j][1]))
                          ans++;
                  }
              }
          }

          return ans;
      }

      // Driver Code
      let arr = [[2, 2], [2, 3]];
      let K = 2, N = 8;
      document.write(willAttack(arr, K, N));

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
```

***时间复杂度*** : O(K*K)
***辅助空间*** : O(1)