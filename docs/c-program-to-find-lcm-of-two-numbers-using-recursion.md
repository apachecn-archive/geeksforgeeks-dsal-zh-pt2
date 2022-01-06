# 用递归求两个数 LCM 的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-to-find-LCM-of-two-numbers-use-recursion/](https://www.geeksforgeeks.org/c-program-to-find-lcm-of-two-numbers-using-recursion/)

给定两个整数 **N** 和 **M** ，任务是使用[递归](https://www.geeksforgeeks.org/recursion/)找到它们的 [LCM](https://www.geeksforgeeks.org/lcm-gq/) 。

**示例:**

> **输入:** N = 2，M = 4
> T3】输出:4
> T6】说明:2，4 的 LCM 为 4。
> 
> **输入:** N = 3，M = 5
> T3】输出:15
> T6】说明:3，5 的 LCM 为 15。

**方法:**思路是用求两个数的 [LCM 的基本初等方法。按照以下步骤解决问题:](https://www.geeksforgeeks.org/program-to-find-lcm-of-two-numbers/)

*   用 **3** 整数参数 **N、M、**和 **K** 定义一个[递归函数](https://www.geeksforgeeks.org/recursive-functions/) **LCM()** ，找到 **N** 和 **M** 的 [LCM](https://www.geeksforgeeks.org/lcm-and-hcf/) 。
*   需要考虑以下基本条件:
    *   如果 **N** 或 **M** 等于 **1** ，则返回 **N * M** 。
    *   如果 **N** 等于 **M** ，则返回 **N** 。
*   **如果 K <分钟(N，M):**
    *   如果 **K** 除了 **N** 和 **M** ，则返回 **K * LCM(N/K，M/K，2)** 。
    *   否则，将 **K** 增加 **1** ，返回 **LCM(N，M，K+1)。**
*   否则，退回 **N** 和 **M** 的产品。
*   Finally, print the result of the recursive function as the required [LCM](https://www.geeksforgeeks.org/lcm-gq/).

    下面是上述方法的实现:

    ## C

    ```
    // C program for the above approach

    #include <stdio.h>

    // Function to return the
    // minimum of two numbers
    int Min(int Num1, int Num2)
    {
        return Num1 >= Num2
                   ? Num2
                   : Num1;
    }

    // Utility function to calculate LCM
    // of two numbers using recursion
    int LCMUtil(int Num1, int Num2, int K)
    {
        // If either of the two numbers
        // is 1, return their product
        if (Num1 == 1 || Num2 == 1)
            return Num1 * Num2;

        // If both the numbers are equal
        if (Num1 == Num2)
            return Num1;

        // If K is smaller than the
        // minimum of the two numbers
        if (K <= Min(Num1, Num2)) {

            // Checks if both numbers are
            // divisible by K or not
            if (Num1 % K == 0 && Num2 % K == 0) {

                // Recursively call LCM() function
                return K * LCMUtil(
                               Num1 / K, Num2 / K, 2);
            }

            // Otherwise
            else
                return LCMUtil(Num1, Num2, K + 1);
        }

        // If K exceeds minimum
        else
            return Num1 * Num2;
    }

    // Function to calculate LCM
    // of two numbers
    void LCM(int N, int M)
    {
        // Stores LCM of two number
        int lcm = LCMUtil(N, M, 2);

        // Print LCM
        printf("%d", lcm);
    }

    // Driver Code
    int main()
    {
        // Given N & M
        int N = 2, M = 4;

        // Function Call
        LCM(N, M);

        return 0;
    }
    ```

    **Output:**

    ```
    4

    ```

    ***时间复杂度:** O(max(N，M))*
    ***辅助空间:** O(1)*