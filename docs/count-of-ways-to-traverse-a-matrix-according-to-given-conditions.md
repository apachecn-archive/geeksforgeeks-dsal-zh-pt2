# 根据给定条件遍历矩阵的次数

> 原文:[https://www . geeksforgeeks . org/根据给定条件遍历矩阵的次数/](https://www.geeksforgeeks.org/count-of-ways-to-traverse-a-matrix-according-to-given-conditions/)

给定一个整数 **N** ，它代表一个 **N x N** 正方形矩阵，任务是通过以下条件打印从正方形矩阵的左上角移动到右下角的方式数:

*   如果指针的当前位置在正方形矩阵的边缘，那么下一步可以是垂直或水平移动，任何步数(像棋盘上的**车**)。
*   如果指针的当前位置在方阵的对角线上，那么下一步也应该在对角线上。(就像棋盘上的**主教**)。
*   如果指针的当前位置在上述两个位置之外的任何位置，那么下一个可能的步骤可以是任何方式，就像**骑士**在棋盘上移动，但是新位置的行列>在旧位置的行列中。

**示例:**

> **输入:** N = 2
> **输出:** 3
> **解释:**
> 三种可能的方式是:
> { 0-0 }–{ 0-1 }–{ 1-1 }
> { 0-0 }–{ 1-0 }–{ 1-1 }
> { 0-0 }–{ 1-1 }
> **输入:** 3
> **输出:** 18
> –{ 1-2 }–{ 2-2 }
> { 0-0 }–{ 0-1 }–{ 0-2 }–{ 2-2 }
> { 0-0 }–{ 0-1 }–{ 1-1 }–{ 2-2 }
> { 0-0 }–{ 0-1 }–{ 2-1 }–{ 2-2 }
> { 0-0 }–{ 0-2 }–{ 1-2 }–{ 2-2 }
> { 0-0 }–{ 0-2 }– –{ 2-2 }
> { 0-0 }–{ 2-0 }–{ 2-1 }–{ 2-2 }
> { 0-0 }–{ 2-0 }–{ 2-2 }
> { 0-0 }–{ 1-1 }–{ 2-2 }
> { 0-0 }–{ 2-2 }

**方法:**思路是[递归](https://www.geeksforgeeks.org/recursion/)检查每一个可能的情况是否到达方阵的末尾。为此，定义了一个递归函数，该函数将当前位置和最后一个位置作为输入参数。以下是递归函数的条件:

*   **基本情况:**函数的基本情况是检查当前指针是否已经到达正方形矩阵中的右下角位置。如果达到，则记录总路数的计数器**计数**递增。如果不能到达最后一个位置，那么函数应该停止，不应该在下一次迭代中调用。这通过以下方式实现:

```
if (cr == er && cc == ec) {
    count++;
    return;
}

if (cr > er || cc > ec) {
   return;
}
```

*   **递归情况:**假设三种类型的遍历是可能的。因此，递归的情况是通过检查当前位置是否递归调用函数。如果当前位置位于方形矩阵的边缘，则指针只能水平或垂直移动。对于每个后续的垂直遍历，水平和垂直遍历还有两种选择。因此，为了跟踪路的总数，这两者都在循环中递归调用。

```
for (int i = 1; i <= er; i++) {
    if (cc == 0 || cr == 0 
       || cr == er || cc == ec) {
        chessboard1(cr, cc + i, er, ec);
    }
}

for (int i = 1; i <= er; i++) {
    if (cc == 0 || cr == 0 
       || cr == er || cc == ec) {
        chessboard1(cr + i, cc, er, ec);
    }
}
```

*   除此之外，如果当前指针在对角线上，那么指针可以对角移动。然而，对于每个后续对角线遍历，另一组后续对角线是可能的。因此，为了跟踪路的总数，使用 for 循环递归调用函数。

```
for (int i = 1; i <= er; i++) {
    if (cr == cc || cr + cc == er) {
        chessboard1(cr + i, cc + i,
                    er, ec);
    }
}
```

*   如果上述情况都不满足，则可以移动下一个位置:
    *   新行>旧行。
    *   新列>旧列。
*   执行上述函数后， **count** 变量中存储的值是遍历方阵的总次数。

以下是上述方法的实现:

## C++

```
// C++ program to count the number
// of ways to traverse the given
// N x N Square Matrix recursively
#include<bits/stdc++.h>
using namespace std;

// Variable to store the
// total number of ways to
// traverse the Square Matrix

// Function to recursively
// count the total number
// of ways to traverse the
// given N x N Square Matrix
void chessboard1(int cr, int cc,
                 int er, int ec,
                 int& count)
{

  // If the last index has been
  // reached, then the count is
  // incremented and returned
  if (cr == er && cc == ec)
  {
    count++;
    return;
  }

  // If the last index cannot
  // be reached
  if (cr > er || cc > ec)
  {
    return;
  }

  // If the current position is
  // neither on the edges nor
  // on the diagonal, then the
  // pointer moves like a knight
  chessboard1(cr + 2, cc + 1,
              er, ec,count);
  chessboard1(cr + 1, cc + 2,
              er, ec,count);

  // If the pointer is on the
  // edges of the Square Matrix
  // next move can be horizontal
  // or vertical

  // This for loop is used to include
  // all the horizontal traversal cases
  // recursively
  for (int i = 1; i <= er; i++)
  {
    if (cc == 0 || cr == 0||
        cr == er || cc == ec)
    {
      chessboard1(cr, cc + i,
                  er, ec,count);
    }
  }

  // This for loop is used to include
  // all the vertical traversal cases
  // recursively
  for (int i = 1; i <= er; i++)
  {
    if (cc == 0 || cr == 0||
        cr == er || cc == ec)
    {
      chessboard1(cr + i, cc,
                  er, ec,count);
    }
  }

  // If the pointer is on the
  // diagonal of the Square Matrix
  // next move is also diagonal.
  // For loop is used to include
  // all the diagonal traversal cases.
  for (int i = 1; i <= er; i++)
  {
    if (cr == cc || cr + cc == er)
    {
      chessboard1(cr + i,  cc + i, 
                  er, ec, count);
    }
  }
}

// Driver code
int main()
{
  int N = 3;
  int count=0;
  chessboard1(0, 0, N - 1, N - 1,count);
  cout<<count;
}

// This code is contributed by chahattekwani71
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count the number
// of ways to traverse the given
// N x N Square Matrix recursively

public class GFG {

    // Variable to store the total number
    // of ways to traverse the Square Matrix
    static int count = 0;

    // Function to recursively
    // count the total number
    // of ways to traverse the
    // given N x N Square Matrix
    public static void chessboard1(
        int cr, int cc,
        int er, int ec)
    {

        // If the last index has been reached, then
        // the count is incremented and returned
        if (cr == er && cc == ec) {
            count++;
            return;
        }

        // If the last index cannot be reached
        if (cr > er || cc > ec) {
            return;
        }

        // If the current position is neither
        // on the edges nor on the diagonal,
        // then the pointer moves
        // like a knight
        chessboard1(cr + 2, cc + 1, er, ec);
        chessboard1(cr + 1, cc + 2, er, ec);

        // If the pointer is on the
        // edges of the Square Matrix
        // next move can be horizontal or vertical

        // This for loop is used to include all the
        // horizontal traversal cases recursively
        for (int i = 1; i <= er; i++) {
            if (cc == 0 || cr == 0
                || cr == er || cc == ec) {
                chessboard1(cr, cc + i, er, ec);
            }
        }

        // This for loop is used to include all the
        // vertical traversal cases recursively
        for (int i = 1; i <= er; i++) {
            if (cc == 0 || cr == 0
                || cr == er || cc == ec) {
                chessboard1(cr + i, cc, er, ec);
            }
        }

        // If the pointer is on the
        // diagonal of the Square Matrix
        // next move is also diagonal.
        // For loop is used to include
        // all the diagonal traversal cases.
        for (int i = 1; i <= er; i++) {
            if (cr == cc
                || cr + cc == er) {

                chessboard1(cr + i,
                            cc + i,
                            er, ec);
            }
        }
    }

    // Driver code
    public static void main(String[] args)
    {

        int N = 3;
        chessboard1(0, 0, N - 1, N - 1);
        System.out.println(count);
    }
}
```

## 蟒蛇 3

```
# Python3 program to count the number
# of ways to traverse the given
# N x N Square Matrix recursively

# Variable to store the
# total number of ways to
# traverse the Square Matrix
count = 0

# Function to recursively
# count the total number
# of ways to traverse the
# given N x N Square Matrix
def chessboard1(cr, cc, er, ec):
  global count
  # If the last index has been
  # reached, then the count is
  # incremented and returned
  if cr == er and cc == ec:
    count+=1
    return

  # If the last index cannot
  # be reached
  if cr > er or cc > ec:
    return

  # If the current position is
  # neither on the edges nor
  # on the diagonal, then the
  # pointer moves like a knight
  chessboard1(cr + 2, cc + 1, er, ec)
  chessboard1(cr + 1, cc + 2, er, ec)

  # If the pointer is on the
  # edges of the Square Matrix
  # next move can be horizontal
  # or vertical

  # This for loop is used to include
  # all the horizontal traversal cases
  # recursively
  for i in range(1, er + 1):
    if (cc == 0 or cr == 0 or cr == er or cc == ec):
      chessboard1(cr, cc + i, er, ec)

  # This for loop is used to include
  # all the vertical traversal cases
  # recursively
  for i in range(1, er + 1):
    if cc == 0 or cr == 0 or cr == er or cc == ec:
      chessboard1(cr + i, cc,er, ec)

  # If the pointer is on the
  # diagonal of the Square Matrix
  # next move is also diagonal.
  # For loop is used to include
  # all the diagonal traversal cases.
  for i in range(1, er + 1):
    if cr == cc or (cr + cc) == er:
      chessboard1(cr + i, cc + i, er, ec)

N = 3
chessboard1(0, 0, N - 1, N - 1)
print(count)

# This code is contributed by suresh07.
```

## C#

```
// C# program to count the number
// of ways to traverse the given
// N x N Square Matrix recursively
using System;

class GFG{

// Variable to store the total number
// of ways to traverse the Square Matrix
static int count = 0;

// Function to recursively
// count the total number
// of ways to traverse the
// given N x N Square Matrix
public static void chessboard1(int cr, int cc,
                               int er, int ec)
{

    // If the last index has been reached, then
    // the count is incremented and returned
    if (cr == er && cc == ec)
    {
        count++;
        return;
    }

    // If the last index cannot be reached
    if (cr > er || cc > ec)
    {
        return;
    }

    // If the current position is neither
    // on the edges nor on the diagonal,
    // then the pointer moves
    // like a knight
    chessboard1(cr + 2, cc + 1, er, ec);
    chessboard1(cr + 1, cc + 2, er, ec);

    // If the pointer is on the edges
    // of the Square Matrix next move
    // can be horizontal or vertical

    // This for loop is used to include all the
    // horizontal traversal cases recursively
    for(int i = 1; i <= er; i++)
    {
        if (cc == 0 || cr == 0 ||
           cr == er || cc == ec)
        {
            chessboard1(cr, cc + i, er, ec);
        }
    }

    // This for loop is used to include all the
    // vertical traversal cases recursively
    for(int i = 1; i <= er; i++)
    {
        if (cc == 0 || cr == 0 ||
           cr == er || cc == ec)
        {
            chessboard1(cr + i, cc, er, ec);
        }
    }

    // If the pointer is on the
    // diagonal of the Square Matrix
    // next move is also diagonal.
    // For loop is used to include
    // all the diagonal traversal cases.
    for(int i = 1; i <= er; i++)
    {
        if (cr == cc || cr + cc == er)
        {
            chessboard1(cr + i, cc + i,
                        er, ec);
        }
    }
}

// Driver code
public static void Main(string[] args)
{
    int N = 3;

    chessboard1(0, 0, N - 1, N - 1);

    Console.Write(count);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to count the number
// of ways to traverse the given
// N x N Square Matrix recursively

// Variable to store the
// total number of ways to
// traverse the Square Matrix
let count = 0

// Function to recursively
// count the total number
// of ways to traverse the
// given N x N Square Matrix
function chessboard1(cr, cc, er, ec)
{

  // If the last index has been
  // reached, then the count is
  // incremented and returned
  if (cr == er && cc == ec)
  {
    count++;
    return;
  }

  // If the last index cannot
  // be reached
  if (cr > er || cc > ec)
  {
    return;
  }

  // If the current position is
  // neither on the edges nor
  // on the diagonal, then the
  // pointer moves like a knight
  chessboard1(cr + 2, cc + 1,
              er, ec);
  chessboard1(cr + 1, cc + 2,
              er, ec);

  // If the pointer is on the
  // edges of the Square Matrix
  // next move can be horizontal
  // or vertical

  // This for loop is used to include
  // all the horizontal traversal cases
  // recursively
  for (let i = 1; i <= er; i++)
  {
    if (cc == 0 || cr == 0||
        cr == er || cc == ec)
    {
      chessboard1(cr, cc + i, er, ec);
    }
  }

  // This for loop is used to include
  // all the vertical traversal cases
  // recursively
  for (let i = 1; i <= er; i++)
  {
    if (cc == 0 || cr == 0||
        cr == er || cc == ec)
    {
      chessboard1(cr + i, cc,er, ec);
    }
  }

  // If the pointer is on the
  // diagonal of the Square Matrix
  // next move is also diagonal.
  // For loop is used to include
  // all the diagonal traversal cases.
  for (let i = 1; i <= er; i++)
  {
    if (cr == cc || cr + cc == er)
    {
      chessboard1(cr + i, cc + i, er, ec);
    }
  }
}

// Driver Code
let N = 3;
chessboard1(0, 0, N - 1, N - 1,count);
document.write(count);

// This code is contributed by jana_sayantan.
</script>
```

**输出:**

```
18
```