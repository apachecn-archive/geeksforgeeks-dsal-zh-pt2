# 给定字符串的字典最小 K 长度子序列

> 原文:[https://www . geeksforgeeks . org/按字典顺序排列的最小 k 长度给定字符串的子序列/](https://www.geeksforgeeks.org/lexicographically-smallest-k-length-subsequence-from-a-given-string/)

给定一个长度为 **N** 的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，任务是从字符串 **S** 中找到字典上最小的 **K** 长度子序列(其中 **K < N** )。

**示例:**

> **输入:**S =“bbcaab”，K = 3
> T3】输出:“aab”
> 
> **输入:**S =“aabdaabc”，K = 3
> **输出:**“AAA”

**天真方法:** 最简单的方法是 [从给定的字符串生成长度为 **K** 的所有可能的子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/) ，并将 [所有子序列](https://www.geeksforgeeks.org/print-subsequences-string/) 存储在 [向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) 中。现在， [对向量](https://www.geeksforgeeks.org/sorting-a-vector-in-c/) 进行排序，并将字符串打印在 **0 <sup>th</sup> 位置** 处，作为字典上最小的子序列。
***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是[栈数据结构](https://www.geeksforgeeks.org/stack-data-structure/)按照递增顺序跟踪字符，得到字典序最小的子序列。按照以下步骤解决问题:

*   初始化一个堆栈，比如说**回答**，这样在字符串的任何一个索引处，堆栈都应该包含到当前索引为止最小的 K 长度子序列。
*   [遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)并执行以下步骤:
    *   [如果堆叠为空](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)，则[将当前角色推入堆叠](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)。
    *   否则，迭代直到字符串 **S[i]** 的当前元素小于堆栈的[顶部元素，并保持](https://www.geeksforgeeks.org/stack-top-c-stl/)[从堆栈](https://www.geeksforgeeks.org/stack-push-and-pop-in-c-stl/)中弹出，以确保堆栈的[大小最多为 **K** 。](https://www.geeksforgeeks.org/stack-empty-and-stack-size-in-c-stl/)
    *   如果上一步后叠加的[大小为**小于 K** ，则将当前角色推入叠加。](https://www.geeksforgeeks.org/stack-size-method-in-java-with-example/)
*   完成上述步骤后，[以相反的顺序打印堆栈中存储的字符](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)以获得结果子序列字符串。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find lexicographically
// smallest subsequence of size K
void smallestSubsequence(string& S, int K)
{
    // Length of string
    int N = S.size();

    // Stores the minimum subsequence
    stack<char> answer;

    // Traverse the string S
    for (int i = 0; i < N; ++i) {

        // If the stack is empty
        if (answer.empty()) {
            answer.push(S[i]);
        }
        else {

            // Iterate till the current
            // character is less than the
            // the character at the top of stack
            while ((!answer.empty())
                   && (S[i] < answer.top())

                   // Check if there are enough
                   // characters remaining
                   // to obtain length K
                   && (answer.size() - 1 + N - i >= K)) {
                answer.pop();
            }

            // If stack size is < K
            if (answer.empty() || answer.size() < K) {

                // Push the current
                // character into it
                answer.push(S[i]);
            }
        }
    }

    // Stores the resultant string
    string ret;

    // Iterate until stack is empty
    while (!answer.empty()) {
        ret.push_back(answer.top());
        answer.pop();
    }

    // Reverse the string
    reverse(ret.begin(), ret.end());

    // Print the string
    cout << ret;
}

// Driver Code
int main()
{
    string S = "aabdaabc";
    int K = 3;
    smallestSubsequence(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

  // Function to find lexicographically
  // smallest subsequence of size K
  static void smallestSubsequence(char []S, int K)
  {

    // Length of String
    int N = S.length;

    // Stores the minimum subsequence
    Stack<Character> answer = new Stack<>();

    // Traverse the String S
    for (int i = 0; i < N; ++i) {

      // If the stack is empty
      if (answer.isEmpty()) {
        answer.add(S[i]);
      }
      else {

        // Iterate till the current
        // character is less than the
        // the character at the top of stack
        while ((!answer.isEmpty())
               && (S[i] < answer.peek())

               // Check if there are enough
               // characters remaining
               // to obtain length K
               && (answer.size() - 1 + N - i >= K)) {
          answer.pop();
        }

        // If stack size is < K
        if (answer.isEmpty() || answer.size() < K) {

          // Push the current
          // character into it
          answer.add(S[i]);
        }
      }
    }

    // Stores the resultant String
    String ret="";

    // Iterate until stack is empty
    while (!answer.isEmpty()) {
      ret+=(answer.peek());
      answer.pop();
    }

    // Reverse the String
    ret = reverse(ret);

    // Print the String
    System.out.print(ret);
  }
  static String reverse(String input) {
    char[] a = input.toCharArray();
    int l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
      char temp = a[l];
      a[l] = a[r];
      a[r] = temp;
    }
    return String.valueOf(a);
  }

  // Driver Code
  public static void main(String[] args)
  {
    String S = "aabdaabc";
    int K = 3;
    smallestSubsequence(S.toCharArray(), K);
  }
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# CPP program for the above approach

# Function to find lexicographically
# smallest subsequence of size K
def smallestSubsequence(S, K):

    # Length of string
    N = len(S)

    # Stores the minimum subsequence
    answer = []

    # Traverse the string S
    for i in range(N):

        # If the stack is empty
        if (len(answer) == 0):
            answer.append(S[i])
        else:

            # Iterate till the current
            # character is less than the
            # the character at the top of stack
            while (len(answer) > 0 and (S[i] < answer[len(answer) - 1]) and (len(answer) - 1 + N - i >= K)):
                answer = answer[:-1]

            # If stack size is < K
            if (len(answer) == 0 or len(answer) < K):

                # Push the current
                # character into it
                answer.append(S[i])

    # Stores the resultant string
    ret = []

    # Iterate until stack is empty
    while (len(answer) > 0):
        ret.append(answer[len(answer) - 1])
        answer = answer[:-1]

    # Reverse the string
    ret = ret[::-1]
    ret = ''.join(ret)

    # Print the string
    print(ret)

# Driver Code
if __name__ == '__main__':
    S = "aabdaabc"
    K = 3
    smallestSubsequence(S, K)

    # This code is contributed by SURENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG
{

  // Function to find lexicographically
  // smallest subsequence of size K
  static void smallestSubsequence(char []S, int K)
  {

    // Length of String
    int N = S.Length;

    // Stores the minimum subsequence
    Stack<char> answer = new Stack<char>();

    // Traverse the String S
    for (int i = 0; i < N; ++i) {

      // If the stack is empty
      if (answer.Count==0) {
        answer.Push(S[i]);
      }
      else {

        // Iterate till the current
        // character is less than the
        // the character at the top of stack
        while ((answer.Count!=0)
               && (S[i] < answer.Peek())

               // Check if there are enough
               // characters remaining
               // to obtain length K
               && (answer.Count - 1 + N - i >= K)) {
          answer.Pop();
        }

        // If stack size is < K
        if (answer.Count==0 || answer.Count < K) {

          // Push the current
          // character into it
          answer.Push(S[i]);
        }
      }
    }

    // Stores the resultant String
    String ret="";

    // Iterate until stack is empty
    while (answer.Count!=0) {
      ret+=(answer.Peek());
      answer.Pop();
    }

    // Reverse the String
    ret = reverse(ret);

    // Print the String
    Console.Write(ret);
  }
  static String reverse(String input) {
    char[] a = input.ToCharArray();
    int l, r = a.Length - 1;
    for (l = 0; l < r; l++, r--) {
      char temp = a[l];
      a[l] = a[r];
      a[r] = temp;
    }
    return String.Join("",a);
  }

  // Driver Code
  public static void Main(String[] args)
  {
    String S = "aabdaabc";
    int K = 3;
    smallestSubsequence(S.ToCharArray(), K);
  }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
//Javascript  program for the above approach

//function for reverse
function reverse(input) {
    a = input;
    var l, r = a.length - 1;
    for (l = 0; l < r; l++, r--) {
      var temp = a[l];
      a[l] = a[r];
      a[r] = temp;
    }
    return a;
  }

// Function to find lexicographically
// smallest subsequence of size K
function smallestSubsequence(S, K)
{
    // Length of string
    var N = S.length;

    // Stores the minimum subsequence
    answer = [];

    // Traverse the string S
    for (var i = 0; i < N; ++i) {

        // If the stack is empty
        if (answer.length==0) {
            answer.push(S[i]);
        }
        else {

            // Iterate till the current
            // character is less than the
            // the character at the top of stack
            while ((answer.length != 0) && (S[i] < answer[answer.length-1])

                   // Check if there are enough
                   // characters remaining
                   // to obtain length K
                   && (answer.length - 1 + N - i >= K)) {
                answer.pop();
            }

            // If stack size is < K
            if (answer.length==0 || answer.length < K) {

                // Push the current
                // character into it
                answer.push(S[i]);
            }
        }
    }

    // Stores the resultant string
    var ret = [];

    // Iterate until stack is empty
    while (answer.length != 0) {
        ret += answer[answer.length -1];
        answer.pop();
    }

    // Reverse the string
    reverse(ret);

    // Print the string
       document.write(ret);
}

var S = "aabdaabc";
var K = 3;
    smallestSubsequence(S, K);

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
aaa
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)