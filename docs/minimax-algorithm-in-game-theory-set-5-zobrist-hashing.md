# 博弈论中的极小极大算法|集合 5 (Zobrist Hashing)

> 原文:[https://www . geesforgeks . org/minimax-博弈论中的算法-set-5-zobrist-hashing/](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-5-zobrist-hashing/)

之前关于这个话题的帖子:[博弈论中的极小极大算法](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-1-introduction/)、[博弈论中的评估函数](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-2-evaluation-function/)、[井字游戏 AI–寻找最优移动](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-3-tic-tac-toe-ai-finding-optimal-move/)、[α-β修剪](https://www.geeksforgeeks.org/minimax-algorithm-in-game-theory-set-4-alpha-beta-pruning/)。

Zobrist Hashing 是一个哈希函数，广泛用于 2 人棋盘游戏。这是换位表中最常用的散列函数。换位表基本上存储以前电路板状态的评估值，因此如果再次遇到这些值，我们只需从换位表中检索存储的值。我们将在后面的文章中介绍换位表。在本文中，我们将以棋盘为例，实现一个散列函数。

#### 伪代码:

```
// A matrix with random numbers initialized once
Table[#ofBoardCells][#ofPieces] 

// Returns Zobrist hash function for current conf-
// iguration of board.
function findhash(board):
    hash = 0
    for each cell on the board :
        if cell is not empty :
            piece = board[cell]
            hash ^= table[cell][piece]
    return hash

```

#### 解释:

Zobrist Hashing 背后的思想是，对于给定的板状态，如果在给定的单元上有一块，我们使用表中相应单元的那块的随机数。

如果随机数中的位数越多，哈希冲突的可能性就越小。因此，通常使用 64 位数字作为标准，这样大的数字不太可能发生哈希冲突。在程序执行期间，该表只需初始化一次。

Zobrist Hashing 之所以在棋盘游戏中被广泛使用，也是因为当玩家移动时，不需要从头开始重新计算 hash 值。由于异或运算的性质，我们可以简单地使用一些异或运算来重新计算哈希值。

#### 实施:

我们将尝试为给定的电路板配置找到一个哈希值。

```
// A program to illustrate Zobeist Hashing Algorithm
#include <bits/stdc++.h>
using namespace std;

unsigned long long int ZobristTable[8][8][12];
mt19937 mt(01234567);

// Generates a Randome number from 0 to 2^64-1
unsigned long long int randomInt()
{
    uniform_int_distribution<unsigned long long int>
                                 dist(0, UINT64_MAX);
    return dist(mt);
}

// This function associates each piece with
// a number
int indexOf(char piece)
{
    if (piece=='P')
        return 0;
    if (piece=='N')
        return 1;
    if (piece=='B')
        return 2;
    if (piece=='R')
        return 3;
    if (piece=='Q')
        return 4;
    if (piece=='K')
        return 5;
    if (piece=='p')
        return 6;
    if (piece=='n')
        return 7;
    if (piece=='b')
        return 8;
    if (piece=='r')
        return 9;
    if (piece=='q')
        return 10;
    if (piece=='k')
        return 11;
    else
        return -1;
}

// Initializes the table
void initTable()
{
    for (int i = 0; i<8; i++)
      for (int j = 0; j<8; j++)
        for (int k = 0; k<12; k++)
          ZobristTable[i][j][k] = randomInt();
}

// Computes the hash value of a given board
unsigned long long int computeHash(char board[8][9])
{
    unsigned long long int h = 0;
    for (int i = 0; i<8; i++)
    {
        for (int j = 0; j<8; j++)
        {
            if (board[i][j]!='-')
            {
                int piece = indexOf(board[i][j]);
                h ^= ZobristTable[i][j][piece];
            }
        }
    }
    return h;
}

// Main Function
int main()
{
    // Uppercase letters are white pieces
    // Lowercase letters are black pieces
    char board[8][9] =
    {
        "---K----",
        "-R----Q-",
        "--------",
        "-P----p-",
        "-----p--",
        "--------",
        "p---b--q",
        "----n--k"
    };

    initTable();

    unsigned long long int hashValue = computeHash(board);
    printf("The hash value is     : %llu\n", hashValue);

    //Move the white king to the left
    char piece = board[0][3];

    board[0][3] = '-';
    hashValue ^= ZobristTable[0][3][indexOf(piece)];

    board[0][2] = piece;
    hashValue ^= ZobristTable[0][2][indexOf(piece)];

    printf("The new hash value is : %llu\n", hashValue);

    // Undo the white king move
    piece = board[0][2];

    board[0][2] = '-';
    hashValue ^= ZobristTable[0][2][indexOf(piece)];

    board[0][3] = piece;
    hashValue ^= ZobristTable[0][3][indexOf(piece)];

    printf("The old hash value is : %llu\n", hashValue);

    return 0;
}
```

#### 输出:

```
The hash value is     : 14226429382419125366
The new hash value is : 15124945578233295113
The old hash value is : 14226429382419125366

```

本文由 [**阿克谢·L·阿拉德亚**](http://dollarakshay.com) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。