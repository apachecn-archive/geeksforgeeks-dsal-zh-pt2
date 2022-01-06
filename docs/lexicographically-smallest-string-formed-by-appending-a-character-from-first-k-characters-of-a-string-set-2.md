# 通过从字符串的前 K 个字符中附加一个字符而形成的字典上最小的字符串|集合 2

> 原文:[https://www . geeksforgeeks . org/通过从字符串集的第一个 k 个字符中附加一个字符而形成的字典最小字符串-2/](https://www.geeksforgeeks.org/lexicographically-smallest-string-formed-by-appending-a-character-from-first-k-characters-of-a-string-set-2/)

给定一个由小写字母和整数组成的字符串 **str** 和一个整数 **K** ，可以对 **str** 执行以下操作

1.  初始化一个空字符串**X =“**”。
2.  从**字符串**的第一个 **K** 字符中提取任意字符，并将其追加到 **X** 中。
3.  从**字符串**中删除所选字符。
4.  当字符串中还有字符时，重复上述步骤。

任务是生成 **X** ，使其在字典上尽可能最小，然后打印生成的字符串。

**示例:**

> **输入:**str = " geek "，K = 2
> **输出:** eegk
> 操作 1:str = " geg "，x = " e "
> 操作 2:str = " GK "，x = " ee "
> 操作 3:str = " k "，x = " EEG "
> 操作
> 
> **输入:** str = "geeksforgeeks "，K = 5
> **输出:**eefggeekors

**方法:**为了得到字典上最小的字符串，我们需要在每次从**字符串**中选择一个字符时，从第一个 **K** 字符中取最小的字符。为此，我们可以将第一个 **K** 字符放在一个 [priority_queue](https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/) (min-heap)中，然后选择最小的字符并将其追加到 **X** 中。然后，将 **str** 中的下一个字符推到优先级队列中，并重复该过程，直到剩下要处理的字符。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the lexicographically 
// smallest required string
string getSmallestStr(string S, int K)
{

    // Initially empty string
    string X = "";

    // min heap of characters
    priority_queue<char, vector<char>, greater<char> > pq;

    // Length of the string
    int i, n = S.length();

    // K cannot be greater than
    // the size of the string
    K = min(K, n);

    // First push the first K characters
    // into the priority_queue
    for (i = 0; i < K; i++)
        pq.push(S[i]);

    // While there are characters to append
    while (!pq.empty()) {

        // Append the top of priority_queue to X
        X += pq.top();

        // Remove the top element
        pq.pop();

        // Push only if i is less than
        // the size of string
        if (i < S.length())
            pq.push(S[i]);

        i++;
    }

    // Return the generated string
    return X;
}

// Driver code
int main()
{
    string S = "geeksforgeeks";
    int K = 5;

    cout << getSmallestStr(S, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.PriorityQueue;

class GFG 
{

    // Function to return the lexicographically
    // smallest required string
    static String getSmallestStr(String S, int K)
    {

        // Initially empty string
        String X = "";

        // min heap of characters
        PriorityQueue<Character> pq = new PriorityQueue<>();

        // Length of the string
        int i, n = S.length();

        // K cannot be greater than
        // the size of the string
        K = Math.min(K, n);

        // First push the first K characters
        // into the priority_queue
        for (i = 0; i < K; i++)
            pq.add(S.charAt(i));

        // While there are characters to append
        while (!pq.isEmpty()) 
        {

            // Append the top of priority_queue to X
            X += pq.peek();

            // Remove the top element
            pq.remove();

            // Push only if i is less than
            // the size of string
            if (i < S.length())
                pq.add(S.charAt(i));

            i++;
        }

        // Return the generated string
        return X;
    }

    // Driver Code
    public static void main(String[] args) 
    {
        String S = "geeksforgeeks";
        int K = 5;
        System.out.println(getSmallestStr(S, K));
    }
}

// This code is contributed by
// sanjeev2552
```

**Output:**

```
eefggeekkorss

```