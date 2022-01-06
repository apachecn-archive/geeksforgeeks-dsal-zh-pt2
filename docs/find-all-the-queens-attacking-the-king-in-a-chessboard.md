# 在棋盘中找到所有攻击国王的女王

> 原文:[https://www . geesforgeks . org/find-all-the-queens-攻击棋盘中的国王/](https://www.geeksforgeeks.org/find-all-the-queens-attacking-the-king-in-a-chessboard/)

给定一个由 8 * 8 棋盘中的 **N** 皇后的坐标组成的 [2D 阵](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/) **皇后[][]** 和一个表示国王坐标的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/) **国王[]** ，任务是找到攻击国王的皇后

**示例:**

> **输入:** queens[][] = {{0，1}，{1，0}，{4，0}，{0，4}，{3，3}，{2，4}}，king[] = {2，3 }
> T3】输出: {{0，1}，{2，4}，{3，3}}
> 
> **说明:**坐标{0，1}和{3，3}处的女王斜向攻击国王，{2，4}处的女王垂直位于国王下方。
> 
> **输入:**皇后[][]] = {{4，1}，{1，0}，{4，0}}，王[] = {0，0}
> **输出:** {{1，0}}

**接近**按照以下步骤解决问题:

*   [迭代数组](https://www.geeksforgeeks.org/iterating-arrays-java/) **皇后[][]** 。
*   对于经过的每个坐标，检查是否有攻击国王的所有可能性，即水平、垂直和对角。如果发现攻击国王，检查以下内容:
    *   如果没有其他女王从那个方向攻击国王，包括作为攻击者的现任国王。
    *   如果一个攻击者已经出现在那个方向，检查当前的女王是否是最近的攻击者。如果被发现是真的，包括作为攻击者的分女王。否则，继续下一个坐标。
*   最后，打印所有坐标。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the queen
// closest to king in an
// attacking position
int dis(vector<int> ans,
        vector<int> attacker)
{
    return abs(ans[0] - attacker[0])
           + abs(ans[1] - attacker[1]);
}

// Function to find all the queens
// attacking the king in the chessboard
vector<vector<int> > findQueens(
    vector<vector<int> >& queens,
    vector<int>& king)
{
    vector<vector<int> > sol;
    vector<vector<int> > attackers(8);

    // Iterating over the coordinates
    // of the queens
    for (int i = 0; i < queens.size(); i++) {

        // If king is horizontally on
        // the right of current queen
        if (king[0] == queens[i][0]
            && king[1] > queens[i][1]) {

            // If no attacker is present
            // in that direction
            if ((attackers[3].size() == 0)

                // Or if the current queen is
                // closest in that direction
                || (dis(attackers[3], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[3] = queens[i];
        }

        // If king is horizontally on
        // the left of current queen
        if (king[0] == queens[i][0]
            && king[1] < queens[i][1]) {

            // If no attacker is present
            // in that direction
            if ((attackers[4].size() == 0)

                // Or if the current queen is
                // closest in that direction
                || (dis(attackers[4], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[4] = queens[i];
        }

        // If the king is attacked by a
        // queen from the left by a queen
        // diagonal above
        if (king[0] - queens[i][0]
                == king[1] - queens[i][1]
            && king[0] > queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[0].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[0], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[0] = queens[i];
        }

        // If the king is attacked by a
        // queen from the left by a queen
        // diagonally below
        if (king[0] - queens[i][0]
                == king[1] - queens[i][1]
            && king[0] < queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[7].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[7], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[7] = queens[i];
        }

        // If the king is attacked by a
        // queen from the right by a queen
        // diagonally above
        if (king[1] - queens[i][1] == 0
            && king[0] > queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[1].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[1], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[1] = queens[i];
        }

        // If the king is attacked by a
        // queen from the right by a queen
        // diagonally below
        if (king[1] - queens[i][1] == 0
            && king[0] < queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[6].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[6], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[6] = queens[i];
        }

        // If a king is vertically below
        // the current queen
        if (king[0] - queens[i][0]
                == -(king[1] - queens[i][1])
            && king[0] > queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[2].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[2], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[2] = queens[i];
        }

        // If a king is vertically above
        // the current queen
        if (king[0] - queens[i][0]
                == -(king[1] - queens[i][1])
            && king[0] < queens[i][0]) {

            // If no attacker is present in
            // that direction
            if ((attackers[5].size() == 0)

                // Or the current queen is
                // the closest attacker in
                // that direction
                || (dis(attackers[5], king)
                    > dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[5] = queens[i];
        }
    }

    for (int i = 0; i < 8; i++)
        if (attackers[i].size())
            sol.push_back(attackers[i]);

    // Return the coordinates
    return sol;
}

// Print all the coordinates of the
// queens attacking the king
void print(vector<vector<int> > ans)
{
    for (int i = 0; i < ans.size();
         i++) {

        for (int j = 0; j < 2; j++)
            cout << ans[i][j] << " ";

        cout << "\n";
    }
}

// Driver Code
int main()
{
    vector<int> king = { 2, 3 };

    vector<vector<int> > queens
        = { { 0, 1 }, { 1, 0 },
            { 4, 0 }, { 0, 4 },
            { 3, 3 }, { 2, 4 } };

    vector<vector<int> > ans
        = findQueens(queens, king);

    print(ans);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;
import java.util.stream.Collectors;

class GFG{

// Method to find the queen closest
// to king in an attacking position
private static int dis(int[] ans, int[] attacker)
{
    return Math.abs(ans[0] - attacker[0]) +
           Math.abs(ans[1] - attacker[1]);
}

// Method to find all the queens
// attacking the king in the chessboard
private static List<List<Integer>> findQueens(
    int[][] queens, int[] king)
{
    List<List<Integer>> sol = new ArrayList<List<Integer>>();
    int[][] attackers = new int[8][2];

    for(int i = 0; i < 8; i++)
    {
        Arrays.fill(attackers[i], -1);
    }

    for(int i = 0; i < queens.length; i++)
    {

        // If king is horizontally on
        // the right of current queen
        if (king[0] == queens[i][0] &&
            king[1] > queens[i][1])
        {

            // If no attacker is present
            // in that direction
            if ((attackers[3][0] == -1) ||

                // Or if the current queen is
                // closest in that direction
                (dis(attackers[3], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[3] = queens[i];
        }

        // If king is horizontally on
        // the left of current queen
        if (king[0] == queens[i][0] &&
            king[1] < queens[i][1])
        {

            // If no attacker is present
            // in that direction
            if ((attackers[4][0] == -1) ||

                // Or if the current queen is
                // closest in that direction
                (dis(attackers[4], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[4] = queens[i];
        }

        // If the king is attacked by a
        // queen from the left by a queen
        // diagonal above
        if (king[0] - queens[i][0] ==
            king[1] - queens[i][1] &&
            king[0] > queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[0][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
                (dis(attackers[0], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[0] = queens[i];
        }

        // If the king is attacked by a
        // queen from the left by a queen
        // diagonally below
        if (king[0] - queens[i][0] ==
            king[1] - queens[i][1] &&
            king[0] < queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[7][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
               (dis(attackers[7], king) >
                   dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[7] = queens[i];
        }

        // If the king is attacked by a
        // queen from the right by a queen
        // diagonally above
        if (king[1] - queens[i][1] == 0 &&
            king[0] > queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[1][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
                (dis(attackers[1], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[1] = queens[i];
        }

        // If the king is attacked by a
        // queen from the right by a queen
        // diagonally below
        if (king[1] - queens[i][1] == 0 &&
            king[0] < queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[6][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
                (dis(attackers[6], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[6] = queens[i];
        }

        // If a king is vertically below
        // the current queen
        if (king[0] - queens[i][0] ==
          -(king[1] - queens[i][1]) &&
            king[0] > queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[2][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
                (dis(attackers[2], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[2] = queens[i];
        }

        // If a king is vertically above
        // the current queen
        if (king[0] - queens[i][0] ==
          -(king[1] - queens[i][1]) &&
            king[0] < queens[i][0])
        {

            // If no attacker is present in
            // that direction
            if ((attackers[5][0] == -1) ||

                // Or the current queen is
                // the closest attacker in
                // that direction
                (dis(attackers[5], king) >
                    dis(queens[i], king)))

                // Set current queen as
                // the attacker
                attackers[5] = queens[i];
        }
    }

    for(int i = 0; i < 8; i++)
        if (attackers[i][0] != -1)
            sol.add(
                Arrays.stream(
                    attackers[i]).boxed().collect(
                        Collectors.toList()));

    // Return the coordinates
    return sol;
}

// Print all the coordinates of the
// queens attacking the king
private static void print(List<List<Integer>> ans)
{
    for(int i = 0; i < ans.size(); i++)
    {
        for(int j = 0; j < 2; j++)
            System.out.print(ans.get(i).get(j) + " ");

        System.out.println();
    }
}

// Driver Code
public static void main(String[] args)
{
    int[] king = { 2, 3 };

    int[][] queens = { { 0, 1 }, { 1, 0 },
                       { 4, 0 }, { 0, 4 },
                       { 3, 3 }, { 2, 4 } };

    List<List<Integer>> ans = findQueens(queens, king);

    print(ans);
}
}

// This code is contributed by jithin
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the queen
# closest to king in an
# attacking position
def dis(ans, attacker):

    return (abs(ans[0] - attacker[0]) +
            abs(ans[1] - attacker[1]))

# Function to find all the
# queens attacking the king
# in the chessboard
def findQueens(queens, king):

    sol = []
    attackers = [[0 for x in range(8)]
                    for y in range(8)]

    # Iterating over the coordinates
    # of the queens
    for i in range(len(queens)):

        # If king is horizontally on
        # the right of current queen
        if (king[0] == queens[i][0] and
            king[1] > queens[i][1]):

            # If no attacker is present
            # in that direction
            if ((len(attackers[3]) == 0)

                # Or if the current queen is
                # closest in that direction
                or ((dis(attackers[3], king) >
                     dis(queens[i], king)))):               

                # Set current queen as
                # the attacker
                attackers[3] = queens[i];

        # If king is horizontally on
        # the left of current queen
        if (king[0] == queens[i][0] and
            king[1] < queens[i][1]):

            # If no attacker is present
            # in that direction
            if ((len(attackers[4]) == 0)

                # Or if the current queen is
                # closest in that direction
                or (dis(attackers[4], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[4] = queens[i];

        # If the king is attacked by a
        # queen from the left by a queen
        # diagonal above
        if (king[0] - queens[i][0] ==
            king[1] - queens[i][1] and
            king[0] > queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[0]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[0], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[0] = queens[i]

        # If the king is attacked by a
        # queen from the left by a queen
        # diagonally below
        if (king[0] - queens[i][0] ==
            king[1] - queens[i][1] and
            king[0] < queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[7]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[7], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[7] = queens[i]

        # If the king is attacked by a
        # queen from the right by a queen
        # diagonally above
        if (king[1] - queens[i][1] == 0 and
            king[0] > queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[1]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[1], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[1] = queens[i]

        # If the king is attacked by a
        # queen from the right by a queen
        # diagonally below
        if (king[1] - queens[i][1] == 0 and
            king[0] < queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[6]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[6], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[6] = queens[i];

        # If a king is vertically below
        # the current queen
        if (king[0] - queens[i][0] ==
            -(king[1] - queens[i][1]) and
            king[0] > queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[2]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[2], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[2] = queens[i]

        # If a king is vertically above
        # the current queen
        if (king[0] - queens[i][0] ==
          -(king[1] - queens[i][1]) and
            king[0] < queens[i][0]):

            # If no attacker is present in
            # that direction
            if ((len(attackers[5]) == 0)

                # Or the current queen is
                # the closest attacker in
                # that direction
                or (dis(attackers[5], king) >
                    dis(queens[i], king))):

                # Set current queen as
                # the attacker
                attackers[5] = queens[i]

    for i in range(8):
        f = 1
        for x in attackers[i]:
          if x != 0:
            f = 0
            break
        if f == 0:
          sol.append(attackers[i])

    # Return the coordinates
    return sol

# Print all the coordinates of the
# queens attacking the king
def print_board(ans):

    for i in range(len(ans)):
        for j in range(2):
            print(ans[i][j],
                  end = " ")

        print()

# Driver Code
if __name__ == "__main__":

    king = [2, 3]
    queens = [[0, 1], [1, 0],
              [4, 0], [0, 4],
              [3, 3], [2, 4]]
    ans = findQueens(queens, king);
    print_board(ans);

# This code is contributed by Chitranayal
```

**Output:** 

```
0 1 
2 4 
3 3

```

***时间复杂度:** O(N)，其中 N 为皇后*
***数量辅助空间:** O(N)*