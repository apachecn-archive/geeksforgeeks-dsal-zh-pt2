# 可以放置在 N*M 棋盘上的最大非攻击骑士数量

> 原文:[https://www . geesforgeks . org/maximum-非攻击-可放置在纳米棋盘上的骑士/](https://www.geeksforgeeks.org/maximum-non-attacking-knights-that-can-be-placed-on-an-nm-chessboard/)

给定一个 **N*M** 棋盘。任务是找到给定棋盘上可以放置的最大骑士数量，这样就不会有骑士攻击其他骑士。

**例**

> **输入:** N = 1，M = 4
> **输出:** 4
> 在棋盘的每个格子上放置一个骑士。
> 
> **输入:** N = 4，M = 5
> T3】输出: 10

**进场:**众所周知，一个骑士可以通过两种方式进行攻击。这里是他可以攻击的地方。
T3】

这里，在图片中，骑士是白色的，只攻击黑色。因此。我们得出结论，骑士只能攻击不同的颜色。
我们可以借助这个事实，并将其用于我们的目的。现在，我们知道骑士攻击不同的颜色，所以我们可以保持所有骑士在同一种颜色，即所有在白色或所有在黑色。从而使骑士数量达到最高。
要找到黑色或白色的数量，它只是船上总块数的一半。

> 总块数= n * m
> 相同颜色的块数= (n * m) / 2

**角箱:**

*   如果只有一行或一列。那么所有的方块都可以被骑士填满，因为骑士不能在同一行或同一列攻击。
    ![](img/2c58316735c1fa6dea4057b1707aa28f.png)
*   如果只有两行或两列。然后每两列(或行)将填充骑士，并且每连续两列(或行)将保持为空。如图所示。
    ![](img/5fa6f18b8359cd8cf90b3b26b28e0eb7.png)

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of the approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function to return the maximum number of
    // knights that can be placed on the given
    // chessboard such that no two
    // knights attack each other
    int max_knight(int n, int m)
    {

        // Check for corner case #1
        // If row or column is 1
        if (m == 1 || n == 1) {

            // If yes, then simply print total blocks
            // which will be the max of row or column
            return max(m, n);
        }

        // Check for corner case #2
        // If row or column is 2
        else if (m == 2 || n == 2) {

            // If yes, then simply calculate
            // consecutive 2 rows or columns
            int c = 0;
            c = (max(m, n) / 4) * 4;

            if (max(m, n) % 4 == 1) {
                c += 2;
            }
            else if (max(m, n) % 4 > 1) {
                c += 4;
            }
            return c;
        }

        // For general case, just print the
        // half of total blocks
        else {
            return (((m * n) + 1) / 2);
        }
    }

    // Driver code
    int main()
    {
        int n = 4, m = 5;

        cout << max_knight(n, m);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of the approach 
    import java.io.*;

    class GFG 
    {

    // Function to return the maximum number of 
    // knights that can be placed on the given 
    // chessboard such that no two 
    // knights attack each other 
    static int max_knight(int n, int m) 
    { 

        // Check for corner case #1 
        // If row or column is 1 
        if (m == 1 || n == 1) 
        { 

            // If yes, then simply print total blocks 
            // which will be the max of row or column 
            return Math.max(m, n); 
        } 

        // Check for corner case #2 
        // If row or column is 2 
        else if (m == 2 || n == 2) 
        { 

            // If yes, then simply calculate 
            // consecutive 2 rows or columns 
            int c = 0; 
            c = (Math.max(m, n) / 4) * 4; 

            if (Math.max(m, n) % 4 == 1)
            { 
                c += 2; 
            } 
            else if (Math.max(m, n) % 4 > 1) 
            { 
                c += 4; 
            } 
            return c; 
        } 

        // For general case, just print the 
        // half of total blocks 
        else 
        { 
            return (((m * n) + 1) / 2); 
        } 
    } 

    // Driver code 
    public static void main (String[] args) 
    {
        int n = 4, m = 5; 
        System.out.println (max_knight(n, m)); 
    }
    }

    // This code is contributed by ajit 
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation of the approach 

    # Function to return the maximum number of 
    # knights that can be placed on the given 
    # chessboard such that no two 
    # knights attack each other 
    def max_knight(n, m) : 

        # Check for corner case #1 
        # If row or column is 1 
        if (m == 1 or n == 1) :

            # If yes, then simply print total blocks 
            # which will be the max of row or column 
            return max(m, n); 

        # Check for corner case #2 
        # If row or column is 2 
        elif (m == 2 or n == 2) :

            # If yes, then simply calculate 
            # consecutive 2 rows or columns 
            c = 0; 
            c = (max(m, n) // 4) * 4; 

            if (max(m, n) % 4 == 1) :
                c += 2; 

            elif (max(m, n) % 4 > 1) :
                c += 4; 

            return c; 

        # For general case, just print the 
        # half of total blocks 
        else :
            return (((m * n) + 1) // 2); 

    # Driver code 
    if __name__ == "__main__" : 

        n = 4; m = 5; 

        print(max_knight(n, m)); 

    # This code is contributed by AnkitRai01
    ```

    ## C#

    ```
    // C# implementation of the approach 
    using System;

    class GFG
    {

    // Function to return the maximum number of 
    // knights that can be placed on the given 
    // chessboard such that no two 
    // knights attack each other 
    static int max_knight(int n, int m) 
    { 

        // Check for corner case #1 
        // If row or column is 1 
        if (m == 1 || n == 1) 
        { 

            // If yes, then simply print total blocks 
            // which will be the max of row or column 
            return Math.Max(m, n); 
        } 

        // Check for corner case #2 
        // If row or column is 2 
        else if (m == 2 || n == 2) 
        { 

            // If yes, then simply calculate 
            // consecutive 2 rows or columns 
            int c = 0; 
            c = (Math.Max(m, n) / 4) * 4; 

            if (Math.Max(m, n) % 4 == 1)
            { 
                c += 2; 
            } 
            else if (Math.Max(m, n) % 4 > 1) 
            { 
                c += 4; 
            } 
            return c; 
        } 

        // For general case, just print the 
        // half of total blocks 
        else
        { 
            return (((m * n) + 1) / 2); 
        } 
    } 

    // Driver code 
    static public void Main ()
    {
        int n = 4, m = 5; 
        Console.Write(max_knight(n, m)); 
    }
    }

    // This code is contributed by Tushil.
    ```

    **Output:**

    ```
    10

    ```