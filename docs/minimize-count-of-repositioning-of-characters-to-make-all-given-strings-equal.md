# 尽量减少字符重新定位的次数，使所有给定的字符串相等

> 原文:[https://www . geesforgeks . org/最小化字符重新定位计数使所有给定字符串相等/](https://www.geeksforgeeks.org/minimize-count-of-repositioning-of-characters-to-make-all-given-strings-equal/)

给定一个由大小为 **N** 的[弦](https://www.geeksforgeeks.org/string-data-structure/)组成的数组 **S** ，任务是检查是否有可能在任意数量的操作中使所有弦**相等**。在一次操作中，**任何**字符都可以从字符串中移除，并插入到**相同**或**不同**字符串中的任意位置。如果可以使字符串相等，则返回所需的最小操作次数**以及“**是**”，否则返回“**否**”。**

****示例:****

> ****输入:** *N = 3，S = {aaa，bbb，CCC }*
> T5】输出:是 6
> **说明:**三个字符串都可以等于字符串 abc，最少 6 次运算**
> 
> *   **{ **a** aa，bbb，ccc} - > {aa， **a** bbb，ccc}**
> *   **{a **a** ，abb，ccc} - > {a，abb， **a** ccc}**
> *   **{a，a **b** bb，accc} - > {a **b** ，abb，accc}**
> *   **{ab，ab **b** ，accc} - > {ab，ab，a **b** ccc}**
> *   **{ab，ab，abcc **c** } - > {ab **c** ，ab，abcc}**
> *   **{abc，ab，abcc **c** } - > {abc，ab **c** ，abc}**
> 
> ****输入:**T2【N = 3，S = {aba，bbb，CDA }T4**输出:**否**

****方法:**让所有**字符串**相等的想法，如果字母在所有字符串中均匀分布，就可以实现。即每个字符的**频率**应该可以被 **N** 整除。按照以下步骤解决给定的问题:**

*   **[初始化一个向量](https://www.geeksforgeeks.org/initialize-a-vector-in-cpp-different-ways/)，说**freq【】**到[存储字符串](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/)每个字符的频率。**
*   **[遍历字符串数组](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)。**
*   **[将每个字符的频率存储在向量](https://www.geeksforgeeks.org/python-frequency-of-each-character-in-string/) **哈希表**中。**
*   **最后，检查任何角色的**频率**是否不是 **N** 的**倍数**，然后打印**否****
*   **否则，用 **N** 划分每个字符的频率，使其在 N 个字符串中均匀分布**
*   **结果答案将是**原始**字符串中的**额外**字符相对于**结果**相等字符串的计数**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to check if strings
// can be formed equal or not
void solve(string S[], int N)
{
    // Vector to store the frequency
    // of characters
    vector<int> freq(26, 0);

    // Traversing the array of strings
    for (int i = 0; i < N; i++) {

        // Traversing characters of the
        // string
        for (auto x : S[i]) {

            // Updating the frequency
            freq[x - 'a']++;
        }
    }

    // Checking for each character of
    // alphabet
    for (int i = 0; i < 26; i++) {

        // If frequency is not multiple
        // of N
        if (freq[i] % N != 0) {
            cout << "No\n";
            return;
        }
    }

    // Divide frequency of each character
    // with N
    for (int i = 0; i < 26; i++)
        freq[i] /= N;

    // Store the count of minimum
    // operations
    int ans = 0;

    for (int i = 0; i < N; i++) {

        // Store frequencies of characters
        // in the original string
        vector<int> vis(26, 0);
        for (char c : S[i])
            vis++;

        // Get the count of extra characters
        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0 && vis[i] > 0) {
                ans += abs(freq[i] - vis[i]);
            }
        }
    }

    cout << "Yes " << ans << endl;
    return;
}

// Driver function
int main()
{
    int N = 3;
    string S[N] = { "aaa", "bbb", "ccc" };

    solve(S, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to check if Strings
// can be formed equal or not
static void solve(String S[], int N)
{

    // Vector to store the frequency
    // of characters
    int []freq = new int[26];

    // Traversing the array of Strings
    for (int i = 0; i < N; i++) {

        // Traversing characters of the
        // String
        for (int x : S[i].toCharArray()) {

            // Updating the frequency
            freq[x - 'a']++;
        }
    }

    // Checking for each character of
    // alphabet
    for (int i = 0; i < 26; i++) {

        // If frequency is not multiple
        // of N
        if (freq[i] % N != 0) {
            System.out.print("No\n");
            return;
        }
    }

    // Divide frequency of each character
    // with N
    for (int i = 0; i < 26; i++)
        freq[i] /= N;

    // Store the count of minimum
    // operations
    int ans = 0;

    for (int s = 0; s < N; s++) {

        // Store frequencies of characters
        // in the original String
        int []vis = new int[26];

        for (char c : S[s].toCharArray())
            vis++;

        // Get the count of extra characters
        for (int i = 0; i < 26; i++) {
            if (freq[i] > 0 && vis[i] > 0) {
                ans += Math.abs(freq[i] - vis[i]);
            }
        }
    }

    System.out.print("Yes " +  ans +"\n");
    return;
}

// Driver function
public static void main(String[] args)
{
    int N = 3;
    String S[] = { "aaa", "bbb", "ccc" };

    solve(S, N);
}
}

// This code is contributed by shikhasingrajput
```

## **蟒蛇 3**

```
# python program for the above approach

# Function to check if strings
# can be formed equal or not
def solve(S, N):

    # Vector to store the frequency
    # of characters
    freq = [0 for _ in range(26)]

    # Traversing the array of strings
    for i in range(0, N):

        # Traversing characters of the
        # string
        for x in S[i]:

            # Updating the frequency
            freq[ord(x) - ord('a')] += 1

    # Checking for each character of
    # alphabet
    for i in range(0, 26):

        # If frequency is not multiple
        # of N
        if (freq[i] % N != 0):
            print("No")
            return

    # Divide frequency of each character
    # with N
    for i in range(0, 26):
        freq[i] //= N

    # Store the count of minimum
    # operations
    ans = 0

    for i in range(0, N):

        # Store frequencies of characters
        # in the original string
        vis = [0 for _ in range(26)]
        for c in S[i]:
            vis[ord(c) - ord('a')] += 1

        # Get the count of extra characters
        for i in range(0, 26):
            if (freq[i] > 0 and vis[i] > 0):
                ans += abs(freq[i] - vis[i])

    print(f"Yes {ans}")
    return

# Driver function
if __name__ == "__main__":

    N = 3
    S = ["aaa", "bbb", "ccc"]

    solve(S, N)

# This code is contributed by rakeshsahni
```

## **C#**

```
// C# program for the above approach
using System;

class GFG{

// Function to check if Strings
// can be formed equal or not
static void solve(String []S, int N)
{

    // List to store the frequency
    // of characters
    int []freq = new int[26];

    // Traversing the array of Strings
    for(int i = 0; i < N; i++)
    {

        // Traversing characters of the
        // String
        foreach (int x in S[i].ToCharArray())
        {

            // Updating the frequency
            freq[x - 'a']++;
        }
    }

    // Checking for each character of
    // alphabet
    for(int i = 0; i < 26; i++)
    {

        // If frequency is not multiple
        // of N
        if (freq[i] % N != 0)
        {
            Console.Write("No\n");
            return;
        }
    }

    // Divide frequency of each character
    // with N
    for(int i = 0; i < 26; i++)
        freq[i] /= N;

    // Store the count of minimum
    // operations
    int ans = 0;

    for(int s = 0; s < N; s++)
    {

        // Store frequencies of characters
        // in the original String
        int []vis = new int[26];

        foreach (char c in S[s].ToCharArray())
            vis++;

        // Get the count of extra characters
        for(int i = 0; i < 26; i++)
        {
            if (freq[i] > 0 && vis[i] > 0)
            {
                ans += Math.Abs(freq[i] - vis[i]);
            }
        }
    }

    Console.Write("Yes " +  ans + "\n");
    return;
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    String []S = { "aaa", "bbb", "ccc" };

    solve(S, N);
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to check if strings
// can be formed equal or not
function solve(S, N)
{

  // Vector to store the frequency
  // of characters
  let freq = new Array(26).fill(0);

  // Traversing the array of strings
  for (let i = 0; i < N; i++) {

    // Traversing characters of the
    // string
    for (x of S[i]) {

      // Updating the frequency
      freq[x.charCodeAt(0) - 'a'.charCodeAt(0)]++;
    }
  }

  // Checking for each character of
  // alphabet
  for (let i = 0; i < 26; i++) {

    // If frequency is not multiple
    // of N
    if (freq[i] % N != 0) {
      document.write("No<br>");
      return;
    }
  }

  // Divide frequency of each character
  // with N
  for (let i = 0; i < 26; i++)
    freq[i] = Math.floor(freq[i] / N);

  // Store the count of minimum
  // operations
  let ans = 0;

  for (let i = 0; i < N; i++) {

    // Store frequencies of characters
    // in the original string
    let vis = new Array(26).fill(0);
    for (c of S[i])
      vis++;

    // Get the count of extra characters
    for (let i = 0; i < 26; i++) {
      if (freq[i] > 0 && vis[i] > 0) {
        ans += Math.abs(freq[i] - vis[i]);
      }
    }
  }

  document.write("Yes " + ans);
  return;
}

// Driver function
let N = 3;
let S = ["aaa", "bbb", "ccc"];

solve(S, N);

// This code is contributed by saurabh_jaiswal.
</script>
```

****Output**

```
Yes 6
```** 

*****时间复杂度:** O(N*26)*
***辅助空间:** O(1)***