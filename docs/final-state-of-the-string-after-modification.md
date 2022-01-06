# 修改后管柱的最终状态

> 原文:[https://www . geesforgeks . org/修改后字符串的最终状态/](https://www.geeksforgeeks.org/final-state-of-the-string-after-modification/)

给定长度为 n 的字符串 *S* ，代表 n 个相邻的盒子。

1.  索引 I 处的字符 *R* 表示第 I 个方框被推向右侧。
2.  另一方面，索引 I 处的 *L* 表示第 I 个盒子被推向左侧。
3.  和一个*。*代表一个空的空间。

我们从初始配置开始，在每个时间单位，一个被推向右边的盒子会把下一个盒子推向右边，同样，一个盒子被推向左边也是如此。任务是当不可能有更多的移动时，打印所有盒子的最终位置。如果有一个子串“R.L”，那么中间的盒子将被从两个方向推，因此不再移动。

**示例:**

> **输入:**S =“RR”。L"
> **输出:** RR。L
> 第一个和第二个箱子正朝着右边。中间的点从两个方向被推动，所以不移动。
> 
> **输入:**S =“R”..r…l .
> **输出:**RRRRRRR . ll .
> 时间单位 1 :
> 第一个箱子推第二个箱子。
> 第三个箱子推第四个箱子。
> 第二个最后一个盒子推第三个最后一个盒子，配置变为
> “RR . RR . ll”
> 在时间单元 2 :
> 第二个盒子推第三个盒子，字符串变为
> “rrrr . ll”

**方法:**我们可以计算每个盒子上施加的净力。我们关心的力是一个盒子离向左的 *R* 或向右的 *L* 有多近，也就是说，我们离得越近，力就越强。

*   从左到右扫描，每次迭代力衰减 *1* ，如果再次遇到 *R* ，力重置为 *N* 。
*   同样，从右向左，我们可以找到从右开始的力(接近 *L* )。
*   对于某些方框结果[i]，如果力相等，则结果为*。*因为两侧对其施加相同力。否则，无论哪种力量更强，我们的结果都是隐含的。

> 对于字符串*S =“R”..从左到右的力是*【7，6，5，7，6，5，4，0，0】*。
> 从右向左的力是*【0，0，0，0，-4，-5，-6，-7，0】*。
> 将它们组合(在每个索引处进行算术加法运算)得到*结果= [7，6，5，7，2，0，-2，-7，0]* 。
> 因此，最终答案是*RRRRRRR . ll .**

下面是上述方法的实现:

## C++

```
// C++ implementation of above approach
#include <bits/stdc++.h>
using namespace std;

// Function to return final
// positions of the boxes
string pushBoxes(string S)
{
    int N = S.length();
    vector<int> force(N, 0);

    // Populate forces going
    // from left to right
    int f = 0;
    for(int i = 0; i < N; i++)
    {
        if (S[i] == 'R')
        {
            f = N;
        }
        else if (S[i] == 'L')
        {
            f = 0;
        }
        else
        {
            f = max(f - 1, 0);
        }
        force[i] += f;
    }

    // Populate forces going from right to left
    f = 0;
    for(int i = N - 1; i >= 0; i--)
    {
        if (S[i] == 'L')
        {
            f = N;
        }
        else if (S[i] == 'R')
        {
            f = 0;
        }
        else
        {
            f = max(f - 1, 0);
        }
        force[i] -= f;
    }

    // return final state of boxes
    string ans;
    for(int f : force)
    {
        ans += f == 0 ? '.' : f > 0 ? 'R' : 'L';
    }
    return ans;
}

// Driver code
int main()
{
    string S = ".L.R...LR..L..";

    // Function call to print answer
    cout << pushBoxes(S);
}

// This code is contributed by sanjeev2552
```

## 蟒蛇 3

```
# Python3 implementation of above approach

# Function to return final
# positions of the boxes
def pushBoxes(S):

    N = len(S)
    force = [0] * N

    # Populate forces going from left to right
    f = 0
    for i in range(0, N):

        if S[i] == 'R':
            f = N
        elif S[i] == 'L':
            f = 0
        else:
            f = max(f - 1, 0)
        force[i] += f

    # Populate forces going from right to left
    f = 0
    for i in range(N - 1, -1, -1):

        if S[i] == 'L':
            f = N
        elif S[i] == 'R':
            f = 0
        else:
            f = max(f - 1, 0)
        force[i] -= f

    # return final state of boxes
    return "".join('.' if f == 0 else 'R' if f > 0 else 'L'
                   for f in force)

# Driver code
S = ".L.R...LR..L.."

# Function call to print answer
print(pushBoxes(S))
```

**Output:** 

```
LL.RR.LLRRLL..

```