# 数组中与给定字符串前缀匹配的最长字符串

> 原文:[https://www . geesforgeks . org/数组中最长的字符串与给定字符串的前缀匹配/](https://www.geeksforgeeks.org/longest-string-in-an-array-which-matches-with-prefix-of-the-given-string/)

给定一个字符串数组 **arr[]** 和 **Q** 查询，其中每个查询由一个字符串 **str** 组成，任务是在数组中找到与给定字符串的前缀 **str** 匹配的最长字符串，即该字符串必须是前缀 **str** 。

**示例:**

> **输入:t1】Arr[]= {“geeksforgeeks”、“GeeksForGeeksd”、“arnab”、“art”}、
> q[]= {“geeksforgeeks”、“ar”、“art”}
> **输出:**
> 
> -1** 
> 
> **输入:** arr[] = {“极客”“极客”“极客”“极客”}，
> q[] = {“极客”“极客”“极客”“极客”“啧啧”}
> **输出:**
> 极客
> -1
> 极客
> -1

**简单方法:**对于每个给定的字符串，遍历数组，检查与给定字符串前缀匹配的字符串，并存储和打印最长的字符串。

**有效方法:**这个问题可以用[特里](https://www.geeksforgeeks.org/trie-insert-and-search/)来解决。我们将形成一个 trie，并将数组的字符串插入 trie 中，找到与给定字符串的前缀完全匹配的最长字符串。

下面是上述方法的实现:

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int ALPHABET_SIZE = 26;

// Trie node
struct TrieNode {
    struct TrieNode* children[ALPHABET_SIZE];

    // isEndOfWord is true if the node represents
    // end of a word
    bool isEndOfWord;
};

// Returns new trie node (initialized to NULLs)
struct TrieNode* getNode(void)
{
    struct TrieNode* pNode = new TrieNode;

    pNode->isEndOfWord = false;

    for (int i = 0; i < ALPHABET_SIZE; i++)
        pNode->children[i] = NULL;

    return pNode;
}

// If not present, inserts key into trie
// If the key is prefix of trie node, just
// marks leaf node
void insert(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            pCrawl->children[index] = getNode();

        if (i == key.length() - 1)

            // Mark last node as leaf
            pCrawl->children[index]->isEndOfWord = true;

        pCrawl = pCrawl->children[index];
    }
}

string getString(char x)
{
    // string class has a constructor
    // that allows us to specify size of
    // string as first parameter and character
    // to be filled in given size as second
    // parameter.
    string s(1, x);

    return s;
}

// Function to return the
// longest required string
string search(struct TrieNode* root, string key)
{
    struct TrieNode* pCrawl = root;

    // Prefix of the string
    string s = "";

    for (int i = 0; i < key.length(); i++) {
        int index = key[i] - 'a';
        if (!pCrawl->children[index])
            break;

        s += getString((char)key[i]);

        pCrawl = pCrawl->children[index];
    }

    if (pCrawl->isEndOfWord)
        return s;

    return "-1";
}

// Driver code
int main()
{
    string arr[] = { "Geeks", "Geek",
                     "Geekss", "Geekks" };
    int n = sizeof(arr) / sizeof(string);

    // Construct trie
    struct TrieNode* root = getNode();
    for (int i = 0; i < n; i++)
        insert(root, arr[i]);

    string queries[] = { "Geek", "Geeks", "Geekk", "Gee" };
    int q = sizeof(queries) / sizeof(string);

    for (int i = 0; i < q; i++)
        cout << search(root, queries[i]) << endl;

    return 0;
}
```

**Output:**

```
Geek
Geeks
-1
-1

```