# 统计字符串中某个字符的频率超过另一个字符的频率的子字符串

> 原文:[https://www . geesforgeks . org/count-substrings-字符频率超过字符串中另一个字符的频率/](https://www.geeksforgeeks.org/count-substrings-having-frequency-of-a-character-exceeding-that-of-another-character-in-a-string/)

给定一个仅由字符 **a** 、 **b** 和 **c** 组成的大小为 **N** 的[字符串 **S** ，任务是找到给定字符串 **S** 的](https://www.geeksforgeeks.org/string-data-structure/)[子字符串](https://www.geeksforgeeks.org/substring-in-cpp/)的数量，使得字符 a**的[频率大于字符 **c** 的频率。](https://www.geeksforgeeks.org/print-characters-frequencies-order-occurrence/)**

**示例:**

> ***输入:**S =【abcc】*
> ***输出:** 2*
> ***解释:***
> *以下是字符出现频率大于字符 c:* 的所有可能的 S(=“abcc”)子串
> 
> 1.  *“a”:a 和 c 的频率分别为 1 和 0。*
> 2.  *“ab”:a 和 c 的频率分别为 1 和 0。*
> 
> *因此，这种子串的计数为 2。*
> 
> ***输入:**S =*abcbabc aaaabbbccc "
> T5】输出: 148

**天真方法:**解决给定问题的最简单方法是[生成给定字符串的所有可能的子串 **S**](https://www.geeksforgeeks.org/program-print-substrings-given-string/) 并计数那些字符[计数](https://www.geeksforgeeks.org/std-count-cpp-stl/)**【a】**大于字符**【c】**计数的子串。检查所有子字符串后，打印总计数的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// substrings having the frequency of
// 'a' greater than frequency of 'c'
void countSubstrings(string& s)
{
    // Stores the size of the string
    int n = s.length();

    // Stores the resultant
    // count of substrings
    int ans = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++) {

        // Store the difference between
        // frequency of 'a' and 'c'
        int cnt = 0;

        // Traverse all substrings
        // beginning at index i
        for (int j = i; j < n; j++) {
            if (s[j] == 'a')
                cnt++;
            else if (s[j] == 'c')
                cnt--;

            // If the frequency of 'a'
            // is greater than 'c'
            if (cnt > 0) {
                ans++;
            }
        }
    }

    // Print the answer
    cout << ans;
}

// Drive Code
int main()
{
    string S = "abccaab";
    countSubstrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
public class GFG
{

// Function to find the number of
// substrings having the frequency of
// 'a' greater than frequency of 'c'
public static void countSubstrings(String s)
{

    // Stores the size of the string
    int n = s.length();

    // Stores the resultant
    // count of substrings
    int ans = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++) {

        // Store the difference between
        // frequency of 'a' and 'c'
        int cnt = 0;

        // Traverse all substrings
        // beginning at index i
        for (int j = i; j < n; j++) {
            if (s.charAt(j) == 'a')
                cnt++;
            else if (s.charAt(j) == 'c')
                cnt--;

            // If the frequency of 'a'
            // is greater than 'c'
            if (cnt > 0) {
                ans++;
            }
        }
    }

    // Print the answer
    System.out.println(ans);
}

// Drive Code
public static void main(String args[])
{
    String S = "abccaab";
    countSubstrings(S);

}
}

// This code is contributed by SoumikMondal
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the number of
# substrings having the frequency of
# 'a' greater than frequency of 'c'
def countSubstrings(s):

    # Stores the size of the string
    n = len(s)

    # Stores the resultant
    # count of substrings
    ans = 0

    # Traverse the given string
    for i in range(n):

        # Store the difference between
        # frequency of 'a' and 'c'
        cnt = 0

        # Traverse all substrings
        # beginning at index i
        for j in range(i, n):
            if (s[j] == 'a'):
                cnt += 1
            elif (s[j] == 'c'):
                cnt -= 1

            # If the frequency of 'a'
            # is greater than 'c'
            if (cnt > 0):
                ans+=1

    # Prthe answer
    print (ans)

# Drive Code
if __name__ == '__main__':
    S = "abccaab"
    countSubstrings(S)

# This code is contributed by mohit kumar 29.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find the number of
// substrings having the frequency of
// 'a' greater than frequency of 'c'
function countSubstrings(s)
{
    // Stores the size of the string
    var n = s.length;

    // Stores the resultant
    // count of substrings
    var ans = 0;
    var i,j;
    // Traverse the given string
    for (i = 0; i < n; i++) {

        // Store the difference between
        // frequency of 'a' and 'c'
        var cnt = 0;

        // Traverse all substrings
        // beginning at index i
        for (j = i; j < n; j++) {
            if (s[j] == 'a')
                cnt++;
            else if (s[j] == 'c')
                cnt--;

            // If the frequency of 'a'
            // is greater than 'c'
            if (cnt > 0) {
                ans++;
            }
        }
    }

    // Print the answer
    document.write(ans);
}

// Drive Code
    var S = "abccaab";
    countSubstrings(S);

</script>
```

## C#

```
// C# program for the above approach
using System;
public class GFG {

    // Function to find the number of
    // substrings having the frequency of
    // 'a' greater than frequency of 'c'
    public static void countSubstrings(string s)
    {

        // Stores the size of the string
        int n = s.Length;

        // Stores the resultant
        // count of substrings
        int ans = 0;

        // Traverse the given string
        for (int i = 0; i < n; i++) {

            // Store the difference between
            // frequency of 'a' and 'c'
            int cnt = 0;

            // Traverse all substrings
            // beginning at index i
            for (int j = i; j < n; j++) {
                if (s[j] == 'a')
                    cnt++;
                else if (s[j] == 'c')
                    cnt--;

                // If the frequency of 'a'
                // is greater than 'c'
                if (cnt > 0) {
                    ans++;
                }
            }
        }

        // Print the answer
        Console.WriteLine(ans);
    }

    // Drive Code
    public static void Main(string[] args)
    {
        string S = "abccaab";
        countSubstrings(S);
    }
}

// This code is contributed by ukasp.
```

**Output:** 

```
11
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**上述方法也可以使用[段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)进行优化。其思想是将字符串 **S** 的所有[前缀的字符**‘a’**和**‘c’**的频率差存储在段树节点中。按照以下步骤解决问题:](https://www.geeksforgeeks.org/string-from-prefix-and-suffix-of-given-two-strings/)

*   初始化一个变量，说**计数**到 **0** ，存储字符**【a】**和**【c】**的频率差。
*   初始化一个变量，比如说 **ans** 到 **0** ，来存储字符**‘a’**的频率大于**‘c’**的子串的计数。
*   用所有的 **0** 初始化[线段树](https://www.geeksforgeeks.org/segment-tree-set-1-sum-of-given-range/)，该线段树将在遍历字符串时更新。
*   由于字符**‘a’**和**‘c’**的出现频率之差也可以为负，所以所有对段树的更新操作都是在将 **N** 添加到要更新的索引中以避免索引为负之后进行的。
*   [更新](https://www.geeksforgeeks.org/iterative-segment-tree-range-maximum-query-with-node-update/)段树中的索引 **(0 + N)** 的值作为**计数的初始值**为 **0** 。
*   [在范围**【0，N–1】**内遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)、 **S** ，并执行以下步骤:
    *   如果当前字符为“a”，则将**计数**增加 **1** 。否则，如果当前字符是“c”，那么将**计数**减 1。
    *   在段树上执行[查询，找到所有小于**计数**的值的总和，因为所有这些子串的 **'a'** 的频率都大于 **'c'** ，并将返回的值存储在一个变量中，比如 **val** 。](https://www.geeksforgeeks.org/iterative-segment-tree-range-maximum-query-with-node-update/)
    *   将**值**的值添加到变量**和**中。
    *   通过将索引**(计数+ N)** 处的值增加 **1** 来更新线段树。
*   完成上述步骤后，打印**和**的值作为子字符串的结果计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to update the segment Tree
void update(int ind, vector<int>& segTree,
            int n)
{
    // Update the value of ind
    ind += n;

    // Increment the leaf node
    segTree[ind]++;

    for (; ind > 1; ind >>= 1) {

        // Update the parent nodes
        segTree[ind >> 1] = segTree[ind]
                            + segTree[ind ^ 1];
    }
}

// Function to get the sum of all the
// elements between low to high - 1
int query(int low, int high,
          vector<int>& segTree, int n)
{
    // Initialize the leaf nodes of
    // the segment tree
    low += n;
    high += n;

    int ans = 0;

    while (low < high) {

        // Node lies completely in the
        // range of low to high
        if (low % 2) {
            ans += segTree[low];
            low++;
        }

        if (high % 2) {
            high--;
            ans += segTree[high];
        }

        // Update the value of nodes
        low >>= 1;
        high >>= 1;
    }

    return ans;
}

// Function to count the number of
// substrings which have frequency of
// 'a' greater than frequency of 'c'.
void countSubstrings(string& s)
{
    // Store the size of the string
    int n = s.length();

    // Initialize segment tree
    vector<int> segTree(4 * n);

    int count = 0;

    // Update the initial value of
    // the count
    update(n, segTree, 2 * n);

    // Stores the required result
    int ans = 0;

    // Traverse the given string
    for (int i = 0; i < n; i++) {

        // Increment count
        if (s[i] == 'a')
            count++;

        // Decrement count
        else if (s[i] == 'c')
            count--;

        // Query the segment tree to
        // find the sum of all values
        // less than count
        int val = query(0, n + count,
                        segTree, 2 * n);
        ans += val;

        // Update the current value of
        // count in the segment tree
        update(n + count, segTree, 2 * n);
    }

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    string S = "abccaab";
    countSubstrings(S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{
    static String s = "abccaab";
    static int n = s.length();
    static int[] segTree = new int[4*n];

    // Function to update the segment Tree
    static void update(int ind, int n)
    {

        // Update the value of ind
        ind += n;

        // Increment the leaf node
        segTree[ind]++;

        for (; ind > 1; ind >>= 1) {

            // Update the parent nodes
            segTree[ind >> 1] = segTree[ind]
                                + segTree[ind ^ 1];
        }
    }

    // Function to get the sum of all the
    // elements between low to high - 1
    static int query(int low, int high, int n)
    {

        // Initialize the leaf nodes of
        // the segment tree
        low += n;
        high += n;

        int ans = 0;

        while (low < high) {

            // Node lies completely in the
            // range of low to high
            if (low % 2 != 0) {
                ans += segTree[low];
                low++;
            }

            if (high % 2 != 0) {
                high--;
                ans += segTree[high];
            }

            // Update the value of nodes
            low >>= 1;
            high >>= 1;
        }

        return ans;
    }

    // Function to count the number of
    // substrings which have frequency of
    // 'a' greater than frequency of 'c'.
    static void countSubstrings()
    {
        int count = 0;

        // Update the initial value of
        // the count
        update(n, 2 * n);

        // Stores the required result
        int ans = 0;

        // Traverse the given string
        for (int i = 0; i < n; i++) {

            // Increment count
            if (s.charAt(i) == 'a')
                count++;

            // Decrement count
            else if (s.charAt(i) == 'c')
                count--;

            // Query the segment tree to
            // find the sum of all values
            // less than count
            int val = query(0, n + count, 2 * n);
            ans += val;

            // Update the current value of
            // count in the segment tree
            update(n + count, 2 * n);
        }

        // Print the answer
        System.out.print(ans);
    }

  // Driver code
    public static void main(String[] args) {
        Arrays.fill(segTree, 0);
        countSubstrings();
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python3 program for the above approach

s = "abccaab"
n = len(s)
segTree = [0]*(4*n)

# Function to update the segment Tree
def update(ind, n):

    # Update the value of ind
    ind += n

    # Increment the leaf node
    segTree[ind]+=1

    while ind > 1:
        # Update the parent nodes
        segTree[ind >> 1] = segTree[ind] + segTree[ind ^ 1]
        ind >>= 1

# Function to get the sum of all the
# elements between low to high - 1
def query(low, high, n):
    # Initialize the leaf nodes of
    # the segment tree
    low += n
    high += n

    ans = 0

    while (low < high):

        # Node lies completely in the
        # range of low to high
        if (low % 2 != 0):
            ans += segTree[low]
            low+=1

        if (high % 2 != 0):
            high-=1
            ans += segTree[high]

        # Update the value of nodes
        low >>= 1
        high >>= 1

    return ans

# Function to count the number of
# substrings which have frequency of
# 'a' greater than frequency of 'c'.
def countSubstrings():

    count = 0

    # Update the initial value of
    # the count
    update(n, 2 * n)

    # Stores the required result
    ans = 0

    # Traverse the given string
    for i in range(n):
        # Increment count
        if (s[i] == 'a'):
            count+=1

        # Decrement count
        elif (s[i] == 'c'):
            count-=1

        # Query the segment tree to
        # find the sum of all values
        # less than count
        val = query(0, n + count, 2 * n)
        ans += val

        # Update the current value of
        # count in the segment tree
        update(n + count, 2 * n)

    # Print the answer
    print(ans)

countSubstrings()

# This code is contributed by suresh07.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    static string s = "abccaab";
    static int n = s.Length;
    static int[] segTree = new int[4*n];

    // Function to update the segment Tree
    static void update(int ind, int n)
    {
        // Update the value of ind
        ind += n;

        // Increment the leaf node
        segTree[ind]++;

        for (; ind > 1; ind >>= 1) {

            // Update the parent nodes
            segTree[ind >> 1] = segTree[ind]
                                + segTree[ind ^ 1];
        }
    }

    // Function to get the sum of all the
    // elements between low to high - 1
    static int query(int low, int high, int n)
    {

        // Initialize the leaf nodes of
        // the segment tree
        low += n;
        high += n;

        int ans = 0;

        while (low < high) {

            // Node lies completely in the
            // range of low to high
            if (low % 2 != 0) {
                ans += segTree[low];
                low++;
            }

            if (high % 2 != 0) {
                high--;
                ans += segTree[high];
            }

            // Update the value of nodes
            low >>= 1;
            high >>= 1;
        }

        return ans;
    }

    // Function to count the number of
    // substrings which have frequency of
    // 'a' greater than frequency of 'c'.
    static void countSubstrings()
    {
        int count = 0;

        // Update the initial value of
        // the count
        update(n, 2 * n);

        // Stores the required result
        int ans = 0;

        // Traverse the given string
        for (int i = 0; i < n; i++) {

            // Increment count
            if (s[i] == 'a')
                count++;

            // Decrement count
            else if (s[i] == 'c')
                count--;

            // Query the segment tree to
            // find the sum of all values
            // less than count
            int val = query(0, n + count, 2 * n);
            ans += val;

            // Update the current value of
            // count in the segment tree
            update(n + count, 2 * n);
        }

        // Print the answer
        Console.Write(ans);
    }

  // Driver code
  static void Main() {
    Array.Fill(segTree, 0);
    countSubstrings();
  }
}

// This code is contributed by divyesh072019.
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    s = "abccaab";
    n = s.length
    segTree = new Array(4*n);
    segTree.fill(0);

    // Function to update the segment Tree
    function update(ind, n)
    {
        // Update the value of ind
        ind += n;

        // Increment the leaf node
        segTree[ind]++;

        for (; ind > 1; ind >>= 1) {

            // Update the parent nodes
            segTree[ind >> 1] = segTree[ind]
                                + segTree[ind ^ 1];
        }
    }

    // Function to get the sum of all the
    // elements between low to high - 1
    function query(low, high, n)
    {
        // Initialize the leaf nodes of
        // the segment tree
        low += n;
        high += n;

        let ans = 0;

        while (low < high) {

            // Node lies completely in the
            // range of low to high
            if (low % 2) {
                ans += segTree[low];
                low++;
            }

            if (high % 2) {
                high--;
                ans += segTree[high];
            }

            // Update the value of nodes
            low >>= 1;
            high >>= 1;
        }

        return ans;
    }

    // Function to count the number of
    // substrings which have frequency of
    // 'a' greater than frequency of 'c'.
    function countSubstrings()
    {
        let count = 0;

        // Update the initial value of
        // the count
        update(n, 2 * n);

        // Stores the required result
        let ans = 0;

        // Traverse the given string
        for (let i = 0; i < n; i++) {

            // Increment count
            if (s[i] == 'a')
                count++;

            // Decrement count
            else if (s[i] == 'c')
                count--;

            // Query the segment tree to
            // find the sum of all values
            // less than count
            let val = query(0, n + count, 2 * n);
            ans += val;

            // Update the current value of
            // count in the segment tree
            update(n + count, 2 * n);
        }

        // Print the answer
        document.write(ans);
    }

    countSubstrings();

   // This code is contributed by decode2207.
</script>
```

**Output:** 

```
11
```

***时间复杂度:** O(N*log N)*
***辅助空间:** O(N)*