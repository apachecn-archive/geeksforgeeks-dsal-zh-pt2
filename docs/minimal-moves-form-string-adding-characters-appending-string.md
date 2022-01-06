# 通过添加字符或追加字符串本身形成字符串的最小移动量

> 原文:[https://www . geesforgeks . org/minimum-moves-form-string-add-characters-appending-string/](https://www.geeksforgeeks.org/minimal-moves-form-string-adding-characters-appending-string/)

给定一个字符串 S，我们需要编写一个程序来检查是否有可能通过多次执行下面的任何操作来构造给定的字符串 S。在每个步骤中，我们可以:

*   在字符串末尾添加任何字符。
*   或者，将字符串附加到字符串本身。

上述步骤可以应用任意次数。我们需要编写一个程序来打印形成字符串所需的最少步骤。

示例:

```
Input : aaaaaaaa
Output : 4 
Explanation: move 1: add 'a' to form "a"
move 2: add 'a' to form "aa"
move 3: append "aa" to form "aaaa" 
move 4: append "aaaa" to form "aaaaaaaa" 

Input: aaaaaa
Output: 4 
Explanation: move 1: add 'a' to form "a"
move 2: add 'a' to form "aa"
move 3: add 'a' to form "aaa" 
move 4: append "aaa" to form "aaaaaa" 

Input: abcabca
Output: 5  

```

解决这个问题的思路是用**动态编程**来统计最小移动次数。创建一个名为 *dp* 的数组，大小为 n，其中 n 是输入字符串的长度。dp[i]存储生成子串(0…i)所需的最小移动次数。根据这个问题，有两种可能的方法:

1.  **dp[i] = min(dp[i]，dp[i-1] + 1)** 表示添加字符。
2.  **dp[i*2+1] = min(dp[i]+1, dp[i*2+1])**, appending of string is done if s[0…i]==s[i+1..i*2+1]

    答案将存储在 **dp[n-1]** 中，因为我们需要形成字符串(0..n-1)索引方式。

    以下是上述思路的实现:

    ## C++

    ```
    // CPP program to print the
    // Minimal moves to form a string
    // by appending string and adding characters
    #include <bits/stdc++.h>
    using namespace std;

    // function to return the minimal number of moves
    int minimalSteps(string s, int n)
    {

        int dp[n];

        // initializing dp[i] to INT_MAX
        for (int i = 0; i < n; i++)
            dp[i] = INT_MAX;

        // initialize both strings to null
        string s1 = "", s2 = "";

        // base case
        dp[0] = 1;

        s1 += s[0];

        for (int i = 1; i < n; i++) {
            s1 += s[i];

            // check if it can be appended
            s2 = s.substr(i + 1, i + 1);

            // addition of character takes one step
            dp[i] = min(dp[i], dp[i - 1] + 1);

            // appending takes 1 step, and we directly
            // reach index i*2+1 after appending
            // so the number of steps is stord in i*2+1
            if (s1 == s2)
                dp[i * 2 + 1] = min(dp[i] + 1, dp[i * 2 + 1]);
        }

        return dp[n - 1];
    }

    // Driver Code
    int main()
    {

        string s = "aaaaaaaa";
        int n = s.length();

        // function call to return minimal number of moves
        cout << minimalSteps(s, n);

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to print the
    // Minimal moves to form a string
    // by appending string and adding characters
    import java.util.*;

    class GFG
    {

    // function to return the minimal number of moves
    static int minimalSteps(String s, int n)
    {

        int []dp = new int[n];

        // initializing dp[i] to INT_MAX
        for (int i = 0; i < n; i++)
            dp[i] = Integer.MAX_VALUE;

        // initialize both strings to null
        String s1 = "", s2 = "";

        // base case
        dp[0] = 1;

        s1 += s.charAt(0);

        for (int i = 1; i < n; i++)
        {
            s1 += s.charAt(i);

            // check if it can be appended
            s2 = s.substring(i + 1, i + 1);

            // addition of character takes one step
            dp[i] = Math.min(dp[i], dp[i - 1] + 1);

            // appending takes 1 step, and we directly
            // reach index i*2+1 after appending
            // so the number of steps is stord in i*2+1
            if (s1 == s2)
                dp[i * 2 + 1] = Math.min(dp[i] + 1, 
                                       dp[i * 2 + 1]);
        }
        return dp[n - 1];
    }

    // Driver Code
    public static void main(String args[])
    {

        String s = "aaaaaaaa";
        int n = s.length();

        // function call to return minimal number of moves
        System.out.println(minimalSteps(s, n)/2);
    }
    }

    // This code is contributed by 
    // Shashank_Sharma
    ```

    ## 蟒蛇 3

    ```
    # Python program to print the 
    # Minimal moves to form a string 
    # by appending string and adding characters 

    INT_MAX = 100000000

    # function to return the 
    # minimal number of moves 
    def minimalSteps(s, n):
        dp = [INT_MAX for i in range(n)] 

        # initialize both strings to null 
        s1 = ""
        s2 = ""

        # base case 
        dp[0] = 1
        s1 += s[0]

        for i in range(1, n):
            s1 += s[i]

            # check if it can be appended 
            s2 = s[i + 1: i + 1 + i + 1]

            # addition of character 
            # takes one step 
            dp[i] = min(dp[i], dp[i - 1] + 1)

            # appending takes 1 step, and 
            # we directly reach index i*2+1 
            # after appending so the number
            # of steps is stord in i*2+1 
            if (s1 == s2): 
                dp[i * 2 + 1] = min(dp[i] + 1, 
                                    dp[i * 2 + 1])

        return dp[n - 1]

    # Driver Code 
    s = "aaaaaaaa"
    n =len(s)

    # function call to return 
    # minimal number of moves 
    print( minimalSteps(s, n) ) 

    # This code is contributed 
    # by sahilshelangia
    ```

    ## C#

    ```
    // C# program to print the
    // Minimal moves to form a string
    // by appending string and adding characters
    using System;

    class GFG
    {

    // function to return the minimal number of moves
    static int minimalSteps(String s, int n)
    {

        int []dp = new int[n];

        // initializing dp[i] to INT_MAX
        for (int i = 0; i < n; i++)
            dp[i] = int.MaxValue;

        // initialize both strings to null
        String s1 = "", s2 = "";

        // base case
        dp[0] = 1;

        s1 += s[0];

        for (int i = 1; i < n; i++)
        {
            s1 += s[i];

            // check if it can be appended
            s2 = s.Substring(i , 1);

            // addition of character takes one step
            dp[i] = Math.Min(dp[i], dp[i - 1] + 1);

            // appending takes 1 step, and we directly
            // reach index i*2+1 after appending
            // so the number of steps is stord in i*2+1
            if (s1 == s2)
                dp[i * 2 + 1] = Math.Min(dp[i] + 1, 
                                    dp[i * 2 + 1]);
        }
        return dp[n - 1];
    }

    // Driver Code
    public static void Main(String []args)
    {

        String s = "aaaaaaaa";
        int n = s.Length;

        // function call to return minimal number of moves
        Console.Write(minimalSteps(s, n)/2);
    }
    }

    // This code has been contributed by 29AjayKumar
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // php program to print the
    // Minimal moves to form a 
    // string by appending string
    // and adding characters

    // function to return the
    // minimal number of moves
    function minimalSteps($s,$n)
    {

        // initializing dp[i] to INT_MAX
        for ($i = 0; $i < $n; $i++)
            $dp[$i] = PHP_INT_MAX;

        // initialize both 
        // strings to null
        $s1 = "";
        $s2 = "";

        // base case
        $dp[0] = 1;

        $s1=$s1.$s[0];

        for ($i = 1; $i < $n; $i++) 
        {
            $s1 = $s1.$s[$i];

            // check if it can 
            // be appended
            $s2 = substr($s, $i + 1, $i + 1);

            // addition of character
            // takes one step
            $dp[$i] = min($dp[$i], 
                      $dp[$i - 1] + 1);

            // appending takes 1 step,
            // and we directly
            // reach index i*2+1 
            // after appending
            // so the number of steps 
            // is stord in i*2+1
            if ($s1 == $s2)
                $dp[$i * 2 + 1] = min($dp[$i] + 1,
                                  $dp[$i * 2 + 1]);
        }

        return $dp[$n - 1];
    }

        // Driver Code
        $s = "aaaaaaaa";
        $n = strlen($s);

        // function call to return
        //minimal number of moves
        echo minimalSteps($s, $n);

    // This code is contributed by mits 
    ?>
    ```

    **Output:**

    ```
    4

    ```

    **时间复杂度:** O(n <sup>2</sup> ，其中 n 为输入字符串的长度。