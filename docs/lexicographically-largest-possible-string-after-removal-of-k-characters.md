# 删除 K 个字符后字典上最大的可能字符串

> 原文:[https://www . geeksforgeeks . org/按字典顺序删除 k 个字符后的最大可能字符串/](https://www.geeksforgeeks.org/lexicographically-largest-possible-string-after-removal-of-k-characters/)

给定一个仅由小写字母组成的字符串 **S** ，任务是通过从给定字符串中移除 **K** 字符来找到字典上最大的字符串。

**示例:**

> **输入:** s = "zyxedcba "，K=1
> **输出:** zyxedcb
> **解释:**给定字符串中 ASCII 值最小的字符是“a”。
> 移除“a”会生成字典中最大的可能字符串。
> 
> **输入:**s =“abcde”，K = 2
> T3】输出: cde

**做法:**
思路是用[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/) it 来解决问题。按照以下步骤解决问题:

*   遍历字符串。
*   对于每个字符，检查它是否大于堆栈顶部[**的字符。如果发现是真的，如果 **K > 0** ，则**](https://www.geeksforgeeks.org/stack-top-c-stl/)**[弹出堆栈的顶部元素。](https://www.geeksforgeeks.org/stack-pop-method-in-java/)**
*   **将字符插入堆栈。**
*   **完成字符串遍历后，如果 **K > 0** ，则移除堆栈的前 K 个元素。**
*   **最后，将堆栈中的字符存储为**答案。**打印**答案**。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement the
// above approach
#include <bits/stdc++.h>
using namespace std;

string largestString(string num, int k)
{
    // final result string
    string ans = "";

    for (auto i : num) {

        // If the current char exceeds the
        // character at the top of the stack
        while (ans.length() && ans.back() < i
               && k > 0) {

            // Remove from the end of the string
            ans.pop_back();

            // Decrease k for the removal
            k--;
        }

        // Insert current character
        ans.push_back(i);
    }

    // Perform remaining K deletions
    // from the end of the string
    while (ans.length() and k--) {
        ans.pop_back();
    }

    // Return the string
    return ans;
}

// Driver Code
int main()
{
    string str = "zyxedcba";
    int k = 1;

    cout << largestString(str, k) << endl;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement the
// above approach
class GFG{

static String largestString(String num, int k)
{

    // Final result String
    String ans = "";

    for(char i : num.toCharArray())
    {

        // If the current char exceeds the
        // character at the top of the stack
        while (ans.length() > 0 &&
               ans.charAt(ans.length() - 1) < i &&
                                          k > 0)
        {

            // Remove from the end of the String
            ans = ans.substring(0, ans.length() - 1);

            // Decrease k for the removal
            k--;
        }

        // Insert current character
        ans += i;
    }

    // Perform remaining K deletions
    // from the end of the String
    while (ans.length() > 0 && k-- > 0)
    {
        ans = ans.substring(0, ans.length() - 1);
    }

    // Return the String
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    String str = "zyxedcba";
    int k = 1;

    System.out.print(largestString(str, k) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## **蟒蛇 3**

```
# Python3 program to implement the
# above approach
def largestString(num, k):

    # Final result string
    ans = []

    for i in range(len(num)):

        # If the current char exceeds the
        # character at the top of the stack
        while(len(ans) and ans[-1] < num[i] and
                                 k > 0):

            # Remove from the end of the string
            ans.pop()

            # Decrease k for the removal
            k -= 1

        # Insert current character
        ans.append(num[i])

    # Perform remaining K deletions
    # from the end of the string
    while(len(ans) and k):
        k -= 1
        ans.pop()

    # Return the string
    return ans

# Driver code
str = "zyxedcba"
k = 1

print(*largestString(str, k), sep = "")

# This code is contributed by divyeshrabadiya07
```

## **C#**

```
// C# program to implement the
// above approach
using System;

class GFG{

static String largestString(String num, int k)
{

    // Final result String
    String ans = "";

    foreach(char i in num.ToCharArray())
    {

        // If the current char exceeds the
        // character at the top of the stack
        while (ans.Length > 0 &&
           ans[ans.Length - 1] < i && k > 0)
        {

            // Remove from the end of the String
            ans = ans.Substring(0, ans.Length - 1);

            // Decrease k for the removal
            k--;
        }

        // Insert current character
        ans += i;
    }

    // Perform remaining K deletions
    // from the end of the String
    while (ans.Length > 0 && k-- > 0)
    {
        ans = ans.Substring(0, ans.Length - 1);
    }

    // Return the String
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    String str = "zyxedcba";
    int k = 1;

    Console.Write(largestString(str, k) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>
    // JavaScript program to implement the
    // above approach
    function largestString(num, k) {
        // Final result String
        var ans = "";

        var str = num.split("");

        for (const i of str) {
          // If the current char exceeds the
          // character at the top of the stack
          while (ans.length > 0 && ans[ans.length - 1] < i && k > 0) {
            // Remove from the end of the String
            ans = ans.substring(0, ans.length - 1);

            // Decrease k for the removal
            k--;
          }

          // Insert current character
          ans += i;
        }

        // Perform remaining K deletions
        // from the end of the String
        while (ans.length > 0 && k-- > 0) {
          ans = ans.substring(0, ans.length - 1);
        }

        // Return the String
        return ans;
    }

     // Driver Code
     var str = "zyxedcba";
     var k = 1;

     document.write(largestString(str, k) + "<br>");
</script>
```

****Output:** 

```
zyxedcb
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(N)**