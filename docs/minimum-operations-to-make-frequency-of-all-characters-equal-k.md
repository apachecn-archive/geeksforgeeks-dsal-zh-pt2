# 使所有字符的频率等于 K 的最小操作

> 原文:[https://www . geesforgeks . org/最小操作使所有字符的频率相等-k/](https://www.geeksforgeeks.org/minimum-operations-to-make-frequency-of-all-characters-equal-k/)

给定一个长度为 n 的字符串 S，任务是找到字符串上所需的最小步数，这样它就正好有相同频率的 **K** 个不同的字母。
**注**:一步到位，我们可以把一个字母换成任何其他字母。
**例:**

```
Input: S = "abbc", N = 4, K = 2
Output: 1 
In one step convert 'c' to 'a'. Hence string has 
two different letters a and b both 
occurring 2 times. 
```

**接近** :

1.  检查 K 是否除以 N，那么只有可能转换给定的字符串，否则不能。
2.  在数组 a 中保持字符串 S 中所有字母的计数
3.  评估 **E = N/K** ，字母在最终字符串中出现的频率。
4.  将频率大于或等于 E 且小于 E 的字母分成两部分。
5.  保持每个字母表将其计数转换为 E 所需的步数，对上述步骤中获得的向量进行排序。
6.  最后，尽一切可能选择:

```
Set 1 : 0   Set 2 : K
Set 1 : 1   Set 2 : K-1 .... so on
```

2.  保留一个*和*变量，以计算第 6 步中所有可能性中的最小步数。
3.  假设 L1 是集合 1 所需的操作数，L2 是集合 2 所需的操作数。那么 L2 L1 的总运营需求是最大的。假设字符串中的“a”少了一个，而“b”多了一个，我们可以将“a”改为“b”，从而减少步骤数。

以下是上述方法的实现:

## C++

```
// C++ program to convert the given string

#include <bits/stdc++.h>
using namespace std;

// Function to find the minimum number of
// operations to convert the given string
void minOperation(string S, int N, int K)
{
    // Check if N is divisible by K
    if (N % K) {
        cout << "Not Possible" << endl;
        return;
    }

    // Array to store frequency of characters
    // in given string
    int count[26] = { 0 };
    for (int i = 0; i < N; i++) {
        count[S[i] - 97]++;
    }

    int E = N / K;

    vector<int> greaterE;
    vector<int> lessE;

    for (int i = 0; i < 26; i++) {

        // Two arrays with number of operations
        // required
        if (count[i] < E)
            lessE.push_back(E - count[i]);
        else
            greaterE.push_back(count[i] - E);
    }

    sort(greaterE.begin(), greaterE.end());
    sort(lessE.begin(), lessE.end());

    int mi = INT_MAX;

    for (int i = 0; i <= K; i++) {

        // Checking for all possibility
        int set1 = i;
        int set2 = K - i;

        if (greaterE.size() >= set1 && lessE.size() >= set2) {

            int step1 = 0;
            int step2 = 0;

            for (int j = 0; j < set1; j++)
                step1 += greaterE[j];

            for (int j = 0; j < set2; j++)
                step2 += lessE[j];

            mi = min(mi, max(step1, step2));
        }
    }

    cout << mi << endl;
}

// Driver Code
int main()
{
    string S = "accb";
    int N = S.size();
    int K = 2;

    minOperation(S, N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to convert the given string
import java.util.*;

class GFG
{

    // Function to find the minimum number of
    // operations to convert the given string
    static void minOperation(String S, int N, int K)
    {
        // Check if N is divisible by K
        if (N % K != 0)
        {
            System.out.println("Not Possible");
        }
        else
        {
            // Array to store frequency of characters
            // in given string
            int [] count = new int[26];

            for (int i = 0; i < N; i++)
            {
                count[(S.charAt(i) - 97)]++;
            }

            int E = N / K;

            Vector<Integer> greaterE = new Vector<>();
            Vector<Integer> lessE = new Vector<>();

            for (int i = 0; i < 26; i++)
            {

                // Two arrays with number of operations
                // required
                if (count[i] < E)
                    lessE.add(E - count[i]);
                else
                    greaterE.add(count[i] - E);
            }

            Collections.sort(greaterE);
            Collections.sort(lessE);

            int mi = Integer.MAX_VALUE;

            for (int i = 0; i <= K; i++)
            {

                // Checking for all possibility
                int set1 = i;
                int set2 = K - i;

                if (greaterE.size() >= set1 &&
                            lessE.size() >= set2)
                {

                    int step1 = 0;
                    int step2 = 0;

                    for (int j = 0; j < set1; j++)
                        step1 += greaterE.get(j);

                    for (int j = 0; j < set2; j++)
                        step2 += lessE.get(j);

                    mi = Math.min(mi, Math.max(step1, step2));
                }
            }

            System.out.println(mi);
        }

    }

    // Driver Code
    public static void main (String[] args)
    {
        String S = "accb";
        int N = S.length();
        int K = 2;

        minOperation(S, N, K);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to convert the given string

# Function to find the minimum number of
# operations to convert the given string
def minOperation(S, N, K):

    # Check if N is divisible by K
    if N % K:
        print("Not Possible")
        return

    # Array to store frequency of
    # characters in given string
    count = [0] * 26
    for i in range(0, N):
        count[ord(S[i]) - 97] += 1

    E = N // K
    greaterE = []
    lessE = []

    for i in range(0, 26):

        # Two arrays with number of
        # operations required
        if count[i] < E:
            lessE.append(E - count[i])
        else:
            greaterE.append(count[i] - E)

    greaterE.sort()
    lessE.sort()

    mi = float('inf')
    for i in range(0, K + 1):

        # Checking for all possibility
        set1, set2 = i, K - i

        if (len(greaterE) >= set1 and
            len(lessE) >= set2):

            step1, step2 = 0, 0

            for j in range(0, set1):
                step1 += greaterE[j]

            for j in range(0, set2):
                step2 += lessE[j]

            mi = min(mi, max(step1, step2))

    print(mi)

# Driver Code
if __name__ == "__main__":

    S = "accb"
    N = len(S)
    K = 2

    minOperation(S, N, K)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to convert the given string
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the minimum number of
    // operations to convert the given string
    static void minOperation(string S, int N, int K)
    {
        // Check if N is divisible by K
        if (N % K != 0)
        {
            Console.WriteLine("Not Possible");
        }
        else
        {
            // Array to store frequency of characters
            // in given string
            int [] count = new int[26];

            for (int i = 0; i < N; i++)
            {
                count[(S[i] - 97)]++;
            }

            int E = N / K;

            List<int> greaterE = new List<int>();
            List<int> lessE = new List<int>();

            for (int i = 0; i < 26; i++)
            {

                // Two arrays with number of operations
                // required
                if (count[i] < E)
                    lessE.Add(E - count[i]);
                else
                    greaterE.Add(count[i] - E);
            }

            greaterE.Sort();
            lessE.Sort();

            int mi = Int32.MaxValue;

            for (int i = 0; i <= K; i++)
            {

                // Checking for all possibility
                int set1 = i;
                int set2 = K - i;

                if (greaterE.Count >= set1 &&
                            lessE.Count >= set2)
                {

                    int step1 = 0;
                    int step2 = 0;

                    for (int j = 0; j < set1; j++)
                        step1 += greaterE[j];

                    for (int j = 0; j < set2; j++)
                        step2 += lessE[j];

                    mi = Math.Min(mi, Math.Max(step1, step2));
                }
            }

            Console.WriteLine(mi);
        }

    }

    // Driver Code
    public static void Main ()
    {
        string S = "accb";
        int N = S.Length;
        int K = 2;

        minOperation(S, N, K);
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript program to convert the given string

// Function to find the minimum number of
// operations to convert the given string
function minOperation(S, N, K)
{
    // Check if N is divisible by K
    if (N % K) {
        document.write( "Not Possible" );
        return;
    }

    // Array to store frequency of characters
    // in given string
    var count = Array(26).fill(0);
    for (var i = 0; i < N; i++) {
        count[S[i].charCodeAt(0) - 97]++;
    }

    var E = N / K;

    var greaterE = [];
    var lessE = [];

    for (var i = 0; i < 26; i++) {

        // Two arrays with number of operations
        // required
        if (count[i] < E)
            lessE.push(E - count[i]);
        else
            greaterE.push(count[i] - E);
    }
    greaterE.sort();
    lessE.sort();

    var mi = 1000000000;

    for (var i = 0; i <= K; i++) {

        // Checking for all possibility
        var set1 = i;
        var set2 = K - i;

        if (greaterE.length >= set1 && lessE.length >= set2) {

            var step1 = 0;
            var step2 = 0;

            for (var j = 0; j < set1; j++)
                step1 += greaterE[j];

            for (var j = 0; j < set2; j++)
                step2 += lessE[j];

            mi = Math.min(mi, Math.max(step1, step2));
        }
    }

    document.write( mi );
}

// Driver Code
var S = "accb";
var N = S.length;
var K = 2;
minOperation(S, N, K);

</script>
```

**Output:** 

```
1
```