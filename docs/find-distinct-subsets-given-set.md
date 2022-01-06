# 使用位屏蔽方法找到给定集合的所有不同子集

> 原文:[https://www . geesforgeks . org/find-distinct-subset-给定-set/](https://www.geeksforgeeks.org/find-distinct-subsets-given-set/)

给定一组正整数，求其所有子集。该集合可以包含重复的元素，因此任何重复的子集都应该在输出中只考虑一次。
**例:**

```
Input:  S = {1, 2, 2}
Output:  {}, {1}, {2}, {1, 2}, {2, 2}, {1, 2, 2}

Explanation: 
The total subsets of given set are - 
{}, {1}, {2}, {2}, {1, 2}, {1, 2}, {2, 2}, {1, 2, 2}
Here {2} and {1, 2} are repeated twice so they are considered 
only once in the output
```

**先决条件:** [能量集](https://www.geeksforgeeks.org/power-set/)
想法是使用位掩码模式生成所有组合，如[上一篇文章](https://www.geeksforgeeks.org/power-set/)中所述。但是如果元素在给定的集合中重复，上一篇文章将打印重复的子集。为了处理重复的元素，我们从给定的子集构造一个字符串，这样具有相似元素的子集将产生相同的字符串。我们维护这样一个唯一字符串的列表，最后我们解码所有这样的字符串来打印它的单个元素。
下面是它的实现–

## C++

```
// C++ program to find all subsets of given set. Any
// repeated subset is considered only once in the output
#include <bits/stdc++.h>
using namespace std;

// Utility function to split the string using a delim. Refer -
// http://stackoverflow.com/questions/236129/split-a-string-in-c
vector<string> split(const string &s, char delim)
{
    vector<string> elems;
    stringstream ss(s);
    string item;
    while (getline(ss, item, delim))
        elems.push_back(item);

    return elems;
}

// Function to find all subsets of given set. Any repeated
// subset is considered only once in the output
int printPowerSet(int arr[], int n)
{
    vector<string> list;

    /* Run counter i from 000..0 to 111..1*/
    for (int i = 0; i < (int) pow(2, n); i++)
    {
        string subset = "";

        // consider each element in the set
        for (int j = 0; j < n; j++)
        {
            // Check if jth bit in the i is set. If the bit
            // is set, we consider jth element from set
            if ((i & (1 << j)) != 0)
                subset += to_string(arr[j]) + "|";
        }

        // if subset is encountered for the first time
        // If we use set<string>, we can directly insert
        if (find(list.begin(), list.end(), subset) == list.end())
            list.push_back(subset);
    }

    // consider every subset
    for (string subset : list)
    {
        // split the subset and print its elements
        vector<string> arr = split(subset, '|');
        for (string str: arr)
            cout << str << " ";
        cout << endl;
    }
}

// Driver code
int main()
{
    int arr[] = { 10, 12, 12 };
    int n = sizeof(arr)/sizeof(arr[0]);

    printPowerSet(arr, n);

    return 0;
}
```

## 蟒蛇 3

```
# Python3 program to find all subsets of
# given set. Any repeated subset is
# considered only once in the output
def printPowerSet(arr, n):

    # Function to find all subsets of given set.
    # Any repeated subset is considered only
    # once in the output
    _list = []

    # Run counter i from 000..0 to 111..1
    for i in range(2**n):
        subset = ""

        # consider each element in the set
        for j in range(n):

            # Check if jth bit in the i is set.
            # If the bit is set, we consider
            # jth element from set
            if (i & (1 << j)) != 0:
                subset += str(arr[j]) + "|"

        # if subset is encountered for the first time
        # If we use set<string>, we can directly insert
        if subset not in _list and len(subset) > 0:
            _list.append(subset)

    # consider every subset
    for subset in _list:

        # split the subset and print its elements
        arr = subset.split('|')
        for string in arr:
            print(string, end = " ")
        print()

# Driver Code
if __name__ == '__main__':
    arr = [10, 12, 12]
    n = len(arr)
    printPowerSet(arr, n)

# This code is contributed by vibhu4agarwal
```

**输出:**

```
10 
12 
10 12 
12 12 
10 12 12 
```

该方法的时间复杂度为:(N*2 <sup>N</sup> )。

参考下面的文章，用回溯法解决这个问题。

[https://www . geeksforgeeks . org/回溯查找所有子集/](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)

本文由**阿迪蒂亚·戈尔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.GeeksforGeeks.org](http://www.contribute.GeeksforGeeks.org)写一篇文章或者把你的文章邮寄到 contribute@GeeksforGeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。