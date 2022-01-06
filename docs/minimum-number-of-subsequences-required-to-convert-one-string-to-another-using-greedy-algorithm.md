# 使用贪婪算法将一个字符串转换为另一个字符串所需的最小子序列数

> 原文:[https://www . geesforgeks . org/最小子序列数-需要使用贪婪算法将一个字符串转换为另一个字符串/](https://www.geeksforgeeks.org/minimum-number-of-subsequences-required-to-convert-one-string-to-another-using-greedy-algorithm/)

给定由小写字母组成的两个字符串 **A** 和 **B** ，任务是从 **B** 中找到形成 **A** 所需的最小数量的[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)。如果无法形成，请打印-1。
**举例:**

> **输入:** A = "aacbe "，B = "aceab"
> **输出:** 3
> **说明:**
> 从 B 创建 A 所需的最小子序列数为“aa”、“cb”和“e”。
> **输入:** A =“极客”，B =“极客之月”
> **输出:** -1
> **说明:**
> 无法创建 A，因为 B 中缺少角色的

对于**蛮力方法**这里参考
[将一个字符串转换为另一个字符串所需的最小子序列数](https://www.geeksforgeeks.org/minimum-number-of-subsequences-required-to-convert-one-string-to-another/)
**贪婪方法:**

1.  创建一个由 **26 * size_of_string_B** 组成的 [2D 数组](https://www.geeksforgeeks.org/multidimensional-arrays-in-java/)，以存储字符索引的出现，并用“无限”值初始化数组。
2.  用字符串 **B** 中的字符索引维护 2D 数组
3.  如果 2D 数组中任何元素的值都是无穷大，则用同一行中的下一个值更新该值。
4.  将指针的位置初始化为 0
5.  迭代字符串 **A** 并针对每个字符–
    *   如果指针的位置是 0，并且 2D 数组中的该位置是无限的，则字符串 **B** 中不存在该字符。
    *   如果 2D 数组中的值不等于无穷大，则用指针所在位置的 2D 数组中的值更新该位置的值，因为它前面的字符不能在子序列中考虑。

下面是上述方法的实现。

## C++

```
// C++ implementation for minimum
// number of subsequences required
// to convert one string to another

#include <iostream>
using namespace std;

// Function to find the minimum number
// of subsequences required to convert
// one string to another
// S2 == A and S1 == B
int findMinimumSubsequences(string A,
                            string B){

    // At least 1 subsequence is required
    // Even in best case, when A is same as B
    int numberOfSubsequences = 1;

    // size of B
    int sizeOfB = B.size();

    // size of A
    int sizeOfA = A.size();
    int inf = 1000000;

    // Create an 2D array next[][]
    // of size 26 * sizeOfB to store
    // the next occurrence of a character
    // ('a' to 'z') as an index [0, sizeOfA - 1]
    int next[26][sizeOfB];

    // Array Initialization with infinite
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < sizeOfB; j++) {
            next[i][j] = inf;
        }
    }

    // Loop to Store the values of index
    for (int i = 0; i < sizeOfB; i++) {
        next[B[i] - 'a'][i] = i;
    }

    // If the value of next[i][j]
    // is infinite then update it with
    // next[i][j + 1]
    for (int i = 0; i < 26; i++) {
        for (int j = sizeOfB - 2; j >= 0; j--) {
            if (next[i][j] == inf) {
                next[i][j] = next[i][j + 1];
            }
        }
    }

    // Greedy algorithm to obtain the maximum
    // possible subsequence of B to cover the
    // remaining string of A using next subsequence
    int pos = 0;
    int i = 0;

    // Loop to iterate over the string A
    while (i < sizeOfA) {

        // Condition to check if the character is
        // not present in the string B
        if (pos == 0 &&
           next[A[i] - 'a'][pos] == inf) {
            numberOfSubsequences = -1;
            break;
        }

        // Condition to check if there
        // is an element in B matching with
        // character A[i] on or next to B[pos]
        // given by next[A[i] - 'a'][pos]
        else if (pos < sizeOfB &&
                  next[A[i] - 'a'][pos] < inf) {
            int nextIndex = next[A[i] - 'a'][pos] + 1;
            pos = nextIndex;
            i++;
        }

        // Condition to check if reached at the end
        // of B or no such element exists on
        // or next to A[pos], thus increment number
        // by one and reinitialise pos to zero
        else {
            numberOfSubsequences++;
            pos = 0;
        }
    }
    return numberOfSubsequences;
}

// Driver Code
int main()
{
    string A = "aacbe";
    string B = "aceab";

cout << findMinimumSubsequences(A, B);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for minimum
// number of subsequences required
// to convert one String to another
class GFG
{

// Function to find the minimum number
// of subsequences required to convert
// one String to another
// S2 == A and S1 == B
static int findMinimumSubsequences(String A,
                            String B)
{

    // At least 1 subsequence is required
    // Even in best case, when A is same as B
    int numberOfSubsequences = 1;

    // size of B
    int sizeOfB = B.length();

    // size of A
    int sizeOfA = A.length();
    int inf = 1000000;

    // Create an 2D array next[][]
    // of size 26 * sizeOfB to store
    // the next occurrence of a character
    // ('a' to 'z') as an index [0, sizeOfA - 1]
    int [][]next = new int[26][sizeOfB];

    // Array Initialization with infinite
    for (int i = 0; i < 26; i++) {
        for (int j = 0; j < sizeOfB; j++) {
            next[i][j] = inf;
        }
    }

    // Loop to Store the values of index
    for (int i = 0; i < sizeOfB; i++) {
        next[B.charAt(i) - 'a'][i] = i;
    }

    // If the value of next[i][j]
    // is infinite then update it with
    // next[i][j + 1]
    for (int i = 0; i < 26; i++) {
        for (int j = sizeOfB - 2; j >= 0; j--) {
            if (next[i][j] == inf) {
                next[i][j] = next[i][j + 1];
            }
        }
    }

    // Greedy algorithm to obtain the maximum
    // possible subsequence of B to cover the
    // remaining String of A using next subsequence
    int pos = 0;
    int i = 0;

    // Loop to iterate over the String A
    while (i < sizeOfA) {

        // Condition to check if the character is
        // not present in the String B
        if (pos == 0 &&
        next[A.charAt(i)- 'a'][pos] == inf) {
            numberOfSubsequences = -1;
            break;
        }

        // Condition to check if there
        // is an element in B matching with
        // character A[i] on or next to B[pos]
        // given by next[A[i] - 'a'][pos]
        else if (pos < sizeOfB &&
                next[A.charAt(i) - 'a'][pos] < inf) {
            int nextIndex = next[A.charAt(i) - 'a'][pos] + 1;
            pos = nextIndex;
            i++;
        }

        // Condition to check if reached at the end
        // of B or no such element exists on
        // or next to A[pos], thus increment number
        // by one and reinitialise pos to zero
        else {
            numberOfSubsequences++;
            pos = 0;
        }
    }
    return numberOfSubsequences;
}

// Driver Code
public static void main(String[] args)
{
    String A = "aacbe";
    String B = "aceab";

    System.out.print(findMinimumSubsequences(A, B));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation for minimum
# number of subsequences required
# to convert one to another

# Function to find the minimum number
# of subsequences required to convert
# one to another
# S2 == A and S1 == B
def findMinimumSubsequences(A, B):

    # At least 1 subsequence is required
    # Even in best case, when A is same as B
    numberOfSubsequences = 1

    # size of B
    sizeOfB = len(B)

    # size of A
    sizeOfA = len(A)
    inf = 1000000

    # Create an 2D array next[][]
    # of size 26 * sizeOfB to store
    # the next occurrence of a character
    # ('a' to 'z') as an index [0, sizeOfA - 1]
    next = [[ inf for i in range(sizeOfB)] for i in range(26)]

    # Loop to Store the values of index
    for i in range(sizeOfB):
        next[ord(B[i]) - ord('a')][i] = i

    # If the value of next[i][j]
    # is infinite then update it with
    # next[i][j + 1]
    for i in range(26):
        for j in range(sizeOfB-2, -1, -1):
            if (next[i][j] == inf):
                next[i][j] = next[i][j + 1]

    # Greedy algorithm to obtain the maximum
    # possible subsequence of B to cover the
    # remaining of A using next subsequence
    pos = 0
    i = 0

    # Loop to iterate over the A
    while (i < sizeOfA):

        # Condition to check if the character is
        # not present in the B
        if (pos == 0 and
        next[ord(A[i]) - ord('a')][pos] == inf):
            numberOfSubsequences = -1
            break

        # Condition to check if there
        # is an element in B matching with
        # character A[i] on or next to B[pos]
        # given by next[A[i] - 'a'][pos]
        elif (pos < sizeOfB and
                next[ord(A[i]) - ord('a')][pos] < inf) :
            nextIndex = next[ord(A[i]) - ord('a')][pos] + 1
            pos = nextIndex
            i += 1

        # Condition to check if reached at the end
        # of B or no such element exists on
        # or next to A[pos], thus increment number
        # by one and reinitialise pos to zero
        else :
            numberOfSubsequences += 1
            pos = 0

    return numberOfSubsequences

# Driver Code
if __name__ == '__main__':
    A = "aacbe"
    B = "aceab"
    print(findMinimumSubsequences(A, B))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation for minimum
// number of subsequences required
// to convert one String to another
using System;

class GFG
{

// Function to find the minimum number
// of subsequences required to convert
// one String to another
// S2 == A and S1 == B
static int findMinimumSubsequences(String A,
                                   String B)
{

    // At least 1 subsequence is required
    // Even in best case, when A is same as B
    int numberOfSubsequences = 1;

    // size of B
    int sizeOfB = B.Length;

    // size of A
    int sizeOfA = A.Length;
    int inf = 1000000;

    // Create an 2D array next[,]
    // of size 26 * sizeOfB to store
    // the next occurrence of a character
    // ('a' to 'z') as an index [0, sizeOfA - 1]
    int [,]next = new int[26,sizeOfB];

    // Array Initialization with infinite
    for (int i = 0; i < 26; i++)
    {
        for (int j = 0; j < sizeOfB; j++)
        {
            next[i, j] = inf;
        }
    }

    // Loop to Store the values of index
    for (int i = 0; i < sizeOfB; i++)
    {
        next[B[i] - 'a', i] = i;
    }

    // If the value of next[i,j]
    // is infinite then update it with
    // next[i,j + 1]
    for (int i = 0; i < 26; i++)
    {
        for (int j = sizeOfB - 2; j >= 0; j--)
        {
            if (next[i, j] == inf)
            {
                next[i, j] = next[i, j + 1];
            }
        }
    }

    // Greedy algorithm to obtain the maximum
    // possible subsequence of B to cover the
    // remaining String of A using next subsequence
    int pos = 0;
    int I = 0;

    // Loop to iterate over the String A
    while (I < sizeOfA)
    {

        // Condition to check if the character is
        // not present in the String B
        if (pos == 0 &&
            next[A[I]- 'a', pos] == inf)
        {
            numberOfSubsequences = -1;
            break;
        }

        // Condition to check if there
        // is an element in B matching with
        // character A[i] on or next to B[pos]
        // given by next[A[i] - 'a',pos]
        else if (pos < sizeOfB &&
                next[A[I] - 'a',pos] < inf)
        {
            int nextIndex = next[A[I] - 'a',pos] + 1;
            pos = nextIndex;
            I++;
        }

        // Condition to check if reached at the end
        // of B or no such element exists on
        // or next to A[pos], thus increment number
        // by one and reinitialise pos to zero
        else
        {
            numberOfSubsequences++;
            pos = 0;
        }
    }
    return numberOfSubsequences;
}

// Driver Code
public static void Main(String[] args)
{
    String A = "aacbe";
    String B = "aceab";

    Console.Write(findMinimumSubsequences(A, B));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation for minimum
// number of subsequences required
// to convert one String to another

// Function to find the minimum number
// of subsequences required to convert
// one String to another
// S2 == A and S1 == B
function findMinimumSubsequences(A,B)
{
    // At least 1 subsequence is required
    // Even in best case, when A is same as B
    let numberOfSubsequences = 1;

    // size of B
    let sizeOfB = B.length;

    // size of A
    let sizeOfA = A.length;
    let inf = 1000000;

    // Create an 2D array next[][]
    // of size 26 * sizeOfB to store
    // the next occurrence of a character
    // ('a' to 'z') as an index [0, sizeOfA - 1]
    let next = new Array(26);

    // Array Initialization with infinite
    for (let i = 0; i < 26; i++) {
        next[i]=new Array(sizeOfB);
        for (let j = 0; j < sizeOfB; j++) {
            next[i][j] = inf;
        }
    }

    // Loop to Store the values of index
    for (let i = 0; i < sizeOfB; i++) {
        next[B[i].charCodeAt(0) - 'a'.charCodeAt(0)][i] = i;
    }

    // If the value of next[i][j]
    // is infinite then update it with
    // next[i][j + 1]
    for (let i = 0; i < 26; i++) {
        for (let j = sizeOfB - 2; j >= 0; j--) {
            if (next[i][j] == inf) {
                next[i][j] = next[i][j + 1];
            }
        }
    }

    // Greedy algorithm to obtain the maximum
    // possible subsequence of B to cover the
    // remaining String of A using next subsequence
    let pos = 0;
    let i = 0;

    // Loop to iterate over the String A
    while (i < sizeOfA) {

        // Condition to check if the character is
        // not present in the String B
        if (pos == 0 &&
        next[A[i].charCodeAt(0)- 'a'.charCodeAt(0)][pos] == inf) {
            numberOfSubsequences = -1;
            break;
        }

        // Condition to check if there
        // is an element in B matching with
        // character A[i] on or next to B[pos]
        // given by next[A[i] - 'a'][pos]
        else if (pos < sizeOfB &&
                next[A[i].charCodeAt(0) - 'a'.charCodeAt(0)][pos] < inf) {
            let nextIndex = next[A[i].charCodeAt(0) - 'a'.charCodeAt(0)][pos] + 1;
            pos = nextIndex;
            i++;
        }

        // Condition to check if reached at the end
        // of B or no such element exists on
        // or next to A[pos], thus increment number
        // by one and reinitialise pos to zero
        else {
            numberOfSubsequences++;
            pos = 0;
        }
    }
    return numberOfSubsequences;
}

// Driver Code
let A = "aacbe";
let B = "aceab";
document.write(findMinimumSubsequences(A, B));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)，其中 N 是要形成的弦的长度(这里 A)
T3】辅助空间复杂度: O(N)，其中 N 是要形成的弦的长度(这里 A)