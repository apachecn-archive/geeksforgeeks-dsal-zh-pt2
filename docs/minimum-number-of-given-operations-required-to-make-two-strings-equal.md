# 使两个字符串相等所需的最小给定操作数

> 原文:[https://www . geesforgeks . org/最小给定操作数-要求使两个字符串相等/](https://www.geeksforgeeks.org/minimum-number-of-given-operations-required-to-make-two-strings-equal/)

给定两个字符串 *A* 和 *B* ，这两个字符串都包含字符 *a* 和 *b* ，并且长度相等。两根弦中有一根 *_* (空格)。任务是通过执行以下最少次数的操作将第一个字符串转换为第二个字符串:

1.  如果 *_* 位于 *i* 位置，则 *_* 可以与位于 *i+1* 或 *i-1* 位置的字符互换。
2.  如果位置 *i+1* 和 *i+2* 的字符不同，那么 *_* 可以与位置 *i+1* 或 *i+2* 的字符互换。
3.  同样，如果位置 *i-1* 和 *i-2* 的字符不同，那么 *_* 可以与位置 *i-1* 或 *i-2* 的字符互换。

**示例:**

> **输入:**A =“ABA _ A”，B =“_ baaa”
> **输出:** 2
> 移动 1:A =“ab _ aa”(用 A[3]交换 A[2])
> 移动 2:A =“_ baaa”(用 A[2]交换 A[0])
> 
> **输入:**A =“A _ B”，B =“ab _”
> T3】输出: 1

**来源:** [定向采访集 7](https://www.geeksforgeeks.org/directi-programming-questions/)

**进场:**

*   在字符串上应用简单的[广度优先搜索](https://www.geeksforgeeks.org/breadth-first-search-or-bfs-for-a-graph/)，用于 BFS 的队列元素将包含一对*字符串，位置*，其中*位置*是字符串*字符串*中 *_* 的位置。
*   同时维护一个映射*和*，该映射将字符串存储为键，最小移动将字符串存储为值。
*   对于队列中的每个字符串 *str* ，根据给定的四个条件生成一个新的字符串 *tmp* ，并将 *vis* 映射更新为*vis【tmp】= vis【str】+1*。
*   重复上述步骤，直到队列为空或生成所需字符串，即 *tmp == B*
*   如果生成了所需的字符串，则返回*vis【str】+1*，这是将 *A* 更改为 *B* 所需的最小操作次数。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number of
// operations to convert string A to B
int minOperations(string s, string f)
{

    // If both the strings are equal then
    // no operation needs to be performed
    if (s == f)
        return 0;

    unordered_map<string, int> vis;

    int n;

    n = s.length();
    int pos = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s[i] == '_') {

            // store the position of '_'
            pos = i;
            break;
        }
    }

    // to store the generated string at every
    // move and the position of '_' within it
    queue<pair<string, int> > q;

    q.push({ s, pos });

    // vis will store the minimum operations
    // to reach that particular string
    vis[s] = 0;

    while (!q.empty()) {
        string ss = q.front().first;
        int pp = q.front().second;

        // minimum moves to reach the string ss
        int dist = vis[ss];
        q.pop();

        // try all 4 possible operations

        // if '_' can be swapped with
        // the character on it's left
        if (pp > 0) {

            // swap with the left character
            swap(ss[pp], ss[pp - 1]);

            // if the string is generated
            // for the first time
            if (!vis.count(ss)) {

                // if generated string is
                // the required string
                if (ss == f) {
                    return dist + 1;
                    break;
                }

                // update the distance for the
                // currently generated string
                vis[ss] = dist + 1;
                q.push({ ss, pp - 1 });
            }

            // restore the string before it was
            // swapped to check other cases
            swap(ss[pp], ss[pp - 1]);
        }

        // swap '_' with the character
        // on it's right this time
        if (pp < n - 1) {
            swap(ss[pp], ss[pp + 1]);
            if (!vis.count(ss)) {
                if (ss == f) {
                    return dist + 1;
                    break;
                }
                vis[ss] = dist + 1;
                q.push({ ss, pp + 1 });
            }
            swap(ss[pp], ss[pp + 1]);
        }

        // if '_' can be swapped
        // with the character 'i+2'
        if (pp > 1 && ss[pp - 1] != ss[pp - 2]) {
            swap(ss[pp], ss[pp - 2]);
            if (!vis.count(ss)) {
                if (ss == f) {
                    return dist + 1;
                    break;
                }
                vis[ss] = dist + 1;
                q.push({ ss, pp - 2 });
            }
            swap(ss[pp], ss[pp - 2]);
        }

        // if '_' can be swapped
        // with the character at 'i+2'
        if (pp < n - 2 && ss[pp + 1] != ss[pp + 2]) {
            swap(ss[pp], ss[pp + 2]);
            if (!vis.count(ss)) {
                if (ss == f) {
                    return dist + 1;
                    break;
                }
                vis[ss] = dist + 1;
                q.push({ ss, pp + 2 });
            }
            swap(ss[pp], ss[pp + 2]);
        }
    }
}

// Driver code
int main()
{

    string A = "aba_a";
    string B = "_baaa";

    cout << minOperations(A, B);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import deque

# Function to return the minimum number of
# operations to convert string A to B
def minOperations(s: str, f: str) -> int:

    # If both the strings are equal then
    # no operation needs to be performed
    if s == f:
        return 0

    vis = dict()
    n = len(s)
    pos = 0
    for i in range(n):
        if s[i] == '_':

            # store the position of '_'
            pos = i
            break

    # to store the generated string at every
    # move and the position of '_' within it
    q = deque()
    q.append((s, pos))

    # vis will store the minimum operations
    # to reach that particular string
    vis[s] = 0

    while q:
        ss = q[0][0]
        pp = q[0][1]

        # minimum moves to reach the string ss
        dist = vis[ss]
        q.popleft()

        ss = list(ss)

        # try all 4 possible operations

        # if '_' can be swapped with
        # the character on it's left
        if pp > 0:

            # swap with the left character
            ss[pp], ss[pp - 1] = ss[pp - 1], ss[pp]
            ss = ''.join(ss)

            # if the string is generated
            # for the first time
            if ss not in vis:

                # if generated string is
                # the required string
                if ss == f:
                    return dist + 1

                # update the distance for the
                # currently generated string
                vis[ss] = dist + 1
                q.append((ss, pp - 1))

            ss = list(ss)

            # restore the string before it was
            # swapped to check other cases
            ss[pp], ss[pp - 1] = ss[pp - 1], ss[pp]
            ss = ''.join(ss)

        # swap '_' with the character
        # on it's right this time
        if pp < n - 1:
            ss = list(ss)
            ss[pp], ss[pp + 1] = ss[pp + 1], ss[pp]
            ss = ''.join(ss)

            if ss not in vis:
                if ss == f:
                    return dist + 1

                vis[ss] = dist + 1
                q.append((ss, pp + 1))

            ss = list(ss)
            ss[pp], ss[pp + 1] = ss[pp + 1], ss[pp]
            ss = ''.join(ss)

        # if '_' can be swapped
        # with the character 'i+2'
        if pp > 1 and ss[pp - 1] != ss[pp - 2]:
            ss = list(ss)
            ss[pp], ss[pp - 2] = ss[pp - 2], ss[pp]
            ss = ''.join(ss)

            if ss not in vis:
                if ss == f:
                    return dist + 1

                vis[ss] = dist + 1
                q.append((ss, pp - 2))

            ss = list(ss)
            ss[pp], ss[pp - 2] = ss[pp - 2], ss[pp]
            ss = ''.join(ss)

        # if '_' can be swapped
        # with the character at 'i+2'
        if pp < n - 2 and ss[pp + 1] != ss[pp + 2]:
            ss = list(ss)
            ss[pp], ss[pp + 2] = ss[pp + 2], ss[pp]
            ss = ''.join(ss)

            if ss not in vis:
                if ss == f:
                    return dist + 1

                vis[ss] = dist + 1
                q.append((ss, pp + 2))

            ss = list(ss)
            ss[pp], ss[pp + 2] = ss[pp + 2], ss[pp]
            ss = ''.join(ss)

# Driver Code
if __name__ == "__main__":

    A = "aba_a"
    B = "_baaa"

    print(minOperations(A, B))

# This code is contributed by
# sanjeev2552
```

**Output:**

```
2

```