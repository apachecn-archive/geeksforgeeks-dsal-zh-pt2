# 通过移除或追加任意数字

来最小化将 N 转换为 K 的幂的操作

> 原文:[https://www . geeksforgeeks . org/通过移除或追加任意数字来最小化运算-转换-n-到-k 的幂/](https://www.geeksforgeeks.org/minimize-operations-to-convert-n-to-a-power-of-k-by-removing-or-appending-any-digit/)

给定一个数 **N** ，任务是找到将给定整数转换为任意次幂 **K** 的最小操作数，其中在每次操作时，可以删除任意数字，或者在整数后面追加任意数字。

**示例:**

> **输入:** N = 247，K = 3
> **输出:** 1
> **说明:**在第 1 次操作中，可以去掉数字 4。因此，N = 27，是 k 的幂
> 
> **输入:** N = 5，K = 2
> **输出:** 2
> **说明:**第一次操作可以去掉数字 5，第二次操作最后追加数字 2 cn。因此，N = 2，是 k 的幂

**方法:**给定问题可以通过将 **K** 的所有幂存储在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)中，并计算将给定整数 **N** 转换为当前幂所需的运算次数来解决。以下是要遵循的步骤:

*   将 **K** 的所有异能储存在[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)T4 异能中。
*   现在[遍历向量](https://www.geeksforgeeks.org/how-to-iterate-through-a-vector-without-using-iterators-in-c/) **幂**，计算将给定整数 **N** 转换为当前幂所需的运算次数，如下所示:
    *   [将给定的整数转换成字符串](https://www.geeksforgeeks.org/converting-string-to-number-and-vice-versa-in-c/) **s1** 和 **s2** 。
    *   初始化两个变量 **i = 0** 和 **j = 0** 。
    *   如果**S1【I】**等于**S2【j】**，则增加 **i** 和 **j** 。否则，只增加 **j** 。
    *   所需操作次数为**S1 . length+S2 . length –( 2 * I)**。
*   在所有值上保持最少的必需操作，这是必需的答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;
#define int long long

// Function to find all powers of
// K in the range [1, 10^18]
vector<int> findPowers(int K)
{
    // Stores the powers of K
    vector<int> powers;
    int val = 1;

    // Loop to iterte over all
    // powers in the range
    while (val <= 1e18) {
        powers.push_back(val);
        val *= K;
    }

    // Return answer
    return powers;
}

// Function to find minimum operations to
// convert given integer into a power of K
int minOperations(int N, int K)
{
    // Store all the powers of K
    vector<int> powers = findPowers(K);

    // Stores the final result
    int res = INT_MAX;

    // Loop to iterate through all
    // the powers of K
    for (int x = 0; x < powers.size(); x++) {

        // Convert integres to strings
        // for easier comparision
        string s1 = to_string(powers[x]);
        string s2 = to_string(N);

        int i = 0, j = 0;

        // Loop to calculate operations
        // required to convert s1 to s2
        while (i < s1.size() && j < s2.size()) {

            // Count no of equal character
            if (s1[i] == s2[j]) {
                i++;
            }

            // Increment j by 1
            j++;
        }

        // Update res
        res = min(res,
                  (int)(s1.size()
                        + s2.size() - 2 * i));
    }

    // Return answer;
    return res;
}

// Driver Code
int32_t main()
{
    int N = 247;
    int K = 3;
    cout << minOperations(N, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find all powers of
// K in the range [1, 10^18]
static Vector<Integer> findPowers(int K)
{
    // Stores the powers of K
    Vector<Integer> powers = new Vector<Integer>();
    int val = 1;

    // Loop to iterte over all
    // powers in the range
    while (val <= (int)(9999999999L)) {
        powers.add(val);
        val *= K;
    }

    // Return answer
    return powers;
}

// Function to find minimum operations to
// convert given integer into a power of K
static int minOperations(int N, int K)
{
    // Store all the powers of K
    Vector<Integer> powers = findPowers(K);

    // Stores the final result
    int res = Integer.MAX_VALUE;

    // Loop to iterate through all
    // the powers of K
    for (int x = 0; x < powers.size(); x++) {

        // Convert integres to Strings
        // for easier comparision
        String s1 = String.valueOf(powers.get(x));
        String s2 = String.valueOf(N);

        int i = 0, j = 0;

        // Loop to calculate operations
        // required to convert s1 to s2
        while (i < s1.length() && j < s2.length()) {

            // Count no of equal character
            if (s1.charAt(i) == s2.charAt(j)) {
                i++;
            }

            // Increment j by 1
            j++;
        }

        // Update res
        res = Math.min(res,
                  (int)(s1.length()
                        + s2.length() - 2 * i));
    }

    // Return answer;
    return res;
}

// Driver Code
public static void main(String[] args)
{
    int N = 247;
    int K = 3;
    System.out.print(minOperations(N, K));

}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 code for the above approach
import sys

# Function to find all powers of
# K in the range [1, 10^18]
def findPowers(K):

    # Stores the powers of K
    powers = []
    val = 1

    # Loop to iterte over all
    # powers in the range
    while (val <= 1e18):
        powers.append(val)
        val *= K

    # Return answer
    return powers

# Function to find minimum operations to
# convert given integer into a power of K

def minOperations(N,  K):

    # Store all the powers of K
    powers = findPowers(K)

    # Stores the final result
    res = sys.maxsize

    # Loop to iterate through all
    # the powers of K
    for x in range(len(powers)):

        # Convert integres to strings
        # for easier comparision
        s1 = str(powers[x])
        s2 = str(N)

        i = 0
        j = 0

        # Loop to calculate operations
        # required to convert s1 to s2
        while (i < len(s1) and j < len(s2)):

            # Count no of equal character
            if (s1[i] == s2[j]):
                i += 1

            # Increment j by 1
            j += 1

        # Update res
        res = min(res,
                  (int)(len(s1)
                        + len(s2) - 2 * i))

    # Return answer;
    return res

# Driver Code
if __name__ == "__main__":

    N = 247
    K = 3
    print(minOperations(N, K))

    # This code is contributed by ukasp.
```

**Output**

```
1
```

***时间复杂度:**O((log N)<sup>2</sup>)*
***辅助空间:** O(1)*