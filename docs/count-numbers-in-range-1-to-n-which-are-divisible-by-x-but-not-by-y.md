# 计算 1 到 N 范围内可被 X 整除但不能被 Y 整除的数字

> 原文:[https://www . geesforgeks . org/count-numbers-in-range-1-n-哪些可以被 x 整除但不能被 y 整除/](https://www.geeksforgeeks.org/count-numbers-in-range-1-to-n-which-are-divisible-by-x-but-not-by-y/)

给定两个正整数 X 和 Y，任务是计算 1 到 N 范围内可被 X 整除但不能被 Y 整除的总数

**示例:**

> **输入:** x = 2，Y = 3，N = 10
> **输出:** 4
> 可被 2 整除但不能被 3 整除的数字是:2，4，8，10
> 
> **输入:** X = 2，Y = 4，N = 20
> **输出:** 5
> 可被 2 整除但不能被 4 整除的数字是:2，6，10，14，18

一个**简单的解决方法**是计算能被 X 整除但不能被 Y 整除的数，就是循环 1 到 N，计算能被 X 整除但不能被 Y 整除的数

**接近**

1.  对于 1 到 N 范围内的每个数字，如果该数字可被 X 整除但不能被 y 整除，则递增计数
2.  打印计数。

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function to count total numbers divisible by
    // x but not y in range 1 to N
    int countNumbers(int X, int Y, int N)
    {
        int count = 0;
        for (int i = 1; i <= N; i++) {
            // Check if Number is divisible
            // by x but not Y
            // if yes, Increment count
            if ((i % X == 0) && (i % Y != 0))
                count++;
        }
        return count;
    }

    // Driver Code
    int main()
    {

        int X = 2, Y = 3, N = 10;
        cout << countNumbers(X, Y, N);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of above approach

    class GFG {

        // Function to count total numbers divisible by
        // x but not y in range 1 to N
        static int countNumbers(int X, int Y, int N)
        {
            int count = 0;
            for (int i = 1; i <= N; i++) {
                // Check if Number is divisible
                // by x but not Y
                // if yes, Increment count
                if ((i % X == 0) && (i % Y != 0))
                    count++;
            }
            return count;
        }

        // Driver Code
        public static void main(String[] args)
        {

            int X = 2, Y = 3, N = 10;
            System.out.println(countNumbers(X, Y, N));
        }
    }
    ```

    ## 蟒蛇 3

    ```
    # Python3 implementation of above approach 

    # Function to count total numbers divisible 
    # by x but not y in range 1 to N 
    def countNumbers(X, Y, N): 

        count = 0; 
        for i in range(1, N + 1):

            # Check if Number is divisible 
            # by x but not Y 
            # if yes, Increment count 
            if ((i % X == 0) and (i % Y != 0)): 
                count += 1; 

        return count; 

    # Driver Code 
    X = 2;
    Y = 3;
    N = 10; 
    print(countNumbers(X, Y, N)); 

    # This code is contributed by mits
    ```

    ## C#

    ```
    // C# implementation of the above approach
    using System;
    class GFG {

        // Function to count total numbers divisible by
        // x but not y in range 1 to N
        static int countNumbers(int X, int Y, int N)
        {
            int count = 0;
            for (int i = 1; i <= N; i++) {
                // Check if Number is divisible
                // by x but not Y
                // if yes, Increment count
                if ((i % X == 0) && (i % Y != 0))
                    count++;
            }
            return count;
        }

        // Driver Code
        public static void Main()
        {

            int X = 2, Y = 3, N = 10;
            Console.WriteLine(countNumbers(X, Y, N));
        }
    }
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    //PHP implementation of above approach 

    // Function to count total numbers divisible by 
    // x but not y in range 1 to N 
    function countNumbers($X, $Y, $N) 
    { 
        $count = 0; 
        for ($i = 1; $i <= $N; $i++)
        { 
            // Check if Number is divisible 
            // by x but not Y 
            // if yes, Increment count 
            if (($i % $X == 0) && ($i % $Y != 0)) 
                $count++; 
        } 
        return $count; 
    } 

    // Driver Code 
    $X = 2;
    $Y = 3;
    $N = 10; 
    echo (countNumbers($X, $Y, $N)); 

    // This code is contributed by Arnab Kundu
    ?>
    ```

    **Output:**

    ```
    4

    ```

    **时间复杂度:O(N)**

    **高效解决方案:**

    1.  在 1 到 N 的范围内，找出可被 X 整除的**总数和可被 Y** 整除的**总数。**
    2.  此外，找出可被 X 或 Y 整除的**总数**
    3.  将可被 X 整除但不能被 Y 整除的总数计算为
        **(可被 X 或 Y 整除的总数)–(可被 Y 整除的总数)**

    以下是上述方法的实现:

    ## C++

    ```
    // C++ implementation of above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function to count total numbers divisible by
    // x but not y in range 1 to N
    int countNumbers(int X, int Y, int N)
    {

        // Count total number divisible by X
        int divisibleByX = N / X;

        // Count total number divisible by Y
        int divisibleByY = N / Y;

        // Count total number divisible by either X or Y
        int LCM = (X * Y) / __gcd(X, Y);
        int divisibleByLCM = N / LCM;
        int divisibleByXorY = divisibleByX + divisibleByY 
                                         - divisibleByLCM;

        // Count total numbers divisible by X but not Y
        int divisibleByXnotY = divisibleByXorY 
                                           - divisibleByY;

        return divisibleByXnotY;
    }

    // Driver Code
    int main()
    {

        int X = 2, Y = 3, N = 10;
        cout << countNumbers(X, Y, N);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java implementation of above approach

    class GFG {

        // Function to calculate GCD

        static int gcd(int a, int b)
        {
            if (b == 0)
                return a;
            return gcd(b, a % b);
        }

        // Function to count total numbers divisible by
        // x but not y in range 1 to N

        static int countNumbers(int X, int Y, int N)
        {

            // Count total number divisible by X
            int divisibleByX = N / X;

            // Count total number divisible by Y
            int divisibleByY = N / Y;

            // Count total number divisible by either X or Y
            int LCM = (X * Y) / gcd(X, Y);
            int divisibleByLCM = N / LCM;
            int divisibleByXorY = divisibleByX + divisibleByY
                                  - divisibleByLCM;

            // Count total number divisible by X but not Y
            int divisibleByXnotY = divisibleByXorY 
                                              - divisibleByY;

            return divisibleByXnotY;
        }

        // Driver Code
        public static void main(String[] args)
        {

            int X = 2, Y = 3, N = 10;
            System.out.println(countNumbers(X, Y, N));
        }
    }
    ```

    ## 蟒蛇 3

    ```
    # Python 3 implementation of above approach
    from math import gcd

    # Function to count total numbers divisible 
    # by x but not y in range 1 to N
    def countNumbers(X, Y, N):

        # Count total number divisible by X
        divisibleByX = int(N / X)

        # Count total number divisible by Y
        divisibleByY = int(N / Y)

        # Count total number divisible 
        # by either X or Y
        LCM = int((X * Y) / gcd(X, Y))
        divisibleByLCM = int(N / LCM)
        divisibleByXorY = (divisibleByX + 
                           divisibleByY - 
                           divisibleByLCM)

        # Count total numbers divisible by 
        # X but not Y
        divisibleByXnotY = (divisibleByXorY - 
                            divisibleByY)

        return divisibleByXnotY

    # Driver Code
    if __name__ == '__main__':
        X = 2
        Y = 3
        N = 10
        print(countNumbers(X, Y, N))

    # This code is contributed by
    # Surendra_Gangwar
    ```

    ## C#

    ```
    // C# implementation of above approach

    using System;
    class GFG {

        // Function to calculate GCD
        static int gcd(int a, int b)
        {
            if (b == 0)
                return a;
            return gcd(b, a % b);
        }

        // Function to count total numbers divisible by
        // x but not y in range 1 to N
        static int countNumbers(int X, int Y, int N)
        {

            // Count total number divisible by X
            int divisibleByX = N / X;

            // Count total number divisible by Y
            int divisibleByY = N / Y;

            // Count total number divisible by either X or Y
            int LCM = (X * Y) / gcd(X, Y);
            int divisibleByLCM = N / LCM;
            int divisibleByXorY = divisibleByX + divisibleByY 
                                            - divisibleByLCM;

            // Count total number divisible by X but not Y
            int divisibleByXnotY = divisibleByXorY 
                                              - divisibleByY;

            return divisibleByXnotY;
        }

        // Driver Code
        public static void Main()
        {

            int X = 2, Y = 3, N = 10;
            Console.WriteLine(countNumbers(X, Y, N));
        }
    }
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP implementation of above approach

    function __gcd($a, $b) 
    { 

        // Everything divides 0 
        if ($a == 0) 
            return $b; 
        if ($b == 0) 
            return $a; 

        // base case 
        if($a == $b) 
            return $a ; 

        // a is greater 
        if($a > $b) 
            return __gcd( $a - $b , $b ); 

        return __gcd( $a , $b - $a ); 
    } 

    // Function to count total numbers divisible 
    // by x but not y in range 1 to N
    function countNumbers($X, $Y, $N)
    {

        // Count total number divisible by X
        $divisibleByX = $N / $X;

        // Count total number divisible by Y
        $divisibleByY = $N /$Y;

        // Count total number divisible by either X or Y
        $LCM = ($X * $Y) / __gcd($X, $Y);
        $divisibleByLCM = $N / $LCM;
        $divisibleByXorY = $divisibleByX + $divisibleByY - 
                                           $divisibleByLCM;

        // Count total numbers divisible by X but not Y
        $divisibleByXnotY = $divisibleByXorY - 
                            $divisibleByY;

        return ceil($divisibleByXnotY);
    }

    // Driver Code
    $X = 2;
    $Y = 3;
    $N = 10;
    echo countNumbers($X, $Y, $N);

    // This is code contrubted by inder_verma
    ?>
    ```

    **Output:**

    ```
    4

    ```

    **时间复杂度:** O(1)