# 需要训练且力量和耐力都比其他选手差的选手数量

> 原文:[https://www . geeksforgeeks . org/比任何其他玩家都需要训练和拥有更少力量和耐力的玩家数量/](https://www.geeksforgeeks.org/count-of-players-who-need-training-and-have-strictly-less-power-and-endurance-than-any-other-player/)

给定 **2D** 阵玩家三个组件**【力量、耐力、id】**。如果一个球员的力量和耐力比任何其他球员都要差，他就需要训练。任务是用他们的 **id** 找到需要训练的玩家数量。

**示例:**

> **输入:** {{5，4，1}、{6，3，2}、{3，5，3}}
> **输出:** 0
> **说明:**没有哪个玩家比其他玩家拥有更猛的力量和耐力。
> 
> **输入:** {{1，1，0}、{2，2，1}、{3，3，2}}
> **输出:**2
> 0 1
> T7】说明:以下是需要特灵的玩家
> id = 0 的玩家，拥有力量= 1，耐力= 1 的玩家严格来说要比 id = 2 的玩家少。
> id = 1，拥有力量= 2，耐力= 2 的玩家严格来说比 id = 2 的玩家要少。
> 所以有 2 个玩家需要练兵。

**进场:**这个问题可以用**贪婪进场**解决。让 **X** 和 **Y** 做两个玩家。选手 **X** 如果存在 **Y** 使得 X**力量为 Y 的<力量，X**的**耐力为 Y** 的<耐力，则需要训练。按照以下步骤解决给定的问题。

*   两个玩家将基于两个参数进行比较。
*   将阵**玩家[][]** 按照非递减的力量顺序排序。
*   如果两个元素具有相同的功率值，那么首先考虑耐力值更大的元素。
*   从**玩家[][]** 阵列右侧迭代，跟踪最大先前续航。
    *   开始时，如果有任何玩家有资格参加训练，存储其 **id** 。
    *   如果当前玩家的耐力小于先前的最大耐力值，则增加玩家的计数。
    *   否则，更新最大续航时间值。
*   返回存储所有需要训练的玩家的 **id** 的数组。

下面是上述方法的实现。

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

bool compare(vector<int>, vector<int>);

vector<int> CountOfPlayers(vector<vector<int> >& qualities)
{
    int count = 0;
    int n = qualities.size();

    sort(qualities.begin(), qualities.end(),
         [](vector<int>& entry1, vector<int>& entry2)
    {

             // If power value is equal
             // for both elements
             // Sort in descending order
             // according to endurance value
             if (entry1[0] == entry2[0])
                 return entry2[1] < entry1[1];

             else
                 return entry1[0] < entry2[0];
         });

    // Keep track of maximum
    // endurance value in right side
    int ma = 0;

    vector<int> res;

    // Traverse the array players
    for (int i = n - 1; i >= 0; i--) {

        // If current endurance
        // value is smaller than
        // max then we will
        // increment the count
        int id = qualities[i][2];
        if (qualities[i][1] < ma) {

            // Adding player
            // to the final array
            res.push_back(id);

            int q1 = qualities[i + 1][0] - qualities[i][0];
            int q2 = ma - qualities[i][1];

            // Increase the count
            count++;
        }

        // Else update max value
        ma = max(ma, qualities[i][1]);
    }

    return res;
}

// Driver Code
int main()
{
    vector<vector<int> > qualities
        = { { 1, 1, 0 }, { 2, 2, 1 }, { 3, 3, 2 } };
    vector<int> ans = CountOfPlayers(qualities);

    // Print total number of players
    // who need traning
    cout << ans.size() << "\n";

    // Printing id of each player
    for (int i = 0; i < ans.size(); i++) {
        cout << ans[i] << " ";
    }

   return 0;
}

    // This code is contributed by rakeshsahni
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
import java.io.*;
import java.util.*;

class GFG {
    private static Vector<Integer>
    CountOfPlayers(int[][] qualities)
    {
        int count = 0;
        int n = qualities.length;

        sort(qualities);

        // Keep track of maximum
        // endurance value in right side
        int max = 0;

        Vector<Integer> res
            = new Vector<Integer>();

        // Traverse the array players
        for (int i = n - 1; i >= 0; i--) {

            // If current endurance
            // value is smaller than
            // max then we will
            // increment the count
            int id = qualities[i][2];
            if (qualities[i][1] < max) {

                // Adding player
                // to the final array
                res.add(id);

                int q1
                    = qualities[i + 1][0]
                      - qualities[i][0];
                int q2 = max - qualities[i][1];

                // Increase the count
                count++;
            }

            // Else update max value
            max = Math.max(max, qualities[i][1]);
        }

        return res;
    }

    // Sort on the array according
    // to the above approach
    public static void sort(int arr[][])
    {
        // Using built-in sort
        // function Arrays.sort
        Arrays.sort(arr, new Comparator<int[]>() {

            @Override
            // Compare values according to columns
            public int compare(int[] entry1,
                               int[] entry2)
            {

                // If power value is equal
                // for both elements
                // Sort in descending order
                // according to endurance value
                if (entry1[0] == entry2[0])
                    return entry2[1] - entry1[1];

                else
                    return entry1[0] - entry2[0];
            }
        });
    }

    // Driver Code
    public static void main(String[] args)
    {
        int[][] qualities
            = { { 1, 1, 0 },
                { 2, 2, 1 },
                { 3, 3, 2 } };
        Vector<Integer> ans
            = CountOfPlayers(qualities);

        // Print total number of players
        // who need traning
        System.out.println(ans.size());

        // Printing id of each player
        for (int i = 0; i < ans.size(); i++) {
            System.out.print(ans.get(i));
            System.out.print(" ");
        }
    }
}
```

## java 描述语言

```
<script>

      // JavaScript Program to implement
      // the above approach
      function CountOfPlayers(qualities)
      {
          let count = 0;
          let n = qualities.length;

          qualities.sort(function (entry1, entry2)
          {

              // If power value is equal
              // for both elements
              // Sort in descending order
              // according to endurance value
              if (entry1[0] == entry2[0])
                  return entry2[1] - entry1[1];

              else
                  return entry1[0] - entry2[0];
          })

          // Keep track of maximum
          // endurance value in right side
          let ma = 0;

          let res = [];

          // Traverse the array players
          for (let i = n - 1; i >= 0; i--) {

              // If current endurance
              // value is smaller than
              // max then we will
              // increment the count
              let id = qualities[i][2];
              if (qualities[i][1] < ma) {

                  // Adding player
                  // to the final array
                  res.push(id);

                  let q1 = qualities[i + 1][0] - qualities[i][0];
                  let q2 = ma - qualities[i][1];

                  // Increase the count
                  count++;
              }

              // Else update max value
              ma = Math.max(ma, qualities[i][1]);
          }

          return res;
      }

      // Driver Code

      let qualities
          = [[1, 1, 0], [2, 2, 1], [3, 3, 2]];
      let ans = CountOfPlayers(qualities);

      // Print total number of players
      // who need traning
      document.write(ans.length + '<br>');

      // Printing id of each player
      for (let i = 0; i < ans.length; i++) {
          document.write(ans[i] + " ");
      }

  // This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
2
1 0 
```

**时间复杂度:** O(NlogN)，其中 N 是数组的大小。

**空间复杂度:** O(1)。