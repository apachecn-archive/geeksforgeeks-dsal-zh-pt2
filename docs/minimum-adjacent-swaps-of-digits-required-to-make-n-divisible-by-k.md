# 使 N 能被 K 整除所需的最少相邻数字互换

> 原文:[https://www . geeksforgeeks . org/最小相邻数字互换-需要使 n 被 k 整除/](https://www.geeksforgeeks.org/minimum-adjacent-swaps-of-digits-required-to-make-n-divisible-by-k/)

给定两个整数 **N** 和 **K** ，任务是计算使整数 **N** 可被 **K** 整除所需的相邻数字互换的最小数量。

**示例:**

> **输入:** N = 12345，K = 2
> **输出:** 1
> **说明:**索引 3 和 t 处的数字可以互换，这样得到的整数是 N = 12354，可以被 2 整除。因此，相邻交换所需的数量是 1，这是最小可能的数量。
> 
> **输入:** N = 10203456，K = 100
> T3】输出: 9

**方法:**给定的问题可以通过迭代给定整数的所有数字的[排列](https://www.geeksforgeeks.org/write-a-c-program-to-print-all-permutations-of-a-given-string/)并检查所有可被 K 整除的整数来解决，[将给定整数转换为当前整数所需的最小相邻交换次数](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-to-convert-a-string-into-its-given-anagram/)。以下是要遵循的步骤:

*   将给定的整数转换成字符**串**的[串](https://www.geeksforgeeks.org/string-data-structure/)，并且[以非递减顺序排序](https://www.geeksforgeeks.org/sorting-algorithms/)字符。
*   使用内置的[next _ arrange()函数](https://www.geeksforgeeks.org/stdnext_permutation-prev_permutation-c/)遍历**字符串**的所有[排列](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)。
*   如果当前排列表示的整数可被 **K** 整除，使用[这个](https://www.geeksforgeeks.org/minimum-number-of-adjacent-swaps-to-convert-a-string-into-its-given-anagram/)算法检查将 **N** 转换为当前整数所需的交换次数。
*   保持变量中所需的最小互换次数，这是必需的答案。

下面是上述方法的实现。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find minimum number of
// swaps requires to convert s1 to s2
int CountSteps(string s1, string s2, int size)
{
    int i = 0, j = 0;
    int result = 0;

    // Iterate over the first string
    // and convert every element
    while (i < size) {
        j = i;

        // Find index element of which
        // is equal to the ith element
        while (s1[j] != s2[i]) {
            j += 1;
        }

        // Swap adjacent elements in
        // the first string
        while (i < j) {

            // Swap elements
            char temp = s1[j];
            s1[j] = s1[j - 1];
            s1[j - 1] = temp;
            j -= 1;
            result += 1;
        }
        i += 1;
    }
    return result;
}

// Function to find minimum number of adjacent
// swaps required to make N divisible by K
int swapDigits(int N, int K)
{
    // Convert the integer into string
    string str = to_string(N);

    // Sort the elements of the string
    sort(str.begin(), str.end());

    // Stores the count of swaps
    int ans = INT_MAX;

    // Iterate over all permutations
    // of the given string
    do {
        // If the current integer
        // is divisible by K
        if (stoi(str) % K == 0)

            // Update ans
            ans = min(ans,
                      CountSteps(to_string(N), str,
                                 str.length()));

    } while (next_permutation(str.begin(),
                              str.end()));

    // Return Answer
    return ans;
}

// Driver Code
int main()
{
    int N = 10203456;
    int K = 100;
    cout << swapDigits(N, K);

    return 0;
}
```

## 蟒蛇 3

```
# Python 3 program for the above approach
import sys

# Function for next permutation
def next_permutation(arr):

    # Find the length of the array
    n = len(arr)

    # Start from the right most digit and
    # find the first digit that is smaller
    # than the digit next to it.
    k = n - 2
    while k >= 0:
        if arr[k] < arr[k + 1]:
            break

        k -= 1

    # Reverse the list if the digit that
    # is smaller than the digit next to
    # it is not found.
    if k < 0:
        arr = arr[::-1]
    else:
        # Find the first greatest element
        # than arr[k] from the end of the list
        for l in range(n - 1, k, -1):
            if arr[l] > arr[k]:
                break

        # Swap the elements at arr[k] and arr[l
        arr[l], arr[k] = arr[k], arr[l]

        # Reverse the list from k + 1 to the end
        # to find the most nearest greater number
        # to the given input number
        arr[k + 1:] = reversed(arr[k + 1:])

    return arr

# Function to find minimum number of
# swaps requires to convert s1 to s2
def CountSteps(s1,  s2,  size):

    i = 0
    j = 0
    result = 0

    # Iterate over the first string
    # and convert every element
    while (i < size):
        j = i
        # Find index element of which
        # is equal to the ith element
        while (s1[j] != s2[i]):
            j += 1

        # Swap adjacent elements in
        # the first string
        while (i < j):

            # Swap elements
            temp = s1[j]
            s1[j] = s1[j - 1]
            s1[j - 1] = temp
            j -= 1
            result += 1
        i += 1
    return result

# Function to find minimum number of adjacent
# swaps required to make N divisible by K
def swapDigits(N,  K):

    # Convert the integer into string
    st = str(N)
    st2 = str(N)

    # Sort the elements of the string
    st = list(st)
    st2 = list(st2)
    st.sort()
    st2.sort()

    # Stores the count of swaps
    ans = sys.maxsize

    # Iterate over all permutations
    # of the given string
    # If the current integer
    # is divisible by K
    while (next_permutation(st) != st2):
        if(int(''.join(st)) % K == 0):
            ans = min(ans,
                      CountSteps(list(str(N)), st,
                                 len(st)))

    # Return Answer
    return ans

# Driver Code
if __name__ == "__main__":

    N = 10203456
    K = 100
    print(swapDigits(N, K))

    # This code is contributed by ukasp.
```

**Output**

```
9
```

***时间复杂度:** O((log N)！*(log N)<sup>2</sup>)*
***辅助空间:** O(log N)*