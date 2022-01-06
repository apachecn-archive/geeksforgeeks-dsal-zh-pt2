# 词典第一个回文串

> 原文:[https://www . geeksforgeeks . org/词典-第一-回文-字符串/](https://www.geeksforgeeks.org/lexicographically-first-palindromic-string/)

重新排列给定字符串的字符，形成字典顺序的第一个回文字符串。如果不存在这样的字符串，显示消息“无回文字符串”。

示例:

```
Input : malayalam
Output : aalmymlaa

Input : apple
Output : no palindromic string

```

**<u>简易进场:</u>**
1。按字母(升序)顺序对字符串进行排序。
2。一个是找到给定字符串在字典上的下一个排列。
3。第一个排列是回文就是答案。

**<u>高效方法:</u>** 回文串属性:
1。如果字符串的长度是偶数，那么字符串中每个字符的频率必须是偶数。
2。如果长度是奇数，那么应该有一个字符的频率是奇数，所有其他字符必须具有偶数频率，并且在字符串的中间必须至少出现一个奇数字符。

**算法**
1。给定字符串中每个字符的存储频率
2。利用上面提到的回文串的属性，检查回文串是否可以形成。
3。如果无法形成回文串，返回“无回文串”。
4。否则我们创建三个字符串，然后返回 front_str + odd_str + rear_str。

*   **odd_str :** 如果没有出现奇数频率的字符，则为空。否则它包含所有出现的奇数字符。
*   **front_str :** 按递增顺序包含字符串中所有偶出现字符的一半。
*   **rear_str** Contains half occurrences of all even occurring characters of string in reverse order of front_str.

    下面是上述步骤的实现。

    ## C++

    ```
    // C++ program to find first palindromic permutation
    // of given string
    #include <bits/stdc++.h>
    using namespace std;

    const char MAX_CHAR = 26;

    // Function to count frequency of each char in the
    // string. freq[0] for 'a',...., freq[25] for 'z'
    void countFreq(string str, int freq[], int len)
    {
        for (int i=0; i<len; i++)
            freq[str.at(i) - 'a']++;
    }

    // Cases to check whether a palindr0mic
    // string can be formed or not
    bool canMakePalindrome(int freq[], int len)
    {
        // count_odd to count no of
        // chars with odd frequency
        int count_odd = 0;
        for (int i=0; i<MAX_CHAR; i++)
            if (freq[i]%2 != 0)
                count_odd++;

        // For even length string
        // no odd freq character
        if (len%2 == 0)
        {
            if (count_odd > 0)
                return false;
            else
                return true;
        }

        // For odd length string
        // one odd freq character
        if (count_odd != 1)
            return false;

        return true;
    }

    // Function to find odd freq char and
    // reducing its freq by 1returns "" if odd freq
    // char is not present
    string findOddAndRemoveItsFreq(int freq[])
    {
        string odd_str = "";
        for (int i=0; i<MAX_CHAR; i++)
        {
            if (freq[i]%2 != 0)
            {
                freq[i]--;
                odd_str = odd_str + (char)(i+'a');
                return odd_str;
            }
        }
        return odd_str;
    }

    // To find lexicographically first palindromic
    // string.
    string findPalindromicString(string str)
    {
        int len = str.length();

        int freq[MAX_CHAR] = {0};
        countFreq(str, freq, len);

        if (!canMakePalindrome(freq, len))
            return "No Palindromic String";

        // Assigning odd freq character if present
        // else empty string.
        string odd_str = findOddAndRemoveItsFreq(freq);

        string front_str = "", rear_str = " ";

        // Traverse characters in increasing order
        for (int i=0; i<MAX_CHAR; i++)
        {
            string temp = "";
            if (freq[i] != 0)
            {
                char ch = (char)(i + 'a');

                // Divide all occurrences into two
                // halves. Note that odd character
                // is removed by findOddAndRemoveItsFreq()
                for (int j=1; j<=freq[i]/2; j++)
                    temp = temp + ch;

                // creating front string
                front_str = front_str + temp;

                // creating rear string
                rear_str = temp + rear_str;
            }
        }

        // Final palindromic string which is
        // lexicographically first
        return (front_str + odd_str + rear_str);
    }

    // Driver program
    int main()
    {
        string str = "malayalam";
        cout << findPalindromicString(str);
        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program to find first palindromic permutation
    // of given string

    class GFG {

        static char MAX_CHAR = 26;

        // Function to count frequency of each char in the
        // string. freq[0] for 'a',...., freq[25] for 'z'
        static void countFreq(String str, int freq[], int len)
        {
            for (int i = 0; i < len; i++)
            {
                freq[str.charAt(i) - 'a']++;
            }
        }

        // Cases to check whether a palindr0mic
        // string can be formed or not
        static boolean canMakePalindrome(int freq[], int len) 
        {
            // count_odd to count no of
            // chars with odd frequency
            int count_odd = 0;
            for (int i = 0; i < MAX_CHAR; i++)
            {
                if (freq[i] % 2 != 0)
                {
                    count_odd++;
                }
            }

            // For even length string
            // no odd freq character
            if (len % 2 == 0)
            {
                if (count_odd > 0) 
                {
                    return false;
                } 
                else
                {
                    return true;
                }
            }

            // For odd length string
            // one odd freq character
            if (count_odd != 1) 
            {
                return false;
            }

            return true;
        }

        // Function to find odd freq char and
        // reducing its freq by 1returns "" if odd freq
        // char is not present
        static String findOddAndRemoveItsFreq(int freq[]) 
        {
            String odd_str = "";
            for (int i = 0; i < MAX_CHAR; i++)
            {
                if (freq[i] % 2 != 0)
                {
                    freq[i]--;
                    odd_str = odd_str + (char) (i + 'a');
                    return odd_str;
                }
            }
            return odd_str;
        }

        // To find lexicographically first palindromic
        // string.
        static String findPalindromicString(String str) 
        {
            int len = str.length();
            int freq[] = new int[MAX_CHAR];
            countFreq(str, freq, len);

            if (!canMakePalindrome(freq, len))
            {
                return "No Palindromic String";
            }

            // Assigning odd freq character if present
            // else empty string.
            String odd_str = findOddAndRemoveItsFreq(freq);

            String front_str = "", rear_str = " ";

            // Traverse characters in increasing order
            for (int i = 0; i < MAX_CHAR; i++)
            {
                String temp = "";
                if (freq[i] != 0)
                {
                    char ch = (char) (i + 'a');

                    // Divide all occurrences into two
                    // halves. Note that odd character
                    // is removed by findOddAndRemoveItsFreq()
                    for (int j = 1; j <= freq[i] / 2; j++) 
                    {
                        temp = temp + ch;
                    }

                    // creating front string
                    front_str = front_str + temp;

                    // creating rear string
                    rear_str = temp + rear_str;
                }
            }

            // Final palindromic string which is
            // lexicographically first
            return (front_str + odd_str + rear_str);
        }

        // Driver program
        public static void main(String[] args) 
        {
            String str = "malayalam";
            System.out.println(findPalindromicString(str));
        }
    } 

    // This code is contributed by Rajput-Ji
    ```

    ## 蟒蛇 3

    ```
    # Python3 program to find first palindromic permutation
    # of given string
    MAX_CHAR = 26;

    # Function to count frequency of each char in the
    # string. freq[0] for 'a',...., freq[25] for 'z'
    def countFreq(str1, freq, len1):

        for i in range(len1):
            freq[ord(str1[i]) - ord('a')] += 1;

    # Cases to check whether a palindr0mic
    # string can be formed or not
    def canMakePalindrome(freq, len1):

        # count_odd to count no of
        # chars with odd frequency
        count_odd = 0;
        for i in range(MAX_CHAR):
            if (freq[i] % 2 != 0):
                count_odd += 1;

        # For even length string
        # no odd freq character
        if (len1 % 2 == 0):
            if (count_odd > 0):
                return False;
            else:
                return True;

        # For odd length string
        # one odd freq character
        if (count_odd != 1):
            return False;

        return True;

    # Function to find odd freq char and
    # reducing its freq by 1returns "" if odd freq
    # char is not present
    def findOddAndRemoveItsFreq(freq):

        odd_str = "";
        for i in range(MAX_CHAR):
            if (freq[i]%2 != 0):
                freq[i]-=1;
                odd_str += chr(i+ord('a'));
                return odd_str;
        return odd_str;

    # To find lexicographically first palindromic
    # string.
    def findPalindromicString(str1):
        len1 = len(str1);

        freq=[0]*MAX_CHAR;
        countFreq(str1, freq, len1);

        if (canMakePalindrome(freq, len1) == False):
            return "No Palindromic String";

        # Assigning odd freq character if present
        # else empty string.
        odd_str = findOddAndRemoveItsFreq(freq);

        front_str = "";
        rear_str = " ";

        # Traverse characters in increasing order
        for i in range(MAX_CHAR):
            temp = "";
            if (freq[i] != 0):
                ch = chr(i + ord('a'));

                # Divide all occurrences into two
                # halves. Note that odd character
                # is removed by findOddAndRemoveItsFreq()
                for j in range(1,int(freq[i]/2)+1):
                    temp += ch;

                # creating front string
                front_str += temp;

                # creating rear string
                rear_str = temp+rear_str;

        # Final palindromic string which is
        # lexicographically first
        return (front_str + odd_str+rear_str);

    # Driver code

    str1 = "malayalam";
    print(findPalindromicString(str1));

    # This code is contributed by mits
    ```

    ## C#

    ```
    // C# program to find first palindromic permutation
    // of given string

    using System;
    class GFG 
    {

        static int MAX_CHAR = 26;

        // Function to count frequency of each char in the
        // string. freq[0] for 'a',...., freq[25] for 'z'
        static void countFreq(string str, int[] freq, int len)
        {
            for (int i = 0; i < len; i++)
            {
                freq[str[i] - 'a']++;
            }
        }

        // Cases to check whether a palindr0mic
        // string can be formed or not
        static bool canMakePalindrome(int[] freq, int len) 
        {
            // count_odd to count no of
            // chars with odd frequency
            int count_odd = 0;
            for (int i = 0; i < MAX_CHAR; i++)
            {
                if (freq[i] % 2 != 0)
                {
                    count_odd++;
                }
            }

            // For even length string
            // no odd freq character
            if (len % 2 == 0)
            {
                if (count_odd > 0) 
                {
                    return false;
                } 
                else
                {
                    return true;
                }
            }

            // For odd length string
            // one odd freq character
            if (count_odd != 1) 
            {
                return false;
            }

            return true;
        }

        // Function to find odd freq char and
        // reducing its freq by 1returns "" if odd freq
        // char is not present
        static string findOddAndRemoveItsFreq(int[] freq) 
        {
            string odd_str = "";
            for (int i = 0; i < MAX_CHAR; i++)
            {
                if (freq[i] % 2 != 0)
                {
                    freq[i]--;
                    odd_str = odd_str + (char) (i + 'a');
                    return odd_str;
                }
            }
            return odd_str;
        }

        // To find lexicographically first 
        // palindromic string.
        static string findPalindromicString(string str) 
        {
            int len = str.Length;
            int[] freq = new int[MAX_CHAR];
            countFreq(str, freq, len);

            if (!canMakePalindrome(freq, len))
            {
                return "No Palindromic String";
            }

            // Assigning odd freq character if present
            // else empty string.
            string odd_str = findOddAndRemoveItsFreq(freq);

            string front_str = "", rear_str = " ";

            // Traverse characters in increasing order
            for (int i = 0; i < MAX_CHAR; i++)
            {
                String temp = "";
                if (freq[i] != 0)
                {
                    char ch = (char) (i + 'a');

                    // Divide all occurrences into two
                    // halves. Note that odd character
                    // is removed by findOddAndRemoveItsFreq()
                    for (int j = 1; j <= freq[i] / 2; j++) 
                    {
                        temp = temp + ch;
                    }

                    // creating front string
                    front_str = front_str + temp;

                    // creating rear string
                    rear_str = temp + rear_str;
                }
            }

            // Final palindromic string which is
            // lexicographically first
            return (front_str + odd_str + rear_str);
        }

        // Driver code
        public static void Main() 
        {
            string str = "malayalam";
            Console.Write(findPalindromicString(str));
        }
    } 

    // This code is contributed by Ita_c.
    ```

    ## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

    ```
    <?php
    // PHP program to find first palindromic permutation
    // of given string
    $MAX_CHAR = 26;

    // Function to count frequency of each char in the
    // string. freq[0] for 'a',...., freq[25] for 'z'
    function countFreq($str, &$freq, $len)
    {
        for ($i = 0; $i < $len; $i++)
            $freq[ord($str[$i]) - ord('a')]++;
    }

    // Cases to check whether a palindr0mic
    // string can be formed or not
    function canMakePalindrome($freq, $len)
    {
        global $MAX_CHAR;

        // count_odd to count no of
        // chars with odd frequency
        $count_odd = 0;
        for ($i = 0; $i < $MAX_CHAR; $i++)
            if ($freq[$i] % 2 != 0)
                $count_odd++;

        // For even length string
        // no odd freq character
        if ($len % 2 == 0)
        {
            if ($count_odd > 0)
                return false;
            else
                return true;
        }

        // For odd length string
        // one odd freq character
        if ($count_odd != 1)
            return false;

        return true;
    }

    // Function to find odd freq char and
    // reducing its freq by 1returns "" if odd freq
    // char is not present
    function findOddAndRemoveItsFreq($freq)
    {
        global $MAX_CHAR;
        $odd_str = "";
        for ($i = 0; $i < $MAX_CHAR; $i++)
        {
            if ($freq[$i] % 2 != 0)
            {
                $freq[$i]--;
                $odd_str .= chr($i+ord('a'));
                return $odd_str;
            }
        }
        return $odd_str;
    }

    // To find lexicographically first palindromic
    // string.
    function findPalindromicString($str)
    {
        global $MAX_CHAR;
        $len = strlen($str);

        $freq=array_fill(0, $MAX_CHAR, 0);
        countFreq($str, $freq, $len);

        if (!canMakePalindrome($freq, $len))
            return "No Palindromic String";

        // Assigning odd freq character if present
        // else empty string.
        $odd_str = findOddAndRemoveItsFreq($freq);

        $front_str = "";
        $rear_str = " ";

        // Traverse characters in increasing order
        for ($i = 0; $i < $MAX_CHAR; $i++)
        {
            $temp = "";
            if ($freq[$i] != 0)
            {
                $ch = chr($i + ord('a'));

                // Divide all occurrences into two
                // halves. Note that odd character
                // is removed by findOddAndRemoveItsFreq()
                for ($j = 1; $j <= (int)($freq[$i]/2); $j++)
                    $temp .= $ch;

                // creating front string
                $front_str .= $temp;

                // creating rear string
                $rear_str = $temp.$rear_str;
            }
        }

        // Final palindromic string which is
        // lexicographically first
        return ($front_str.$odd_str.$rear_str);
    }

    // Driver code
    $str = "malayalam";
    echo findPalindromicString($str);

    // This code is contributed by mits
    ?>
    ```

    **输出:**

    ```
    aalmymlaa

    ```

    **时间复杂度:** O(n)，其中 n 为输入字符串的长度。假设字符串字母表的大小是常数。

    本文由**阿育什·乔哈里**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

    如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。