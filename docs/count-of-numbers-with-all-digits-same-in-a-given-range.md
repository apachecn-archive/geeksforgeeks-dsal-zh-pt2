# 给定范围内所有数字相同的数字计数

> 原文:[https://www . geesforgeks . org/给定范围内所有数字相同的数字计数/](https://www.geeksforgeeks.org/count-of-numbers-with-all-digits-same-in-a-given-range/)

给定两个整数 **L** 和 **R** 表示一个范围的起始值和结束值，任务是计算该范围内所有数字相同的所有数字，如 1、22、444、3333 等。

**示例:**

> **输入:** L = 12，R = 68
> **输出:** 5
> **说明:**
> { 22，33，44，55，66}是给定范围内数字相同的数字。
> 
> **输入:** L = 1，R = 32
> T3】输出: 11

**天真方法:**迭代从 L 到 R 的所有数字，对于每个数字，检查它是否所有的数字都相同。如果是，则增加所需的计数。在末尾打印此计数。

**有效方法:**这个想法是基于 1、11、111 等的倍数(1 到 9)的所有数字都是相同的。
例如:

```
1 times 1 = 1 (All digits are same)
2 times 1 = 2 (All digits are same)
3 times 1 = 3 (All digits are same)
.
.
9 times 1 = 9 (All digits are same)

Similarly
1 times 11 = 11 (All digits are same)
2 times 11 = 22 (All digits are same)
3 times 11 = 33 (All digits are same)
.
.
9 times 11 = 99 (All digits are same)

Same is the case for 111, 1111, etc.

```

因此，这些步骤可以定义为:

1.  找出 r 中的位数。这将决定要创建的连续 1 的长度，在此之前我们必须检查。
    例如，如果 R = 100，那么长度(R) = 3。因此，我们只需要检查 1、11 和 111 的倍数。
2.  对于从 1 到长度(R)的连续 1 的每个长度:
    *   将它们与从 **2** 到 **9** 的所有值相乘
    *   检查是否在**【L，R】**范围内。
    *   如果是，则增加所需数量的计数。
3.  打印所需的数字计数。

    下面的代码是上述方法的实现:

    ## C++

    ```
    // C++ program to count the
    // total numbers in the range
    // L and R which have all the
    // digit same

    #include <bits/stdc++.h>
    using namespace std;

    // Function that count the
    // total numbersProgram between L
    // and R which have all the
    // digit same
    int count_same_digit(int L, int R)
    {
        int tmp = 0, ans = 0;

        // length of R
        int n = log10(R) + 1;

        for (int i = 0; i < n; i++) {

            // tmp has all digits as 1
            tmp = tmp * 10 + 1;

            // For each multiple
            // of tmp in range 1 to 9,
            // check if it present
            // in range [L, R]
            for (int j = 1; j <= 9; j++) {

                if (L <= (tmp * j)
                    && (tmp * j) <= R) {

                    // Increment the required count
                    ans++;
                }
            }
        }
        return ans;
    }

    // Driver Program
    int main()
    {
        int L = 12, R = 68;

        cout << count_same_digit(L, R)
             << endl;
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to count the
    // total numbers in the range
    // L and R which have all the
    // digit same
    import java.util.*;

    class GFG{

    // Function that count the total 
    // numbersProgram between L and 
    // R which have all the digit same
    static int count_same_digit(int L, int R)
    {
        int tmp = 0, ans = 0;

        // Length of R
        int n = (int)Math.log10(R) + 1;

        for(int i = 0; i < n; i++)
        {

           // tmp has all digits as 1
           tmp = tmp * 10 + 1;

           // For each multiple of tmp 
           // in range 1 to 9, check if
           // it present in range [L, R]
           for(int j = 1; j <= 9; j++)
           {
              if (L <= (tmp * j) && (tmp * j) <= R) 
              {
                  // Increment the required count
                  ans++;
              }
           }
        }
        return ans;
    }

    // Driver code
    public static void main(String[] args)
    {
        int L = 12, R = 68;

        System.out.println(count_same_digit(L, R));
    }
    }

    // This code is contributed by offbeat
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to count the
    # total numbers in the range
    # L and R which have all the
    # digit same
    import math

    # Function that count the
    # total numbersProgram between L
    # and R which have all the
    # digit same
    def count_same_digit(L, R):

        tmp = 0; ans = 0;

        # length of R
        n = int(math.log10(R) + 1);

        for i in range(0, n):

            # tmp has all digits as 1
            tmp = tmp * 10 + 1;

            # For each multiple
            # of tmp in range 1 to 9,
            # check if it present
            # in range [L, R]
            for j in range(1, 9):

                if (L <= (tmp * j) and (tmp * j) <= R):

                    # Increment the required count
                    ans += 1;

        return ans;

    # Driver Code
    L = 12; R = 68;

    print(count_same_digit(L, R))

    # This code is contributed by Nidhi_biet
    ```

    ## C#

    ```
    // C# program to count the
    // total numbers in the range
    // L and R which have all the
    // digit same
    using System;

    class GFG{

    // Function that count the total 
    // numbersProgram between L and 
    // R which have all the digit same
    static int count_same_digit(int L, int R)
    {
        int tmp = 0, ans = 0;

        // Length of R
        int n = (int)Math.Log10(R) + 1;

        for(int i = 0; i < n; i++)
        {

            // tmp has all digits as 1
            tmp = tmp * 10 + 1;

            // For each multiple of tmp 
            // in range 1 to 9, check if
            // it present in range [L, R]
            for(int j = 1; j <= 9; j++)
            {
                if (L <= (tmp * j) && (tmp * j) <= R) 
                {
                    // Increment the required count
                    ans++;
                }
            }
        }
        return ans;
    }

    // Driver code
    public static void Main()
    {
        int L = 12, R = 68;

        Console.Write(count_same_digit(L, R));
    }
    }

    // This code is contributed by Code_Mech
    ```

    **Output:**

    ```
    5

    ```

    ***时间复杂度:** O(长度(R))*