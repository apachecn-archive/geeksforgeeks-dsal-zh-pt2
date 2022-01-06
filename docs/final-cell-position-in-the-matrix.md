# 矩阵中的最终单元位置

> 原文:[https://www . geesforgeks . org/final-cell-in-matrix 位置/](https://www.geeksforgeeks.org/final-cell-position-in-the-matrix/)

给定命令列表 U(上)、D(下)、L(左)和 R(右)以及矩阵中初始单元格位置(x，y)的数组。遵循给定的命令，找到对象在矩阵中的最终单元格位置。假设最终所需的单元位置存在于矩阵中。
**例** :

```
Input : command[] = "DDLRULL"
        x = 3, y = 4
Output : (1, 5)

Input : command[] = "LLRUUUDRRDDDULRLLUDUUR"
        x = 6, y = 5
Output : (6, 3)
```

来源: [Flipkart 访谈(SDE-校园一号)。](https://www.geeksforgeeks.org/flipkart-interview-sde-1-on-campus/)

**进场:**以下为步骤:

1.  分别计算 U(上)、D(下)、L(左)和 R(右)运动的杯、杯口、裂缝和裂缝。
2.  计算 final _ x = x+(cright–child)和 final _ y = y+(cdown–cup)。

最终单元格位置为(final_x，final_y)

## C++

```
// C++ implementation to find the final cell position
// in the given matrix
#include <bits/stdc++.h>

using namespace std;

// function to find the final cell position
// in the given matrix
void finalPos(char command[], int n,
              int x, int y)
{
    // to count up, down, left and cright
    // movements
    int cup, cdown, cleft, cright;

    // to store the final coordinate position
    int final_x, final_y;

    cup = cdown = cleft = cright = 0;

    // traverse the command array
    for (int i = 0; i < n; i++) {
        if (command[i] == 'U')
            cup++;
        else if (command[i] == 'D')
            cdown++;
        else if (command[i] == 'L')
            cleft++;
        else if (command[i] == 'R')
            cright++;
    }

    // calculate final values
    final_x = x + (cright - cleft);
    final_y = y + (cdown - cup);

    cout << "Final Position: "
         << "("
         << final_x << ", " << final_y << ")";
}

// Driver program to test above
int main()
{
    char command[] = "DDLRULL";
    int n = (sizeof(command) / sizeof(char)) - 1;
    int x = 3, y = 4;
    finalPos(command, n, x, y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// the final cell position
// in the given matrix
import java.util.*;
import java.lang.*;
import java.io.*;

class GFG
{
// function to find the
// final cell position
// in the given matrix
static void finalPos(String command, int n,
                              int x, int y)
{
    // to count up, down, left
    // and cright movements
    int cup, cdown, cleft, cright;

    // to store the final
    // coordinate position
    int final_x, final_y;

    cup = cdown = cleft = cright = 0;

    // traverse the command array
    for (int i = 0; i < n; i++)
    {
        if (command.charAt(i) == 'U')
            cup++;
        else if (command.charAt(i) == 'D')
            cdown++;
        else if (command.charAt(i)== 'L')
            cleft++;
        else if (command.charAt(i) == 'R')
            cright++;
    }

    // calculate final values
    final_x = x + (cright - cleft);
    final_y = y + (cdown - cup);

    System.out.println("Final Position: " +
                       "(" + final_x + ", " +
                              final_y + ")");
}

// Driver Code
public static void main(String []args)
{
    String command = "DDLRULL";
    int n = command.length();
    int x = 3, y = 4;
    finalPos(command, n, x, y);
}
}

// This code is contributed
// by Subhadeep
```

## C#

```
// C# implementation to find
// the final cell position
// in the given matrix
class GFG
{
// function to find the
// final cell position
// in the given matrix
static void finalPos(string command, int n,
                              int x, int y)
{
    // to count up, down, left
    // and cright movements
    int cup, cdown, cleft, cright;

    // to store the final
    // coordinate position
    int final_x, final_y;

    cup = cdown = cleft = cright = 0;

    // traverse the command array
    for (int i = 0; i < n; i++)
    {
        if (command[i] == 'U')
            cup++;
        else if (command[i] == 'D')
            cdown++;
        else if (command[i]== 'L')
            cleft++;
        else if (command[i] == 'R')
            cright++;
    }

    // calculate final values
    final_x = x + (cright - cleft);
    final_y = y + (cdown - cup);

    System.Console.WriteLine("Final Position: " +
                             "(" + final_x + ", " +
                                    final_y + ")");
}

// Driver Code
public static void Main()
{
    string command = "DDLRULL";
    int n = command.Length;
    int x = 3, y = 4;
    finalPos(command, n, x, y);
}
}

// This code is contributed
// by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation to find the final
// cell position in the given matrix

// function to find the final cell
// position in the given matrix
function finalPos($command, $n, $x, $y)
{
    // to count up, down, left and
    // cright movements
    $cup; $cdown; $cleft; $cright;

    // to store the final coordinate
    // position
    $final_x; $final_y;

    $cup = $cdown = $cleft = $cright = 0;

    // traverse the command array
    for ($i = 0; $i < $n; $i++)
    {
        if ($command[$i] == 'U')
            $cup++;
        else if ($command[$i] == 'D')
            $cdown++;
        else if ($command[$i] == 'L')
            $cleft++;
        else if ($command[$i] == 'R')
            $cright++;
    }

    // calculate final values
    $final_x = $x + ($cright - $cleft);
    $final_y = $y + ($cdown - $cup);

    echo "Final Position: " . "(" .
                  $final_x . ", " .
                  $final_y . ")";
}

// Driver Code
$command = "DDLRULL";
$n = strlen($command);
$x = 3; $y = 4;
finalPos($command, $n, $x, $y);

// This code is contributed
// by Akanksha Rai
```

## java 描述语言

```
<script>

// JavaScript implementation to find
// the final cell position
// in the given matrix

// function to find the
// final cell position
// in the given matrix
function finalPos(command, n, x, y)
{
    // to count up, down, left
    // and cright movements
    let cup, cdown, cleft, cright;

    // to store the final
    // coordinate position
    let final_x, final_y;

    cup = cdown = cleft = cright = 0;

    // traverse the command array
    for (let i = 0; i < n; i++)
    {
        if (command[i] == 'U')
            cup++;
        else if (command[i] == 'D')
            cdown++;
        else if (command[i]== 'L')
            cleft++;
        else if (command[i] == 'R')
            cright++;
    }

    // calculate final values
    final_x = x + (cright - cleft);
    final_y = y + (cdown - cup);

    document.write("Final Position: " +
                             "(" + final_x + ", " +
                                    final_y + ")");
}

// driver code

    let command = "DDLRULL";
    let n = command.length;
    let x = 3, y = 4;
    finalPos(command, n, x, y);

</script>
```

**输出:**

```
Final Position: (1, 5)
```

**时间复杂度** : O(n)，其中![n  ](img/31d70d7c99878a33c601d487c9b6eb43.png "Rendered by QuickLaTeX.com")为命令数。