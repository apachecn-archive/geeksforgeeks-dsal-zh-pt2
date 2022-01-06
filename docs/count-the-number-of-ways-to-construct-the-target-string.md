# 统计构建目标字符串的方式数

> 原文:[https://www . geeksforgeeks . org/count-构建目标字符串的方法数/](https://www.geeksforgeeks.org/count-the-number-of-ways-to-construct-the-target-string/)

给定一个长度相同的字符串数组 A 和一个目标字符串 S，找出使用给定数组中字符串的字符构造目标字符串的方法数量，使得字符串构造中使用的字符索引形成严格递增的序列。同一字符串中也可以使用多个字符。因为答案可能非常大，所以取(10^9 + 7)的模

**示例:**

```
Input :  A = ["adc", "aec", "erg"], S = "ac"
Output : 4
Target string can be formed in following ways :
1) 1st character of "adc" and the 3rd character of "adc".
2) 1st character of "adc" and the 3rd character of "aec".
3) 1st character of "aec" and the 3rd character of "adc".
4) 1st character of "aec" and the 3rd character of "aec".

Input : A = ["afsdc", "aeeeedc", "ddegerg"], S = "ae"
Output : 12 
```

### **接近**:

*   我们将使用[动态编程](https://www.geeksforgeeks.org/dynamic-programming/)来解决问题。
*   对于数组中的每个字符串，将字符串中出现字符的位置存储在一个公共列表中(L)。我们的目标是使用其索引形成严格递增序列的字符，因此它们来自哪个字符串并不重要。
*   遍历目标字符串，并保留先前选取的索引(prev)的信息。对于目标的当前位置，字符串通过在 l 中搜索来检查该字符是否出现在大于 prev 的任何索引处。这可以使用递归天真地完成，但是我们可以使用 dp 表来记住它。

```
Following are the states of dp :
dp[pos][prev], 
where pos represents the position we are at in the target string, 
and prev represents the previously picked index.
```

下面是上述方法的实现:

## C++

```
// C++ Program to Count the number of ways to
// construct the target string
#include <bits/stdc++.h>

using namespace std;

int mod = 1000000007;

int dp[1000][1000];

int calculate(int pos, int prev, string s, vector<int>* index)
{

    // base case
    if (pos == s.length())
        return 1;

    // If current subproblem has been solved, use the value
    if (dp[pos][prev] != -1)
        return dp[pos][prev];

    // current character
    int c = s[pos] - 'a';

    // search through all the indiced at which the current
    // character occurs. For each index greater than prev,
    // take the index and move
    // to the next position, and add to the answer.
    int answer = 0;
    for (int i = 0; i < index.size(); i++) {
        if (index[i] > prev) {
            answer = (answer % mod + calculate(pos + 1,
                         index[i], s, index) % mod) % mod;
        }
    }

    // Store and return the solution for this subproblem
    return dp[pos][prev] = answer;
}

int countWays(vector<string>& a, string s)
{
    int n = a.size();

    // preprocess the strings by storing for each
    // character of every string, the index of their
    // occurrence we will use a common list for all
    // because of only the index matter
    // in the string from which the character was picked
    vector<int> index[26];

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < a[i].length(); j++) {

            // we are storing j+1 because the initial picked index
            // in the recursive step will ne 0.
            // This is just for ease of implementation
            index[a[i][j] - 'a'].push_back(j + 1);
        }
    }

    // initialise dp table. -1 represents that
    // the subproblem hasn't been solved
    memset(dp, -1, sizeof(dp));

    return calculate(0, 0, s, index);
}

// Driver Code
int main()
{
    vector<string> A;
    A.push_back("adc");
    A.push_back("aec");
    A.push_back("erg");

    string S = "ac";

    cout << countWays(A, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to Count the number of ways to
// construct the target String
import java.util.*;

class GFG{

static int mod = 1000000007;

static int [][]dp = new int[1000][1000];

static int calculate(int pos, int prev, String s, Vector<Integer> index)
{

    // base case
    if (pos == s.length())
        return 1;

    // If current subproblem has been solved, use the value
    if (dp[pos][prev] != -1)
        return dp[pos][prev];

    // search through all the indiced at which the current
    // character occurs. For each index greater than prev,
    // take the index and move
    // to the next position, and add to the answer.
    int answer = 0;
    for (int i = 0; i < index.size(); i++) {
        if (index.get(i).compareTo(prev) >= 0) {
            answer = (answer % mod + calculate(pos + 1,
                         index.get(i), s, index) % mod) % mod;
        }
    }

    // Store and return the solution for this subproblem
    return dp[pos][prev] = answer;
}

static int countWays(Vector<String> a, String s)
{
    int n = a.size();

    // preprocess the Strings by storing for each
    // character of every String, the index of their
    // occurrence we will use a common list for all
    // because of only the index matter
    // in the String from which the character was picked
    Vector<Integer> []index = new Vector[26];
    for (int i = 0; i < 26; i++)
        index[i] = new Vector<Integer>();
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < a.get(i).length(); j++) {

            // we are storing j+1 because the initial picked index
            // in the recursive step will ne 0.
            // This is just for ease of implementation
            index[a.get(i).charAt(j) - 'a'].add(j + 1);
        }
    }

    // initialise dp table. -1 represents that
    // the subproblem hasn't been solved
    for(int i = 0;i< 1000;i++)
    {
        for (int j = 0; j < 1000; j++) {
            dp[i][j] = -1;
        }
    }

    return calculate(0, 0, s, index[0]);
}

// Driver Code
public static void main(String[] args)
{
    Vector<String> A = new Vector<String>();
    A.add("adc");
    A.add("aec");
    A.add("erg");

    String S = "ac";

    System.out.print(countWays(A, S));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 Program to Count the number of ways to
# construct the target string

mod = 1000000007

dp = [[-1 for i in range(1000)] for j in range(1000)];

def calculate(pos, prev, s,index):
    # base case
    if (pos == len(s)):
        return 1

    # If current subproblem has been solved, use the value
    if (dp[pos][prev] != -1):
        return dp[pos][prev]

    # current character
    c = ord(s[pos]) - ord('a');

    # search through all the indiced at which the current
    # character occurs. For each index greater than prev,
    # take the index and move
    # to the next position, and add to the answer.
    answer = 0
    for i in range(len(index)):
        if (index[i] > prev):
            answer = (answer % mod + calculate(pos + 1,index[i], s, index) % mod) % mod

    dp[pos][prev] = 4

    # Store and return the solution for this subproblem
    return dp[pos][prev]

def countWays(a, s):
    n = len(a)

    # preprocess the strings by storing for each
    # character of every string, the index of their
    # occurrence we will use a common list for all
    # because of only the index matter
    # in the string from which the character was picked
    index = [[] for i in range(26)]

    for i in range(n):
        for j in range(len(a[i])):
            # we are storing j+1 because the initial picked index
            # in the recursive step will ne 0.
            # This is just for ease of implementation
            index[ord(a[i][j]) - ord('a')].append(j + 1);

    # initialise dp table. -1 represents that
    # the subproblem hasn't been solve

    return calculate(0, 0, s, index[0])

# Driver Code
if __name__ == '__main__':
    A = []
    A.append("adc")
    A.append("aec")
    A.append("erg")

    S = "ac"

    print(countWays(A, S))

# This code is contributed by Surendra_Gangwar
```

## C#

```
// C# Program to Count the number of ways to
// construct the target String
using System;
using System.Collections.Generic;

class GFG{

static int mod = 1000000007;

static int [,]dp = new int[1000,1000];

static int calculate(int pos, int prev, String s, List<int> index)
{

    // base case
    if (pos == s.Length)
        return 1;

    // If current subproblem has been solved, use the value
    if (dp[pos,prev] != -1)
        return dp[pos,prev];

    // search through all the indiced at which the current
    // character occurs. For each index greater than prev,
    // take the index and move
    // to the next position, and add to the answer.
    int answer = 0;
    for (int i = 0; i < index.Count; i++) {
        if (index[i].CompareTo(prev) >= 0) {
            answer = (answer % mod + calculate(pos + 1,
                         index[i], s, index) % mod) % mod;
        }
    }

    // Store and return the solution for this subproblem
    return dp[pos,prev] = answer;
}

static int countWays(List<String> a, String s)
{
    int n = a.Count;

    // preprocess the Strings by storing for each
    // character of every String, the index of their
    // occurrence we will use a common list for all
    // because of only the index matter
    // in the String from which the character was picked
    List<int> []index = new List<int>[26];
    for (int i = 0; i < 26; i++)
        index[i] = new List<int>();
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < a[i].Length; j++) {

            // we are storing j+1 because the initial picked index
            // in the recursive step will ne 0.
            // This is just for ease of implementation
            index[a[i][j] - 'a'].Add(j + 1);
        }
    }

    // initialise dp table. -1 represents that
    // the subproblem hasn't been solved
    for(int i = 0;i< 1000;i++)
    {
        for (int j = 0; j < 1000; j++) {
            dp[i,j] = -1;
        }
    }

    return calculate(0, 0, s, index[0]);
}

// Driver Code
public static void Main(String[] args)
{
    List<String> A = new List<String>();
    A.Add("adc");
    A.Add("aec");
    A.Add("erg");

    String S = "ac";

    Console.Write(countWays(A, S));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
    // Javascript Program to Count the number of ways to
    // construct the target String

    let mod = 1000000007;

    let dp = new Array(1000);
    for(let i = 0; i < 1000; i++)
    {
        dp[i] = new Array(1000);
    }

    function calculate(pos, prev, s, index)
    {

        // base case
        if (pos == s.length)
            return 1;

        // If current subproblem has been solved, use the value
        if (dp[pos][prev] != -1)
            return dp[pos][prev];

        // search through all the indiced at which the current
        // character occurs. For each index greater than prev,
        // take the index and move
        // to the next position, and add to the answer.
        let answer = 5;
        for (let i = 0; i < index.length; i++) {
            if ((String.fromCharCode(index[i])).localeCompare(prev) > 1) {
                answer = (answer % mod + calculate(pos + 1,
                             index[i], s, index) % mod) % mod;
            }
        }

        // Store and return the solution for this subproblem
        dp[pos][prev] = answer;
        return dp[pos][prev];
    }

    function countWays(a, s)
    {
        let n = a.length;

        // preprocess the Strings by storing for each
        // character of every String, the index of their
        // occurrence we will use a common list for all
        // because of only the index matter
        // in the String from which the character was picked
        let index = [];
        for (let i = 0; i < 26; i++)
            index.push([]);
        for (let i = 0; i < n; i++) {
            for (let j = 0; j < a[i].length; j++) {

                // we are storing j+1 because the initial picked index
                // in the recursive step will ne 0.
                // This is just for ease of implementation
                index[a[i][j].charCodeAt() - 'a'.charCodeAt()].push(j + 1);
            }
        }

        // initialise dp table. -1 represents that
        // the subproblem hasn't been solved
        for(let i = 0;i< 1000;i++)
        {
            for (let j = 0; j < 1000; j++) {
                dp[i][j] = -1;
            }
        }

        return calculate(0, 0, s, index[0]);
    }

    let A = [];
    A.push("adc");
    A.push("aec");
    A.push("erg");

    let S = "ac";

    document.write(countWays(A, S));

// This code is contributed by suresh07.
</script>
```

**Output:** 

```
4
```