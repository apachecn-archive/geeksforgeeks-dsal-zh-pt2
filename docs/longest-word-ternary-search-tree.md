# 三元搜索树中最长的单词

> 原文:[https://www . geesforgeks . org/long-word-三元-search-tree/](https://www.geeksforgeeks.org/longest-word-ternary-search-tree/)

给定一组用三元搜索树表示的单词，找出其中最大单词的长度。
示例:

```
Input : {"Prakriti", "Raghav", 
           "Rashi", "Sunidhi"}
Output : Length of largest word in 
         ternary search tree is: 8

Input : {"Boats", "Boat", "But", "Best"}
Output : Length of largest word in 
         ternary search tree is: 5
```

先决条件:[三元搜索树](https://www.geeksforgeeks.org/ternary-search-tree/)
思想是递归搜索左子树、右子树和等树的最大值。
如果当前字符与根的字符增量相同，则为 1。

## C

```
// C program to find the length of largest word
// in ternary search tree
#include <stdio.h>
#include <stdlib.h>
#define MAX 50

// A node of ternary search tree
struct Node
{
    char data;

    // True if this character is last
   // character of one of the words
    unsigned isEndOfString: 1;

    struct Node *left, *eq, *right;
};

// A utility function to create a new
// ternary search tree node
struct Node* newNode(char data)
{
    struct Node* temp =
     (struct Node*) malloc(sizeof( struct Node ));
    temp->data = data;
    temp->isEndOfString = 0;
    temp->left = temp->eq = temp->right = NULL;
    return temp;
}

// Function to insert a new word in a Ternary
// Search Tree
void insert(struct Node** root, char *word)
{
    // Base Case: Tree is empty
    if (!(*root))
        *root = newNode(*word);

    // If current character of word is smaller
    // than root's character, then insert this
    // word in left subtree of root
    if ((*word) < (*root)->data)
        insert(&( (*root)->left ), word);

    // If current character of word is greater
    // than root's character, then insert this
    // word in right subtree of root
    else if ((*word) > (*root)->data)
        insert(&( (*root)->right ), word);

    // If current character of word is same as
    // root's character,
    else
    {
        if (*(word+1))
            insert(&( (*root)->eq ), word+1);

        // the last character of the word
        else
            (*root)->isEndOfString = 1;
    }
}

// Function to find max of three numbers
int max(int a, int b, int c)
{
    int max;
    if (a >= b && a >= c)
        max = a;
    else if (b >= a && b >= c)
        max = b;
    else
        max = c;
}

// Function to find length of largest word in TST
int maxLengthTST(struct Node *root)
{
    if (root == NULL)
        return 0;
    return max(maxLengthTST(root->left),
               maxLengthTST(root->eq)+1,
               maxLengthTST(root->right));
}

// Driver program to test above functions
int main()
{
    struct Node *root = NULL;
    insert(&root, "Prakriti");
    insert(&root, "Raghav");
    insert(&root, "Rashi");
    insert(&root, "Sunidhi");
    int value = maxLengthTST(root);
    printf("Length of largest word in "
    "ternary search tree is: %d\n", value);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the length of largest word
// in ternary search tree
public class GFG {

    static final int MAX = 50;

    // A node of ternary search tree
    static class Node
    {
        char data;

        // True if this character is last
        // character of one of the words
        int isEndOfString = 1;

        Node left, eq, right;

        // constructor
        Node(char data)
        {
            this.data = data;
            isEndOfString = 0;
            left = null;
            eq = null;
            right = null;
        }
    }

    // Function to insert a new word in a Ternary
    // Search Tree
    static Node insert(Node root, String word, int i)
    {
        // Base Case: Tree is empty
        if (root == null)
            root = new Node(word.charAt(i));

        // If current character of word is smaller
        // than root's character, then insert this
        // word in left subtree of root
        if (word.charAt(i) < root.data)
            root.left = insert(root.left, word, i);

        // If current character of word is greater
        // than root's character, then insert this
        // word in right subtree of root
        else if (word.charAt(i) > root.data)
            root.right = insert(root.right, word, i);

        // If current character of word is same as
        // root's character,
        else
        {
            if (i + 1 < word.length())
                root.eq = insert(root.eq, word, i + 1);

            // the last character of the word
            else
                root.isEndOfString = 1;
        }
        return root;
    }

    // Function to find max of three numbers
    static int max(int a, int b, int c)
    {
        int max;
        if (a >= b && a >= c)
            max = a;
        else if (b >= a && b >= c)
            max = b;
        else
            max = c;
        return max;
    }

    // Function to find length of largest word in TST
    static int maxLengthTST(Node root)
    {
        if (root == null)
            return 0;
        return max(maxLengthTST(root.left),
                   maxLengthTST(root.eq)+1,
                   maxLengthTST(root.right));
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        Node root = null;
        root = insert(root, "Prakriti", 0);
        root = insert(root, "Raghav",  0);
        root = insert(root, "Rashi", 0);
        root = insert(root, "Sunidhi", 0);
        int value = maxLengthTST(root);
        System.out.println("Length of largest word in "+
        "ternary search tree is: "+ value);
    }
}
// This code is contributed by Sumit Ghosh
```

## C#

```
// C# program to find the length of largest word
// in ternary search tree
using System;

class GFG
{

    static readonly int MAX = 50;

    // A node of ternary search tree
    public class Node
    {
        public char data;

        // True if this character is last
        // character of one of the words
        public int isEndOfString = 1;

        public Node left, eq, right;

        // constructor
        public Node(char data)
        {
            this.data = data;
            isEndOfString = 0;
            left = null;
            eq = null;
            right = null;
        }
    }

    // Function to insert a new word in a Ternary
    // Search Tree
    static Node insert(Node root, String word, int i)
    {
        // Base Case: Tree is empty
        if (root == null)
            root = new Node(word[i]);

        // If current character of word is smaller
        // than root's character, then insert this
        // word in left subtree of root
        if (word[i] < root.data)
            root.left = insert(root.left, word, i);

        // If current character of word is greater
        // than root's character, then insert this
        // word in right subtree of root
        else if (word[i] > root.data)
            root.right = insert(root.right, word, i);

        // If current character of word is same as
        // root's character,
        else
        {
            if (i + 1 < word.Length)
                root.eq = insert(root.eq, word, i + 1);

            // the last character of the word
            else
                root.isEndOfString = 1;
        }
        return root;
    }

    // Function to find max of three numbers
    static int max(int a, int b, int c)
    {
        int max;
        if (a >= b && a >= c)
            max = a;
        else if (b >= a && b >= c)
            max = b;
        else
            max = c;
        return max;
    }

    // Function to find length of largest word in TST
    static int maxLengthTST(Node root)
    {
        if (root == null)
            return 0;
        return max(maxLengthTST(root.left),
                maxLengthTST(root.eq) + 1,
                maxLengthTST(root.right));
    }

    // Driver code
    public static void Main()
    {
        Node root = null;
        root = insert(root, "Prakriti", 0);
        root = insert(root, "Raghav", 0);
        root = insert(root, "Rashi", 0);
        root = insert(root, "Sunidhi", 0);
        int value = maxLengthTST(root);
        Console.WriteLine("Length of largest word in "+
        "ternary search tree is: "+ value);
    }
}

/* This code contributed by PrinciRaj1992 */
```

## java 描述语言

```
<script>
    // Javascript program to find the length of largest word
    // in ternary search tree
    let MAX = 50;

    class Node
    {
        constructor(data) {
           this.left = null;
           this.right = null;
           this.data = data;
           this.isEndOfString = 0;
           this.eq = null;
        }
    }

    // Function to insert a new word in a Ternary
    // Search Tree
    function insert(root, word, i)
    {
        // Base Case: Tree is empty
        if (root == null)
            root = new Node(word[i]);

        // If current character of word is smaller
        // than root's character, then insert this
        // word in left subtree of root
        if (word[i] < root.data)
            root.left = insert(root.left, word, i);

        // If current character of word is greater
        // than root's character, then insert this
        // word in right subtree of root
        else if (word[i] > root.data)
            root.right = insert(root.right, word, i);

        // If current character of word is same as
        // root's character,
        else
        {
            if (i + 1 < word.length)
                root.eq = insert(root.eq, word, i + 1);

            // the last character of the word
            else
                root.isEndOfString = 1;
        }
        return root;
    }

    // Function to find max of three numbers
    function max(a, b, c)
    {
        let Max;
        if (a >= b && a >= c)
            Max = a;
        else if (b >= a && b >= c)
            Max = b;
        else
            Max = c;
        return Max;
    }

    // Function to find length of largest word in TST
    function maxLengthTST(root)
    {
        if (root == null)
            return 0;
        return max(maxLengthTST(root.left),
                   maxLengthTST(root.eq)+1,
                   maxLengthTST(root.right));
    }

    let root = null;
    root = insert(root, "Prakriti", 0);
    root = insert(root, "Raghav",  0);
    root = insert(root, "Rashi", 0);
    root = insert(root, "Sunidhi", 0);
    let value = maxLengthTST(root);
    document.write("Length of largest word in "+
                       "ternary search tree is: "+ value);

// This code is contributed by divyeshrabadiya07.
</script>
```

**输出:**

```
Length of largest word in ternary search tree is: 8
```

本文由**普拉克里提·古普塔**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。