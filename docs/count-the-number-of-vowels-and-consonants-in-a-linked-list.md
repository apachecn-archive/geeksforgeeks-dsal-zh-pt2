# 统计链表中元音和辅音的个数

> 原文:[https://www . geeksforgeeks . org/count-link-list 中元音和辅音的数量/](https://www.geeksforgeeks.org/count-the-number-of-vowels-and-consonants-in-a-linked-list/)

给定一个包含小写英文字母的链表，任务是计算链表中存在的辅音和元音的数量。

**示例:**

> **输入:**链表:a->B->o->y->e->z->NULL
> T3】输出:T5】元音:3
> 辅音:3
> 
> **输入:**链表:a->e->B->c->s->e->y->t->NULL
> T3】输出:T5】元音:3
> 辅音:5

**方法:**要解决此问题，请按照以下步骤操作:

1.  创建两个变量，**元音**和**辅音**分别存储元音和辅音的个数。用 0 初始化它们。
2.  现在，开始遍历链表，如果字符与[a，e，I，o，u]集合中的任何一个匹配，则将**元音**增加 1，否则将**辅音**增加 1。
3.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the abpve approach

#include <bits/stdc++.h>
using namespace std;

// A linked list node
struct Node {
    char data;
    struct Node* next;

    Node(char key)
    {
        data = key;
        next = NULL;
    }
};

// Utility function to check if a character
// is a vowel or not
bool isVowel(char x)
{
    return (x == 'a' || x == 'e'
            || x == 'i' || x == 'o'
            || x == 'u');
}

// Function to count the number
// of vowels and consonants
void count(struct Node* head)
{
    int vowel = 0;
    int consonant = 0;

    for (Node* itr = head; itr != NULL; itr = itr->next) {
        if (isVowel(itr->data)) {
            vowel++;
        }
        else {
            consonant++;
        }
    }
    cout << "Vowel: " << vowel << endl;
    cout << "Consonant: " << consonant << endl;
}

// Driver Code
int main()
{

    Node* head = new Node('u');
    head->next = new Node('h');
    head->next->next = new Node('d');
    head->next->next->next = new Node('a');
    head->next->next->next->next = new Node('n');

    count(head);

    return 0;
}
```

**Output**

```
Vowel: 2
Consonant: 3

```

**时间复杂度:**O(N)
T3】辅助空间: O(1)