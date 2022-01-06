# 所有给定句子中的最小字数

> 原文:[https://www . geesforgeks . org/在所有给定的句子中字数最少/](https://www.geeksforgeeks.org/minimum-count-of-words-among-all-the-given-sentences/)

给定 **N** 个小写句子，任务是在所有这些句子中找到最小字数。

**示例:**

> ***输入:** arr[] = {*
> *【有一头牛】、*
> *【牛是我们的母亲】、*
> *【牛给我们奶且奶是甜的】、*
> *【有一个爱牛的男孩】}*
> ***输出:** 4*
> ***解释:**既有第一个也有第二个*
> 
> **输入:**【arr[]=
> *【ABC AAC ABCD CCC】，**【AC ABC CCA】，**【abca aaac ABCD CCC】*

**方法:**这是一个基于实现的问题。这个想法是为所有给定的句子找到一个句子中的[字数，并在一个变量中保持最小的字数，这个变量就是所需的答案。](https://www.geeksforgeeks.org/count-words-in-a-given-string/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find count of
// words in the given string
int countword(string& a)
{
    // Stores word count
    int count = 1;
    for (int i = 0; i < a.size(); i++) {

        // If a new word is
        // encountered
        if (a[i] == ' ')
            count++;
    }

    // Return count
    return count;
}

// Function to find minimum count of
// words among all given sentences
int countleastWords(string arr[], int N)
{
    // Stores the final answer
    int ans = INT_MAX;

    // Loop to iterate over sentences
    for (int i = 0; i < N; i++) {

        // Stores count of words
        // in ith sentence
        int temp = countword(arr[i]);

        // Update answer
        if (temp < ans)
            ans = temp;
    }

    // Return Answer
    return ans;
}
// Driver code
int main()
{
    string arr[] = { "there is a cow", 
                     "cow is our mother",
                     "cow gives us milk and \
                      milk is sweet",
                     "there is a boy who loves cow" };
    int N = 4;

    cout << countleastWords(arr, N) << endl;
    return 0;
}
```

**Output**

```
4

```

***时间复杂度:** O(N * M)其中 M 是所有句子的平均字符数*
***辅助空间:** O(1)*