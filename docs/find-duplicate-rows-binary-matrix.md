# 在二进制矩阵中找到重复的行

> 原文:[https://www . geesforgeks . org/find-重复-行-二进制-矩阵/](https://www.geeksforgeeks.org/find-duplicate-rows-binary-matrix/)

给定一个元素只有 0 和 1 的二进制矩阵，我们需要打印与矩阵中已经存在的行重复的行。
示例:

```
Input : {1, 1, 0, 1, 0, 1},
    {0, 0, 1, 0, 0, 1},
    {1, 0, 1, 1, 0, 0},
    {1, 1, 0, 1, 0, 1},
    {0, 0, 1, 0, 0, 1},
    {0, 0, 1, 0, 0, 1}.

Output :
There is a duplicate row at position: 4 
There is a duplicate row at position: 5 
There is a duplicate row at position: 6 
```

这个问题主要是[在二进制矩阵](https://www.geeksforgeeks.org/print-unique-rows/)中寻找唯一行的扩展。
一个**简单的解决方案**就是一个一个的遍历所有的行。对于每一行，检查它是否存在于其他任何地方。如果是，打印该行。
时间复杂度:O(ROW^2 x COL)
辅助空间:O(1)
**使用 Trie** [的最优解 Trie](https://www.geeksforgeeks.org/trie-insert-and-search/) 是一种高效的数据结构，用于存储和检索字符集较小的数据。搜索复杂度作为密钥长度是最优的。
解决问题的方法是首先在二进制 trie 中插入矩阵，然后如果新添加的行已经存在于 trie 中，那么我们现在认为它是一个重复的行

## C

```
// C++ program to find duplicate rows
// in a binary matrix.
#include<bits/stdc++.h>

const int MAX = 100;

/*struct the Trie*/
struct Trie
{
    bool leaf;
    Trie* children[2];
};

/*function to get Trienode*/
Trie* getNewTrieNode()
{
    Trie* node = new Trie;
    node->children[0] = node->children[1] = NULL;
    node->leaf = false;
    return node;
}

/* function to insert a row in Trie*/
bool insert(Trie*& head, bool* arr, int N)
{
    Trie* curr = head;

    for (int i = 0; i < N; i++)
    {
        /*creating a new path if it don not exist*/
        if (curr->children[arr[i]] == NULL)
            curr->children[arr[i]] = getNewTrieNode();

        curr = curr->children[arr[i]];
    }

    /*if the row already exist return false*/
    if (curr->leaf)
        return false;

    /* making leaf node tree and return true*/
    return (curr->leaf = true);
}

void printDuplicateRows(bool mat[][MAX], int M, int N)
{
    Trie* head = getNewTrieNode();

    /*inserting into Trie and checking for duplicates*/
    for (int i = 0; i < M; i++)

        // If already exists
        if (!insert(head, mat[i], N))
            printf("There is a duplicate row"
                  " at position: %d \n", i+1);

}

/*driver function to check*/
int main()
{
    bool mat[][MAX] =
    {
        {1, 1, 0, 1, 0, 1},
        {0, 0, 1, 0, 0, 1},
        {1, 0, 1, 1, 0, 0},
        {1, 1, 0, 1, 0, 1},
        {0, 0, 1, 0, 0, 1},
        {0, 0, 1, 0, 0, 1},
    };

    printDuplicateRows(mat, 6, 6);
    return 0;
}
```

输出:

```
There is a duplicate row at position: 4 
There is a duplicate row at position: 5 
There is a duplicate row at position: 6 
```

**另一种方法不使用 Trie，但不适用于大量列**
另一种方法是转换行的十进制等价物，并检查新行是否具有相同的十进制等价物，那么它就是重复行。如果列数很大，它将不起作用。

下面是上述方法的实现。

## C++

```
#include<iostream>
#include<vector>
#include<set>
using namespace std;
vector<int> repeatedRows(vector<vector<int>> matrix, int M, int N)
{

    set<int>s;

    // vector to store the repeated rows
    vector<int>res;

    for(int i=0;i<M;i++){
        // calculating decimal equivalent of the row
        int no=0;
        for(int j=0;j<N;j++){
            no+=(matrix[i][j]<<j);
        }

        /*
        rows with same decimal equivatent will be same,
        therefore, checking through set if the calculated equivalent was
        present before;
        if yes then add to thee result otherwise insert in the set
        */
        if(s.find(no)!=s.end()){
            res.push_back(i);
        }
        else{
            s.insert(no);
        }
    }

    return res;

}
int main() {

  vector<vector<int>>matrix={
        {1, 1, 0, 1, 0, 1},
        {0, 0, 1, 0, 0, 1},
        {1, 0, 1, 1, 0, 0},
        {1, 1, 0, 1, 0, 1},
        {0, 0, 1, 0, 0, 1},
        {0, 0, 1, 0, 0, 1},};

  int m=matrix.size();
  int n=matrix[0].size();
  vector<int>res=repeatedRows(matrix,m,n);
  for(int e:res){
     cout<< "There is a duplicate row at position: "<<e+1 << '\n';
  }

    return 0;
}
```

**Output**

```
There is a duplicate row at position: 4
There is a duplicate row at position: 5
There is a duplicate row at position: 6
```

时间复杂度= 0(M * N)

空间复杂度= 0(M)，其中 M 是行数

本文由**普拉纳夫**供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](http://www.write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 review-team@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。