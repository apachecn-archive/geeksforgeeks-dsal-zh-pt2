# 仅由非递增顺序的元音组成的最长子串的长度

> 原文:[https://www . geesforgeks . org/最长子串长度-仅由非递增顺序的元音组成/](https://www.geeksforgeeks.org/length-of-the-longest-substring-consisting-only-of-vowels-in-non-increasing-order/)

给定一个由小写字母组成的大小为 **N** 的[字符串](https://www.geeksforgeeks.org/string-class-in-java/) **S** ，任务是打印最长的[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的长度，该子字符串仅由按非递增顺序排序的元音组成。

**示例:**

> **输入:**S = " ueiaeaiouoiea "
> T3】输出: 6
> **说明:**唯一只由非递增顺序的元音组成的子串是子串{S[9]，S[15]}，为“uuoiea”。
> 
> **输入:**S = " uuuioea "
> T3】输出: 0

**方法:**给定的问题可以使用 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 解决。按照以下步骤解决问题:

*   将所有元音存储在一个数组中，按照降序说 **ch[]** 。
*   初始化三个变量 **res，j，**和**计数**为 **0** ，存储所需子串的最长长度，迭代所有元音，分别存储满足条件的当前子串的长度。
*   另外，初始化一个 [HashSet](https://www.geeksforgeeks.org/hashset-in-java/) 比如 **mp** 来存储满足条件的当前子串的所有不同字符。
*   [使用变量 **i** 迭代字符串](https://www.geeksforgeeks.org/iterate-over-the-characters-of-a-string-in-java/) **S** 的字符，并执行以下操作:
    *   如果 **S[i]** 等于 **ch[j]** ，则将 **S[i]** 加到 **mp** 上，然后将 **j** 和**递增 **1** 计数**。如果 **mp** 的大小等于 **5** ，则将 **res** 更新为最大**RES****计数**。
    *   否则，如果 **j + 1** 小于 **5** 且**S【I】**等于**ch【j+1】**，则增加 **j** 和**将**计数为 **1** ，并将**S【I】**加至 **mp** 。如果 **mp** 的大小等于 **5** ，则更新 **res** 至最大**RES****计数**。
    *   否则，如果 **S[i]** 等于“ **u** ”，则将 **0** 分配给 **j** 并将 **1** 分配给**计数**，将 **S[i]** 添加到 **mp** 。否则，将 **0** 分配给 **j** 和**计数**。
*   完成上述步骤后，打印 **res** 的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find length of the
// longest substring consisting only
// of vowels in non-increasing order
int count(string S, int N)
{

    // Stores all vowels in decreasing order
    char ch[] = { 'u', 'o', 'i', 'e', 'a' };

    // Stores current index of array ch[]
    int j = 0;

    // Stores the result
    int res = 0;

    // Stores the count
    // of current substring
    int count = 0;

    // Declare a HashSet to store the vowels
    unordered_set<char> mp;

    // Traverse the string, S
    for(int i = 0; i < N; ++i)
    {

        // If S[i] is equal to ch[j]
        if (S[i] == ch[j])
        {

            // Increment count by 1
            ++count;

            // Add S[i] in the mp
            mp.insert(S[i]);

            // If length of mp is 5, update res
            if (mp.size() == 5)
            {
                res = max(res, count);
            }
        }

        // Else if j+1 is less than 5 and
        // S[i] is equal to ch[j+1]
        else if (j + 1 < 5 && S[i] == ch[j + 1])
        {

            // Add the S[i] in the mp
            mp.insert(S[i]);

            // Increment count by 1
            ++count;

            // Increment j by 1
            j++;

            // If length of mp is 5, update res
            if (mp.size() == 5)
            {
                res = max(res, count);
            }
        }
        else
        {

            // Clear the mp
            mp.clear();

            // If S[i] is 'u'
            if (S[i] == 'u')
            {

                // Add S[i] in the mp
                mp.insert('u');

                // Update j and assign 1 to count
                j = 0;
                count = 1;
            }

            // Else assign 0 to j and count
            else
            {
                j = 0;
                count = 0;
            }
        }
    }

    // Return the result
    return res;
}

// Driver Code
int main()
{
    string S = "ueiaoaeiouuoiea";
    int N = S.size();

    // Function Call
    cout << count(S, N);

    return 0;
}

// This code is contributed by Kingash
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find length of the
    // longest substring consisting only
    // of vowels in non-increasing order
    static int count(String S, int N)
    {

        // Stores all vowels in decreasing order
        char ch[] = { 'u', 'o', 'i', 'e', 'a' };

        // Stores current index of array ch[]
        int j = 0;

        // Stores the result
        int res = 0;

        // Stores the count
        // of current substring
        int count = 0;

        // Declare a HashSet to store the vowels
        HashSet<Character> mp = new HashSet<>();

        // Traverse the string, S
        for (int i = 0; i < N; ++i) {

            // If S[i] is equal to ch[j]
            if (S.charAt(i) == ch[j]) {

                // Increment count by 1
                ++count;

                // Add S[i] in the mp
                mp.add(S.charAt(i));

                // If length of mp is 5, update res
                if (mp.size() == 5) {
                    res = Math.max(res, count);
                }
            }

            // Else if j+1 is less than 5 and
            // S[i] is equal to ch[j+1]
            else if (j + 1 < 5
                     && S.charAt(i) == ch[j + 1]) {

                // Add the S[i] in the mp
                mp.add(S.charAt(i));

                // Increment count by 1
                ++count;

                // Increment j by 1
                j++;

                // If length of mp is 5, update res
                if (mp.size() == 5) {
                    res = Math.max(res, count);
                }
            }
            else {

                // Clear the mp
                mp.clear();

                // If S[i] is 'u'
                if (S.charAt(i) == 'u') {

                    // Add S[i] in the mp
                    mp.add('u');

                    // Update j and assign 1 to count
                    j = 0;
                    count = 1;
                }

                // Else assign 0 to j and count
                else {
                    j = 0;
                    count = 0;
                }
            }
        }

        // Return the result
        return res;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        String S = "ueiaoaeiouuoiea";
        int N = S.length();

        // Function Call
        System.out.println(count(S, N));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find length of the
# longest substring consisting only
# of vowels in non-increasing order
def count1(S, N):

    # Stores all vowels in decreasing order
    ch = ['u', 'o', 'i', 'e', 'a']

    # Stores current index of array ch[]
    j = 0

    # Stores the result
    res = 0

    # Stores the count
    # of current substring
    count = 0;

    # Declare a HashSet to store the vowels
    mp = set()

    # Traverse the string, S
    for i in range(N):

        # If S[i] is equal to ch[j]
        if (S[i] == ch[j]):

            # Increment count by 1
            count += 1

            # Add S[i] in the mp
            mp.add(S[i])

            # If length of mp is 5, update res
            if (len(mp) == 5):
                res = max(res, count)

        # Else if j+1 is less than 5 and
        # S[i] is equal to ch[j+1]
        elif (j + 1 < 5 and S[i] == ch[j + 1]):

            # Add the S[i] in the mp
            mp.add(S[i])

            # Increment count by 1
            count += 1

            # Increment j by 1
            j += 1

            # If length of mp is 5, update res
            if (len(mp) == 5):
                res = max(res, count)
        else:

            # Clear the mp
            mp.clear()

            # If S[i] is 'u'
            if (S[i] == 'u'):

                # Add S[i] in the mp
                mp.add('u')

                # Update j and assign 1 to count
                j = 0
                count = 1

            # Else assign 0 to j and count
            else:
                j = 0
                count = 0

    # Return the result
    return res

# Driver Code
if __name__ == '__main__':

    S = "ueiaoaeiouuoiea"
    N = len(S)

    # Function Call
    print(count1(S, N))

# This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find length of the
// longest substring consisting only
// of vowels in non-increasing order
function count(S, N)
{

    // Stores all vowels in decreasing order
    let ch = [ 'u', 'o', 'i', 'e', 'a' ];

    // Stores current index of array ch[]
    let j = 0;

    // Stores the result
    let res = 0;

    // Stores the count
    // of current substring
    let count = 0;

    // Declare a HashSet to store the vowels
    let mp = new Map();

    // Traverse the string, S
    for(let i = 0; i < N; ++i)
    {

        // If S[i] is equal to ch[j]
        if (S[i] == ch[j])
        {

            // Increment count by 1
            ++count;

            // Add S[i] in the mp
            mp.set(S[i], "");

            // If length of mp is 5, update res
            if (mp.size == 5)
            {
                res = Math.max(res, count);
            }
        }

        // Else if j+1 is less than 5 and
        // S[i] is equal to ch[j+1]
        else if (j + 1 < 5 && S[i] == ch[j + 1])
        {

            // Add the S[i] in the mp
            mp.set(S[i], "");

            // Increment count by 1
            ++count;

            // Increment j by 1
            j++;

            // If length of mp is 5, update res
            if (mp.size == 5)
            {
                res = Math.max(res, count);
            }
        }
        else
        {

            // Clear the mp
            mp.clear();

            // If S[i] is 'u'
            if (S[i] == 'u')
            {

                // Add S[i] in the mp
                mp.set('u', "");

                // Update j and assign 1 to count
                j = 0;
                count = 1;
            }

            // Else assign 0 to j and count
            else
            {
                j = 0;
                count = 0;
            }
        }
    }

    // Return the result
    return res;
}

// Driver Code
let S = "ueiaoaeiouuoiea";
let N = S.length;

// Function Call
document.write(count(S, N));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)