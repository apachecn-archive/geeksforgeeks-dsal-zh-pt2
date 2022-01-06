# 看假期能不能休

> 原文:[https://www . geesforgeks . org/find-如果假期可以带走或不可以带走/](https://www.geeksforgeeks.org/find-if-the-vacation-can-be-taken-or-not/)

给出了以下值:

*   **N** 为考试剩余天数。
*   **S** 为备考科目数。
*   **C** 为每个科目需要准备的章节数。
*   **H** 是准备一章的小时数。
*   **L** 是期望假期的天数。这个假期，学习不能做。
*   **T** 是一个人一天可以学习的小时数。

任务是确定想要的假期是否可以休。如果可以获得，则打印**是**，否则打印**否**。

**示例:**

> **输入:** N = 1，S = 2，C = 3，H = 4，L = 5，T = 6
> **输出:**无
> 要求的学习时数= S * C * H = 24
> 如果休假可以完成的学习时数=(N–L)* T =-24
> 由于休假后的可用时间<要求的总时间，
> 因此不能休假。
> 
> **输入:** N = 12，S = 5，C = 8，H = 3，L = 2，T = 20
> **输出:**是
> 要求的学习时数= S * C * H = 120
> 如果休假可以完成的学习时数=(N–L)* T = 200
> 由于休假后的可用时间>要求的总时间，
> 因此可以休假。

**进场:**

1.  将 **S** 、 **C** 和 **H** 相乘，得出**所需的学习时数**。

    > 要求的学习时数= S * C * H

2.  现在找到如果休假可以完成的**小时学习。这些小时将相当于我们剩余的天数乘以 **T** 小时(即(N-L)*T)。

    > 如果休假,可以完成的学习小时数=(N–L)* T** 
3.  Now check if the required hours are less than or equal to the hours of study that can be done if the vacation is taken. If true, then print **Yes**, else print **No**.

    下面是上述方法的实现:

    ## C++

    ```
    // C++ program to find
    // if the Vacation can be taken or not

    #include <bits/stdc++.h>
    using namespace std;

    // Function to find if the Vacation
    // is possible or not
    int isPossible(int N, int S, int C, int H,
                   int L, int T)
    {

        // Find the required number of hours of study
        int total_time_required = S * C * H;

        // find the hours of study that can be done
        // if the vacation is taken
        int available_time_after_vacation = (N - L) * T;

        // check if the required hours are less than
        // or equal to the hours of study
        // that can be done if the vacation is taken
        if (available_time_after_vacation
            >= total_time_required)
            return 1;
        return 0;
    }

    // Driver Code
    int main()
    {
        int N = 12, S = 5, C = 8,
            H = 3, L = 2, T = 20;

        if (isPossible(N, S, C, H, L, T))
            cout << "Yes" << endl;
        else
            cout << "No" << endl;

        N = 1, S = 2, C = 3,
        H = 4, L = 5, T = 6;

        if (isPossible(N, S, C, H, L, T))
            cout << "Yes" << endl;
        else
            cout << "No" << endl;

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find
    // if the Vacation can be taken or not
    class GFG
    {

    // Function to find if the Vacation
    // is possible or not
    static int isPossible(int N, int S, int C, int H,
                           int L, int T)
    {

        // Find the required number of hours of study
        int total_time_required = S * C * H;

        // find the hours of study that can be done
        // if the vacation is taken
        int available_time_after_vacation = (N - L) * T;

        // check if the required hours are less than
        // or equal to the hours of study
        // that can be done if the vacation is taken
        if (available_time_after_vacation
            >= total_time_required)
            return 1;
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 12, S = 5, C = 8,
            H = 3, L = 2, T = 20;

        if (isPossible(N, S, C, H, L, T) == 1)
            System.out.print("Yes" + "\n");
        else
            System.out.print("No" + "\n");

        N = 1; S = 2; C = 3;
        H = 4; L = 5; T = 6;

        if (isPossible(N, S, C, H, L, T)==1)
            System.out.print("Yes" + "\n");
        else
            System.out.print("No" + "\n");
    }
    }

    // This code is contributed by 29AjayKumar
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to find
    # if the Vacation can be taken or not

    # Function to find if the Vacation
    # is possible or not
    def isPossible(N, S, C, H, L, T):

        # Find the required number of hours of study
        total_time_required = S * C * H

        # find the hours of study that can be done
        # if the vacation is taken
        available_time_after_vacation = (N - L) * T

        # check if the required hours are less than
        # or equal to the hours of study
        # that can be done if the vacation is taken
        if (available_time_after_vacation >= total_time_required):
            return 1
        return 0

    # Driver Code
    N = 12
    S = 5
    C = 8
    H = 3
    L = 2
    T = 20

    if (isPossible(N, S, C, H, L, T)):
        print("Yes")
    else:
        print("No")

    N = 1
    S = 2
    C = 3
    H = 4
    L = 5
    T = 6

    if (isPossible(N, S, C, H, L, T)):
        print("Yes")
    else:
        print("No")

    # This code is contributed by SHUBHAMSINGH10
    ```

    ## C#

    ```
    // C# program to find
    // if the Vacation can be taken or not
    using System;

    class GFG
    {

    // Function to find if the Vacation
    // is possible or not
    static int isPossible(int N, int S, int C, int H,
                        int L, int T)
    {

        // Find the required number of hours of study
        int total_time_required = S * C * H;

        // find the hours of study that can be done
        // if the vacation is taken
        int available_time_after_vacation = (N - L) * T;

        // check if the required hours are less than
        // or equal to the hours of study
        // that can be done if the vacation is taken
        if (available_time_after_vacation
            >= total_time_required)
            return 1;
        return 0;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 12, S = 5, C = 8,
            H = 3, L = 2, T = 20;

        if (isPossible(N, S, C, H, L, T) == 1)
            Console.Write("Yes" + "\n");
        else
            Console.Write("No" + "\n");

        N = 1; S = 2; C = 3;
        H = 4; L = 5; T = 6;

        if (isPossible(N, S, C, H, L, T)==1)
            Console.Write("Yes" + "\n");
        else
            Console.Write("No" + "\n");
    }
    }

    // This code is contributed by 29AjayKumar
    ```

    **Output:**

    ```
    Yes
    No

    ```