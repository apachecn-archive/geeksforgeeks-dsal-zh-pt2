# 赢家最多玩的游戏

> 原文:[https://www.geeksforgeeks.org/maximum-games-played-winner/](https://www.geeksforgeeks.org/maximum-games-played-winner/)

有 N 个玩家正在玩锦标赛。我们需要找到获胜者可以玩的最大游戏数量。在这个锦标赛中，只有当两个玩家玩的游戏之间的差异不超过一个时，才允许他们互相对战。
**例:**

```
Input  : N = 3
Output : 2
Maximum games winner can play = 2
Assume that player are P1, P2 and P3
First, two players will play let (P1, P2)
Now winner will play against P3, 
making total games played by winner = 2

Input  : N = 4
Output : 2
Maximum games winner can play = 2
Assume that player are P1, P2, P3 and P4
First two pairs will play lets (P1, P2) and 
(P3, P4). Now winner of these two games will 
play against each other, making total games
played by winner = 2
```

我们可以通过首先计算所需的最小玩家数量来解决这个问题，这样获胜者将玩 x 个游戏。一旦计算出来，实际问题就正好相反。现在假设 dp[i]表示需要的最小玩家数量，以便赢家玩 I 游戏。我们可以将 dp 值之间的递归关系写成，
DP[I+1]= DP[I]+DP[I–1]，因为如果亚军参加了(I–1)场比赛，而胜者参加了 I 场比赛，并且所有与他们比赛的玩家都不相交，那么胜者参加的比赛总数将是这两组玩家的总和。
上面的递归关系可以写成 DP[I]= DP[I–1]+DP[I–2]
这和斐波那契数列关系是一样的，所以我们最终的答案会是输入中小于等于给定玩家数的最大斐波那契数的指数。

## C++

```
// C/C++ program to find maximum number of
// games played by winner
#include <bits/stdc++.h>
using namespace std;

// method returns maximum games a winner needs
// to play in N-player tournament
int maxGameByWinner(int N)
{
    int dp[N];

    // for 0 games, 1 player is needed
    // for 1 game, 2 players are required
    dp[0] = 1;   
    dp[1] = 2;

    // loop until i-th Fibonacci number is 
    // less than or equal to N
    int i = 2;
    do {
        dp[i] = dp[i - 1] + dp[i - 2];
    } while (dp[i++] <= N);

    // result is (i - 2) because i will be
    // incremented one extra in while loop
    // and we want the last value which is
    // smaller than N, so one more decrement
    return (i - 2);
}

// Driver code to test above methods
int main()
{
    int N = 10;
    cout << maxGameByWinner(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find maximum number of
// games played by winner
class Max_game_winner {

    // method returns maximum games a winner needs
    // to play in N-player tournament
    static int maxGameByWinner(int N)
    {
        int[] dp = new int[N];

        // for 0 games, 1 player is needed
        // for 1 game, 2 players are required
        dp[0] = 1;   
        dp[1] = 2;

        // loop until i-th Fibonacci number is 
        // less than or equal to N
        int i = 2;
        do {
            dp[i] = dp[i - 1] + dp[i - 2];
        } while (dp[i++] <= N);

        // result is (i - 2) because i will be
        // incremented one extra in while loop
        // and we want the last value which is
        // smaller than N, so one more decrement
        return (i - 2);
    }

    // Driver code to test above methods
    public static void main(String args[])
    {
        int N = 10;
        System.out.println(maxGameByWinner(N));
    }
}
//This code is contributed by Sumit Ghosh
```

## 蟒蛇 3

```
# Python3 program to find maximum
# number of games played by winner

# method returns maximum games
# a winner needs to play in
# N-player tournament

def maxGameByWinner(N):
    dp = [0 for i in range(N)]

    # for 0 games, 1 player is needed
    # for 1 game, 2 players are required
    dp[0] = 1
    dp[1] = 2

    # loop until i-th Fibonacci
    # number is less than or
    # equal to N
    i = 1
    while dp[i] <= N:
        i = i + 1
        dp[i] = dp[i - 1] + dp[i - 2]

    # result is (i - 1) because i will be
    # incremented one extra in while loop
    # and we want the last value which is
    # smaller than N, so
    return (i - 1)

# Driver code
N = 10
print(maxGameByWinner(N))

# This code is contributed
# by sahilshelangia
```

## C#

```
// C# program to find maximum number
// of games played by winner
using System;

class GFG {

    // method returns maximum games a
    // winner needs to play in N-player
    // tournament
    static int maxGameByWinner(int N)
    {
        int[] dp = new int[N];

        // for 0 games, 1 player is needed
        // for 1 game, 2 players are required
        dp[0] = 1;
        dp[1] = 2;

        // loop until i-th Fibonacci number
        // is less than or equal to N
        int i = 2;

        do {
            dp[i] = dp[i - 1] + dp[i - 2];
        } while (dp[i++] <= N);

        // result is (i - 2) because i will be
        // incremented one extra in while loop
        // and we want the last value which is
        // smaller than N, so one more decrement
        return (i - 2);
    }

    // Driver code
    public static void Main()
    {
        int N = 10;
        Console.Write(maxGameByWinner(N));
    }
}

// This code is contributed by Nitin Mittal.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find maximum number
// of games played by winner

// Method returns maximum games
// a winner needs to play in
// N-player tournament
function maxGameByWinner($N)
{
    $dp[$N]=0;

    // for 0 games, 1 player is needed
    // for 1 game, 2 players are required
    $dp[0] = 1;
    $dp[1] = 2;

    // loop until i-th Fibonacci number is
    // less than or equal to N
    $i = 2;
    do
    {
        $dp[$i] = $dp[$i - 1] + $dp[$i - 2];
    } while ($dp[$i++] <= $N);

    // result is (i - 2) because i will be
    // incremented one extra in while loop
    // and we want the last value which is
    // smaller than N, so one more decrement
    return ($i - 2);
}

    // Driver Code
    $N = 10;
    echo maxGameByWinner($N);

// This code is contributed by nitin mittal
?>
```

## java 描述语言

```
<script>

// Javascript program to find maximum number of
// games played by winner

    // method returns maximum games a winner needs
    // to play in N-player tournament
    function maxGameByWinner(N)
    {
        let dp = new Array(N).fill(0);

        // for 0 games, 1 player is needed
        // for 1 game, 2 players are required
        dp[0] = 1;   
        dp[1] = 2;

        // loop until i-th Fibonacci number is 
        // less than or equal to N
        let i = 2;
        do {
            dp[i] = dp[i - 1] + dp[i - 2];
        } while (dp[i++] <= N);

        // result is (i - 2) because i will be
        // incremented one extra in while loop
        // and we want the last value which is
        // smaller than N, so one more decrement
        return (i - 2);
    }

// driver program

        let N = 10;
        document.write(maxGameByWinner(N));

// This code is contributed by code_hunt.
</script>
```

**输出:**

```
4
```

本文由 [**乌卡什·特里维迪**](https://in.linkedin.com/in/utkarsh-trivedi-253069a7) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。