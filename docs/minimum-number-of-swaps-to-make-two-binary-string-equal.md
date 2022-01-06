# 使两个二进制字符串相等的最小交换次数

> 原文:[https://www . geesforgeks . org/最小交换次数使两个二进制字符串相等/](https://www.geeksforgeeks.org/minimum-number-of-swaps-to-make-two-binary-string-equal/)

给定两个长度相等的二进制字符串，任务是找到使它们相等的最小交换次数。仅允许在两个不同字符串的两个字符之间进行交换，如果字符串不能相等，则返回-1。

**示例:**

```
Input: s1 = "0011", s2 = "1111" 
Output: 1
Explanation:
Swap s1[0] and s2[1].After swap
s1 = 1011 and s2 = 1011 

Input: s1 = "00011", s2 = "01001"
Output: 2
Swap s1[1] and s2[1]. After swap
s1 = 01011, s2 = 00001 
Swap s1[3] and s2[1]. After swap,
s1 = 01001, s2 = 01001

```

**进场:**

*   允许 s1[i]和 s2[j]的交换，因此我们需要找出两个字符串在哪个位置不同。如果 s1[i]和 s2[i]相同，我们不会交换它们。*   如果 s1[i]和 s2[i]不相同，那么我们可以找到 3 种模式:
    1.  00 和 11，我们可以执行对角线交换，结果将是 01 01 或 10 10。在对角交换的情况下，我们需要形成对来解决这种类型的不均衡。恢复单个对所需的交换是 1。
    2.  11 和 00，我们可以执行对角线交换，结果将是 01 01 或 10 10。在对角交换的情况下，我们需要形成对来解决这种类型的不均衡。恢复单个对所需的交换是 1。
    3.  10 和 01，我们可以执行垂直交换，结果将是 00 11 或 11 00，这种类型将转换为类型 1 或类型 2 问题，并进行另一次对角交换，使它们相等。我们需要结对来解决这种类型的不均衡。恢复单个对所需的交换是 2。*   From the above observation, we can follow the below greedy method:
    1.  计算 s1[i] = 0 和 s2[i] = 1 (count0)的位置。在每对类型 1 中，我们需要(count0)/2 个对角交换。
    2.  计算 s1[i] =1 和 s2[i] = 0 (count1)的位置。在每对类型 2 中，我们需要(count1)/2 个对角交换。
    3.  如果 count0 和 count1 都是偶数，我们可以输出答案= ((count0) + (count1))/2。如果 count0 和 count1 都是奇数，我们可以有一对 3 型不均衡，所以我们需要 2 个额外的交换。将答案输出为((count0) + (count1))/2 + 2。如果 count0 和 count1 中的一个是奇数，我们就不能使两个字符串相等。因为在所有情况下我们都需要成对，奇数计数意味着单个位置将被单独留下，使得 2 个字符串不相等。

    以下是上述方法的实现:

    ## C++

    ```
    // C++ program for
    // the above approach
    #include <bits/stdc++.h>
    using namespace std;

    // Function to calculate
    // min swaps to make
    // binary strings equal
    int minSwaps(string& s1, string& s2)
    {

        int c0 = 0, c1 = 0;

        for (int i = 0; i < s1.size(); i++) {
            // Count of zero's
            if (s1[i] == '0' && s2[i] == '1') {
                c0++;
            }
            // Count of one's
            else if (s1[i] == '1' && s2[i] == '0') {
                c1++;
            }
        }

        // As discussed
        // above
        int ans = c0 / 2 + c1 / 2;

        if (c0 % 2 == 0 && c1 % 2 == 0) {
            return ans;
        }
        else if ((c0 + c1) % 2 == 0) {
            return ans + 2;
        }
        else {
            return -1;
        }
    }

    // Driver code
    int main()
    {

        string s1 = "0011", s2 = "1111";
        int ans = minSwaps(s1, s2);

        cout << ans << '\n';

        return 0;
    }
    ```

    ## Java 语言(一种计算机语言，尤用于创建网站)

    ```
    // Java program for the above approach 

    class GFG 
    {

        // Function to calculate 
        // min swaps to make 
        // binary strings equal 
        static int minSwaps(String s1, String s2) 
        { 

            int c0 = 0, c1 = 0; 

            for (int i = 0; i < s1.length(); i++)
            { 
                // Count of zero's 
                if (s1.charAt(i) == '0' && s2.charAt(i) == '1')
                { 
                    c0++; 
                }

                // Count of one's 
                else if (s1.charAt(i) == '1' && s2.charAt(i) == '0')
                { 
                    c1++; 
                } 
            } 

            // As discussed 
            // above 
            int ans = c0 / 2 + c1 / 2; 

            if (c0 % 2 == 0 && c1 % 2 == 0)
            { 
                return ans; 
            } 
            else if ((c0 + c1) % 2 == 0) 
            { 
                return ans + 2; 
            } 
            else
            { 
                return -1; 
            } 
        } 

        // Driver code 
        public static void main (String[] args)
        { 

            String s1 = "0011", s2 = "1111"; 
            int ans = minSwaps(s1, s2); 

            System.out.println(ans); 

        } 

    }

    // This code is contributed by AnkitRai01
    ```

    ## 蟒蛇 3

    ```
    # Python3 program for 
    # the above approach 

    # Function to calculate 
    # min swaps to make 
    # binary strings equal 
    def minSwaps(s1, s2) : 

        c0 = 0; c1 = 0; 

        for i in range(len(s1)) :

            # Count of zero's 
            if (s1[i] == '0' and s2[i] == '1') :
                c0 += 1; 

            # Count of one's 
            elif (s1[i] == '1' and s2[i] == '0') :
                c1 += 1; 

        # As discussed above 
        ans = c0 // 2 + c1 // 2; 

        if (c0 % 2 == 0 and c1 % 2 == 0) :
            return ans; 

        elif ((c0 + c1) % 2 == 0) :
            return ans + 2; 

        else :
            return -1; 

    # Driver code 
    if __name__ == "__main__" : 

        s1 = "0011"; s2 = "1111"; 

        ans = minSwaps(s1, s2); 

        print(ans); 

    # This code is contributed by AnkitRai01
    ```

    ## C#

    ```
    // C# program for the above approach 
    using System;

    class GFG 
    {

        // Function to calculate 
        // min swaps to make 
        // binary strings equal 
        static int minSwaps(string s1, string s2) 
        { 

            int c0 = 0, c1 = 0; 

            for (int i = 0; i < s1.Length; i++)
            { 
                // Count of zero's 
                if (s1[i] == '0' && s2[i] == '1')
                { 
                    c0++; 
                }

                // Count of one's 
                else if (s1[i] == '1' && s2[i] == '0')
                { 
                    c1++; 
                } 
            } 

            // As discussed 
            // above 
            int ans = c0 / 2 + c1 / 2; 

            if (c0 % 2 == 0 && c1 % 2 == 0)
            { 
                return ans; 
            } 
            else if ((c0 + c1) % 2 == 0) 
            { 
                return ans + 2; 
            } 
            else
            { 
                return -1; 
            } 
        } 

        // Driver code 
        public static void Main ()
        { 

            string s1 = "0011", s2 = "1111"; 
            int ans = minSwaps(s1, s2); 

            Console.WriteLine(ans); 

        } 

    }

    // This code is contributed by AnkitRai01
    ```

    **Output:**

    ```
    1

    ```

    **时间复杂度:** O(n)