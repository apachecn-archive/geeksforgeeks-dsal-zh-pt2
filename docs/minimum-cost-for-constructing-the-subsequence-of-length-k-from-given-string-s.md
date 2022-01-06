# 从给定字符串 S 构建长度为 K 的子序列的最小成本

> 原文:[https://www . geeksforgeeks . org/从给定字符串 s 构建长度为 k 的子序列的最低成本/](https://www.geeksforgeeks.org/minimum-cost-for-constructing-the-subsequence-of-length-k-from-given-string-s/)

给定一个由小写英文字母 **N** 和整数 **K** 组成的[字符串](https://www.geeksforgeeks.org/string-data-structure/) **S** ，以及一个表示每个小写英文字母成本的大小为 **26** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **成本[]** ，任务是从字符串的字符中找出构建长度为 **K** 的[子序列](https://www.geeksforgeeks.org/print-subsequences-string/)的最小成本

**示例:**

> **输入:** S = "aabcbc "，K = 3，cost[] = {2，1，3，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9}
> **输出:** 4
> **解释:**
> 构造大小为 K(= 3)的字符串的一种方法是:
> 形成取二的字符串“abb”
> 因此，构建字符串“abb”的总成本为(2 + 2 = 4)，这是可能的最小值。
> 
> **输入:** S = "aaaca "，K = 1，成本[] = {2，1，3，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，9，}
> **输出:** 2

**逼近**:给定的问题可以通过[将数组](https://www.geeksforgeeks.org/quick-sort/)**cost【】**按照递增的顺序排序来解决，并且包括给定字符串 **S** 中存在的具有最小成本的第一个 **K** 字符。按照以下步骤解决问题:

*   初始化一个 char 和 int 对的[向量，比如说， **V** 来存储角色和该角色的成本。](https://www.geeksforgeeks.org/pair-in-cpp-stl/)
*   另外，初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)称 **mp** ，键为字符，值为整数，存储字符串 **S** 每个字符的[频率。](https://www.geeksforgeeks.org/print-the-frequency-of-each-character-in-alphabetical-order/)
*   [使用变量 **i** 遍历给定的字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-c/)，并在每次迭代中增加**MP【S[I]】**的值。
*   [使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**，并在每次迭代中将对 **{char('a' + i)，cost【I】}**追加到对 **V** 的向量中。
*   [根据对](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)的第二个元素，对对【V】**的向量进行排序。**
*   **现在，初始化一个变量，将**最小成本**设为 **0** 来存储长度为 **K** 的子序列的最小成本。**
*   **[使用变量 **i** 迭代范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，25】**，并执行以下步骤:

    *   初始化一个变量，说**把**算作 **mp['a' + i]** 。
    *   如果**计数**的值小于 **K** ，则加上**计数*V[i]的值。将**设置为**最小成本**的值，并将 **K** 的值更新为**K–计数**。
    *   否则，添加 **K*V[i]。其次**到**的值闵成本**和[打破循环](https://www.geeksforgeeks.org/break-statement-cc/)。** 
*   **完成上述步骤后，打印**最小成本**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Custom comparator to sort according
// to the second element
bool comparator(pair<char, int> p1,
                pair<char, int> p2)
{
    return p1.second < p2.second;
}

// Function to find the minimum cost
// to construct a subsequence of the
// length K
int minimumCost(string S, int N,
                int K, int cost[])
{
    // Stores the minimum cost
    int minCost = 0;

    // Stores the pair of character
    // and the cost of that character
    vector<pair<char, int> > V;

    // Stores the frequency of each
    // character
    unordered_map<char, int> mp;

    // Iterate in the range [0, N-1]
    for (int i = 0; i < N; i++)
        mp[S[i]]++;

    // Iterate in the range [0, 25]
    for (int i = 0; i < 26; i++) {
        V.push_back({ char('a' + i), cost[i] });
    }

    // Sort the vector of pairs V
    // wrt the second element
    sort(V.begin(), V.end(), comparator);

    // Iterate in the range [0, 25]
    for (int i = 0; i < 26; i++) {

        // Stores the frequency of the
        // current char in the string
        int count = mp[char('a' + i)];

        // If count is less than
        // or equal to K
        if (count >= K) {

            // Update the value of
            // minCost
            minCost += V[i].second * K;
            break;
        }
        else if (count < K) {

            // Update the value of
            // minCost
            minCost += V[i].second * count;

            // Update the value
            // of K
            K = K - count;
        }
    }

    // Print the value of minCost
    return minCost;
}

// Driver Code
int main()
{
    string S = "aabcbc";
    int K = 3;
    int cost[26] = { 2, 1, 3, 9, 9, 9, 9,
                     9, 9, 9, 9, 9, 9, 9,
                     9, 9, 9, 9, 9, 9, 9,
                     9, 9, 9, 9, 9 };
    int N = S.length();
    cout << minimumCost(S, N, K, cost);

    return 0;
}
```

## **蟒蛇 3**

```
# Python3 program for the above approach

# Function to find the minimum cost
# to construct a subsequence of the
# length K
def minimumCost(S, N, K, cost):

    # Stores the minimum cost
    minCost = 0

    # Stores the pair of character
    # and the cost of that character
    V = []

    # Stores the frequency of each
    # character
    mp = {}

    # Iterate in the range [0, N-1]
    for i in range(N):
        if (S[i] in mp):
            mp[S[i]] += 1
        else:
            mp[S[i]] = 1

    # Iterate in the range [0, 25]
    for i in range(26):
        V.append([chr(ord('a') + i), cost[i]])

    # Sort the array of pairs V
    # with the second element
    while (1):
        flag = 0

        for i in range(len(V) - 1):
            if (V[i][1] > V[i + 1][1]):
                temp = V[i]
                V[i] = V[i + 1]
                V[i + 1] = temp
                flag = 1

        if (flag == 0):
            break

    # Iterate in the range [0, 25]
    for i in range(26):

        # Stores the frequency of the
        # current char in the string
        count = mp[chr(ord('a') + i)]

        # If count is less than
        # or equal to K
        if (count >= K):

            # Update the value of
            # minCost
            minCost += V[i][1] * K
            break

        elif (count < K):

            # Update the value of
            # minCost
            minCost += V[i][1] * count

            # Update the value
            # of K
            K = K - count

    # Print the value of minCost
    return minCost

# Driver Code
S = "aabcbc"
K = 3
cost = [ 2, 1, 3, 9, 9, 9, 9,
         9, 9, 9, 9, 9, 9, 9,
         9, 9, 9, 9, 9, 9, 9,
         9, 9, 9, 9, 9 ]
N = len(S)

print(minimumCost(S, N, K, cost))

# This code is contributed by _saurabh_jaiswal
```

## **java 描述语言**

```
<script>
// Javascript program for the above approach

// Function to find the minimum cost
// to construct a subsequence of the
// length K
function minimumCost(S, N, K, cost) {
    // Stores the minimum cost
    let minCost = 0;

    // Stores the pair of character
    // and the cost of that character
    let V = [];

    // Stores the frequency of each
    // character
    let mp = new Map();

    // Iterate in the range [0, N-1]
    for (let i = 0; i < N; i++) {
        if (mp.has(S[i])) {
            mp.set(S[i], mp.get(S[i]) + 1)
        } else {
            mp.set(S[i], 1)
        }
    }

    // Iterate in the range [0, 25]
    for (let i = 0; i < 26; i++) {
        V.push([String.fromCharCode('a'.charCodeAt(0) + i), cost[i]]);
    }

    // Sort the array of pairs V
    // with the second element

    while (1) {
        let flag = 0;

        for (let i = 0; i < V.length - 1; i++) {
            if (V[i][1] > V[i + 1][1]) {
                let temp = V[i];
                V[i] = V[i + 1];
                V[i + 1] = temp;
                flag = 1
            }
        }
        if(flag == 0){
            break
        }
    }

    // Iterate in the range [0, 25]
    for (let i = 0; i < 26; i++) {

        // Stores the frequency of the
        // current char in the string
        let count = mp.get(String.fromCharCode('a'.charCodeAt(0) + i));

        // If count is less than
        // or equal to K
        if (count >= K) {

            // Update the value of
            // minCost
            minCost += V[i][1] * K;
            break;
        }
        else if (count < K) {

            // Update the value of
            // minCost
            minCost += V[i][1] * count;

            // Update the value
            // of K
            K = K - count;
        }
    }

    // Print the value of minCost
    return minCost;
}

// Driver Code

let S = "aabcbc";
let K = 3;
let cost = [2, 1, 3, 9, 9, 9, 9,
    9, 9, 9, 9, 9, 9, 9,
    9, 9, 9, 9, 9, 9, 9,
    9, 9, 9, 9, 9];
let N = S.length;
document.write(minimumCost(S, N, K, cost));

// This code is contributed by gfgking.
</script>
```

****Output:** 

```
4
```** 

*****时间复杂度:**O(N)*
T5**辅助空间:** O(1)**