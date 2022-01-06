# 将 N 表示为和所需的最小回文数|集合 1

> 原文:[https://www . geeksforgeeks . org/最小回文数-需要表示 n-as-sum-set-1/](https://www.geeksforgeeks.org/minimum-number-of-palindromes-required-to-express-n-as-a-sum-set-1/)

给定一个数 N，我们必须找到将 N 表示为它们的和所需的最小回文数。
**例:**

> **输入:** N = 11
> **输出:** 1
> 11 本身就是回文。
> **输入:** N = 65
> **输出:** 3
> 65 可以表示为三个回文的和(55，9，1)。

**方法:**
我们可以用动态规划来解决这个问题。其思想是首先[以排序的方式生成直到 N](https://www.geeksforgeeks.org/generate-palindromic-numbers-less-n/) 的所有回文，然后我们可以将这个问题视为[子集和问题](https://www.geeksforgeeks.org/subset-sum-problem-dp-25/)的变体，其中我们必须找到最小子集的大小，使得其和为 N。
**下面是上述方法的实现:**

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Declaring the DP table as global variable
vector<vector<long long> > dp;

// A utility for creating palindrome
int createPalindrome(int input, bool isOdd)
{
    int n = input;
    int palin = input;

    // checks if number of digits is odd or even
    // if odd then neglect the last digit of input in
    // finding reverse as in case of odd number of
    // digits middle element occur once
    if (isOdd)
        n /= 10;

    // Creates palindrome by just appending reverse
    // of number to itself
    while (n > 0) {
        palin = palin * 10 + (n % 10);
        n /= 10;
    }

    return palin;
}

// Function to generate palindromes
vector<int> generatePalindromes(int N)
{
    vector<int> palindromes;
    int number;

    // Run two times for odd and even length palindromes
    for (int j = 0; j < 2; j++) {
        // Creates palindrome numbers with first half as i.
        // Value of j decides whether we need an odd length
        // or even length palindrome.
        int i = 1;
        while ((number = createPalindrome(i++, j)) <= N)
            palindromes.push_back(number);
    }

    return palindromes;
}

// Function to find the minimum
// number of elements in a sorted
// array A[i..j] such that their sum is N
long long minimumSubsetSize(vector<int>& A, int i, int j, int N)
{
    if (!N)
        return 0;

    if (i > j || A[i] > N)
        return INT_MAX;

    if (dp[i][N])
        return dp[i][N];

    dp[i][N] = min(1 + minimumSubsetSize(A, i + 1, j,
                                         N - A[i]),
                   minimumSubsetSize(A, i + 1, j, N));

    return dp[i][N];
}

// Function to find the minimum
// number of palindromes that N
// can be expressed as a sum of
int minimumNoOfPalindromes(int N)
{
    // Getting the list of all palindromes upto N
    vector<int> palindromes = generatePalindromes(N);

    // Sorting the list of palindromes
    sort(palindromes.begin(), palindromes.end());

    // Initializing the DP table
    dp = vector<vector<long long> >(palindromes.size(),
                                    vector<long long>(N + 1, 0));

    // Returning the required value
    return minimumSubsetSize(palindromes, 0,
                             palindromes.size() - 1, N);
}

// Driver code
int main()
{
    int N = 65;
    cout << minimumNoOfPalindromes(N);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Declaring the DP table as global variable
dp = [[0 for i in range(1000)] for i in range(1000)]

# A utility for creating palindrome
def createPalindrome(input, isOdd):

    n = input
    palin = input

    # checks if number of digits is odd or even
    # if odd then neglect the last digit of input in
    # finding reverse as in case of odd number of
    # digits middle element occur once
    if (isOdd):
        n //= 10

    # Creates palindrome by just appending reverse
    # of number to itself
    while (n > 0):
        palin = palin * 10 + (n % 10)
        n //= 10

    return palin

# Function to generate palindromes
def generatePalindromes(N):

    palindromes = []
    number = 0

    # Run two times for odd and even length palindromes
    for j in range(2):

        # Creates palindrome numbers with first half as i.
        # Value of j decides whether we need an odd length
        # or even length palindrome.
        i = 1
        number = createPalindrome(i, j)
        while number <= N:
            number = createPalindrome(i, j)
            palindromes.append(number)
            i += 1

    return palindromes

# Function to find the minimum
# number of elements in a sorted
# array A[i..j] such that their sum is N
def minimumSubsetSize(A, i, j, N):

    if (not N):
        return 0

    if (i > j or A[i] > N):
        return 10**9

    if (dp[i][N]):
        return dp[i][N]

    dp[i][N] = min(1 + minimumSubsetSize(A, i + 1, j, N - A[i]),
                    minimumSubsetSize(A, i + 1, j, N))

    return dp[i][N]

# Function to find the minimum
# number of palindromes that N
# can be expressed as a sum of
def minimumNoOfPalindromes(N):

    # Getting the list of all palindromes upto N
    palindromes = generatePalindromes(N)

    # Sorting the list of palindromes
    palindromes = sorted(palindromes)

    # Returning the required value
    return minimumSubsetSize(palindromes, 0, len(palindromes) - 1, N)

# Driver code
N = 65
print(minimumNoOfPalindromes(N))

# This code is contributed by mohit kumar 29
```

**Output:** 

```
3
```