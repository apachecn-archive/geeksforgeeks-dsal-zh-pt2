# 检查字符串链表是否形成回文的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-to-check-if-a-link-list-string-forms-a-回文/](https://www.geeksforgeeks.org/c-program-to-check-if-a-linked-list-of-strings-forms-a-palindrome/)

给定一个处理字符串数据的链表，检查数据是否是回文？
**例:**

```
Input: a -> bc -> d -> dcb -> a -> NULL
Output: True
String "abcddcba" is palindrome.

Input: a -> bc -> d -> ba -> NULL
Output: False
String "abcdba" is not palindrome. 
```

想法很简单。从给定的链表中构造一个字符串，并检查构造的字符串是否是回文。

## C/C++

```
// Program to check if a given linked list 
// of strings form a palindrome
#include <bits/stdc++.h>
using namespace std;

// Link list node 
struct Node
{
    string data;
    Node* next;
};

// A utility function to check if str 
// is palindrome or not
bool isPalindromeUtil(string str)
{
    int length = str.length();

    // Match characters from beginning 
    // and end.
    for (int i = 0; i < length / 2; i++)
        if (str[i] != str[length - i - 1])
            return false;

    return true;
}

// Returns true if string formed by linked
// list is palindrome
bool isPalindrome(Node *node)
{
    // Append all nodes to form a string
    string str = "";
    while (node != NULL)
    {
        str.append(node->data);
        node = node->next;
    }

    // Check if the formed string is 
    // palindrome
    return isPalindromeUtil(str);
}

// A utility function to print a given 
// linked list
void printList(Node *node)
{
    while (node != NULL)
    {
        cout << node->data << " -> ";
        node = node->next;
    }
    printf("NULL");
}

/* Function to create a new node with 
   given data */
Node *newNode(const char *str)
{
    Node *new_node = new Node;
    new_node->data = str;
    new_node->next = NULL;
    return new_node;
}

// Driver code
int main()
{
    Node *head = newNode("a");
    head->next = newNode("bc");
    head->next->next = newNode("d");
    head->next->next->next = 
    newNode("dcb");
    head->next->next->next->next = 
    newNode("a");
    isPalindrome(head)? printf("true"):
                        printf("false");
    return 0;
}
```

**Output:**

```
true
```

更多详情请参考[查看字符串链表是否形成回文](https://www.geeksforgeeks.org/check-linked-list-strings-form-palindrome/)整篇文章！