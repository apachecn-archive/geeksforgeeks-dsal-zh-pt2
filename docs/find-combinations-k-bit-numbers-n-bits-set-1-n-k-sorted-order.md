# 查找所有设置了 n 位的 k 位数字组合，其中 1 < = n < = k，排序顺序为

> 原文:[https://www . geesforgeks . org/find-combinations-k-bit-numbers-n-bits-set-1-n-k-sorted-order/](https://www.geeksforgeeks.org/find-combinations-k-bit-numbers-n-bits-set-1-n-k-sorted-order/)

给定一个数字 k，找到设置了 n 位的 k 位数字的所有可能组合，其中 1 <= n <= k。解决方案应该首先打印设置了一位的所有数字，然后打印设置了两位的数字，..直到所有 k 位都被设置的数字。如果两个数字具有相同的设定位数，那么较小的数字应该排在第一位。

示例:

```
Input: K = 3
Output:  
001 010 100 
011 101 110 
111 

Input: K = 4
Output:  
0001 0010 0100 1000 
0011 0101 0110 1001 1010 1100 
0111 1011 1101 1110 
1111 

Input: K = 5
Output:  
00001 00010 00100 01000 10000 
00011 00101 00110 01001 01010 01100 10001 10010 10100 11000 
00111 01011 01101 01110 10011 10101 10110 11001 11010 11100 
01111 10111 11011 11101 11110 
11111 

```

我们需要找到 k 比特数与 n 个集合比特的所有可能组合，其中 1 <= n <= k，如果我们仔细分析，我们会看到这个问题可以进一步分为子问题。我们可以通过在长度为 k-1 和 n-1 的所有组合前面加上 0，然后在长度为 k-1 和 n-1 的所有组合前面加上 1 来找到长度为 k 和 n 的所有组合。我们可以使用动态规划来保存子问题的解决方案。

以下是上述想法的 C++实现–

```
// C++ program find all the possible combinations of 
// k-bit numbers with n-bits set where 1 <= n <= k
#include <iostream>
#include <vector>
using namespace std;
// maximum allowed value of K
#define K 16

// DP lookup table
vector<string> DP[K][K];

// Function to find all combinations k-bit numbers with 
// n-bits set where 1 <= n <= k
void findBitCombinations(int k)
{
    string str = "";

    // DP[k][0] will store all k-bit numbers  
    // with 0 bits set (All bits are 0's)
    for (int len = 0; len <= k; len++) 
    {
        DP[len][0].push_back(str);
        str = str + "0";
    }

    // fill DP lookup table in bottom-up manner
    // DP[k][n] will store all k-bit numbers  
    // with n-bits set
    for (int len = 1; len <= k; len++)
    {
        for (int n = 1; n <= len; n++)
        {
            // prefix 0 to all combinations of length len-1 
            // with n ones
            for (string str : DP[len - 1][n])
                DP[len][n].push_back("0" + str);

            // prefix 1 to all combinations of length len-1 
            // with n-1 ones
            for (string str : DP[len - 1][n - 1])
                DP[len][n].push_back("1" + str);
        }
    }

    // print all k-bit binary strings with
    // n-bit set
    for (int n = 1; n <= k; n++) 
    {
        for (string str : DP[k][n])
            cout << str << " ";

        cout << endl;
    }
}

// Driver code
int main()
{
    int k = 5;
    findBitCombinations(k);

    return 0;
}
```

输出:

```
00000 
00001 00010 00100 01000 10000 
00011 00101 00110 01001 01010 01100 10001 10010 10100 11000 
00111 01011 01101 01110 10011 10101 10110 11001 11010 11100 
01111 10111 11011 11101 11110 
11111

```

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。