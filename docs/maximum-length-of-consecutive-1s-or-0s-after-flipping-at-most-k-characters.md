# 最多翻转 K 个字符后连续 1 或 0 的最大长度

> 原文:[https://www . geesforgeks . org/最多翻转 k 个字符后连续 1 或 0 的最大长度/](https://www.geeksforgeeks.org/maximum-length-of-consecutive-1s-or-0s-after-flipping-at-most-k-characters/)

给定一个大小为 **N** 的[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** 和一个整数 **K** ，任务是在翻转给定二进制字符串 **S** 的最多 K 个字符后，找到连续 **1s** 或 **0s** 的最大长度。

**示例**:

> **输入:**S =“1001”，K = 1
> **输出:** 3
> **解释:**
> 翻转字符串索引 3 处的 K =(1)字符将字符串 S 修改为“1000”。现在连续 0 的最大长度是 3，这是必需的结果。
> 
> **输入:** S = "11011011 "，K = 3
> T3】输出: 8

**逼近:**给定的问题可以使用[双指针逼近](https://www.geeksforgeeks.org/two-pointers-technique/)和[滑动窗口逼近](https://www.geeksforgeeks.org/window-sliding-technique/)来解决。按照以下步骤解决给定的问题:

*   初始化一个[函数](https://www.geeksforgeeks.org/functions-in-c/)，说出**最大长度(S，N，ch，K)** ，在翻转**最多 K 个**字符后，找到字符的最大长度 **ch** ，使用以下步骤:
    1.  初始化一个变量，比如说 **cnt** ，它在窗口中存储字符 **ch** 的计数。
    2.  初始化一个变量，比如左边的**，它存储结果窗口的开始。**
    3.  **初始化一个变量，比如说**和**，它将连续 **K** 字符的合成长度存储为 **ch** ，最多在**K**翻转之后。**
    4.  **使用变量**右**遍历字符串 **S** ，并执行以下步骤:

        *   如果 **S【右】**的值为 **ch** ，则将 **cnt** 的值增加 **1** 。
        *   迭代直到 **cnt** 的值大于 **K** ，然后将左指针递增，将 **cnt** 的值递减 **1** 。
        *   将 **ans** 的值更新为 **ans** 和**的最大值(右–左+ 1)** 。** 
*   **完成上述步骤后，打印**最大长度(S，N，' 0 '，K)** 和**最大长度(S，N，' 1 '，K)** 返回的最大值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum length
// continuous segment of character c after
// flipping at most K characters
int maxLength(string str, int n,
              char c, int k)
{
    // Stores the maximum length
    int ans = -1;

    // Stores the count of char 'c'
    int cnt = 0;

    // Start of window
    int left = 0;

    for (int right = 0; right < n; right++) {

        if (str[right] == c) {
            cnt++;
        }

        // Remove the extra 'c' from left
        while (cnt > k) {
            if (str[left] == c) {
                cnt--;
            }

            // Increment the value of
            // the left
            left++;
        }

        // Update the resultant maximum
        // length of character ch
        ans = max(ans, right - left + 1);
    }

    return ans;
}

// Function to find the maximum length
// of consecutive 0s or 1s by flipping
// at most K characters of the string
int maxConsecutiveSegment(string S, int K)
{
    int N = S.length();

    // Print the maximum of the maximum
    // length of 0s or 1s
    return max(maxLength(S, N, '0', K),
               maxLength(S, N, '1', K));
}

// Driver Code
int main()
{
    string S = "1001";
    int K = 1;
    cout << maxConsecutiveSegment(S, K);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
public class GFG {

    // Function to find the maximum length
    // continuous segment of character c after
    // flipping at most K characters
    static int maxLength(String str, int n,
                  char c, int k)
    {

        // Stores the maximum length
        int ans = -1;

        // Stores the count of char 'c'
        int cnt = 0;

        // Start of window
        int left = 0;

        for (int right = 0; right < n; right++) {

            if (str.charAt(right) == c) {
                cnt++;
            }

            // Remove the extra 'c' from left
            while (cnt > k) {
                if (str.charAt(left) == c) {
                    cnt--;
                }

                // Increment the value of
                // the left
                left++;
            }

            // Update the resultant maximum
            // length of character ch
            ans = Math.max(ans, right - left + 1);
        }

        return ans;
    }

    // Function to find the maximum length
    // of consecutive 0s or 1s by flipping
    // at most K characters of the string
    static int maxConsecutiveSegment(String S, int K)
    {
        int N = S.length();

        // Print the maximum of the maximum
        // length of 0s or 1s
        return Math.max(maxLength(S, N, '0', K),
                   maxLength(S, N, '1', K));
    }

    // Driver Code
    int main()
    {

        return 0;
    }

  // Driver code
    public static void main (String[] args) {

        String S = "1001";
        int K = 1;
        System.out.println(maxConsecutiveSegment(S, K));

    }
}

// This code is contributed by AnkThon
```

## **蟒蛇 3**

```
# python program for the above approach

# Function to find the maximum length
# continuous segment of character c after
# flipping at most K characters
def maxLength(str, n, c, k):

    # Stores the maximum length
    ans = -1

    # Stores the count of char 'c'
    cnt = 0

    # Start of window
    left = 0

    for right in range(0, n):

        if (str[right] == c):
            cnt += 1

        # Remove the extra 'c' from left
        while (cnt > k):
            if (str[left] == c):
                cnt -= 1

            # Increment the value of
            # the left
            left += 1

        # Update the resultant maximum
        # length of character ch
        ans = max(ans, right - left + 1)

    return ans

# Function to find the maximum length
# of consecutive 0s or 1s by flipping
# at most K characters of the string
def maxConsecutiveSegment(S,  K):

    N = len(S)

    # Print the maximum of the maximum
    # length of 0s or 1s
    return max(maxLength(S, N, '0', K), maxLength(S, N, '1', K))

# Driver Code
if __name__ == "__main__":

    S = "1001"
    K = 1
    print(maxConsecutiveSegment(S, K))

# This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for the above approach
using System;
public class GFG
{

    // Function to find the maximum length
    // continuous segment of character c after
    // flipping at most K characters
    static int maxLength(String str, int n,
                  char c, int k)
    {

        // Stores the maximum length
        int ans = -1;

        // Stores the count of char 'c'
        int cnt = 0;

        // Start of window
        int left = 0;

        for (int right = 0; right < n; right++)
        {

            if (str[right] == c)
            {
                cnt++;
            }

            // Remove the extra 'c' from left
            while (cnt > k)
            {
                if (str[left] == c)
                {
                    cnt--;
                }

                // Increment the value of
                // the left
                left++;
            }

            // Update the resultant maximum
            // length of character ch
            ans = Math.Max(ans, right - left + 1);
        }

        return ans;
    }

    // Function to find the maximum length
    // of consecutive 0s or 1s by flipping
    // at most K characters of the string
    static int maxConsecutiveSegment(String S, int K)
    {
        int N = S.Length;

        // Print the maximum of the maximum
        // length of 0s or 1s
        return Math.Max(maxLength(S, N, '0', K),
                   maxLength(S, N, '1', K));
    }

    // Driver code
    public static void Main()
    {

        String S = "1001";
        int K = 1;
        Console.WriteLine(maxConsecutiveSegment(S, K));

    }
}

// This code is contributed by Saurabh Jaiswal
```

## **java 描述语言**

```
<script>
    // JavaScript program for the above approach

    // Function to find the maximum length
    // continuous segment of character c after
    // flipping at most K characters
    const maxLength = (str, n, c, k) => {
        // Stores the maximum length
        let ans = -1;

        // Stores the count of char 'c'
        let cnt = 0;

        // Start of window
        let left = 0;

        for (let right = 0; right < n; right++) {

            if (str[right] == c) {
                cnt++;
            }

            // Remove the extra 'c' from left
            while (cnt > k) {
                if (str[left] == c) {
                    cnt--;
                }

                // Increment the value of
                // the left
                left++;
            }

            // Update the resultant maximum
            // length of character ch
            ans = Math.max(ans, right - left + 1);
        }

        return ans;
    }

    // Function to find the maximum length
    // of consecutive 0s or 1s by flipping
    // at most K characters of the string
    const maxConsecutiveSegment = (S, K) => {
        let N = S.length;

        // Print the maximum of the maximum
        // length of 0s or 1s
        return Math.max(maxLength(S, N, '0', K), maxLength(S, N, '1', K));
    }

    // Driver Code
    let S = "1001";
    let K = 1;
    document.write(maxConsecutiveSegment(S, K));

// This code is contributed by rakeshsahni

</script>
```

****Output:** 

```
3
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**